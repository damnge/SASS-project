# Learning SASS

This is assigment for Vefskolinn course, Module number 3. In this project, I've shown some useful methods in SASS like:

- Nesting
- Variables
- Used different components and connected it to the styleshit thanks to the @use and @forward method
- Created constructors with help of @mixins to avoid repetition

## Nesting Selectors

Nesting is the process of placing selectors inside the scope of another selector:

- In programming, a variable’s scope is the context in which a variable is defined and available to use.
- In Sass, it’s helpful to think of the scope of a selector as any of the code between its opening { and closing } curly brackets.
- Selectors that are nested inside the scope of another selector are referred to as children. The former selector is referred to as the parent. This is just like the relationship observed in HTML elements.
- In SCSS, nesting is not limited only to selectors. You can also nest common CSS properties if you append a : colon suffix after the name of the property.

### Nesting inside child inside parent element

```
.parent {
  color: red;
  .child {
    font-size: 14px;
  }
}
```

### Nesting CSS properties if you append a : colon suffix

```
.parent {
  font : {
    family: Roboto, sans-serif;
    size: 12px;
    decoration: none;
  }
}
```

## Variables In Sass

Variables in SCSS allow you to assign an identifier of your choice to a specific value.
Why is that useful? Unlike in CSS, if you need to tweak a value, you’ll only have to update it in one place and the change will be reflected in multiple rules.
In Sass, $ is used to define and reference a variable:

```
$primary-color: rgba(255,255,255,0.3);
```

## Sass(y) Types

There are different data types you can assign to a variable in CSS.
In addition to the color data type we have seen, there are also:

- Numbers, such as 8.11, 12, and 10px. Notice that while 10 has a unit of px associated with it, it is still considered a number.
- Strings of text, with and without quotes. Some examples are "potato", 'tomato', span.
- Booleans, or simply true and false.
- null, which is considered an empty value.

## Maps & Lists

In addition to color, numbers, strings, booleans, and null, Sass also has two other data types, lists and maps.

- Lists can be separated by either spaces or commas. For example, the following list denotes font properties, such as:

```
1.5em Helvetica bold;
```

or

```
Helvetica, Arial, sans-serif;
```

Note: You can also surround a list with parentheses and create lists made up of lists.

- Maps are very similar to lists, but instead each object is a key-value pair. The typical map looks like:

```
(key1: value1, key2: value2);
```

Note: In a map, the value of a key can be a list or another map.

## Modular Structure

### @forward and @use

The @forward rule loads a Sass stylesheet and makes its mixins, functions, and variables available when your stylesheet is loaded with the @use rule. It makes it possible to organize Sass libraries across many files, while allowing their users to load a single entry-point file.

The @use rule can be used to import other stylesheets as modules, the components of which can then be accessed in a modular fashion. The namespace for the module is just the last component of the path, but can be aliased using ‘as’.

## What is a Mixin?

In addition to variables and nesting, Sass has multiple constructs that reduce repetition.
In Sass, a mixin lets you make groups of CSS declarations that you want to reuse throughout your site.
The notation for creating a mixin is as follows:

```
@mixin backface-visibility {
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -ms-backface-visibility: hidden;
  -o-backface-visibility: hidden;
}
```

## Mixins: Arguments

Mixins also have the ability to take in a value.
An argument, or parameter, is a value passed to the mixin that will be used inside the mixin, such as $visibility in this example:

```
@mixin backface-visibility($visibility) {
  backface-visibility: $visibility;
  -webkit-backface-visibility: $visibility;
  -moz-backface-visibility: $visibility;
  -ms-backface-visibility: $visibility;
  -o-backface-visibility: $visibility;
}
```

In fact, you should only ever use a mixin if it takes an argument. We will learn more about this in a later exercise.
The syntax to pass in a value is as follows:
@include backface-visibility(hidden);
In the code above, hidden is passed in to the backface-visibility mixin, where it will be assigned as the value of its argument, $visibility.

## Default Value Arguments

Mixin arguments can be assigned a default value in the mixin definition by using a special notation.
A default value is assigned to the argument if no value is passed in when the mixin is included. Defining a default value for each argument is optional.
The notation is as follows:

```
@mixin backface-visibility($visibility: hidden) {
   backface-visibility: $visibility;
  -webkit-backface-visibility: $visibility;
  -moz-backface-visibility: $visibility;
  -ms-backface-visibility: $visibility;
  -o-backface-visibility: $visibility;
}
```

In the example above, if no value is passed in when backface-visibility is included, hidden would be assigned to all properties.

## Mixin Facts

In general, here are 5 important facts about arguments and mixins:

- Mixins can take multiple arguments.
- Sass allows you to explicitly define each argument in your @include statement.
- When values are explicitly specified you can send them out of order.
- If a mixin definition has a combination of arguments with and without a default value, you should define the ones with no default value first.
- Mixins can be nested.

Here are some concrete examples of the rules:

```
@mixin dashed-border($width, $color: #FFF) {
  border: {
     color: $color;
     width: $width;
     style: dashed;
  }
}

span { //only passes non-default argument
    @include dashed-border(3px);
}

p { //passes both arguments
    @include dashed-border(3px, green);
}

div { //passes out of order but explicitly defined
   @include dashed-border(color: purple, width: 5px);
}
```

Thank you for your attention! Happy building!
