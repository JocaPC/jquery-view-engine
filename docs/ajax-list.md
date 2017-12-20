[Home](index)
# Populating lists from the AJAX calls

Did you ever need to fetch JSON data from some REST API and show the data into a web page?
**[JOVN](https://github.com/JocaPC/jquery-view-engine)** is a view engine that simplifies loading of data retrieved using 
AJAX requests into HTML pages.

Imagine that you have an API on *api/companies.js* URL that returns JSON response and that
you need to show the returned JSON array into a list on the HTML page. With **[JOVN](https://github.com/JocaPC/jquery-view-engine)** this is a simple piece of code:

```javascript
$.ajax({url:"api/companies.js", dataType:"json"})
    .done(function(response){
        $("#list").view(response);
    });
```

You don't need to dynamically generate DOM elements or install some frameworks such as Angular or React, and create complex templates. With **[JOVN](https://github.com/JocaPC/jquery-view-engine)** you just need one line of code to load JSON data from the response into an element in HTML.

# How it works?

Let's imagine that we have an API on the URL *api/companies.js* that returns the following JSON content:

```javascript
[
    {
        "ID": 1,
        "Name": "Emkay Entertainments",
        "Address": "Nobel House, Regent Centre"
    },
    {
        "ID": 2,
        "Name": "The Empire",
        "Address": "Milton Keynes Leisure Plaza"
    },
    {
        "ID": 3,
        "Name": "Asadul Ltd",
        "Address": "Hophouse"
    }
]
```
We need to load these object via AJAX call and show them in some HTML list.

We just need to define an empty list where the companies be will be placed:

```html
<ul id="list">
    <li> 
        <a href="details.html" class="bind-ID">
            <span class="bind-Name"></span>
        </a>, 
        <span class="bind-Address"></span>
    </li>
</ul>
```

We need to mark HTML elements in this template using CSS classes that match property names of JSON objects.
If JSON object has **ID**, **Name**, and **Address** properties, the target HTML elements must have **bind-ID**, **bind-Name**, and **bind-Address** CSS classes.

Once everything is setup, we just need to send AJAX request and bind data from the response into the template:

```javascript
$.ajax({url:"api/companies.js", dataType:"json"})
    .done(function(response){
        $("#list").view(response);
    });
```

**view()** method that is applied on a template will take the objects from the argument
and load every object in the list. It will match HTML elemnets in the template with the
properties by name and place the values of the JSON objects as content of HTML fields. This
method will clone <LI> items in the template and create one <LI> item for every object in the JSON array. You can find live example [here](examples/ajax-list.html).


## See also

 - [Populating HTML form](form)
 - [Populating HTML lists](iterators)
 - [Populating HTML dropdown from AJAX request](ajax-dropdown)

[Home](index)


