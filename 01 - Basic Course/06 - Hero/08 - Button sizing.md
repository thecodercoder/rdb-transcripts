# Button sizing

Our primary button does look good-- let's open the design and then put the website next to it so we can eyeball if there are any issues.

Ok, one thing I'm noticing is that it looks like there's not quite enough space between the `hero__content` paragraph and the button. Also, the button on the website looks a bit taller than what we have in the design.

Let's first look at the space issue. This is weird, because we did set the `margin-block-end` for the hero paragraph earlier.

Let's see what's going on here and inspect the button and the paragraph tag. And if we hover over the paragraph tag, it does look like there's a bottom margin, but it's sort of going through the button until it hits the button text.

This looks like it might be another margin collapse situation, although it's different from our previous one where the top margin was extending outside the parent. What's happening here is that elements that are display inline will have margin collapse.

We mentioned earlier in the course that some HTML tags are set to display inline by default, like span and img tags. Anchor or a-tags like we have for the buttons, are another tag that are display inline. If you ever have to check, you can inspect the element in question, go to the `Computed` tab, check the `Browser Styles` box to make it display all the default browser styles, and then filter for `display`. And now we can see that this button is set to display inline.

So to get rid of the margin collapse, we'll want to change that. If I go to the `Rules` tab and add `display: block` to the anchor link, the bottom margin from the paragraph starts working, but the button is now super wide. This is because display block elements will by default take up 100% of the available width unless their width is explicitly set.

The paragraph and the h1 tag are also display block, and if you hover over them, you can see that they're taking up 100% of the width. But we don't want that for the button, because we only want it to be the width of the text content.

What we can do is set the anchor link for the button to be `display: inline-block` -- this is the hybrid between display block and display inline, where it will act like an inline element and not take up 100% of the available width. But it also prevents margin collapse from happening.

And I think I'm going to want this for all buttons, so let's go back to button.scss and add `display: inline-block` to the top of the style rules in the `button` class. And now, when we reload the page we have that space we need between the paragraph and the button. And if we inspect the paragraph, we can see that the bottom margin ends right where the button is, which is what we want.

Also, if we compare the website to the design, our other issue of the button being too tall seems to have been fixed. You can see if I toggle the `display: inline-block` rule in the dev tools, the button height seems to change. We can see this in the `Layout` tab too-- when we uncheck it, the anchor link defaults to `display: inline` and the height goes up.

The reason for this is because of the extra little descender space added to the bottom of the text. This is what happened up in our Top Navigation too. You can get rid of the descender space if you set `display` to either `inline-block` or `block`. So that's why `display: inline-block` fixed this problem.

Ok, now that the general button styles are fixed, let's add styles for that clear button with white border. If we go to the design and select that button, we can check the border width in the right sidebar, in the `Stroke` panel. It says 2px, which is what we'll set the border width to for this button. And the border and text color are white.

Going back to our styles, let's add a new class under the primary class, which we'll call `&.secondary`. Again we need the ampersand since the `secondary` class will be in the same element as the `button` class.

Now let's get the custom properties for that secondary button. In colors.scss, we'll copy `--button-secondary-bg` for the transparent background, and then set the `background-color` to it. The next property, `--button-secondary-border` is something we didn't have for the primary button, but since this one is clear with the white border, it's a bit different.

I'm going to copy the custom prop, and then in the button styles I'm going to add the `border` property and then set it to `2px solid` and then `var()` and the custom prop in it. And if we save and check out the website, we can see that the clear button is showing up!

Now the buttons look pretty good, however there's a very small issue. If we inspect the buttons, the first one is 42px tall. But the second button is now 46px tall, which is 4 pixels more. What's going on?

If we go to the `Layout` tab while the second button is selected in the source code, and look at the `Box Model` panel, we can see that we have 18px of height from the content, then 12px of padding, and there's also 2 px of border on both top and bottom added to the total height. Since the first button doesn't have a border, it doesn't have those 4 pixels of border to get added to the height.

We could use `outline` instead of `border`, but one thing you need to be careful about is that `outline` is used by the browser to indicate when a link is being focused on.

If we go back to the `Rules` tab, and click the `:hov` icon to the right of the `Filter Styles` textbox, we can force a pseudo-class like hover or focus. The pseudo-class we want to force is `focus-visible`. If we check that box, the browser will behave as if we had focused on the button by tabbing through the website content.

You can see a thin white outline around the `Pricing` button now. If we used `outline` to make the white border, it would override the default browser styles to indicate when the element has focus.

So in this case, I think it's better to use `border`, and to add some more styles to fix the height difference between the buttons. To make the first solid button have the same height as the second clear one, there's a couple of solutions.

One is to add a 2px teal border to the first button, so that the border is the same color as the background, and then subtract 2px from both top and bottom padding to compensate for the extra height coming from the border.

So in our button styles, I'll change the vertical padding from `u.rem(12)` to `u.rem(10)`. And now if we save and check out the website, if we inspect the buttons they are both 46px tall now, which does match what we have in the design.
