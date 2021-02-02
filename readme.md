# imimobile front end test

Thank you for agreeing to take part in the imimobile front end developer practical assessment.

## The brief
This exercise will test the following skills.

* Your eye for detail and accuracy
* Your ability to learn to work with tools you've never likely worked with before.
* HTML
* Utility CSS
* Your understanding of the basics of JavaScript (types, syntax, operators, etc)
* Your knowledge of version control

### What you need to do

Please refer to the Figma file you can find here: <a href="https://www.figma.com/file/tHoMhTvo5aFEmY2Va3nHGd/Test?node-id=0%3A1" target="_blank">Figma file</a>.

You have been asked to build out a code example block for Textlocal to use as part of a marketing campaign to promote its PHP API for sending SMS. The page uses the standard landing page template, and so the header, hero, and footer are provided pre-built. These contain examples of how we write HTML, and use Tailwind, and Alpine, so please review them before starting to write any code.

Please add your code where you can see the `<!-- Code goes here -->` line. You do not need to make any admendments to the code already provided.

We have provided the three code examples you will need. There are three; POST, GET, and Class. These are pre-marked up and should not be change. You will find them in the `partials/php` folder.

The only things you need to build are the heading, subcopy, link to documents (just use `href="#"` for any links), buttons, and the logic to display each code snippet.

In the html element, you will see one called `method: 'post'`. This is the AlpineJS key you will use for the button toggles. Please look at how we have built the country selector to get an understanding how this works. Alternatively, you can review the Alpine JS documentation with the tabs example.

Please use version control. If you do not know how to use version control, please note that you do not when you return the example. Please do not push back up to the example. Create your own repo and provide a link to the test.

## The tools we use

### Statamic

We use a CMS called Statamic. It simplifies creating front ends for websites, as it abstracts any PHP away from you. Instead you work with a templating language called Antlers.

Don't worry too much about this, as this test is focused 100 per cent on your knowledge of HTML, CSS, and JS.

### Tailwind CSS
Tailwind CSS is a utility-first CSS framework. It’s goal is to solve two of the biggest problems of writing CSS.

The first is that naming things is hard. By removing the need to think about what to call a class, it allows you to focus fully on the properties and values you need to use.

The second is that as CSS code bases become larger, they become exponentially more difficult to maintain. They also become much harder to amend and add to, without introducing bugs. Throw in a team of developers at varying levels of experience of CSS and the code base itself, and it can become difficult to work with in as little as six months. After as little as 12 months, it can become impossible to make changes without knowing if it will impact a different part of the website to the one you’re working on. This ends up requiring extensive testing, or there is a risk of introducing bugs which may remain hidden for months, or even years.

#### Writing utility CSS
Instead of using class names that describe what you’re building (known as semantic CSS), like button, with utility CSS, you use small repeatable classes that describe what the class does. For example, let’s say you’ve been asked to build a button. If you’ve never used utility-first CSS, you might be used to writing them like in Figure 1.

```css
.button {
  align-items: center;
  background-color: #415afb;
  border-radius: 8px;
  color: #ffffff;
  cursor: pointer;
  display: flex;
  font-size: 14px;
  font-weight: 900;
  justify-content: center;
  line-height: 16px;
  padding: 12px 16px;
  transition: color 150ms ease-in-out;
}

.button:hover,
.button:focus {
  background-color: #263597;
}
```
*Figure 1. An example of traditional written CSS.*

In more advanced CSS methodologies (e.g. BEM), you might separate out certain properties and values to avoid overriding them during rendering, or to avoid issues with specificity (see Figure 2).

```css
/* The base button class */
.button {
  align-items: center;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  font-size: 14px;
  font-weight: 900;
  justify-content: center;
  line-height: 16px;
  padding: 12px 16px;
  transition: color 150ms ease-in-out;
}

/* Blue button classes */
.button--blue {
  background-color: #415afb;
  color: #ffffff;
}

.button--blue:hover,
.button--blue:focus {
  background-color: #263597;
}

/* Teal button classes */
.button--teal {
  background-color: #66e5e1;
  color: #ffffff;
}

.button--teal:hover,
.button--teal:focus {
  background-color: #3c8986;
}
```
*Figure 2: An example of an advanced CSS methodology approach to preventing CSS specificity and overrides.*

The idea behind this approach is that by identifying what might change – and separating them into their own modifier classes – you can keep CSS classes small and avoid the complexity that often arises in larger codebases.

#### Coding the same button, but with utility CSS
In utility CSS, we use small class names that are linked to the property and value you want to apply to the HTML element. For example, padding is often shortened to p. You then add the amount of padding you want to apply.

In Tailwind, we use a scale of 1:4. I.e. 1 in Tailwind, is equal to 4px. So 4 in Tailwind is 16px, and 10 is 40px. This is because Tailwind uses REM values, which can easily be split into four (0.25rem = 1px). On the whole, all of our designs (with the exception of some utilities such as font sizes and max-widths) stick to this 4 times scale.

To give you an example, let’s look at the padding in that button. In the example above, we applied padding: 12px 16px, which is short hand for 12px on the top and bottom, and 16px left and right.

Let’s compare how padding would be applied in semantic CSS, and in utility CSS (using Tailwind’s 4x scale).

```html
<!-- Semantic CSS -->
<a href="/link" class="button button--blue">This is a link button</a>

<!-- Utility CSS (padding only) -->
<a href="/link" class="py-3 px-4">This is a link button</a>
```

Because the two values are different, we use two different classes. To more easily understand what is going on here, let’s look at the code that Tailwind generates for these two classes:

```css
/* 1rem = 16px */

.py-3 {
  padding-top: 0.75rem; /* 12px */
  padding-bottom: 0.75rem;
}

.px-4 {
  padding-left: 1rem; /* 16px */
  padding-right: 1rem;
}
```

If we take the rest of the button class properties and values, and we convert them to Tailwind classes, you'll end up with something that looks like this:

```html
<a href="/link" class="align-center bg-blue-500 rounded-md text-white cursor-pointer flex text-sm font-extrabold justify-center leading-4 py-3 px-4 transition-color duration-150 ease-in-out">This is a link button</a>
```

This equates to:

```css
.button {
  align-items: center; /* align-center */
  background-color: #415afb; /* bg-blue-500 – the number is defined in the config */
  border-radius: 8px; /* rounded-md */
  color: #ffffff; /* text-white */
  cursor: pointer; /* cursor-pointer */
  display: flex; /* flex */
  font-size: 14px; /* text-sm */
  font-weight: 900; /* font-extrabold */
  justify-content: center; /* justify-center */
  line-height: 16px; /* leading-4 */
  padding: 12px 16px; /* py-3 px-4 */
  transition: color 150ms ease-in-out; /* transition-color duration-150 ease-in-out */
}
```

### Responsive classes

Every utility class in Tailwind can be applied conditionally at different breakpoints, which makes it a piece of cake to build complex responsive interfaces without ever leaving your HTML.

For example, if you wanted to make the button's padding slightly larger at a medium breakpoint (768px and above), you can write the following:

```html
<a href="/link" class="py-3 px-4 md:py-4 md:px-6">This is a link button</a>
```

This is the same as:

```css
/* 1rem = 16px */

.py-3 {
  padding-top: 0.75rem; /* 12px */
  padding-bottom: 0.75rem;
}

.px-4 {
  padding-left: 1rem; /* 16px */
  padding-right: 1rem;
}

@media (min-width: 768px) {
  .py-4 {
    padding-top: 1rem; /* 16px */
    padding-bottom: 1rem;
  }

  .px-6 {
    padding-left: 1.5rem; /* 24px */
    padding-right: 1.5rem;
  }
}
```

You can read more about Tailwind CSS by <a href="https://tailwindcss.com/docs" target="_blank">clicking here</a>.

## AlpineJS

AlpineJS is a small JavaScript library that allows you to easily add behaviour a website.

It makes it simple to add functionality that would normally require a lot of JavaScript, or a much heavier framework like Vue or React.

For example, in the test, you need to build an accordion.

Let's say you have a simple structure like below:

```html
<div>
  <button>Tab One</button>
  <div>
    <!-- Tab One -->
  </div>
  <button>Tab Two</button>
  <div>
    <!-- Tab Two -->
  </div>
  <button>Tab Three</button>
  <div>
    <!-- Tab Three -->
  </div>
</div>
```

We can use the `x-data` property on the div that wraps the accordion. Inside this, we'll define the default 'state' of the accordion. As per the design, this is the first tab. 

*Note: Alpine uses `x-` to namespace the data event and prevent another tool from accidentally activating it, or overriding it.*

As such, we'd do something like:

```html
<div x-data="{ tab: 'one' }">
  <button>Tab One</button>
  <div>
    <!-- Tab One -->
  </div>
  <button>Tab Two</button>
  <div>
    <!-- Tab Two -->
  </div>
  <button>Tab Three</button>
  <div>
    <!-- Tab Three -->
  </div>
</div>
```

This tells Alpine that the default 'tab' to be open is one. Tab doesn't have to be called tab, of course, but in this context, it makes sense.

Next, we need a way to tell Alpine what button you've clicked, and as such, which tab you want to be visible.

This can be achieved using the `@click` property. This tells Alpine to do something when it is clicked. For example, when a user clicks this button, we want the value of `tab` to change to be equal to then value of the button.

```html
<div x-data="{ tab: 'one' }">
  <button @click="tab = 'one'">Tab One</button>
  <div>
    <!-- Tab One -->
  </div>
  <button>Tab Two</button>
  <div>
    <!-- Tab Two -->
  </div>
  <button>Tab Three</button>
  <div>
    <!-- Tab Three -->
  </div>
</div>
```

Next, we need to tell Alpine which tab content to show (we don't want them all visible for example).

This can be done using the `x-show` property. It's a boolean value (i.e. true or false). If the value of `x-show` is the same as `x-data` (remember, this changes to the value of what a user select when they click on the element with a `@click` property).

This would look like:

```html
<div x-data="{ tab: 'one' }">
  <button @click="tab = 'one'">Tab One</button>
  <div x-show="tab === 'one'">
    <!-- Tab One -->
  </div>
  <button>Tab Two</button>
  <div>
    <!-- Tab Two -->
  </div>
  <button>Tab Three</button>
  <div>
    <!-- Tab Three -->
  </div>
</div>
```

### Changing the look of an element based on state (binding)

There are times where you need to bind something like the value of a class to an element based on the value of the data. Don't worry if that felt like it went whoosh over your head. Let's say you have a button. That button should have a different style if it is selected. This is where you would bind the state of the data to the button.

You can see more about the <a href="https://github.com/alpinejs/alpine#x-bind" target="_blank">x-bind feature here</a>.

One thing the docs don't explicitly show, but which is useful to know, is how to bind to a value when it isn't a boolean. Let's say you have a tab panel. You want to style all buttons, but give a different style to one that is the active button. Let's say the `x-data` property is called `tab`, and the property of the button you want to style is the string `'ford'`. You can use this approach:

```html
<a
  class="default classes go here"
  :class="{ 'active classes go here': tab === 'ford' }"
>
```

Let's say you want to make the border and text blue when the button a Ford is selected in the tab panel.

You code would look something like this:

```html
<a
  class="focus:outline-none focus:border-blue-500 flex border-2 rounded-full border-gray-300 py-2 px-4 bg-white mr-1"
  :class="{ 'border-blue-500 text-blue-500': tab === 'ford' }"
>
```

This will only apply the border-blue-500 and text-blue-500 classes WHEN the value of tab is equal to Ford. Otherwise it will be the default values defined in the class, or inherited from its parents.

### Other functionality

Toggling the display of content isn't all that Alpine is capable of. For example, it has a number of tools like adding basic animation, and data binding. Feel free to play around with it in the test if you have time.

You can read the developer docs for AlpineJS by <a href="https://github.com/alpinejs/alpine" target="_blank">clicking here</a>.