---
layout: post
title: 'Floating Labels'
excerpt_separator: <!--- more --->
comments: true
description: 'A look at the floating labels pattern'
twitterdescription: 'A look at the floating labels pattern - by Brett East'
tags: ['css', 'forms']
---

You may have recently seen a new design pattern in web and mobile form fields called Floating Labels. Popularised in a [blog post by Brad Frost](http://bradfrost.com/blog/post/float-label-pattern/) and referencing a [gif mockup by Matt D Smith](https://dribbble.com/shots/1254439--GIF-Mobile-Form-Interaction), I thought that I would show my own working version of the concept.<!--- more --->

![A floating labels example by Matt D Smith](/images/matt-d-smith-floating-labels.gif){: .img-responsive style="width: 400px; margin: 0 auto 40px;"}

To begin with I wanted to redesign the input fields for a site that I was working on that the time - they were using left aligned labels in some places and labels positioned inside the form field, both of which pose problems for small screens

It was also important to be semantic, my background working for the Australian government has (fortunately) instilled a strong need to write semantic and wcag2.0 friendly code. It was also important for usability reasons to have additional 'helper' or 'placeholder' text if necessary.

<p data-height="938" data-theme-id="21248" data-slug-hash="yJarjo" data-default-tab="result" data-user="bretteast" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/bretteast/pen/yJarjo/">Contact form modal</a> by Brett East (<a href="http://codepen.io/bretteast">@bretteast</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

In the above example I add and remove a style to the label based on whether or not the field has a value or focus, and remove it on blur if nothing has been entered.

This is a relatively simple approach and I use it to also allow for additional 'placeholder' text. As you can see in the textarea, the placeholder text disappears when the label floats to the top.

I welcome any feedback on improving this design in the discussion section and feel free to go ahead and fork the codepen.
