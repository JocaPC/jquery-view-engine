# Using JQuery Orthodox View eNgine

To use **JOVN** you would need:
 - HTML code that will be used as template. You can use standard HTML, HTML5 elements, with your own CSS code, Twitter Bootstrap or similar.
 - JSON object that will be used as a model that populates the HTML template.

Once you have these two, you just need to convert the HTML template into the view and set the model object that needs to be bonded:

```html
 $("div#myHtmlTemplate").view(model);
```

And that's it - your model object would be placed into the template. No overcomplicating - simple solution for a simple task.

In the following sections, you can see more details on how to use it. 

## Model object

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

## HTML template

Template is a **plain HTML code** where **JOVN** will place fields from the model object. Only requirement is that elements that should be populated must match the fields in model object by **id**, **name**, or **class**. An example of HTML template is shown below: 

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
Element must have `id` or `name` attributes that matches. If you want to use class you should place a class with the prefix `bind-` (for example, `bind-Address` or `bind-Contact`). **JOVN** will match elements in the template with the properties in the model object by names and set the values of the HTML elements using the data from model object.

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

This is a simple example, but **JOVN** can do much more such as:
 - populating list of elements from JavaScript array object - if **JOVN** finds an array of elements in the model it will replicate target HTML element in the template, which is useful for the lists, tables, etc.
 - [populating any HTML input field in the form](docs/form).
 
 You can find examples on the following pages:
 - Create [list](examples/list.html) of company records using a simple `UL` list.
 - Populate [table](examples/table.html) of companies and apply [JQuery DataTables](https://datatables.net/) plugin.
 - Create [panels](examples/panels.html) that show list of companies and related information about manager and employees.
 - Populate complex [forms](examples/edit.html) with any HTML input field.

If you want to keep it simple, **JOVN** is a view engine for you.
**JOVN** plugin works with the large number of HTML elements from plain `SPAN`, `P`, `DIV`, to various `INPUT` (text, checkbox, radio, HTML5 types), `SELECT`, `TEXTAREA`, etc.

## See also

 - [Populating HTML form](docs/form)
 - [Populating HTML lists](docs/iterators)