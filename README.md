# Flexbox Simplified

This repository summarizes the most important concepts of flexbox. It is based on multiple tutorials and articles, attempting to condense the most practical use cases of flexbox for future reference.

## Table of Contents

- [Flexbox Simplified](#flexbox-simplified)
  - [Table of Contents](#table-of-contents)
  - [Cheat Sheets](#cheat-sheets)
  - [What is Flexbox?](#what-is-flexbox)
  - [Flexbox Properties](#flexbox-properties)
    - [Parent Properties](#parent-properties)
      - [`flex-direction`](#flex-direction)
      - [`flex-wrap`](#flex-wrap)
      - [`flex-flow`](#flex-flow)
      - [`justify-content`](#justify-content)
      - [`align-items`](#align-items)
      - [`align-content`](#align-content)
      - [`gap`](#gap)
    - [Child Properties](#child-properties)
      - [`order`](#order)
      - [`flex-grow`](#flex-grow)
      - [`flex-shrink`](#flex-shrink)
      - [`flex-basis`](#flex-basis)
      - [`flex`](#flex)
      - [`align-self`](#align-self)
  - [Even Columns](#even-columns)
  - [Space Between Columns](#space-between-columns)
  - [Fix Stretching of Flex Items](#fix-stretching-of-flex-items)
  - [Column Widths and Flexbox](#column-widths-and-flexbox)
  - [Vertical Centering with Flexbox](#vertical-centering-with-flexbox)
  - [Flexbox and `margin: auto`](#flexbox-and-margin-auto)

## Cheat Sheets

[Design Patterns](https://attachments.convertkitcdnn.com/150663/071438c9-d64f-469c-83c3-d0dd6105a3a0/useful-flexbox-patterns.pdf?utm_campaign=Landing%20Page%20or%20Form%20-%201884631&utm_medium=email&utm_source=convertkit)

[Properties](https://attachments.convertkitcdnn.com/150663/880a7521-9332-4b0e-a172-fd65f7c59e36/flexbox%20properties.pdf?utm_campaign=Landing%20Page%20or%20Form%20-%202846534&utm_medium=email&utm_source=convertkit)

## What is Flexbox?

Flexbox is a layout model that allows elements to align and distribute space within a container. It is a one-dimensional layout model, as opposed to CSS Grid, which is a two-dimensional layout model.

It's main purpose in modern CSS is to provide an efficient way to align container items on a single axis, center items within a parent, or even create spread out layouts.

To use flexbox, you must first declare a parent element as a flex container. This is done by setting the `display` property to `flex`

Consider the following HTML:

```html
<div class="row">
	<div class="item">Item 1</div>
	<div class="item">Item 2</div>
	<div class="item">Item 3</div>
</div>
```

By setting `display: flex` on the parent element, it becomes a flex container, and its direct children become flex items.

By default, its `flex-direction` is set to `row`, which means that the flex items will be laid out horizontally, from left to right.

```css
.row {
	display: flex;
	/* flex-direction: row - happens implicitly */
}
```

You'll notice that Item 1, Item 2, and Item 3 are now laid out horizontally, from left to right. Typically, `div` or block-level elements have a width of 100% by default. But flex items are different.

**Flex items want to shrink to be as small as possible.**

For example, if we change the content of the first item to be a single character, it will shrink and be even smaller than the other items. And, if we remove the content entirely, it will disappear, as it now has a width of 0.

Also, when declaring `display: flex`, it's going to try everything it possibly can to fit all of the items in a single row, even **overflowing** the container if there are too many items.

One last thing to keep in mind is that when you call `display: flex` on an element and it turns into a flex container, its default `align-items` property is set to `stretch`. This means that the items will stretch to fill the height of the container. And, in CSS, the height of a container is determined by the content inside of it.

In other words, the height of flex items will stretch to match the height of the tallest item. This is troublesome for `img` elements as they'll appear stretched.

## Flexbox Properties

Flexbox has a number of properties that can be used to control the layout of flex items within a flex container. Since it's a layout model, there are properties for the flex container or parent, and properties for the flex items or children.

### Parent Properties

#### `flex-direction`

The `flex-direction` property controls the direction in which flex items are laid out within a flex container. It can be set to one of four values:

- `row` (default)
- `row-reverse` (reverse of `row`)
- `column` (vertical)
- `column-reverse` (reverse of `column`)

By setting `row-reverse` or `column-reverse`, the items will be laid out in the opposite direction.

#### `flex-wrap`

The `flex-wrap` property controls whether flex items should wrap onto multiple lines or not. It can be set to one of three values:

- `nowrap` (default)
- `wrap` (wrap onto multiple lines)
- `wrap-reverse` (reverse of `wrap`)

By setting `wrap`, we can fix the issue of overflowing items if there are too many.

By setting `wrap-reverse`, the items will wrap onto multiple lines, but from bottom to top.

#### `flex-flow`

The `flex-flow` property is a shorthand for `flex-direction` and `flex-wrap`. Its syntax is as follows:

- `flex-flow: <flex-direction> <flex-wrap>`

#### `justify-content`

The `justify-content` property controls the alignment of flex items along the main axis. It can be set to one of five values:

- `flex-start` (default)
- `flex-end`
- `center`
- `space-between`
- `space-around`
- `space-evenly`

`justify-content: flex-start` will align the items from the left, as you'd expect.

`justify-content: flex-end` will align the items from the right.

`justify-content: center` will align the items centered horizontally.

`justify-content: space-between` will align the items so that there is equal space between each item, but not at the beginning or end.

`justify-content: space-around` will align the items so that there is equal space between each item, but the space at the beginning and end is half the size of space.

`justify-content: space-evenly` is similar to `space-around`, but the space between each item and the container edges are equal.

We can see an image below of what the various alignments look like (credit: [CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)):

![Alignment](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg)

#### `align-items`

The `align-items` property controls the alignment of flex items along the cross axis. It can be set to one of five values:

- `stretch` (default)
- `flex-start`
- `flex-end`
- `center`
- `baseline`

`align-items: stretch` will stretch the items to fill the container vertically, while respecting `min-height` and `max-height` properties.

`align-items: flex-start` will align the items from the top.

`align-items: flex-end` will align the items from the bottom.

`align-items: center` will align the items centered vertically.

`align-items: baseline` will align the items so that their baselines of text are aligned.

We can see an image below of what the various alignments look like (credit: [CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)):

![Alignment](https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg)

#### `align-content`

The `align-content` property controls is similar to `align-items` with the same values, but it controls the alignment for multi-line flex containers. It aligns the entire structure itself.

**It will have no effect on single-line flex containers.**

We can see an image below of what the various alignments look like (credit: [CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)):

![Alignment](https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg)

#### `gap`

The `gap` property is a shorthand for `row-gap` and `column-gap`. However, due to the symmetrical layouts used in modern websites, it's the go-to property for spacing between flex items.

It will only control the spacing between flex items, not including outer edges.

Its syntax is as follows:

- `gap: <row-gap> <column-gap>`

If you want to set the gap individually, you can use `row-gap` and `column-gap` instead.

### Child Properties

#### `order`

The `order` property controls the order in which flex items are laid out within a flex container.

By default, its value is `0`, meaning items are laid out in the source order, or HTML.

The higher the value, the later the item will be laid out. So, if we set the first item to `order: 1`, it will be laid out after all flex items with an `order` value of `0`.

In other words, it will be laid out last, since all other items still have a default `order` value of `0`.

#### `flex-grow`

The `flex-grow` property controls what amount of the available space inside the flex container the flex item should take up. It accepts a unitless value that serves as a proportion.

For example, if all items have a `flex-grow` value of `1`, they will take up equal space inside the flex container.

If one item has a `flex-grow` value of `2`, it will take up twice as much space as the other items.

#### `flex-shrink`

The `flex-shrink` property is like `flex-grow` but defines the ability for a flex item to shrink if necessary.

The default value is `1`, which means that the item will shrink relative to the size of the container if necessary.

If we set an item to `flex-shrink: 0`, it will not shrink.

If we set an item to `flex-shrink: 2`, it will shrink twice as much, or in half, in relation to the other items.

#### `flex-basis`

The `flex-basis` property is like `width` in that it defines the default size of an element before the remaining space is distributed.

By default, all flex items have `flex-basis: auto`, which means it will be sized based on the `width` property anyway.

However, this changes if we set the `flex-direction` to `column`.

Consider the following CSS:

```css
.container {
	display: flex;
	flex-direction: column;
}

.item {
	flex-basis: 300px;
}
```

In this case, the `flex-basis` will dictate the `height` because its based on the main axis.

Also, `max-width` and `max-height` will still take precedence over `flex-basis`.

#### `flex`

The `flex` property is a shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.

**_It is recommended to use this shorthand rather than setting the individual properties because it will set the other values intelligently._**

Its syntax is as follows:

- `flex: <flex-grow> <flex-shrink> <flex-basis>`

By default, it is set to `0 1 auto`.

If you set it with a single value, like `flex: 5`, it changes the `flex-basis` to `0%`.

So, it would be like setting `flex-grow: 5`, `flex-shrink: 1`, and `flex-basis: 0%`.

#### `align-self`

The `align-self` property controls the alignment of a single flex item along the cross axis. It allows the default aligment specified by `align-items` to be overridden for individual flex items, accepting the same values.

We can see an image below that shows an example of `align-self` in action (credit: [CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)):

![Alignment](https://css-tricks.com/wp-content/uploads/2018/10/align-self.svg)

## Even Columns

By default, flex items in a flex container will want to shrink to be as small as possible to keep everything on one line. If we have items with different content, they will have different widths, and therefore the columns will not be even.

If you want even columns in a flex container, you can do one of two things:

- Set `flex-grow: 1` on each item
- Give each item a width of 100%

```css
.item {
	flex-grow: 1;
}
```

```css
.item {
	width: 100%;
}
```

## Space Between Columns

If you want to have space between columns, you can use the `gap` property on the flex container.

```css
.container {
	display: flex;
	gap: 1rem;
}
```

If you want to specify the gap between rows and columns individually, you can use `row-gap` and `column-gap`.

## Fix Stretching of Flex Items

As mentioned, creating a flex container with `display: flex` will cause the flex items to stretch to fill the height of the container. This is because the default value of `align-items` is `stretch`. So, in other words, all flex items will stretch to match the height of the tallest item.

This can make `img` elments look distorted. There are three ways to fix this:

- Set `align-items: flex-start` on the flex container
- Set `align-self: flex-start` on the flex item
- Wrap the `img` in a `div` (this fixes it because the `div` will stretch, not the `img`)

Ideally, the second option is the best since it doesn't require any extra markup and is isolated to the flex item that needs it.

```css
.child {
	align-self: flex-start;
}
```

## Column Widths and Flexbox

With flexbox, flex items are always trying to take up the full width, or 100% of the flex container.

You might be thinking: **wait, don't flex items try to shrink as small as possible?**

While this is true, it's only if there's not enough content or if there is not enough space for the item(s) to take up the full width of the container.

So, if you have a flex container with multiple items, you can specify what proportion of the width each item should take up using `width`.

For example, if you have a flex container with two items, and you want the first item to take up 25% of the width and the second item to take up 75% of the width, you can do the following:

```css
.child-1 {
	width: 25%;
}

.child-2 {
	width: 75%;
}
```

Make sure you understand the concept here. For example, let's say you only set the width of the first child like so:

```css
.child-1 {
	width: 80%;
}
```

In this case, the second-child will actually overpower the first child and be larger (assuming there's enough content). For your intended result, you need to set the width of both children explicitly.

## Vertical Centering with Flexbox

Typically, Flexbox makes it easy to center items vertically. This is very useful as horizontal centering is usually easier in CSS with auto margins and `text-align: center`.

The reason vertical centering is easy with Flexbox is because, by default, flex items will stretch to fill the height of the container.

But what do you do in the rare occasion that `align-items: center` doesn't work?

This usually means that one of the container's ancestors has a height of `auto` and isn't a flex container.

Consider the following HTML:

```html
<div class="hero">
	<div class="container">
		<h1>Hero Title</h1>
		<p>Hero description</p>
	</div>
</div>
```

Even if you have a visual height on the `.hero` element using `padding` or `min-height`, centering the content of the container is **not** as simple as the following CSS:

```css
.container {
	display: flex;
	align-items: center;
}
```

This is because the `.hero` div has a height of `auto` and is not a flex container. So, the `h1` and `p` that become flex items will only stretch to fill the height of the `.container` div, not the `.hero` div.

To fix this, make sure all ancestors are flex containers like so:

```css
.hero {
	display: flex;
	/* min-height or padding */
}

.container {
	display: flex;
	align-items: center;
}
```

One more thing to keep in mind is the way Flexbox actually aligns content. In Flexbox, the `align-items` property aligns flex items along the cross axis. But this isn't always the vertical axis. It depends on the `flex-direction` property.

If you have `flex-direction: column` set, then `align-items` will align items horizontally because the axes are flipped. In this case, you would need to use `justify-content` to align items vertically.

## Flexbox and `margin: auto`

Flexbox makes it easy to justify content with `justify-content`. But what if you want to center a single item? Or what if you want to justify a single item to the very end of the container?

There's no `justify-self` property in Flexbox. Instead, you can use `margin: auto` or auto margins to achieve the same effect.

Consider the following HTML of a primary navigation, albeit a contrived example:

```html
<nav class="primary-nav">
	<a href="#">Home</a>
	<a href="#">About</a>
	<a href="#">Contact</a>
	<a href="#">Blog</a>
	<a href="#">Careers</a>
	<a href="#">Login</a>
</nav>
```

Let's say you want to center the first four links and have the last two links on the right side of the container. You can do this with Flexbox and auto margins like so:

```css
.primary-nav {
	display: flex;
	justify-content: center;
}

.primary-nav a:nth-child(5) {
	margin-left: auto;
}
```

Notice how we begin by centering all the links with `justify-content: center`. Then, we use `margin-left: auto` on the fifth link to push it and subsequent items to the right side of the container.

If you wanted, you could also use `margin-right: auto` on the first link to have it all the way to the left. Remember to have your `nav` or parent element take up the full width of the container for this to work.
