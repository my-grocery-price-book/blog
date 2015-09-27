---
title: Vagrant and Ansible the ultimate combo
date: 2015-09-27
tags: challenges, tools
---

So for the last few months I have been using [Vagrant](https://www.vagrantup.com/) and 
[Ansible](http://www.ansible.com/configuration-management) for any new projects that I have to work on. READMORE

The idea behind vagrant is to allow you to isolate all the software requirements to run your code for different projects
inside separate virtual machines. Vagrant makes it easier to work on different projects with conflicting requirements by
isolating them in different virtual machines. For example, two different projects requiring different versions of MYSQL.
It also has the added benefit of not cluttering your actual machine with all the projects unique and different software 
requirements.

Ansible is a powerful automation tool that allows you to easily setup new (and old) servers with the required
software it needs. This makes setting up new enviroments a breeze. 

The combination of Anisble and Vagrant is currently a real powerful way of setting up development
enviroments quickly. If you add the Ansible scripts to your source control, you will have the changing requirements
of your application setup in your source history. 

I have recently taken the challenge of destroying my virtual machines every Monday and rebuilding it using Vagrant and
 Ansible. The idea being that I should be able to continue working within minutes and if that is not the case, updating
 the Ansible scripts with the required changes. This will help me make sure anything important required to work on the
 project is in source control, whether that be code, data or software setup.

This is currently my prefered method of working with the my-grocery-price-book-code. If you too are interested in this
sort of setup, I recommended you take a look at  
[Vagrantfile](https://bitbucket.org/grantspeelman/my-grocery-price-book.co.za/src/d43c1610845416273530eb526e038c42bb70b813/Vagrantfile?at=master&fileviewer=file-view-default#Vagrantfile-120)
and the
[Ansible Scripts](https://bitbucket.org/grantspeelman/my-grocery-price-book.co.za/src/d43c1610845416273530eb526e038c42bb70b813/ansible/?at=master)
of the my grocery price book code.

Also if you have not worked with either of the 2 before or would like to know more about them, I recommend you check
out their Getting Started pages:
[Vagrant](https://docs.vagrantup.com/v2/getting-started/) and [Ansible](http://docs.ansible.com/ansible/intro_getting_started.html)

