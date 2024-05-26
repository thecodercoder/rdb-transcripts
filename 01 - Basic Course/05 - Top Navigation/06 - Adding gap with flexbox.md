# Adding gap with flexbox

The other issue we need to fix is in the links themselves. We need to add space between the items, because right now they're right next to each other. In the past, we had to use either margin or padding to add space, but fortunately with both flexbox and grid we can take advantage of the `gap` property.

Going back to the Flexbox Guide, if we scroll down more, the `gap` property is set on the flex parent, and it controls the space between flex items. And it will only add space between flex items-- so if an item is first or last, it won't add space on the edges, which is really nice. Let's check out the design to see how much space between items we want.

In Figma, if I click into the design to select an individual text link, then hold down the Alt key and hover my mouse over a link next to it, Figma tells me that there is 40px of space between items.

Back in VS Code, if we go to the `topnav__links` selector, we can add the gap property there. And in terms of whether to use pixels or rems for gap, I think either is ok-- I might use pixels for this, because if we change the browser base font size to something significantly larger, we don't necessarily want the space to get really huge too.

What we can do is try `40px` first, and then change the base font size to see if the links are still reasonably readable if the space between them doesn't change. Let's try that.

We'll set gap to `40px`, and then open our browser settings and set the base font size to 32 so it's double the size. Then if we go back to the website and manually reload, we can see the text is much larger. The `40px` of space is still `40px`, it hasn't doubled since pixels are an absolute unit which won't get affected if you change the base font size.

Now, just for comparison's sake, let's also see what it would look like if we used rems instead of pixels. Back in our styles, I'll change the `40px` to `u.rem(40)` to use rems. And if we go back to the website the space between the links is now double to `80px` between them.

I think in this case either rems or pixels is fine. I might change it back to `40px` just because it was still readable, and it gives more space on the website to the text itself. So let's change that back to `40px` and then in our settings change the base font size back to the default 16.
