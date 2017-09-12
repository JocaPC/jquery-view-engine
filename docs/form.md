[Home](../README.md)

# Populating form elements with JQuery View Engine

**[JOVN](../README.md)** enables you to easily populate elements of a HTML form using data in a JavaScript objects (models).

First, you need to put a plain HTML code in your page that represents an empty form that you want to show:

```html
<form id="companyForm" method="post">
    <input type="hidden" name="ID"></input>

    <label for="Name">Name</label>
    <input name="Name" type="text"/>

    <label for="Address">Address</label>
    <textarea name="Address" rows="3" cols="10"></textarea>

    <label for="Town">Town</label>
    <select name="Town">
        <option value="London">London City</option>
        <option value="Liverpool">Liverpool City</option>
        <option value="Lothian">Lothian City</option>
        <option value="Newcastle">Newcastle City</option>
        <option value="Buckinghamshire">Buckinghamshire City</option>
        <option value="Essex">Essex City</option>  
    </select>

    <label for="Region">Region</label>
    <select name="Region" id="Region">
    </select>
</form>
```

This template is a pure HTML form without any custom attributes or placeholders. Any HTML/CSS designer can modify this code without any problem.
Every element in the HTML form has a `name` (or `id`) attribute. **JOVN** use this convention to populate elements in the form.

The following JavaScript code can fill the form above:

```javascript
// Fill options in #Region SELECT list:
$("#Region").view(["North","West","South","East"]);

// Prepare object that will be shown in the form
var company = {
    ID:17,
    Name:"Emkay Entertainments",
    Address:"Nobel House, Regent Center",
    Town:"Lothian",
    Region:"East"
};

// Fill form with data in the model object
$("form#companyForm").view(company);

```

Some elements such as `SELECT` might have options that are statically embeded in HTML, while other need to be dynamically populated. In the example above, Region list is initially empty, and we can use it as a template and populate it using `$("#Region").view(["North","West","South","East"])`. This code will fill the select list with the four values in the array. 

In order to bind JSON object to the form, you would need to put names or id attributes of the form elements that matches the properties in JSON object. **JOVN** uses this convention to bind elements.

When we apply a view() function on a template and provide an object that should be bound as an argument, **JOVN** will go through the properties of the object, find the matching elements in the form and populate them.

**JOVN** will analyze each type of the input and decide how to populate it (for example it will set the value of text inputs, check the checkboxes, select options in the lists or radio buttons by name.) This way, the common logic that we use to manually populate elements depending on a type is built-in into the view engine.

See live demo of the complex form with different HTML elements that is populated using **JOVN** view engine in [this example](../examples/edit.html).

[Home](../README.md)