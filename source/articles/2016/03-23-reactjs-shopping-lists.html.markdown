---
title: Reactjs Shopping Lists
date: 2016-03-23
tags: gems,services,javascript
---

I have been recently trying out 
[reactjs](https://facebook.github.io/react/) and decided to rebuild the shopping list section using it.
 [give it a try](http://www.my-grocery-price-book.co.za/shopping_lists), you can login as a Guest.READMORE

To get started with react and rails I used a gem called [react-rails](https://github.com/reactjs/react-rails). 
The gem allows you to do server side rendering as well which I thought could be pretty useful. 
Getting everything setup was as simple as following their README and I was building react examples in no time.

I also added [eslint](http://eslint.org/) as a linting utility for my .jsx files. Getting this running required nodejs 
and npm. I managed to figure (with a bit of GoOgle) I could install what I needed globally using npm.

    npm install -g eslint eslint-config-standard eslint-plugin-standard eslint-plugin-react
    
once installed you create a [.eslintrc](https://github.com/my-grocery-price-book/www/blob/1bc730bdb6e9cac48c254f10576f5b96e50336df/.eslintrc)
 file and run it as follows.

    eslint app/assets/javascripts/**/*
    
All in all I am quite happy with the outcome of the shopping list and also really enjoying using reactjs. 
Next up is figuring out how to write jasmine tests for my react components.
