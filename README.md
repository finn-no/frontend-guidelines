DRAFT

# Frontend in FINN.no

These are some guidelines for frontend code in FINN. It's meant as guidelines both when implementing, and when reviewing code.

All frontend code in FINN should follow a few principles. It should be performant, accessible, and secure, and we should aim to have good fallbacks.

One should have a good reason before breaking the rules in these guidelines.

## Performance

*(This does not cover the basics, e.g. minification and avoiding requests. It is assumed everyone is familiar with that already.)*

It is not OK for elements to jump around. That is, on first paint, elements should be in their final position with their dimensions set. Not only does it look bad when elements are jumping, it can severely destroy the performance of the site, since whenever dimensions change, the browser has to do a layout, usually across the whole document.

For things loading async, this means that space has to be reserved.

Make sure elements don't repaint on scroll...

Minimize layout...

Test the page on an old device. If it's slow: profile.

...


## Accessibility

*(This will cover the techical part of accessibility, but it also needs to be designed in an accessible way.)*

Make sure everyhing can be navigated with the keyboard, and be interacted with like native controls.

Use semantically appropriate elements whenever possible, e.g. a button is a `<button>`. Lots of accessibility comes for free when doing so.

Make sure the focus is always right. When opening a dialog, focus the dialog or an element inside of it. When closing the dialog, focus the element that opened the dialog. Libraries should handle this automatically.

Test the page in a screen reader. Make sure it reads correctly, and that it doesn't read unnecessary things (duplicate stuff, file names of imagaes, etc). For example, if you use `<hr>` for purely decorative purposes (a horizontal line), use `role="presentation"`, so that screen readers don't announce it as e.g. "separator".

Another example: In many cases, images should not have an alt text. (In some cases not even an alt attribute.) For example, the alt text in `<p><img src="profilepic.png" alt="Jane Doe"> Jane Doe</p>` is redundant and actually bad, because a screen reader would read the name twice. `alt=""` would be correct here.


## Fallback to native

For custom widgets, use native elements as fallback, or for the model. For example, a custom range slider can use two input elements with the lower and upper values as the model.

If one wants to submit a URL with some query arguments with XHR, use a `<form>`, listen for its submit event, serialize the form's elements values and submit it, and prevent the form from submitting. You get fallback for free.

## General

All icons should be SVG. If not excessively large, it should be inline, and preferably as an `<svg>` element. For fallback, a text is usually OK. It can be inside of a `<title>` element in the SVG. For example:

```
<svg ... title="Share on Twitter">
	<title>Share on Twitter</title>
	<path .../>
</svg>
```

## Common mistakes

* Using `<br>` is usually wrong. It should most likely be marked up as paragraphs.
* Adding padding and margin classes (e.g. `pal`, `mbm`) on and element is usually wrong. The defaults should in most cases not be touched, to make things consistent across the site.
