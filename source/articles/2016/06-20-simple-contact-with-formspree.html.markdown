---
title: Creating a simple Contact form using formspree.io
date: 2016-06-20
tags: services
---

Creating a simple contact form with Ruby on Rails is straight forward and simple but I found an even
simpler way of doing your contact form.READMORE 

If all you want is an email sent to you with the details of
the contact form then I recommend that you take a look at [formspree](https://formspree.io/). It allows
you to add a form on your page that will be emailed to a desired address and it's real simple to
get going.

Here is the form html used on my-grocery-price-book.co.za

~~~ html
    <form action="https://formspree.io/info@my-grocery-price-book.co.za"
          method="POST">
      <input type="hidden" name="_next" value="<%= thank_you_url %>" />
      <input type="hidden" name="_subject" value="My Price Grocery Book contact" />
      <input type="text" name="_gotcha" style="display:none" />
      <div class="form-group">
        <label for="input_your_name">Your Name</label>
        <input id="input_your_name" name="name" class="form-control" placeholder="Your Name">
      </div>
      <div class="form-group">
        <label for="input_email_address">Email address</label>
        <input type="email" name="_replyto" class="form-control" id="input_email_address" placeholder="Email">
      </div>
      <div class="form-group">
        <label for="textarea_message">Message</label>
        <textarea class="form-control" rows="3" name="message" id="textarea_message"></textarea>
      </div>
      <button type="submit" class="btn btn-default">Send</button>
    </form>
~~~

Thats it, you now have a contact form. Because the form is plain html you can even use this on
static sites. Have a look on the [formspree website](https://formspree.io/) for more details.