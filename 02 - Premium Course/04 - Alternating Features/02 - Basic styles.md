## Basic styles

Alright, now we can start adding our styles. First off, let's get those text styles to match the design. In Figma, I'm going to look at the main headline first, and then we'll do the kicker. On desktop, the h3 style is 44 pixels, and on mobile it is 36. If we go back to our website and inspect the h3 styles, it is getting its font-size set from our default typography styles.

Before changing anything, let's look back at the design and see if we already have h3 tags that need these style rules. If I scroll back up to the outline, we have h3 tags in the 3-column Features section that we built already. And those are 24px which is what we have in our typography styles.

So maybe we can do what we did for the paragraph styles, and add a helper class for the larger h3 tag font sizes in the Alternating Features section. In VS Code, I'm going to use the Quick Open menu with Ctrl-P and type in "typography" to open the typography.scss file.

In the h3 tag selector, I'll add a helper class like what we have for the paragraph tag. Since right now we're just working with 2 sizes, I'll make the new helper class "&.large". And now we can add the font size for the larger h3 tag.

In our design, it was 36px on mobile and 44px on desktop. So let's go to the "fluid typography calculator", and set the Min font-size to 36px, the Max font-size to 44px, then Min Viewport to 375px and Max Viewport to 1200px.

And now in the Result panel we have our clamp() function, so let's copy that and go back to VS Code and paste it in. And I want to get rid of the long decimal places, so we'll round down for the first number to 2.02rem, and round the second number up to 0.97vw.

And again I'm going to convert the minimum font size to use our rem() function just so we can quickly look back and know how many pixels it is. So for the fallback font-size, I'll set that to "u.rem(36)", then copy it and set it also as the first minimum parameter in the clamp() function. Then I'll replace the last parameter with "u.rem(44)."

Now we need to add that helper class to the HTML markup. So I'll copy the "large" class name, then in the index.html file, I'll add a class to the h3 tag, and paste it in.

Let's also check the line-height. In the typography.scss file, the line-height for the h3 tag is 1, so we should also double-check the line-height in Figma. For desktop, the headline is 44px font-size and line-height is also 44. And on mobile the font-size is 36 and the line-height is also 36. So they are both a line-height of 1, which means it's 100% of the font-size so they will be the same. So what we have is correct.

The other thing we want to check is the margin-bottom of the headline. In Figma I'm going to check the space between the headline and the description. For desktop it is 10px, and for mobile it looks like it is also 10px.

And just for kicks, let's see what the margin-bottom is for the 3-column Features. And it looks like it's also 10px on both mobile and desktop. So I'm going to check the website to see where we added margin-bottom for that h3 tag.

On our website it's coming from the "features\_\_title" class. So I think we can move that style away from the "features" styles and just have it globally for the h3 tag since it's the same in both sections. Just to make things slightly more efficient.

That is in features.scss, so in VS Code I'll Quick Open the features.scss file, and down in the "features\_\_title" selector I'm going to copy that "margin-block-end" style rule, and delete that whole selector since we don't need it anymore.

Then in the typography.scss file, I'll paste the rule in the h3 tag styles. And save. And now in the website, the 3-column Features h3 tag has the margin-block end rule, and the Alternating Features h3 tag has the same style.

And to check the font-sizes, I'll inspect the h3 tag. And in the "Computed" tab, the font-size is 44px for desktop, which is right. And if we switch to iPhone it is 36px which is also correct. And in the "Rules" tab we can see that our line-height of 1 is also in effect.

We also need to add the kicker styles. If we look in Figma, the kicker text is 24px font-size and 24px line-height on desktop, and on mobile it is 20px and 20px. So let's go back to the Fluid Typography Calculator, and for Min Font Size set it to 20px, Max Font Size to 24px, Min Viewport to 375px, and Max Viewport to 1200px.

Then we'll copy the result, and as far as where to put these styles, let's put them in the typography.scss file, in the "large" h3 tag styles. We want to target a span that is a child of the h3 tag, so in the "large" class selector I'll add a nested "span" selector and paste in the font-size styles. And let's get rid of the long decimals, rounding to 1.14rem and 0.48vw.

Also, just as a sidenote, you may have heard to not use child or descendent selectors in CSS because they are require more processing on the browser side compared to other selectors like class or id. But while this is true, the difference between them is incredibly small, especially with modern browsers. So you don't need to worry about performance in terms of your selectors.

Now that we have the font-size set, let's see what else we need for the kicker. In Figma if we check the kicker text, in the right sidebar it tells us that it is bold. This should be already inherited from the h3 styles, since browsers will by default make any h-tag font-weight bold. And we need to make the text all caps, which we can do by adding the "text-transform" property and setting it to "uppercase".

Ok! I think that should be it. Let's check our website. The kicker text looks good! The only problem is that it's on the same line as the other h3 text. One way you could fix this is by manually typing a line break or br-tag in the HTML after the kicker text. But generally it's not considered good practice to add spacing by using a line break, since we can use other properties.

So a better solution would be to set the span tag to be "display: block". By default, a span is an inline element, which the browser will display inline with other elements. By setting it to "display: block", the span tag will then be on its own line. And it looks like we'll also need to add some space under the span tag.

Let's go to Figma to check how much space the kicker needs under it. On desktop it has 10px, and on mobile it's also 10px. So we can add that in the span selector, I'll add it after the "display" property, to keep the layout styles separate from the text styles. And we want that to be "margin-block-end: u.rem(10)". And now the kicker and the headline text styles look pretty good!

Next up, let's add the paragraph styles. In Figma if I select the desktop description, it says that the font-size is 24px, then on mobile it is 20px. Since we know we have those helper classes for paragraphs, let's check and see if one of them has those font-sizes.

If we scroll down a bit, it looks like for paragraphs, the "medium" class is 20px for mobile as the minimum font-size in the clamp() function, and 24px for desktop as the max size. This is one reason why I like converting the clamp() function font sizes from rems to using my rem() function, so I can quickly eyeball the sizes.

Let's add the "medium" class to the paragraph tag. And now on the website, for mobile sizes the medium paragraph is about 20px, and if we change to desktop, it is 24px.

Okay, so that's it for the text styles!

Let's now check out the styles for the image. Right now it's set to 100% width, which is good if we're at mobile viewports, but we need it to not get super big on desktop widths like you can see here.

So far, we've been making our images default to a width of 100%, and controlling their final width by setting a max-width to the width in the design in the section-specific styles. And it's been working for the other images in the site.

However, in this section, we have 3 images of different sizes. And I don't want to have to control the width in this kind of manual way for all 3 of them, if possible. So for the Alternating Features section, I might change the image styles and set "width" to "auto" to override the default 100% width. Then each individual image in the section will get its size from the width and height attributes in the HTML markup. And then I'll set the "max-width" to 100% so that the images don't overflow on smaller viewports.

Let's try that. In our styles, for the "alt-feature\_\_image", I'll add "width: auto" and then "max-width: 100%". And now in the website the laptop image isn't super huge, and if I go to a smaller mobile viewport the image gets smaller as the container gets smaller, and doesn't look skewed. Okay, I think this is good.

Alright, now we have the basic styles set for the text and image elements.

I think we're safe to now add the markup for the other 2 rows of this section. If we go to the index.html file, I'm going to select the "alt-feature\_\_row" div that contains the first row, and press Ctrl-D twice to duplicate it twice. And on our website, we can see that we have 3 rows of content now. Let's update the images and text for those other 2 rows.

Going into Figma, the image in the second row is called "tablet-phone", which should match the filename for the SVG we exported for this. Back in VS Code, in the image tag, I'm going to delete the old filename and then start typing "tablet", then auto-complete loads up the options we have, and I'll select the "tablet-phone" SVG and press Tab or Enter.

We do need to update some of the other attributes in the image tag. The alt text I'll change to say "tablet and phone showing the Mythos dashboard". And then let's save what we have so far. We also need to get the width and height, so let's do what we did before, and press Ctrl-P or Cmd-P for the Quick Open menu, and start typing "tablet" and open "tablet-phone.svg". In the SVG code, let's copy the width and height attributes, then go back to the index.html file and replace the previous attributes.

That's good for the image, now let's get the new text copy. I'm going to go to the second row with the tablet and phone image, and start copying the text. First let's get the kicker text, "immediate notifications" and then in VS Code, go to the second "alt-feature\_\_row" and paste it in the h3 span. Then let's get the headline text, copy that, and paste it in the h3 after the span.

Next up is the paragraph text. And we have that one phrase that's in bold magenta text, which we're assuming is link text. So let's copy the whole paragraph, and in VS Code paste it in the paragraph tag, and then save so the Prettier extension will wrap the text for us. Now let's make those two words, "consectetur adipiscing" a link by adding an anchor tag around them. And in real life this link would navigate to a different URL with the "href" attribute. So I'll add the "href" but then just leave it blank since this is just a pretend website. We'll add the link styles in a little bit.

Ok! I think that's all we need to update for the second row. Let's do a check on how that looks in the website. It looks pretty good.

Let's update the third row to have the right image and copy. In Figma, if I select the image in the third row, it's called "tablet-payments". In our code, in the third row image tag, I'm going to delete the "laptop-check" filename and start typing "tablet". Then in auto-complete let's select the "tablet-payments.svg" filename. And let's update the alt text to say "tablet showing the Mythos dashboard".

Then we need to get the width and height of the image. I'll use the Quick Open menu again and type in "tablet", then select "tablet-payments.svg". And I'll copy the width and height attributes and paste them in the image tag to replace the old ones.

Now let's get the copy. In Figma let's copy the kicker, "Protected Payments" and paste the text in the h3 span. Then we'll copy the headline, "Send payments from anywhere" and paste that in the h3 tag after the span. Last, let's copy that paragraph text, and notice that it has a link in there as well. So let's paste that in the paragraph tag. And add an anchor link where those words are, again leaving the href attribute blank since it isn't a real link.

Ok! Now let's save and check out the website. And things look pretty good.
