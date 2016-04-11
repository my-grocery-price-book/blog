---
title: Writing jasmine test for reactjs components on Ruby on Rails 
date: 2016-04-11
tags: gems, javascript
---

Now that I have manage to write a few components using reactjs/rails and 
I feel I understand the basics of reactjs, I wanted to be able to write tests for
my components. I looked into using [jasmine-rails](https://github.com/searls/jasmine-rails)
for testing my components. 

Installing it was as simple as following the Gems [README](https://github.com/searls/jasmine-rails#installation).
You will need [PhantomJS](http://phantomjs.org/) if you want to run your test headless (checkout out 
[phantomjs-binary](https://github.com/searls/jasmine-rails#phantomjs-binary) and [phantomjs gem](https://rubygems.org/gems/phantomjs) 
if not) otherwise visiting http://localhost:3000/specs can also be used. 

The next step was creating a helper js file to make [reactjs TestUtils](http://facebook.github.io/react/docs/test-utils.html) 
available.
`spec/javascripts/helpers/default_helper.js`

~~~ javascript
  const TestUtils = React.addons.TestUtils;
~~~

This made it possible to write my first test

`spec/javascripts/components/confirm_delete.js`

~~~ javascript
  describe('ConfirmDelete', function() {
    var react_document;
    var dom_node;
  
    beforeEach(function() {
      react_document = TestUtils.renderIntoDocument(
          React.createElement(ConfirmDelete, {modal_id: "ten"})
      );
      dom_node = ReactDOM.findDOMNode(react_document);
    });
  
    it("works", function () {
      expect(dom_node.nodeName).toEqual('DIV');
      expect(dom_node.attributes.id.value).toEqual('ten');
    });
  });
~~~

One last hiccup was attempting to make my test files jsx. There seems to be a issue with
"sprockets 3" and "jasmine-rails" ( check out this 
[github issue](https://github.com/searls/jasmine-rails/issues/178) for more details).
 In the mean time to work around this I downgraded my sprockets to 
 "gem 'sprockets', '~> 2.7'" and edited `jasmine.yml` with the following:
 
~~~ yaml
spec_files:
  - "**/*[Ss]pec.{jsx,js}"
~~~

This allowed me to rename my test file to jsx and my test with the JSX syntax.

`spec/javascripts/components/confirm_delete.jsx`

~~~ javascript
describe('ConfirmDelete', function() {
  var react_dom;
  var dom_node;

  beforeEach(function() {
    react_dom = TestUtils.renderIntoDocument(
        <ConfirmDelete modal_id="ten"/>
    );
    dom_node = ReactDOM.findDOMNode(react_dom);
  });

  it("works", function () {
    expect(dom_node.nodeName).toEqual('DIV');
    expect(dom_node.attributes.id.value).toEqual('ten');
  });
});
~~~

That is it :) 

 * More Reading on [Jasmine](http://jasmine.github.io/2.0/introduction.html)
 * More Reading on [reactjs TestUtils](http://facebook.github.io/react/docs/test-utils.html) 