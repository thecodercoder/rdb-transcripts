## Font sizing

Next let's check the font-size for all the elements. The h3 tag on mobile is 24px and 1 line-height, and on desktop it is also 24px and 24.

Then on our website, the h3 tag is getting its font-size from our global typography styles, and I can see line-height is 1. Then to get the calculated px size, in the "Computed" tab, if I filter for "font-size" it says 24 which is correct.

Next let's check the paragraph styles while we're here, and it says 18px on "Computed" and in the "Rules" it has line-height of 1.3. If we go to Figma, and select on mobile, the paragraph is 16px and 21px line-height.

If we check that on our calculator, 21 divided by 16 is 1.3, so the line-height is correct. Then on desktop the font is also 16 and 21. So it's supposed to be 16 on all devices, which is smaller than what it is now.

I don't think we added this size in our typography styles, but let's take a look. Okay in typography.scss our paragraph styles are 18px by default, and then we added helper classes for larger sizes.

So do we want to create a new helper class for this extra small size, or do we want to set the size just in the blog styles? I think I could foresee in this hypothetical website, that we might want this extra small paragraph text in the future.

So let's create a new helper class here. It's slightly awkward because this is smaller than the default paragraph font-size, so the sizes will be slightly out of order with a new helper class. But I think it's okay.

Before the "medium" helper class I'll create a new selector with "ampersand dot xsmall" and in it set "font-size" to "u.rem(16)". Then we'll need to add the class to the paragraph tag in our index.html file. And that is in the "blog\_\_text" div, paragraph tag.

Okay, when we save and check out the website, now we can see the paragraph is smaller, and in the "Rules" it is 1rem or 16 pixels, which is what we want.

The last thing I'm noticing is that the "blog\_\_meta" text is different sizes and also need to be aligned. If I go to the design, in the mobile version it looks like the text is 14px and line-height of 14px too.

On our website, if I inspect the "time" tag in the blog meta text, in the "Computed" tab if I filter for "font-size", it is 16px coming from the default font font size on the website. And the paragraph is 18px coming from our paragraph typography styles.

Ideally, we want to be able to set the font-size of both the time and paragraph tags to be 14px. So we might think we can set that style rule on the "blog\_\_meta" class and then the child elements will inherit the font-size.

However, let's try this out in our styles. I'm going to the "blog\_\_meta" class write "font-size: 14px", let's save and see what happens. It looks like it affected the time tag but not the paragraph. We can check this if we toggle that style rule.

So why is this not working for both? If I select the time tag in the markup view, it doesn't have any font-sizes on the element itself, so it only has the inherited font-size, which is why it did change.

However, if we check the paragraph tag, it's getting its font-size from the typography styles we set on the paragraph tag. And we can see the inherited font-size from the "blog\_\_meta" class, but it's getting overridden.

When we talked about specificity earlier in the course, I mentioned that a type or tag style is the least specific, and will get overridden by a class style, and the class in turn can get overridden by an ID style.

But the key here is that those are for styles that target the actual element. Inherited styles set on a parent or ancestor element will not override styles that target the actual element itself.

So this is why the typography styles on the paragraph tag are getting applied-- the "blog\_\_meta" class font-size is targeting its parent, not the paragraph tag itself. So the style rule on the paragraph tag will override the inherited style.

So, going back to our styles, how can we fix this so both time tag and paragraph tag get targeted?

If you want to try this yourself first, feel free to pause here and then resume when you want to see what I do.

So, I think that the easiest way to target both element in the "blog\_\_meta" would be to do what we did above with the "blog\_\_text" margin-- use a wildcard child selector.

In the "blog\_\_meta" class, I'll nest a wildcard selector and in it, move the font-size rule inside it. And now when we save, both elements are the smaller 14px size.

Let's inspect the paragraph and see what's going on with the specificity now. So at the top as the most specific we have the style we added on the "blog\_\_meta" children with the wildcard element selector. And it is overriding the font-size on the paragraph tag styles.

However one thing to note is that with specificity, the wildcard doesn't count towards the specificity number for tag selectors. So the rule we just added has a specificity of 0-1-0 for just one class.

If I click into the paragraph typography selector and add the "blog\_\_meta" class to it, that will give the typography style rule a specificity of 0-1-1 for 1 class and 1 tag selector. And this makes it override the ".blog\_\_text" selector.

That's another little quirk that I wanted to mention to you since it's not completely intuitive, in my opinion. Let's reload to refresh our saved styles.

Things with the font-size seem good now. The last thing we need to do for the "blog\_\_meta" styles is put the "8 min read" paragraph on the same row as the date, but all the way to the right side.

I think flexbox will be the quickest way to do this. In our styles for the "blog\_\_meta" div since it's the parent, we can add "display: flex". And when we save, we have both on the same line. Although it looks like the paragraph text is slightly up from the date.

Let's figure out where this is coming from. One thing I can think of is to check the "display" property on both to make sure we don't have extra space on the bottom. I'll select the time tag and in the "Computed" tab I'll check the default browser styles and then filter for "display". And it is display block, and the paragraph is also block. So that is not the cause.

The other thing I can think of is to check that we have the line-height set. I think we want them both to have the same line-height, of 1. If I filter the computed styles for "line-height", the paragraph says 18px which is coming from the typography styles. And the time tag says "normal" which is a browser default.

So both elements have a different line-height, which we'll need to fix in our styles. Going to VS Code, in our "blog\_\_meta" wildcard styles, let's add "line-height: 1" to set it on both. And now when we save, the elements are lined up.

Now we want to align the date to the left and the read time to the right. We can do this by adding "justify-content: space-between" to put both grid children on the far edges. Okay, and that looks pretty good.

One thing I forgot is to make the date in all caps. I think it's best to do this in CSS as opposed to literally typing the text in all caps, just in case it ever has to change, it will be a lot easier to make that change in CSS.

So, this is for the date. I might just add a tag selector nested in our "blog\_\_meta" styles, since we have the wildcard tag selector anyway. And the time tag makes it pretty clear what is getting affected.

In our styles, after the wildcard selector, I'll add "time" and in it set "text-transform: uppercase". And now the date is uppercase.

I think we are pretty good on the text block styles. The last thing I can see is that we want rounded corners on the image and filter. If we go back to Figma, let's find where we set the corners.

If I click into the "Background" layer, in the right sidebar, it looks like it has a corner radius of 16px. So let's look at our website and in the markup view, we need to figure out where we want to set this.

If I try setting it on the image tag, I'd also have to set it on the filter. Let me show you in the styles-- for the "blog\_\_image" I can add "border-radius: 16px" and it rounds the image, but you can see the corners of the filter showing up.

And it feels inefficient to have to put the same style on both elements. What we can do instead is to not put the border-radius on the image, but on the parent, the "blog\_\_item" element.

If I add it just in the browser styles, nothing happens. Because the parent itself doesn't have a visible background color or image so you could see the corners.

But we can in a way "clip" all its children elements and basically force the rounded corners to apply to everything in the "blog\_\_item". If we also set "overflow: hidden", now everything has the rounded corners.

This is one really cool application of "overflow: hidden", where adding the border-radius on the "blog\_\_item" cut off the parts of the corner outside the curve. And the overflow property controls what happens with content outside the bounds of the element.

So in our case, it's hiding the sharp corners of the image and the filter that are outside the bounds of the rounded corners of the parent.

Alright, I think this looks pretty good. Let's copy those style rules and go back to VS Code. And in the "blog\_\_item" selector, let's paste them under the grid styles. And now when we save, we have our rounded corners on the entire card.

Let's put the website up next to the Figma design and eyeball the card styles. Things look pretty good-- the card is a lot taller than what we have in the design, and also if we increase the viewport width the card gets super wide too.

We'll fix these sizing issues, once we add the markup for the other cards, which we will do next!
