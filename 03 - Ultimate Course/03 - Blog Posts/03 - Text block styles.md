## Text block styles

Next up, let's start styling that white text block. In Figma, if I select all the text elements inside the card and hold down Alt, there's 16 pixels of padding inside the card.

You can see this also in the right sidebar, in the "Auto layout" panel, if you hover over the different icons under the arrows, it tells us that there are 16px of gap between items, and then 16px of both horizontal and vertical padding.

And down in the Fill panel it also says that the background color is white. I think we already have this saved in our colors.

Let's go back to VS Code and start writing our styles. If we go to the colors.scss file, I think it makes sense to use the "main-bg" custom prop for the text block. So let's copy that one and go to the blog.scss file.

The text block is in the "blog\_\_text" selector, so in there I'm going to write "background-color" and set it to "var()" and then paste in the "--main-bg" custom prop.

Let's also add "padding" and set it to 16px. I'm going to use pixels because I don't want this space to scale up if the browser base font size increases, to give the actual text elements more real estate.

I'm also going to use grid in the text block so we can use gap to add space between the elements. There's already space between them, but I think those are probably from browser defaults, which are probably not the correct size we need.

So I'm going to add "display: grid" and "gap: u.rem(16)" because we probably do want to scale up the space between readable lines of text.

And when we save, we do have our padding around the text elements. But there are some pretty big issues. One is that we can't see the image anymore, the white block is taking up all the space.

This is due to the default behaviors of grid, where if we look in our dev tools, in the markup view we have the "blog\_\_item" grid parent, and it's getting its height set by the image because of the aspect ratio of the image, it's setting the height based on the width that it is.

And because elements have a default "align" value of either auto or normal, this means that they will by default stretch vertically to the height of the parent, making all their heights the same.

This is actually what we want for the "blog\_\_filter" since we want it to be the same height as the image tag. But we don't want the "blog\_\_text" to stretch. We want it to be centered vertically.

So, let's go in our styles to the "blog\_\_text" and add "align-self: center". And now we can see on the website that the white text block is not stretching anymore, but is the height of its content.

It also looks like the gradient in the "blog\_\_filter" is showing through the text, which we don't want. I think what's happening is because all the "blog\_\_item" elements are the default position static, so the mix-blend-mode is getting blended with the text that's on top of it.

So I think we want to sort of separate the "blog\_\_text" element from the image and the filter. Just in the browser, if we set it to be "position: relative" then it will create a new stacking context and be stacked on top of the image and filter.

So that works. We could also instead of position relative [ uncheck ] set "isolation: isolate" which will create a new stacking context without adding any other style behaviors. I might use this since we don't really need it to be relative other than to be on top of the other elements. So let's copy that style rule, and paste it in the styles.

Now when we save, the card text looks good and doesn't have that gradient bleeding through. We're getting closer with the white block styles! Let's go to Figma and see what else we need to do.

One thing that I can see is that we need to have some space around the sides of the white block too. If I select it and hold down Alt, there's 10px of space to the left and right.

Usually I would want to use padding on the parent element to add space between the item and its parent, but this case is a little complicated. Because we're stacking the 3 child elements all on top of one another, adding padding on the parent will add space around the image and filter too, which we don't want.

So I think the best solution to add that space is actually to add margin on the right and left of the "blog\_\_text". And that should be fine-- it shouldn't cause margin collapse since we're only setting the horizontal margins, and it's also a grid child and a grid parent.

The last two things will create a new block formatting context, which is a different thing from a stacking context. I talked about block formatting contexts earlier in the course, when we were first building the hero. Basically, creating one will prevent vertical margins from "collapsing" outside of the element's parent element.

Let's try this and see. In our styles, maybe before the padding, I'll add "margin-inline: 10px" to add space on the sides, and we'll use pixels so it doesn't scale up because it won't affect readability.

Okay, and when we save, we have our space! We also need to round the corners. Going back to Figma, if I click on the "Post content" layer, in the top right "Frame" panel the bottom right measurement says 8px for corner radius, which is border radius.

In our styles I'll add this, maybe under the padding. And I'll use pixels and set the "border-radius" to "8px".

In the design there was also some shadow around the text block. So still on the "Post content" layer, in the right sidebar if we scroll down, towards the bottom under "Effects" it says "Drop shadow" which we can load as "box-shadow" in CSS.

If we click on the little sun icon on the left, we have a pop-up menu with the shadow settings. And I'll open VS Code on the left.

First let's get that color and save it as a custom property. It looks like the text-dark color, "383A4A" at 40% opacity. So in VS Code in our colors.scss file, I'm going to copy the "text-dark" color value, and then let's create a new custom prop for this.

After the "blog-gradient" colors, I'll write "--blog-shadow". And then paste in the HSL color. And we need to change it to HSLA since we're adding opacity with the Alpha number. Then in the color value, I'll add a comma after the 25% and then add the opacity number, "40%".

Then let's save, and copy that "blog-shadow" custom prop name. And then in our "blog\_\_text" styles at the bottom I'll start adding "box-shadow" and we need the numbers first, so from Figma the first one is the X value which is "0".

Then the Y value which is "4px" and we do need that unit. Then the blue value which is "10px". And "spread" is optional so we can just omit that, then the color so I'll write "var()" and then paste in our "--blog-shadow" custom prop.

Alright, so now on our website, the card looks closer to the design. We have the rounded corners, and it's a bit harder to see but there is a bit of shadow around it. We can inspect the block and in the "Rules" we can toggle the "box-shadow" rule so you can see how it looks with and without the shadow.

I think the card itself looks pretty good. However we still need to style the text inside the card and fix the spacing between the text elements.

---

Let's fix the spacing first. In our dev tools I'm going to turn on the grid highlighting inside the "blog\_\_text" element. So we have the 16 px of space between the grid children, but there's also space under it looks like all the text elements.

If we hover over each one, the h3 tag has a bottom margin, and the paragraph, and also the paragraph in the "blog\_\_meta" div.

So I think it might be easiest to target any child element inside the "blog_text" div and set its margin to 0. In our styles I'm going to nest a wildcard to target any child or descendent element-- not the direct child selector because then the paragraph inside the "blog\_\_meta" div won't get affected.

Then in there I'll set "margin" to 0. And now when we save, all the extra space is gone, so that's good.

Next, let's fix the color for the h3 tag-- if we inspect it, it's getting its magenta color from our typography styles. I think I might want to rework those link styles, to be honest. Initially we made it so that links that are in blocks of text like paragraphs will be magenta and stand out.

But it is causing some issues, not a huge issue, but I don't want to have to keep writing styles to change the color of links. So I'm going to try to make this typography rule a bit more specific.

Let's go to VS Code and also go to the typography.scss file. And if we scroll down to the bottom we have our style rule here. What I'm going to do is only set this magenta color if the anchor tag is inside a paragraph tag. And hopefully that will limit the magenta happening when we don't actually want it to.

So I'm going to change the selector to be "p" and then the direct child selector, right angle bracket. Then "a". Okay, let's save, and now on our website the h3 tag is no longer magenta-- it's now the default purple link color from the browser.

So we are going to have to change the color of this link to be gray like the design. And maybe on hover we'll have it change to magenta.

If we go back to the index.html file, the title link is an anchor link inside the "blog\_\_title" class h3 tag. Let's add that in our styles. In the "blog\_\_title" selector, I'll add the anchor tag selector, otherwise it won't be able to override the browser default style on the anchor tag.

Then in the styles, let's write "color" and set it to the dark text custom prop with the var() function and in it, the name "--text-dark". And when we save, the title is now dark gray.

Now let's add the hover state to make the text magenta. If you want to try this on your own first, pause the video here, and then play it again when you're ready to see what I did.

[ pause ]

Okay, under the color style rule, I'm going to nest the hover pseudo-class selector. We're starting with an ampersand because it is on the anchor tag itself, then a colon and "hover".

And in the styles I'll change the color to the magenta color. If you're not sure what color to use, let's go to the colors.scss file and I think the "text-link" custom prop is the one we'd like to use. We used it for the text links and also the footer links.

Back in the blog styles, I'll set the hover state color to "var(--text-link)". And now when we save, when we hover over the title text, it is now magenta.
