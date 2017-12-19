# JOVN - JQuery Orthodox View eNgine

**JOVN** is probably the simplest possible JavaScript View Engine that you can find, and I hope that next-gen view engines will follow this usage pattern. **JOVN** has the following characteristics:

-   **Easy to learn** – There are not custom syntax, placeholders, rules, or constraints. If you know HTML, then you probably already know how to use this view engine.
-   **Smart** - has built-in logic that automatically recognizes template elements by type and figure-out how to populate values into the elements. It knows when to set inner text, value, select the option, or repeat the template without some explicit **for** directive.
-   **Cross-browser** - it is based on JQuery library, so it will work on any browser that is supported by JQuery.
-   **Small** - 1.2KB minified.

There are no frameworks, or custom templating syntax. Just write the standard/plan HTML code that you want to show in the browser, take your JavaScript object that contains data and bind them.

**JOVN** is something that I see as the right way (or **Orthodox** - from Greek *ὀρθοδοξία*, orthodoxia – "right opinion") to design client-side view engine from the **front-end developer perspective**. I believe that a view engine needs to be simple and easy to learn because it is not an *equation solver*, it should handle all tedious rules for binding that we constantly use in the scripts, and it should make our life easier.

**JOVN** is a view engine that follows MVC concepts
 1. You need to prepare pure HTML in your page that represents a template that will be used to show the data,
 2. You need to prepare JavaScript object that represents the model that will be shown in the template,
 3. You need to convert template into the view and provide model object that will be shown in the template:

```html
 $("div#template").view(data);
```

**JOVN** will handle various types of HTML elements, populate inner text of `P`, `DIV`, `SPAN`, and other simple elements, set the value `INPUT`, `SELECT`, and other form elements, replicate HTML elements that are bound to the arrays, etc. 

If you like the concept see more detaile [HERE](https://jocapc.github.io/jquery-view-engine/)