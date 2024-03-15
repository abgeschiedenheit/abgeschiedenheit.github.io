# accessible hyperlinks: :after

2023-10-05

A way to make hyperlinks accessible is by explictly informing the user when a hyperlink points externally. An option for this would be to use a north east arrow immediately after a hyperlink to denote it is _going outside_.

Now, we don't want to have to copy and paste the HTML entity, HTML code, hex code, or even the UTF-8 character itself each time for an external hyperlink. Luckily, CSS has [attribute selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors):

> The CSS attribute selector matches elements based on the element having a given attribute explicitly set, with options for defining an attribute value or substring value match.

This is to mean we can have an anchor element, `<a>`, with an attribute, in our case `href`, matching a particular value, [`[attr*=value]`](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors#attrvalue_6):

> Represents elements with an attribute name of attr whose value contains at least one occurrence of value within the string.

If we reflect a bit on what differentiates a local-pointing hyperlink versus an external-pointing hyperlink, we may come to the conclusion that external hyperlinks have two forward slashes in that `https://`. Where we are currently: `a[href*="//"]`.

**Note:** [`href`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href) is not strictly restricted to HTTP-based URLs, e.g.: `tel:`, `mailto:`, and `sms`. Therefore, we may also have something like `a[href*="mailto:"]`.

At this point, we want to create a [pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements):

> A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s).

What we are interested in our particular case is the [`::after`](https://developer.mozilla.org/en-US/docs/Web/CSS/::after) psuedo-element:

> In CSS, `::after` creates a pseudo-element that is the last child of the selected element. It is often used to add cosmetic content to an element with the [`content`](https://developer.mozilla.org/en-US/docs/Web/CSS/content) property. It is inline by default.

As mentioned above, `::after`, indeed, is commonly used to add cosmetic content:

> The `content` CSS property replaces content with a generated value. It can be used to define what is rendered inside an element or pseudo-element. For elements, the content property specifies whether the element renders normally (`normal` or `none`) or is replaced with an image (and associated "alt" text). For pseudo-elements and margin boxes, `content` defines the content as images, text, both, or none, which determines whether the element renders at all.

The [CSS code for a north east arrow](https://www.toptal.com/designers/htmlarrows/arrows/north-east-arrow/) is the `\2197`. And so:

```css
a[href*="//"]::after {
  display: inline-block;
  /* north east arrow */
  content: "\2197";
}
```
