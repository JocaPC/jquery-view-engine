# JOVN - JQuery Ordinary View eNgine

Do you need just a simple, ordinary view engine that will bind JSON data to the HTML view? 
**JOVN** is probably the simplest possible JavaScript View Engine that you can find, and I hope that next-gen view engines will follow this usage pattern. **JOVN** has the following characteristics:

-   **Easy to learn** – There are no custom syntax, placeholders, rules, or constraints. If you know HTML, then you probably already know how to use this view engine.
-   **Unobtrusive** - you don't need to mix pure HTML code with some custom directives. You can bind data to view using ordinary classes, names, and id attributes. The goal is to have full separation of pute UI code from actions.
-   **Smart** - has built-in logic that automatically recognizes template elements by type and figure-out how to populate values into the elements. It knows when to set inner text, value, select the option, or repeat the template without some explicit **for** directive.
-   **Cross-browser** - it is based on JQuery library, so it will work on any browser that is supported by JQuery.
-   **Small** - 1.2KB minified.

There are no frameworks, or custom templating syntax. Just write the standard/plan HTML code that you want to show in the browser, take your JavaScript object that contains data and bind them.

> This might be perfect choice if you are using some templates such as [bootstrap](https://getbootstrap.com). You can take original templates from bootstrap examples, place them in your page and just bind data to them without any modification in the original template code.

**JOVN** is something that I see as the right way to design client-side view engine from the **front-end developer perspective**. I believe that a view engine needs to be simple and easy to learn because it is not an *equation solver*, it should handle all tedious rules for binding that we constantly use in the scripts, and it should make our life easier.

First, you need a plain HTML that represents a template:
```html
<div id="template">
    <h1 id="Name"></h1>
    <label>Description:</label>
    <textarea name="Desc"></textarea>
    <ul>
        <li class="bind-Tags"></li>
    </ul>
</div>
```

You need a **minimal time** to learn how to use **JOVN** template language because it is plain/well-known HTML. There are no placeholders such as **&#123;&#123;Name&#125;&#125;** or **&lt;% Name %&gt;**, and no restriction in HTML such as forbidden attributes.
If you have HTML/CSS specialist who create HTML code/prototype - you can directly use their code as a template without rewriting. Also, HTML/CSS designers completely unfamiliar with JavaScript/front-end development can directly change the template.

Once you define a template, you need a JavaScript object that will be used to populate it:
```javascript
{   Name: "JOVN",
    Desc: "The simplest view engine",
    Tags: ["View engine", "JavaScript", "SPA"]
}
```
This can be local JavaScript variable or object fetched from REST API via Ajax call.

The result that you would like to see is:
```html
<div id="template">
    <h1 id="Name">JOVN</h1>
    <label>Description:</label>
    <textarea name="Desc">The simplest view engine</textarea>
    <ul>
        <li class="bind-Tags">View engine</li>
        <li class="bind-Tags">JavaScript</li>
        <li class="bind-Tags">SPA</li>
    </ul>
</div>
```

**JOVN** is a view engine that enables you to do this with a single line of code:
```html
 $("div#template").view(data);
```
**JOVN** will handle various types of HTML elements, populate inner text of `P`, `DIV`, `SPAN`, and other simple elements, set the value `INPUT`, `SELECT`, and other form elements, replicate HTML elements that are bound to the arrays, etc. 

See the live example on [jsFiddle](https://jsfiddle.net/jocapc/4rzv83vt/).

This is the view engine that will do all binding magic for you and require minimal effort to use it.

## Why yet another view engine?

A long time ago, long before Angular, React and other templating engines, I needed a quick way to take JSON object via AJAX call and show it in the client side. I created a small library that loads JSON objects into HTML.

Then AngularJS appeared, and I really liked it. I thought that Angular will be the solution for client-side templating and single-page applications (and to be honest it is in the most cases). Then Angular 2 appeared that became too heavy framework for my use cases. Yeah, it is great, but in some cases, it is too complex for some simple tasks.

I looked at ReactJS and I initially liked the idea, but in some cases JSX syntax and mixing JavaScript and HTML in the same place is not something that I would use to simply bind the object to HTML code.

With respect to Mustache, Vue.js, and other alternative templating engines - I really need something simpler. Therefore, I decided to write a simple view engine for a simple use case.

The question is - why we need a custom templating syntax? I believe that HTML is in most of the cases sufficient to describe template, so I wanted to use standard HTML as a view template. This is idea behind **JOVN** view engine - let's use plain HTML to define view template and just bind the object into the view to show the data.

Also, why would we need custom attributes like for to tell the view engine that it should bind elements from array into the list or table? If the source is an array, view engine should be smart enough to figure out that array should be replicated in list (unfortunately most of the view engines are not so smart). 

Finally, do you hate when you need to populate form elements and then you set `value`, `checked`, `selected` and other properties in each input field depending on the type. Would it be nice just to say that you want to put value “Hello” into an element with some id, and let view engine figure out how to place it?
**JOVN** do exactly this magic. Whenever it finds some form input, it will look at the type and automatically determine should it set the `value`, `inner text`, `checked` property, etc.

So, I wrote this view engine because I needed simplicity.

The only prerequisite is [JQuery library](https://jquery.com/) that is used to bind object into HTML template.

## How to obtain this library?

**JOVN** is a single JavaScript file that you can download from the GitHub project:
 - Full [source code]https://github.com/JocaPC/jquery-view-engine/blob/master/src/jquery.view-engine.js).
 - [Minified 1.2KB](https://github.com/JocaPC/jquery-view-engine/blob/master/src/jquery.view-engine.min.js.gz) version.

 Once you take one of these files just include it into your HTML page. You would also need to include [JQuery library](https://jquery.com/) in your page.

## See also
 - [Using View Engine](usage)
 - [Populating HTML form](form)
 - [Populating HTML lists](iterators)