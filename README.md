# JQVEN - JQuery View ENgine

**JQVEN** is probably the simplest possible JavaScript View Engine. There are no frameworks, or custom templating syntax. Just write the standard/plan HTML code that you want to show in the browser, take your JavaScript object that contains data and bind them.

**JQVEN** is a view engine that enables you to do this.

## Why yet another view engine?

A long time ago, long before Angular, React and other templating engines, I needed a quick way to take JSON object via AJAX call and show it in the client side. I created a small library that loads JSON objects into HTML.

Then AngularJS appeared, and I really liked it. I thought that Angular will be the solution for client-side templating and single-page applications (and to be honest it is in the most cases). Then Angular 2 appeared that became too heavy framework for my use cases. Yeah, it is great, but in some cases, it is too complex for some simple tasks.

I looked at ReactJS and I liked it too, but in some cases JSX syntax and mixing JavaScript and HTML in the same place is not something that I would use to simply bind the object to HTML code.

With respect to Mustache, Vue.js, and other alternative templating engines - I really need something simpler.

The question is - why we need a custom templating syntax? I believe that HTML is in most of the cases sufficient to describe template, so I wanted to use standard HTML as a view template. This is idea behind **JQVEN** plugin - let's use plain HTML to define view template and just bind the object into the view to show the data.

The only prerequisite is JQuery library that is used to bind object into HTML template.

## Usage

To use **JQVEN** you would need:
 - HTML code that will be used as template. You can use standard HTML, HTML5 elements, with your own CSS code, Twitter Bootstrap or similar.
 - JSON object that will be used as a model that populates the HTML template.

Once you have these two, you just need to convert the HTML template into the view and set the model object that needs to be binded:

```html
 $("div#myHtmlTemplate").view(model);
```

And that's it - your model object would be placed into the template. No overcomplicating - simple solution for a simple task. In the following sections you can see more details on how to use it.

### HTML template

Template is a **plain HTML code**. Only requirement is that elements that should be populated must match the fields in model object by **id**, **name**, or **class**. An example of HTML template is shown below: 

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

The **h1** tag in the template has id *Name* and it would be used to display a name. input and select tags will be used to show Address and Contact method.

### Model object

Once HTML template is defined JSON object that will be used to populate template must be defined. Example of object that can populate template shown above is shown in the following listing: 
```javascript
var model = {
    "Name":"ACME Co",
    "Address":"Spanish Street 3, Belgrade",
    "Contact":"Phone"
}
```
This can be local object built in JavaScript code, or JSON object fetched from a web server via AJAX call.

Object has three properties (Name, Address, and Contact) that will be injected into the template.

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

If you want to keep it simple, **JQVEN** is a view engine for you.
**JQVEN** plugin works with the large number of HTML elements from plan SPAN, P, DIV, to various INPUT (text, checkbox, radio, HTML5 types), SELECT, TEXTAREA, etc.
