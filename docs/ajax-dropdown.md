[Home](index)
# Populating dropdowns from the AJAX calls

Here is a solution for one common problem. Imagine that you have a dropdown lis tin a form and that you need to populate the values in the list from some remote REST API.
**[JOVN](https://github.com/JocaPC/jquery-view-engine)** is a view engine that simplifies loading of data retrieved using 
AJAX requests into dropdowns pages.

Imagine that you have an API on *api/regions.js* URL that returns all regions that you need to put in some dropdown as JSON response. With **[JOVN](https://github.com/JocaPC/jquery-view-engine)** this is a simple piece of code:

```javascript
$.ajax({url:"api/region.js"})
    .done(function(response){
        $("#Region").view(response);
    });
```

Thsi is a standard code that loads data from remote API with AJAX call. the only specific thing is a line `$("#Region").view(response);` that loads the response into dropdown list with id `Region`. With **[JOVN](https://github.com/JocaPC/jquery-view-engine)** you just need one line of code to load JSON data from the response into an element in HTML.

# How it works?

Let's imagine that we have an API on the URL *api/regions.js* that returns the following JSON content:

```javascript
["North","West","South","East"]
```

We need to load these object via AJAX call and show them in some HTML SELECT list.

We just need to define an empty list where the companies be will be placed:

```html
<form id="companyForm" >
    
    <label for="Region">Choose a region</label>
    <select name="Region" id="Region">
    </select>

</form>
```
Once everything is setup, we just need to send AJAX request and bind data from the response into the template:

```javascript
$.ajax({url:"api/regions.js"})
    .done(function(response){
        $("#Region").view(response);
    });
```

**view()** method that is applied on a SELECT list will take the objects from the AJAX response
and load every object in the list. This method will generate and clone <OPTION> nodes inside <SELECT> element for every item in the array that should be used to populate data.
DOM that will be generated looks like:

```html
<select name="Region" id="Region">
    <option value="North">North</option>
    <option value="West">West</option>
    <option value="South">South</option>
    <option value="East">East</option>
</select>
```
**[JOVN](https://github.com/JocaPC/jquery-view-engine)** will use strings from that array to populate value and text of the generated <OPTION> nodes. You can find live example [here](examples/ajax-list.html).

# Complex example
In the previous, basic example, we have used simple string array to populate dropdown. This structure loads the same values both as options that are shown to user, and the values that will be sent to server.

However, in many cases you will to have different key/value pairs in the list and you might need to have one option pre-selected. **[JOVN](https://github.com/JocaPC/jquery-view-engine)** also supports this use case.

Your API needs to return the array of objects with the following properties:
 - `text` the value that will be shown to the user.
 - `value` the value that will be stored in `value` attribute.
 - `selected` if the current option should be preselected.

An example of this response is shown in the following code:
```javascript
[
    {"text":"North","value":"N"},
    {"text":"West","value":"W"},
    {"text":"South","value":"S","selected":true},
    {"text":"East","value":"E"}
]
```
Once you load this object into an empty list using `$("#Region").view(response);`, you will see the following DOM:
```html
<select name="Region" id="Region">
    <option value="N">North</option>
    <option value="W">West</option>
    <option selected="selected" value="S">South</option>
    <option value="E">East</option>
</select>
```

## See also

 - [Populating HTML form](form)
 - [Populating HTML lists](iterators)
 - [Populating HTML lists from AJAX request](ajax-list)

[Home](index)


