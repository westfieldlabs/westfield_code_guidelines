---
title: Accessibility Guidelines
resource_prefix: ../
---

# Accessibility Guidelines
***

Web accessibility is the practice of making websites and web applications usable by people with disabilities. 15-20% of the world's population has some kind of disability. We strive to create an inclusive web experience for all users. Our guidelines are based on global industry standards created by the [W3C Web Accessibility Initiative](http://www.w3.org/WAI/intro/wcag.php).

The guidelines below are meant to be a high level overview of how we are striving to make our projects more accessible, it is not meant to be used as an all inclusive checklist.

## Regional Standards

As we need to meet the minimum standards for multiple regions we will develop to at least the minimum requirements of WCAG 2.0 AA compliance. The specific standard requirments by applicable region are listed below:

AU/NZ: **Disability Compliance Act** - states that “Non-government websites and web resources whose development commences after July 1 2010 should comply with [WCAG 2.0](http://www.w3.org/TR/WCAG20/) to a minimum of AA-Level conformance

UK: **The Equality Act 2010 (EQA)**  is the legal reference in the UK for Discrimination and it entered into force on 1 October 2010 with additional provisions for recruitment in April 2011.  Compliance to Priority 1 (A) is mandatory and we should have at least WCAG 2.0 - Priority 2 (AA) compliance

US: **[Section 508 of The Rehabilitation Act](http://www.section508.gov/)**

***

## Guiding Principles of Accessibility (POUR)

TODO: Expand on guiding principles

The four main guiding principles of accessibility in WCAG 2.0 are:

* Perceivable
* Operable
* Understandable
* Robust

***

## General Guidelines and Best Practices

### Structure and Hierarchy
Pages that are well structured, follow proper syntax, and pass the [W3C validator](http://validator.w3.org/nu/) are most accessible.

Use the correct heading level e.g. `h1` followed by `h2`, then `h3` etc. Do not use heading level as a means of formatting text, e.g. do not style a heading as `h3` simply because it has the same font size and style. Instead use the appropriate heading level and add a class that matches the design.

{% highlight html %}
// Good
<h1>Heading 1</h1>
<h2>Heading 2</h2>

// Good - when your h2 is styled as an h3
<h1>Heading 1</h1>
<h2 class="h3">Heading 2</h2>

// Bad - when your h2 is styled as an h3
<h1>Heading 1</h1>
<h3>Heading 2</h3>
{% endhighlight %}

### Provide skip link
All templates should include a skip link to allow assistive technologies to go directly to the desired content or to skip over navigation elements that are common to every page. This is only a temporary fix until ARIA landmark roles are better supported. The skip link should have a href value that matches the id of the main container. We use a value of `main`.

{% highlight html %}
<a href="#main" class="u-hide-visually">Skip to content</a>

...

<!-- The skip link's href should match the id of the main content container -->
<main id="main" role="main"></main>
{% endhighlight %}

### Provide meaningful alt text
Every non-text element needs a text alternative that provides an equivalent to the image content. Alt text should present the content and function, not necessarily a description of the image and use the fewest number of words necessary.

{% highlight html %}
// Good
<img src="images/logo.png" alt="Westfield Labs">

// Bad
<img src="images/logo.png" alt="logo">
{% endhighlight %}

If an image is purely decorative and has no relevant content or function then the image should have an empty alternative text value. Leaving out the alt text value altogether causes a screen reader to read out the URL of the image instead.

{% highlight html %}
// Good
<img src="images/herobanner.png" alt="">

// Bad
<img src="images/herobanner.png">
{% endhighlight %}

*Additional Reading: [WebAim Alternative Text](http://webaim.org/techniques/alttext/)*

### Form fields should have an associated label
Form fields must have a label associated to it, otherwise they will not be accessible to screensreaders. The label's attribute needs to match the id of the form field. This also helps increase the click area of the form field. Use helper classes e.g. `.u-hide-visually` to hide a label that is not visible in the design.

{% highlight html %}
// Good
<label for="search">Search</label>
<input type="search" id="search">

// Good - hide label visually
<label for="search" class="u-hide-visually">Search</label>
<input type="search" id="search">

// Bad - label for attribute doesn't match the form field id
<label for="searchField">Search</label>
<input type="search" id="search">

// Bad - no label
<input type="search" id="search">
{% endhighlight %}

### Buttons vs. Anchors
It is important to remember that semantic markup means behavior and not visuals. This comes up most often with the use of anchors buttons. `<button` and `<a>` respond differently to keyboard events and screen readers by default. The standard behavior for an `<a>` is to navigate to the URL of the link. If your link requires a non meaningful href then it should probably be a `<button>`. A button is used to control the user interface rather than taking the user to a new destination.

*Additional Reading: [Anchors, Buttons, and Accessibility](http://formidablelabs.com/blog/2014/05/08/anchors-buttons-and-accessibility/)*

## WAI-ARIA

TODO: rewrite intro to ARIA

> WAI-ARIA is a specification that provides a means of describing roles, states, and properties for custom widgets so that they are recognisable and usable by > assistive technology users. WAI-ARIA also provides a mechanism to ensure that > users of assistive technologies are aware of updates in the application.

### Landmark Roles
Document landmark roles were defined to give structure to a page and to help assistive technologies orient themselves within a document. A template can be broken into these common regions with clearly marked navigational landmark roles.

* `<header>` with `role="banner"` on the container usually wrapping site wide content e.g. logo, navigation, global search.
* `<nav>` with `role="navigation"`
    * Nav elements should only be used on major navigation blocks.
* `role="main"` on the container around the main content.
* `role="complementary"` on the aside element (container with supporting information on the document).
* `role="contentinfo"` on the footer element (container around metadata of the document e.g. footnote, copyright statement).

### Form Accessibility

#### Required fields
The `aria-required` property indicates that user input is required on the control before the form can successfully be submitted.

{% highlight html %}
<label for="name">Name</label>
<input type="text" id="name" aria-required="true">
{% endhighlight %}

*Additional Reading: [Introduction to WAI-ARIA](https://dev.opera.com/articles/introduction-to-wai-aria/)*

## Keyboard Accessibility

TODO: Keyboard Accessibility minimum standards

*Additional Reading: [WebAim Keyboard Accessibility](http://webaim.org/techniques/keyboard/)*

## Color contrast

Choose color and contrast wisely.

* Never use color alone to convey information. Use a symbol, graphic or treatment that will work in a monochromatic environment.
* Make sure that color contrast is strong, especially between text and background.
* Be especially cautious of red/green color combinations.

Check your color selections using these resources:

* [Contrast Checker](http://webaim.org/resources/contrastchecker/) for AA and AAA compliance.
* [Color Oracle](http://colororacle.org/) simulates color vision impairment

*Additional Reading: [Integrating Contrast Checks in your web workflow](http://24ways.org/2014/integrating-contrast-checks-in-your-web-workflow/)*

## JavaScript

TODO: Progressive enhancement

Some components require JavaScript, ensure you can still access the content after JS has been turned off.

* Provide keyboard event handlers in addition to mouse event handlers when possible.

### Tab index

TODO: You should never set custom tab index's.
JS tab index -1/0

## CSS

### Helper Classes

TODO: More about helpers, and specify these are specific examples to aurora.

There are a few helper classes you can use throughout to help make your site accessible.

* `.u-hide` hides elements from both screen readers and the document flow.
* `.u-hide-visually` hides elements only visually but are still available to screen readers.

***

## Testing

TODO: Testing tips

***

## Resources

* [W3C Web Accessibility Initiative](http://www.w3.org/WAI/intro/wcag.php)
* [WebAim's WCAG 2.0 Checklist](http://webaim.org/standards/wcag/checklist)
* [HTML5 Doctor](http://html5doctor.com/element-index/)
