---
title: Current System Architecture
date: 2015-09-09
tags: challenges, gems
---

Having a system architecture might seem like overkill for this project, but I am hoping it will help me keep the
system in my head and help make more insightful decisions. READMORE

I almost always find it easy to talk about system architecture when you have a diagram. So I decided to create one using
[draw.io](https://www.draw.io/)

![alt text](/images/GrocerySystemArch.svg "Grocery Price Book System Architecture")

So the goal is to link the traditional Grocery Price Book with the of Crowd Sourcing. This will hopefully make it
easier for people to share pricing information thus increasing the power of your Price Book. 

The system has been split into 2 main apps. The User Facing Price Book application part that will handle all the user 
specific information and a API to store all the pricing infomation. This should make it possible for vendors to load 
their pricing infomation into the API if they want to.This is all still mostly theory at the moment. 
Hoping to start eating my own dog food soon.

On a slightly different note...

I have recently completed 'viewing your prices' on the price book page which pulls its infomation from the API.
Things left to do is build the 'Shopping List' and completing the 'Price Compare' sections, then we should have 
our MVP.
