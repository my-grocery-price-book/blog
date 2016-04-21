---
title: Simple Reactjs AutoComplete using Typehead's Bloodhound
date: 2016-04-21
tags: javascript
---

I wanted to add autocomplete to the shopping list, hopefully making it easier to build 
them. Using Reactjs made it very difficult  to use out of the box autocompletes like 
[typeahead](https://twitter.github.io/typeahead.js/) and 
[jquery ui autocomplete](https://jqueryui.com/autocomplete/) READMORE
because Reactjs uses a [virtual dom](http://tonyfreed.com/blog/what_is_virtual_dom). Another
requirement I wanted was to display the suggestions above the input making it a bit more mobile 
friendly.

The solution I came up with is using typeahead's 
[bloodhound engine](https://github.com/twitter/typeahead.js/blob/master/doc/bloodhound.md#remote)
and adding the results to the reactjs render myself.

Here is an example of the minimum code required to get this running:

~~~ javascript
var SampleAutoComplete = React.createClass({

  getInitialState: function () {
    return {name: "", suggestions: [], 
            more_suggestions: [], bloodhound_initialized: false};
  },

  handleNameChange: function (e) {
    if(e.target.value === "") {
      this.setState({name: "", suggestions: [], more_suggestions: []});
    } else {
      this.findSuggestions(e.target.value);
      this.setState({name: e.target.value});
    }
  },

  findSuggestions: function(name) {
    if (this.state.bloodhound_initialized) {
      this.bloodhound.search(name,
          this.handleNameSuggestions,
          this.handleAdditionalNameSuggestions)
    }
  },

  handleNameSuggestions: function (suggested_names) {
    this.setState({suggestions: suggested_names});
  },

  handleAdditionalNameSuggestions: function (suggested_names) {
    this.setState({more_suggestions: suggested_names});
  },

  componentDidMount: function () {
    this.bloodhound = Bloodhound({
      datumTokenizer: Bloodhound.tokenizers.whitespace,
      queryTokenizer: Bloodhound.tokenizers.whitespace,
      sufficient: 3,
      prefetch: { url: "/my/prefetch/url.json" },
      remote: { url: "/my/remote/url.json?query=%QUERY", 
                wildcard: '%QUERY' }
    });
    this.bloodhound.initialize().done(this.bloodhoundInitialized);
  },

  bloodhoundInitialized: function () {
    this.setState({bloodhound_initialized: true});
  },

  render: function () {
    var state = this.state;

    var suggestions = state.suggestions.concat(this.state.more_suggestions).slice(0,3);

    var rendered_suggestions = suggestions.map(function (name) {
      return (
          <button className="name-suggestion" key={"suggested-" + name}>{name}</button>
      );
    });

    return <div>
      <div className="col-xs-12">{rendered_suggestions}</div>
      <div className="col-xs-12">
        <input value={state.name} onChange={this.handleNameChange}
               autoComplete={state.bloodhound_initialized ? 'off' : 'on'} />
      </div>
    </div>;
  }
});
~~~

You can find the grocery app version of the code in theses pull requests: 
[Shopping list autocomplete](https://github.com/my-grocery-price-book/www/pull/12/files) and
[Additional suggestions on shopping list](https://github.com/my-grocery-price-book/www/pull/13)

Also feel free to login as a Guest and give it a try yourself with creating a shopping list on
 [My Grocery Price Book](http://www.my-grocery-price-book.co.za/shopping_lists)