## Hero wrapper styles

What we're going to do now with the styles is to rework the wrapper styles, just for the hero section. We have to do this because, if we look back at Figma, the wave image is extending all the way across the entire viewport.

Having content go all the way to the very edges is sometimes called "full bleed." This term comes from the printing world to mean printing all the way to the edge of the page without any space or borders around it.

Most of the content on the website is getting limited by our wrapper styles to 1200px wide. But we want the wave image to not be limited by that, and to be full bleed.

In the past, I would probably use position absolute on the wave image, in order to break it out of the normal flow of the document so it can break out of the wrapper limitations. However, while position absolute would work in this situation, and it's honestly still used a lot for these kinds of design problems, I think there's a better and more modern way to do this.

We'll be reworking the wrapper for the hero section by using CSS grid. And the best part is, we can get it to handle both the 1200px max width for most content, but also any parts of the website that we want to be full bleed.

With all that in mind, let's go to the index.html file, because we need to add that wave image to the Hero section.

In the Hero section tag, right now we have the wrapper div, then the unicorn image, and the "hero\_\_text" div. Where do we want to add the wave image? Initially, it might make sense to add it after the unicorn image and text, since it's at the bottom of the section.

However, if you remember, in the design, the unicorn image is overlapping the wave image and is on top of the wave image. So by default, the browser will stack elements that come later in the markup order on top of previous elements, if they are styled to overlap.

Since I want the wave image to be under the other Hero content, it'll make it easier if we put the wave image first in the Hero section. That way we won't have to write special style rules for z-index to control how the Hero elements stack.

Inside the Hero section tag, I'm going to add the new image tag before the "hero\_\_wrapper" div. And I'll give it a class of "hero\_\_wave". Then in the "src" attribute, I'll add a forward slash, "img", and select "hero-wave.svg". I'm going to leave the "alt" attribute as an empty string because the image is purely decorative, so doing this will let screen readers ignore the image instead of reading out the entire file name.

And the next thing we want to do is add "width" and "height" attributes, so I'm going to open the sidebar, and open the SVG file. And I can copy the "width" and "height" attributes right from the SVG tag, then paste it in the "hero-wave" image tag.

And now when we save, we can see the wave image is loading, which is good.

I also want to make some other changes in the Hero markup here. Because we're essentially going to be redoing the wrapper styles for the Hero, I'm going to delete the "wrapper hero\_\_wrapper" class from the div, and rename it to something different. Since this div contains the image and text, I'm going to rename the class to just "hero\_\_content".

And you might realize that the paragraph tag is also called "hero\_\_content", but we didn't end up using this class selector for anything, so I'm going to delete it from the paragraph tag, but leave the "large" class since that is being used.

So now, in the Hero section tag, its direct children are the "hero\_\_wave" image, and the "hero\_\_content" div. And we're going to want the section tag to be the grid parent for our new, full bleed wrapper styles. I'm going to create a new class name for this, maybe "fb-wrapper" and add it after the "hero" class.

And, I want to create some similar class names for the content that we both want to be full bleed, and content that we want limited to the 1200 pixels wide.

The "hero-wave" image we want to be full bleed, so I'm going to add a class name called "fb-wrapper\_\_full". And for the "hero\_\_content" div, we'll add a class name of "fb-wrapper\_\_content".

I'm creating these new "fb-wrapper" classes because the class names can get reused if in the future, we have another section that needs full bleed content.

Now that we have our markup and new class names, we can start writing our styles to for our full bleed layout.

Even though I did create a new "fb-wrapper" class, I'm going to bend the rules a little and put the styles in the "wrapper.scss" partial instead of creating a whole new partial.

Let's open the wrapper.scss partial, I'm going to press Ctrl or Command + P to open the Quick Open menu, then type in "wrapper", and open the wrapper.scss file. It's just a bit quicker than searching through the Solution Explorer.

Now, under the "wrapper" class, I'm going to create a whole new class selector-- NOT nested. And call it "fb-wrapper". Then nested in it, I'll add selectors for "&\_\_full" and then "&\_\_content".

Those are our selectors. Now we need to write the styles for this new grid parent. And to help illustrate what these styles will do, let's go back to Figma, and I'll show you what our grid column and row arrangement will be.

In Figma, I created a diagram of the grid in the Hero section, in a layer called "grid template". When I unhide it, we have our grid.

This grid has one row, created with the horizontal magenta lines, and it is between lines 1 and 2.

And it has 3 columns created with the vertical yellow lines. The middle column, between lines 2 and 3, is the 1200px max width wrapper that we've been using in our existing wrapper class. We should be able to reuse the code for this grid column.

Then there are 2 columns on either side, and those will take up whatever available space is left over, and it will be equally divided between both of them.

And then for mobile, we want the grid to behave in the same way as our wrapper did, where we'll have some space on either side of the content.

Let's go into our styles and build this out.

In the "fb-wrapper" selector, we'll make this a grid parent by setting "display: grid". Then we want to add "grid-template-columns" and this is where we'll have our 3 columns. The first and last we're going to set to "1fr" so that any available space will be divided equally among them.

And for the middle column, we can reuse our min() function from the original "wrapper" class, so I'm going to copy that and paste it after the first "1fr".

So now the "grid-template-columns" should be set to "1fr", then the min() function which will have a max-width of 1200px on larger viewports using our rem() function, but also leave 24px of space on either side for smaller viewports. And the last column will be "1fr".

One cool feature of grid is that instead of using the grid line numbers, you can actually give them names. With our 3 grid columns, we have 4 grid lines. The first line will be before the first "1fr" column, and we can give it a name inside of square brackets. So I'm going to write "[fb-start]" for the first line, because this is where full bleed content will begin.

Then between the first and second columns is the second grid line, and I'll name that "[content-start]", since that's where we want the limited content to begin. After the second column is the end of the limited content, so I'll add another square bracket, and name this "[content-end]".

And the last line, after the last column will be where full bleed content ends, so after the last "1fr" I'll write "[fb-end]".

Now, we have our grid template, but on the website things look a bit weird. So let's assign the grid children to their position in the grid template.

I'm going to start with the "fb-wrapper\_\_content" which contains the unicorn image and the text. We want to place that in the middle column, between the "content-start" and "content-end" grid lines. So in the "fb-wrapper\_\_content" selector, I'll write "content-start / content-end". This is the same syntax as if we'd written "2 / 3". But having named grid lines makes our styles a little more intuitive, I think.

Now let's place the "fb-wrapper\_\_full" element, I'll write "grid-column" and set it to "fb-start / fb-end".

And on the website, I'll zoom out a bit so you can see the whole thing. And let's go to the "Layout" tab, and highlight the "fb-wrapper" grid, then scroll down to the grid template diagram.

We can see that we have 2 rows in our grid-- created because we have 2 grid children and since we didn't explicitly assign either of them to a row, by default the browser will put them in separate rows.

So the hero\_\_wave image is going full bleed, and since it is the first grid child in the markup, it's been automatically assigned to the first row. Then the "hero\_\_content" is within the middle column, and is assigned to the second row.

So we need to explicitly assign both of them to the first row in the grid template, so that we can make them overlap. And since they're both in the same row, we can set them to the same "grid-row" value.

The easiest way to do this is to create a new selector inside "fb-wrapper" and write "right angle bracket" to target the direct child of "fb-wrapper", then a wildcard so the child element can be any tag. And I'll set this to "grid-row: 1 / 2" so both children will be placed in the first row.

Now when we save, if we go back to the "Layout" tab, in the grid diagram there is now only 1 row, and we can see that the unicorn is actually overlapping the wave image. Which is progress!

Now, we need to make the wave image aligned to the bottom of the grid. By default, the grid children will be aligned vertically to the top or start of the grid.

We can align just the wave image in the "&\_\_full" selector, and I'll write "align-self" and set it to "end". And when we save, now the wave image is aligned to the bottom of the grid.

The next thing we need to do is put the unicorn and hero\_\_text into 2-columns on desktop.
