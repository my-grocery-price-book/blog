---
title: Acceptance testing multiple sessions/actors using capybara 
date: 2016-03-31
tags: gems
---

I recently wanted to add functionality that would allow multiple shoppers to work on the same Price Book.READMORE 
I wanted to write my feature spec in such a way that it was obvious that there were multiple actors and it allowed me to 
easily capture common logic like signing in.

I wanted to use 2 gems to archive this, obviously [capybara](https://github.com/jnicklas/capybara) and secondly
[capybara-email](https://github.com/dockyard/capybara-email) for emails

I created a [base class](https://gist.github.com/grantspeelman/cf1a333ea187285f6adfb1b929d3b198) I felt was independent 
of the app

~~~ ruby
class PersonaSession
  include Capybara::DSL
  include Capybara::Email::DSL

  # override to stop usage of global current_session
  def page
    @page ||= Capybara::Session.new(Capybara.current_driver, Capybara.app)
  end

  def click_link_in_email(link_name)
    email = open_email(@email)
    host = Rails.configuration.action_mailer.default_url_options[:host]
    link_path = email.find_link(link_name)[:href].gsub("http://#{host}", '')
    visit link_path
  end

  def perform(&block)
    instance_exec(&block)
  end
end
~~~

Then I created a shopper specific class

~~~ ruby
class ShopperPersonaSession < PersonaSession
  def initialize(email:)
    super()
    @email = email
    @password = 'password'
  end

  def sign_up
    visit '/shoppers/sign_up' unless current_path.try(:include?, '/shoppers/sign_up')
    fill_in 'Email', with: @email
    fill_in 'Password', with: @password
    fill_in 'Password confirmation', with: @password
    click_button 'Sign up'
  end
end
~~~

This allowed me to write a test like this

~~~ ruby
class SharingAShoppingListTest < FeatureTest
  setup do
    @grant = ShopperPersonaSession.new(email: 'grant@example.com')
    @grant.sign_up
    @kate = ShopperPersonaSession.new(email: 'kate@example.com')
  end

  test 'Grant and kate work together on a shopping list' do
    @grant.perform do
      click_link 'Price Book'
      click_link 'Invite'
      fill_in 'Name', with: 'Kate'
      fill_in 'Email', with: 'kate@example.com'
      click_button 'Invite'
    end

    @kate.perform do
      click_link_in_email 'My Price Book'
      sign_up
      click_button 'Accept'
    end

    @grant.perform do
      click_link 'Shopping List'
      click_on 'New Shopping List'
      click_button 'Edit Title'
      fill_in 'Title', with: 'Our Shopping'
      click_button 'Update'
    end

    assert @grant.has_css?('span', text: 'Our Shopping')
    assert @grant.has_no_css?('span', text: 'Update Failed')

    @kate.perform do
      click_link 'Shopping List'
      click_link 'Items'
      fill_in 'Item name', with: 'bread'
      fill_in 'Unit', with: 'loaves'
      fill_in 'Amount', with: '2'
      click_button 'Add'
    end

    assert @kate.has_content?('bread')

    @grant.click_link 'Refresh'

    assert @grant.has_content?('bread')
  end
end
~~~