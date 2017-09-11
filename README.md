# JQVN - JQuery View eNgine

**JQVN** is probably the simplest possible JavaScript View Engine.
-	**Easy to learn** – There are not custom syntax, placeholders, rules, or constraints. If you know HTML, then you probably already know how to use this view engine.
-	**Smart** - has built-in logic that automatically recognizes template elements by type and figure out how to populate values into the elements. 
-   **Cross-browser** - it is based on JQuery library, so it will work on any browser that is supported by JQuery.
-	**Small** - 1.2KB minified.

There are no frameworks, or custom templating syntax. Just write the standard/plan HTML code that you want to show in the browser, take your JavaScript object that contains data and bind them.

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

You need a **minimal time** to learn how to use **JQVN** template language because it is plain/well-known HTML. There are no placeholders such as &#123;&#123; Name &#124;&#124; or `<% Name %>`, and no restriction in HTML such as forbidden attributes.
If you have HTML/CSS specialist who create HTML code/prototype - you can directly use their code as a template without rewriting. Also, HTML/CSS designers completely unfamiliar with JavaScript/front-end development can directly change the template.

Once you define a template, you need a JavaScript object that will be used to populate it:
```javascript
{   Title: "JQVN"
    Desc: "The simplest view engine",
    Tags: ["View engine", "JavaScript", "SPA"]
}
```
The result that you would like to see is:
```html
<div id="template">
    <h1 id="Name">JQVN</h1>
    <label>Description:</label>
    <textarea name="Desc">The simplest view engine</textarea>
    <ul>
        <li class="bind-Tags">View engine</li>
        <li class="bind-Tags">JavaScript</li>
        <li class="bind-Tags">SPA</li>
    </ul>
</div>
```

**JQVN** is a view engine that enables you to do this with a single line of code:
```html
 $("div#template").view(data);
```
**JQVN** will handle various types of HTML elements, populate inner text of `P`, `DIV`, `SPAN`, and other simple elements, set the value `INPUT`, `SELECT`, and other form elements, replicate HTML elements that are bound to the arrays, etc. 

This is the view engine that will do all binding magic for you and require minimal effort to use it.

## Why yet another view engine?

A long time ago, long before Angular, React and other templating engines, I needed a quick way to take JSON object via AJAX call and show it in the client side. I created a small library that loads JSON objects into HTML.

Then AngularJS appeared, and I really liked it. I thought that Angular will be the solution for client-side templating and single-page applications (and to be honest it is in the most cases). Then Angular 2 appeared that became too heavy framework for my use cases. Yeah, it is great, but in some cases, it is too complex for some simple tasks.

I looked at ReactJS and I liked it too, but in some cases JSX syntax and mixing JavaScript and HTML in the same place is not something that I would use to simply bind the object to HTML code.

With respect to Mustache, Vue.js, and other alternative templating engines - I really need something simpler. Therefore, I decided to write a simple view engine for a simple use case.

The question is - why we need a custom templating syntax? I believe that HTML is in most of the cases sufficient to describe template, so I wanted to use standard HTML as a view template. This is idea behind **JQVN** view engine - let's use plain HTML to define view template and just bind the object into the view to show the data.

Also, why would we need custom attributes like for to tell the view engine that it should bind elements from array into the list or table? If the source is an array, view engine should be smart enough to figure out that array should be replicated in list (unfortunately most of the view engines are not so smart). 

Finally, do you hate when you need to populate form elements and then you set `value`, `cheched`, `selected` and other properties in each input field depending on the type. Would it be nice just to say that you want to put value “Hello” into an element with some id, and let view engine figure out how to place it?
**JQVN** do exactly this magic. Whenever it finds some form input, it will look at the type and automatically determine should it set the `value`, `inner text`, `checked` property, etc.

So, I wrote this view engine because I need a **Magic**.

The only prerequisite is [JQuery library](https://jquery.com/) that is used to bind object into HTML template.

## Usage

To use **JQVN** you would need:
 - HTML code that will be used as template. You can use standard HTML, HTML5 elements, with your own CSS code, Twitter Bootstrap or similar.
 - JSON object that will be used as a model that populates the HTML template.

Once you have these two, you just need to convert the HTML template into the view and set the model object that needs to be bonded:

```html
 $("div#myHtmlTemplate").view(model);
```

And that's it - your model object would be placed into the template. No overcomplicating - simple solution for a simple task.

In the following sections, you can see more details on how to use it. 

> Unlike in documentation for other view engines, here you will not find intro, tutorials, how to guides, tips & tricks. This single page would probably be enough to learn everything about this view engine.

### Model object

First, we need a model object - data that we want to display to the user. Example of object that can populate template shown above is shown in the following listing: 

```javascript
var model = {
    "Name":"ACME Co",
    "Address":"Spanish Street 3, Belgrade",
    "Contact":"Phone"
}
```
This can be local object built in JavaScript code, or JSON object fetched from a web server via AJAX call.
This object has three properties (`Name`, `Address`, and `Contact`) that will be displayed in the web page.

### HTML template

Template is a **plain HTML code** where **JQVN** will place fields from the model object. Only requirement is that elements that should be populated must match the fields in model object by **id**, **name**, or **class**. An example of HTML template is shown below: 

```html
<div id="content">
    <h1 id="Name"></h1>

    <label for="Address">Address:</label>
    <input name="Address"></input> 
    
    <label for="Contact">Contact by:</label>
    <select name="Contact">
        <option value="Email"/>
        <option value="Phone"/>
        <option value="Skype"/>
    </select>
</div>
```

The `h1` tag in the template has id `Name` and it would be used to display a name. `input` and `select` tags will be used to show `Address` and `Contact` method.
Element must have `id` or `name` attributes that matches. If you want to use class you should place a class with the prefix `bind-` (for example, `bind-Address` or `bind-Contact`). **JQVN** will match elements in the template with the properties in the model object by names and set the values of the HTML elements using the data from model object.

## Binding JSON object to the template

Once HTML template and JSON object are defined, JSON object can be loaded into the HTML code. This can be achieved by using the following line of JavaScript code:

```javascript
$('div#content').view(model);
```

As a result, 'model' object will be loaded into the HTML fragment, like here:

```html
<div id="content">
    <h1 id="Name">ACME Co.</h1>
    
    <label for="Address">Address:</label>
    <input name="Address" value="Spanish Street 3, Belgrade"></input> 
    
    <label for="Contact">Contact by:</label>
    <select name="Contact">
        <option value="Email"/>
        <option value="Phone" selected/>
        <option value="Skype"/>
    </select>
</div>
```
As you can see, there are not custom {{placeholders}} or directives like in the other engines. Use pure HTML and just bind the standard JSON object into the view. 

This is a simple example, but **JQVN** can do much more such as:
 - populating list of elements from JavaScript array object - if **JQVN** finds an array of elements in the model it will replicate target HTML element in the template, which is useful for the lists, tables, etc.
 - populating any HTML input field in the form.
 
 You can find examples on the following pages:
 - Create [list](examples/list.html) of company records using a simple `UL` list.
 - Populate [table](examples/table.html) of companies and apply [JQuery DataTables](https://datatables.net/) plugin.
 - Create [panels](examples/panels.html) that show list of companies and related infomation about manager and employees.
 - Populate complex [forms](examples/edit.html) with any HTML input field.

If you want to keep it simple, **JQVN** is a view engine for you.
**JQVN** plugin works with the large number of HTML elements from plain `SPAN`, `P`, `DIV`, to various `INPUT` (text, checkbox, radio, HTML5 types), `SELECT`, `TEXTAREA`, etc.

## How to obtain this library?

**JQVN** is a single JavaScript file that you can download from the GitHub project:
 - Full [source code](src/jquery.view-engine.js).
 - [Minified 1.2KB](src/jquery.view-engine.min.js.gz) version.

 Once you take one of these files just include it into your HTML page. You would also need to include [JQuery library](https://jquery.com/) in your page.

