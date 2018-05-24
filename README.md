# Selectors, jQuery, Events

**NOTE:** Sample code this lecture uses has been provided. Please familiarize yourself with both `index.html` as well as `index.css`. 

## Objectives

This lesson aims to further students' understanding of JavaScript's interaction
with the DOM and how jQuery eases the barrier between the two. 

## SWBATS

+ JAVASCRIPT/JQUERY - Explain jQuery's relationship to JavaScript
+ JAVASCRIPT/JQUERY - Require jQuery so that it is available to use in a project
+ JAVASCRIPT/JQUERY - Explain the use case of a DOM selector
+ JAVASCRIPT/JQUERY - Use a DOM selector to select an HTML element
+ JAVASCRIPT - Debug syntax errors with external tools
+ JAVASCRIPT - Explain what an event listener is and how it's used

## Introduction

#### What is jQuery?

Developed by [John Resig](http://en.wikipedia.org/wiki/John_Resig), jQuery is a
fast, small, and feature-rich JavaScript library. It makes things like DOM
traversal and manipulation, event handling, animation, and getting information
from other servers much simpler. It accomplishes this with an easy-to-use API
that works across virtually all browsers. 

We learned in our JavaScript lessons that we can write _functions_ that contain
a complex variety of steps. The jQuery library is like a _shareable_ set of
JavaScript functions that wrap many complex steps into a simple, easy to use
package. The simplicity and wide compatibility is what has made jQuery shine!

Before we dive deeper into jQuery itself, let's first consider a crucial concept
that it assists with: _selecting DOM elements_.

Up until now, we've been working with plain old JavaScript by itself (aka
"vanilla JavaScript"). If we wanted to select the body tag, we'd do something like this:

```js
document.querySeletor("body");
```

What if we could make that a bit shorter, while also maximizing cross
compatibility with older browsers? A win-win! jQuery was created as a way to
make DOM manipulation quick and painless. jQuery, syntax is very similar to CSS
selectors — we can wrap these selectors (which are just strings) inside of `$()`.
It's as easy as this!

```js
$('body')
```

As another example, lets say we wanted to grab all the 'img' tags from a page.
In JavaScript, we would use a different method, `querySeletorAll` like so:

```js
document.querySeletorAll("img");
```

This would get us a collection of all the image tags
on a page. But in jQuery, we still can just use:

```js
$('img')
```

**NOTE:** These selection examples should be shown in real time (with the Chrome Developer Console), preferably on a website the students are familiar with! 

Technically, our JavaScript and jQuery return two different types of
collections, but they both act very much like arrays and can be treated as
though they are.

It's clear that jQuery makes things easier for us. We'll take a look at
additional selectors below. When more complex actions are required, jQuery
becomes even more valuable. The jQuery syntax is tailor-made for **selecting**
HTML elements and performing some **action** on the element(s).

Basic syntax is: `$(selector).action()`

- A `$` sign to define/access jQuery
- A (*selector*) to "query (or find)" HTML elements
- A jQuery *action*() to be performed on the element(s)

You'll see `$` a lot — every line of jQuery code should start with the `$`, so
get familiar with it!


## Using jQuery

Let's say you have a really basic webpage with a blue square. The HTML could
look something like this:

```html
<!--index.html-->
<!doctype html>
<html>
  <head>
    <title>Box</title>
    <!-- links to CSS and fonts here -->
  </head>
  <body>
    <h1>Box</h1>
    <div id="square">
      <div id="close-square"><i class="fa fa-times"></i></div>
      <h2>Welcome to the site!</h2>
    </div>
    <div class="content">
      <p>Lorem ipsum...</p>
      <p>Nulla eget sem...</p>
      <p>Integer efficitur...</p>
    </div>
    <!-- add JavaScript's jQuery library here -->
    <!-- add custom JavaScript here -->
  </body>
</html>
```

And when rendered in the browser, the page looks like this:

![blue welcome box on top of
text](http://web-dev-readme-photos.s3.amazonaws.com/js/intro-to-jquery/blue-box.png)

**NOTE:** The starter html has been provided in this repository. `open index.html` to display it in the browser for the students. 

While it's nice to greet the users, we don't want that box to stay there for
*forever*. Our job is to make that blue welcome box fade after the page is
loaded using jQuery. 

The first step to accomplishing this challenge is to load jQuery on the page.
What we mean by this is that, to make use of the jQuery code, we have to make
sure the code was sent to the browser along with the website itself. We can see
easily see that 

**NOTE:** While tempting to show the students that, by default, the jQuery library is not loaded with websites, Chrome has automatically provided a `$()` alias around `document.querySeletor`. This means typing `$('img')` will provide a valid return that looks very much like jQuery is working :(. Instead, consider showing an attempt to use a specific jQuery library method before we get into the next section. It will throw error, and we get to display to the students the before and after effect of importing the library. For our sample page, `$('img').mouseup()` will do the trick. After we import the library, attempt the function again and compare the response in the console.

#### Loading jQuery

The first step is to include a link to the jQuery library so we can use it.
We'll let Google host our jQuery library. (To see all the JavaScript libraries
that Google hosts, take a look at [this
site](https://developers.google.com/speed/libraries/).) It's [best
practice](http://stackoverflow.com/a/5046472/2890716) to put this script tag
right before the body of the page ends (right before the `</body>` tag).

```html
      <!-- ... -->
    </div>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <!-- add custom JavaScript here -->
  </body>
</html>
```

To check that you loaded jQuery correctly, you should be able to open up your
browser's console (`command ⌘` + `option` + `J` if you're using Chrome). To be
sure that your imported the library, invoke a specific jQuery function or the module itself (i.e.
`jQuery`) and assert that it is not throwing error/undefined:

![correctly loaded
jQuery](https://curriculum-content.s3.amazonaws.com/KWK/with-without-jquery.png)

**NOTE:** Though, by default, Chrome has a function named `$()`, after you import jQuery the `$` will act as an alias for it. You can see this because the return value of simply typing `$` is different before and after jQuery is imported. 

#### Selecting Elements

We've already touched on basic JavaScript selectors. Now let's explore how
jQuery makes manipulating DOM elements much easier. While it has tons of
specialized selector functions built in, (including, but not limited to:
last-child, nth-type-of, next sibling, input selector), we will explore the most
commonly used ones. Take a look at the [MDN
docs](https://api.jquery.com/category/selectors/) for a full list.
[Here's](https://www.w3schools.com/jquery/trysel.asp) a terrific site to try
some out.

Now that we've loaded the jQuery library, the next step is to use jQuery as a
communicator with the DOM: "Hey, we want to do something with that blue box!".
Since the box has an id of `square`, we can target it with CSS using the hash
symbol like so: `#square`. To tell JavaScript we're using the jQuery library, we
prefix our code with the dollar sign: `$`. Then we'll pass jQuery a parameter of
the id we want to target wrapped in quotes:

```js
$("#square")
```

To see what this jQuery returns, we'll open our browser's console (remember
the keyboard shortcut is `command ⌘` + `option` + `J` for Chrome) and run the
code. The return value will be the browser's representation (also known as the
*DOM object*) of the blue square:

![dom blue
square](https://curriculum-content.s3.amazonaws.com/KWK/jquery-element-return.png)

Woah! What are we actually seeing here? jQuery has returned to us an object.
Albeit built-up, this plain old JavaScript Object has a lot of quality-of-life
properties and functions attached to it. For example, if we wanted to get the
actual text inside of the element's tags, we could call: `$("#square").text()`!

Let's put this JavaScript directly in our `index.html` file, where we will
sandwich this code between two `<script>` tags. It is important to put this code
_after_ loading jQuery, since it relies on that library:

```html
    <!-- ... -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script>
      $("#square") // we'll add code here in the next section, as the selector by itself isn't useful
    </script>
    <!-- ... -->
```

With jQuery, we can select tags directly, as is the case when we use `$('body')`
or `$('img')`. We've also seen here that we can select elements by _id_, by
writing a `#` in front of the id name, like this: `$('#square')` (just like it
would be written in a CSS file. Any guess how we would select by class? Just
like CSS, we can get elements by class name by adding a `.` in front of the
name: `$('.<className>')`

#### Adding Behavior to Elements

Okay, so we've loaded jQuery and used it to select an element on our page but we
haven't done anything with the element we now have. As an example, let's assume
we want the element to slowly disappear from view.  Thankfully, jQuery has this
functionality built in! The function we want to use is called `fadeOut()`, docs
[here](http://api.jquery.com/fadeout/). This function accepts several parameters
and one is the length of time that the animation should take in milliseconds.
Two seconds sounds reasonable so we'll call `fadeOut(2000)` on the blue square
element we selected:

```html
    <!-- ... -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script>
      $("#square").fadeOut(2000)
    </script>
    <!-- ... -->
```

**NOTE:** You can also run this in Chrome Console to show the function in action that way. 

Awesome! When the page is loaded, the blue box fades completely after two seconds. It should transition from opaque to transparent:

![faded blue box](http://web-dev-readme-photos.s3.amazonaws.com/js/intro-to-jquery/faded.png)

So much better than having it hang there for eternity, isn't it? There are a ton of
other effects that jQuery has functions for, just take a look at [the effects
list](https://api.jquery.com/category/effects/).


#### Events

Sites respond to user actions in many ways. From a user perspective, think of a menu expanding downwards when you click on a header, or an element changing tint when you hover over it. From a code perspective, two main things occur:
  - the program fires an 'event', such as "Hey this element was hovered over!" or "A user clicked on this element!"
  - the program then runs some function that it knows should be executed whenever the event is fired, such as "fade out the element attached to the event"

In JavaScript, these kind of things are called **DOM events** and the code
written to trigger the action is called an **event listener** or **event
handler**. Let's implement an **event handler** for when an element is clicked
now.

###### On Click Event Handler

Often, instead of the box fading out on its own, you have to click on the `x` to
close it. Our second challenge is to do just this and make the box disappear
when the user clicks on a little `x` located on the element. To accomplish this
task, we'll be using jQuery's ['on' handler](http://api.jquery.com/on/). We will
need to:
  - Identify the element we want the listener to be on
  - Attach an **event listener** for clicks on the element
  - Provide some code to run when the element is clicked

The first thing we need to do is identify the element we want to listen for clicks on. Take a look at `index.html`. 

**NOTE:** Now is a good time to query the students to see if they can tell you how the jQuery call should be written. 

We are after the 'x' element, which has an id of `#close-square`. Using jQuery, we can capture this easily.  

```html
<script>
  var el = $("#close-square")
</script>
```

Now that we have the element in hand, we need to attach that event listener.
jQuery provides us with the `element.on()` function to do just this. The `on()`
event handler's first parameter is the event, it should answer the question, "On
*what*?". Since we are interested in the user clicking the `x`, we'll use the
string "click" as the first argument. There are other events, to see all of
them, take a look [at this
list](https://developer.mozilla.org/en-US/docs/Web/Events). The second parameter
we'll pass to `on()` is a function, which we'll augment in a minute:

```html
<script>
  var el = $("#close-square")
  
  function doOnClick() {
    console.log("x was clicked!")
  }
  
  el.on("click", doOnClick)
</script>
```

**NOTE:** Make sure to execute this step, showing the log in the Chrome Console. 

When the user clicks on the square, we want the blue box to fade out just like before. Let's put that in the function we are affixing to the event listener!

```html
<script>
  var el = $("#close-square")

  function doOnClick() {
    console.log("x was clicked!")
    $("#square").fadeOut(2000)
  }

  el.on("click", doOnClick)
</script>
```

Cool! Now the blue box stays on the page until the user clicks the little `x` in
the top-right corner of it.

#### Separating JS From HTML

While adding small snippets of JavaScript directly to an HTML page using
`<script>` tags will do the job, it's a better practice to keep the JavaScript
in a separate file instead. If we liked, we could create an `index.js` file with
this code, then simply import that with out HTML instead of having it directly
in the file.

```javascript
// index.js
var el = $("#close-square")

function doOnClick() {
  console.log("x was clicked!")
  $("#square").fadeOut(2000)
}

el.on("click", doOnClick)
```

Now we'll link to this file:

```html
    <!-- ... -->
    </div>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
    <script src="index.js"></script>
  </body>
</html>
```

And BOOM! Everything is still working as intended and we have the benefit of
modular code. Keeping stylesheets and JavaScripts separate from your HTML is a
great habit to get into. 

## Reading Errors in the Browser

The console is a great place to start if your JavaScript code is
behaving differently than you might expect. Often the browser will reveal
syntax errors through printouts to the browser's console. They could look like
`TypeErrors`, `SyntaxErrors`, etc. Here's an example:

```
Uncaught SyntaxError: Unexpected token '}' index.js:8 
```

Make it a habit to use the console to do error handling. It may seem tedious at
first, but as you grow as programmers you will find error messages incredibly
informative and second nature to read. With a little bit of practice, you won't
even _actually_ read them anymore. You will find your eyes snapping to the error
type, the message, the line number, and then returning to your code to fix the
problem. Above, we see **SyntaxError**, **Unexpected blah blah... '{' (is what I
really want)**, **line 8 in index.js**. 
