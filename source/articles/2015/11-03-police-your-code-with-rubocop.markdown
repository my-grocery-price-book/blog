---
title: Police your code with Rubocop
date: 2015-11-03
tags: code quality, gems
---

Keeping your code on a project in shape is a daily challenge but there is a a ruby gem called 
[rubocop](https://github.com/bbatsov/rubocop) that can help you with this.
READMORE

I have been using [rubocop](https://github.com/bbatsov/rubocop) on the grocery app and a few other projects for a while 
now. It's is really a great tool to help keep your code quality in check. Rubocop is a Ruby static code analyzer that 
is based on the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) and 
[Rails Style Guide](https://github.com/bbatsov/rails-style-guide).

Getting started with it is real simple:

~~~shell
  gem install rubocop
  rubocop -R # run inside your Rails Project
~~~

You might feel that some of these suggestions are splitting hairs. For example things such as single quotes vs double quotes, 
indentations and blank lines. These simple ones are usually easily fixed by using rubocop's builtin autofix functionality. 
Just run `rubocop -aR` which will automatically update your code for these more simpler rules.

Rules that you feel is against your personal style, eg documenting classes, methods should not start with "get" or 
"set" as it can easily be turned off or tuned by adding a .rubocop.yml to your project root folder.
 
If you follow those guideslines and refactor accordly you should end with simpler, more readable and more maintainable
code.

