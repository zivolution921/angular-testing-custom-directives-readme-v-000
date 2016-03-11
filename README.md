# Testing Custom Directives

## Overview

Now that we know all about custom directives, we need to test them. We do this via protractor.

## Objectives

- Describe Directive testing
- Write a unit test for our custom Directives

## Testing directives

We already know how to use protractor to test our HTML output, so the explanation on how to test directives is very similar.

Our protractor setup currently runs a local webserver so we have a web page to test in our tests - this is the `index.html` that we've used before (you can see an example in this repo). Here we include all of our directives etc, and we use them like we would inside a normal application. This allows protractor to use the directive like a normal user would.

Inside this repo, we've got a counter directive that increments when we click on the directive. Let's test this.

Inside our `index.html`, we have this:

```html
<counter></counter>
```

This initialises and puts our counter directive on the page.

Now, in our `Index.spec.js` file inside `spec/`, we can grab the page.

```js
describe('Directive Test', function() {
	browser.get('http://localhost:8080');
});
```

Now let's grab our counter directive - this has the class `counter`. Let's also grab the current count.

```js
describe('Directive Test', function() {
	browser.get('http://localhost:8080');

	var counter = element(by.css('.counter'));
	var count = element(by.css('.counter__count'));
});
```

Now we can test that the counter displays an initial 0 count by grabbing the innerHTML.

```js
describe('Directive Test', function() {
	browser.get('http://localhost:8080');

	var counter = element(by.css('.counter'));
	var count = element(by.css('.counter__count'));

	it('should have an initial 0 count', function () {
		expect(count.getInnerHtml()).toEqual('Current count: 0');
	});
});
```

Awesome! Now, let's click on the counter and check that it increments the counter correctly.

```js
describe('Directive Test', function() {
	browser.get('http://localhost:8080');

	var counter = element(by.css('.counter'));
	var count = element(by.css('.counter__count'));

	it('should have an initial 0 count', function () {
		expect(count.getInnerHtml()).toEqual('Current count: 0');
	});

	it('should increment when we click on it', function () {
		counter.click();

		expect(count.getInnerHtml()).toEqual('Current count: 1');
	});

});
```

Sorted - now our directive is tested, and is working perfectly!