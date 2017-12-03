[Home](../README.md)

# Populating form elements with JQuery View Engine

**[JOVN](../README.md)** enables you to easily populate elements of a HTML form using data in a JavaScript objects (models). It is ideal solution for populating forms dynamiaclcly from a AJAX call.

Let's imagine that you have an empty HTML form in your page:
```html
<form id="companyForm" method="post">

    <input name="Name" type="text"/>

    <textarea name="Address" rows="3" cols="10"></textarea>

</form>
```
And you have a JavaScript model object fetched from some REST API:
```javascript
var model = {
    Name:"Emkay Entertainments",
    Address:"Nobel House, Regent Center"
};
```
In order to bind the object **model** to the form with id **#companyForm**, you need a **single line of code**:
```javascript
$("#companyForm").view(model);
```

**[JOVN](../README.md)** has a **view()** function that will automatically match the properties in JavaScript object (*Name* and *Address* in this example) to the form elements by **id** or **name** attributes.

#Complex example
In this example, we will load more complex form with input, textare, select list, and radio button elements. We will load two objects into this form:
 - One array that represents a list of options that will be dynamically populated, 
 - One object that will be loaded into elements of the form. 

First, we need to put a plain HTML code in a HTML page that represents an empty form that you want to show:

```html
<form id="companyForm" method="post">
    <input type="hidden" name="ID"></input>

    <label for="Name">Name</label>
        <input name="Name" type="text"/>

    <label for="Address">Address</label>
        <textarea name="Address" rows="3" cols="10"></textarea>

    <label for="Region">Region</label>
        <select name="Region" id="Region">
    </select>

    <label class="radio-inline">
        <input name="Active" type="radio" value="Active"/>Active
    </label>
</form>
```

This template is a pure HTML form without any custom attributes or placeholders. Any HTML/CSS designer can modify this code without any problem.
Every element in the HTML form has a `name` (or `id`) attribute. **JOVN** use this convention 
 to populate elements in the form.

```javascript
// Fill options in #Region SELECT list:
var listOptions = ["North","West","South","East"]);
var company = {
    ID:17,
    Name:"Emkay Entertainments",
    Address:"Nobel House, Regent Center",
    Town:"Lothian",
    Region:"East",
    Active: true
};
```

The following JavaScript code can fill the form above:

```javascript
// Fill options in #Region SELECT list:
$("#Region").view(listOption);

// Fill form with data in the model object:
$("form#companyForm").view(company);
```

Some elements such as `SELECT` might have options that are statically embeded in HTML, while other need to be dynamically populated. In the example above, Region list is initially empty, and we can use it as a template and populate it using `$("#Region").view(["North","West","South","East"])`. This code will fill the select list with the four values in the array. 

When we apply a view() function on a template and provide an object that should be bound as an argument, **JOVN** will go through the properties of the object, find the matching elements in the form and populate them.

**JOVN** will analyze each type of the input and decide how to populate it (for example it will set the value of text inputs, check the checkboxes, select options in the lists or radio buttons by name.) This way, the common logic that we use to manually populate elements depending on a type is built-in into the view engine.

See live demo of the complex form with different HTML elements that is populated using **JOVN** view engine in [this example](../examples/edit.html).

[Home](../README.md)