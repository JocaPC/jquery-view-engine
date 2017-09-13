[Home](../README.md)

# Populating lists with JQuery View Engine

**[JOVN](../README.md)** is a view engine that enables you to easily load JavaScript objects into pure HTML templates. One of the key differences between **[JOVN](../README.md)** and other view engines is the technique that binds arrays to the HTML elements.

Most of the view engines have some special directives or custom attributes that you need to put into the template to instruct view engine to clone a template element for each object in an array. As an example, Angular has `*ngFor` attribute that you need to put into the HTML element that should be repeated, and the value of this attribute is some "expression" that iterates trough the array of objects:

```html
<ul>
    <li *ngFor="let hero of heroes">
        &#123;&#123;hero&#125;&#125;
    </li>
</ul>
```

Unlike Angular, **JOVN** don't have expression syntax that iterates trough the arrays. You just need to put an HTML element that will be target for every array element, and put a CSS class in the format `bind-<<arrayName>>`, like in the following example:

```html
<ul>
    <li class="bind-heroes"/>
</ul>
```

If we bind an array named `heroes` to this `li` element, **JOVN** will check the type of the input object, and since it is an array, it will automatically replicate `li` element for each array element.

In the following Angular example, we have more complex HTML list:

```html
<ul>
    <li *ngFor="let hero of heroes">
        <span class="badge">&#123;&#123;hero.id&#125;&#125;</span> <span>&#123;&#123;hero.name&#125;&#125;</span>
    </li>
</ul>
```

The equivalent in **JOVN** would look like:
```html
<ul>
    <li class="bind-heroes">
        <span class="badge bind-id"/> <span class="bind-name"/>
    </li>
</ul>
```

Class `bind-heroes` would be used to bind `heroes` array to `li` element. Within each `li` element we have two `span` elements that would be used as the targets for `id` and `name` objects in each object of `heroes` array.

As you can notice, there is no custom syntax or directives. If the elements are properly matched with the array elements, **JOVN** will automatically clone HTML element for each array element.

You can find few additional examples here:
 - Binding array of companies to a [list](../examples/list.html),
 - Binding array of companies to a [table](../examples/table.html).

[Home](../README.md)


