# Default browser styles

One weird thing about CSS that I need to point out is related to that space between the widgets. We didn't add any margins or other properties to the widgets that would cause a space to occur. But one is there! What's going on here?

The space itself is actually from some default browser styles that are applied to some HTML elements. One example is that a paragraph will automatically have margin-top and margin-bottom added to it, even if you don't say anything in your styles. We actually canceled out the default margin-top value in our `_typography.scss` file where we set margin-top of the h tags and the paragraph tags to zero. So just for demonstration purposes, let's comment out the `margin-top: 0` for the h tags and the paragraph tag. That way they will take the default margins from the browser.

In the browser inspector, if I select the paragraph tag and then click on the `Layout` tab and the `Box Model` panel, it tells us that the paragraph has 16px of margin-top and margin-bottom. This 16px is from Firefox itself-- it adds the margin that's the same size as the font-size, which in our case is 1rem or 16px. And other browsers will do the same thing. If this seems weird and confusing to you, I'm right there with you.

I think these automatic margins are sort of a holdover from back before CSS existed, and webpages were written with just straight-up HTML, so that they looked like Word documents. If you think about it from that point in time, it does kinda make sense that having some spacing added for you automatically would help save time when you're writing the website content.

Unfortunately, even though we can control spacing now with CSS, we still have this feature that can cause unexpected behavior. So it's just good to know if you're wondering why some elements have spacing when you didn't give it spacing in your styles.

And there's another very strange quirk that comes along with the automatic margins. And that's what is called "margin collapse." We can see this happening on the website right now.

Another element that has default margins is the h2 and other h tags. If we select the h2 tag and go to the "Layout" tab again, it tells us that the h2 tag has a top and bottom margin. This margin is calculated by multiplying the font-size of the h tag by 0.83 for Firefox (and this exact amount might be slightly different across other browsers). So it's a margin of slightly less than the font-size itself.

You might be wondering, if the h2 tag has that margin-top, why is the purple background from the sidebar widget not including the margin? Instead, the margin is going outside the purple box. And, under the h2 tag, there is space because of the margin-bottom, but there's also a margin-top from the paragraph tag underneath it. But if we hover over the h2 and then the paragraph tags, it looks like the paragraph's top margin is getting included in the h2's bottom margin.

Both these weird things are because of margin collapse. If you have two elements and they have margins between them, the browser will only give a space that matches the biggest margin value-- the other margin collapses instead of getting added to the space.

And in the same way, both the top margin of the h2 tag and the bottom margin of the paragraph tag collapse and don't get included in the parent sidebar widget element.

How do you fix these weird quirks if you ever encounter them? You can get rid of the quirks if you apply some CSS style rules to the parent that creates what MDN (Mozilla Developer Network) calls a "block formatting context" which will get rid of the margin collapse effect -- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context

You might be doing some of these on your own without realizing it. If you add a border to the parent, like `border 1px solid`, the margins will then be included in the parent element. Or some padding, like `padding: 20px`. These are things that you might just add since we do want some extra space around the text in the sidebar widgets. This will also happen if you make the parent a flex or grid parent.

MDN has a whole list of conditions that will create a new block formatting context. I don't fully understand it myself to be perfectly honest, but the way I understand it is, if you start adding additional styles to the parent it will get out of that old, default Word doc way of displaying the elements, and instead behave according to the explicit style rules that you're adding. Again this is a very weird quirk that I wish didn't happen, but it still is happening, so we need to learn to work with it.

Anyway, that is a very long explanation, but back in our styles, let's uncomment the `margin-top` rules and then in the `_grid.scss` file add a little padding to our sidebar widgets. I'm going to set it to `u.rem(16)` to add 16px all around. Now we're ready to make the different widget themes!
