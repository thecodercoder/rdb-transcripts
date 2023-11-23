# Media Queries

Also, if you're not really into the clamp() function or it just seems like too much for you right now, you can always go back and use media queries. I know that some people are against using media queries these days, especially for typography.

But in my opinion, they still get the job done, and the code in your styles is reasonably understandable, even though it takes more lines of code. It won't fluidly scale as you increase the viewport width, but I don't think it matters too much.

Let me show you how you could set up the font-size styles using media queries. So if I comment out the font-size rule using clamp(), we'll leave the fallback font-size as our mobile size. And let's convert that to use our rem() function, so it should say "u.rem(42)".

Then we can add a breakpoint mixin and use "medium" for tablet styles, and set the font-size to something between 42 and 72 pixels, like 60px. Then we can add another breakpoint mixin for the "large" size and set the font-size to 72.

So again, this approach isn't as nice and efficient as the fluid clamp() function, because it requires more lines of code. If we save, and check out the website, the font size will change as the viewport changes.

You can see the breakpoints where the font size jumps in size, since it's not using the clamp() function which makes the font size change based on the viewport width as you change it. But it does work, and I think a lot of websites are still using media queries for font-size changes.

I just wanted to show you both options so that you can understand how they work. I'm going to comment out the media queries and uncomment the font-size using clamp() since I do think it's a better solution.

Let's now set up our font-size for the h2 tag, and use the Fluid Typography Calculator for that. Since you've seen me do it for the h1 tag, if you want, you can try to do it yourself for the h2 tag styles.

In the design, the h2 tag will be the smaller headings, like in the magenta full width block where it says "Angel investment matching in real time." So you'll need to get the font size for both desktop and mobile, and put them into the calculator.

If you want to try it yourself, you can go ahead and pause the video now, and then unpause when you're done to see if you matched what I will be doing.

[ pause ]

Ok! Let's set up the h2 font sizes.

Looking at the design, the headline text on desktop is 48px. And if we go to the mobile design it is 36px.

So, going to the calculator, we'll set the Min Font Size to 36px since that's what's on the mobile design, and we don't want the font size to be smaller than that. And the Min Viewport I'll set to the iPhone viewport width at 375px. Then the Max Font Size will be 48px, and I'll set the Max Viewport to 1200px.

Then let's copy the two font-size rules and paste it in our code, in the typography.scss file, for the h2 tag selector. And I'll reduce the decimals to be two places so they're not so long.

And if you want to use the rem() function so we still have the pixel numbers, you can replace the fallback font-size with "u.rem(36)" so it's 36 pixels converted to rems. And in the clamp() function the minimum number can also be "u.rem(36)" and the maximum will be the desktop font-size, "u.rem(48)".

Alright! Now we'll need to update the index.html file to include an h2 tag. So let's go to Figma and copy that h2 text "Angel investment matching in real time". Then in our index.html file, I'll duplicate the section tag, then in the copy, change the h1 tag to an h2 tag, and paste in the h2 text.

And in the website you can see the new section. If we inspect that h2 heading you can see the font-size getting set using clamp(). And let's check that the font sizes are working.

So I'm going to click on the Computed tab, and when we change the viewport down to a mobile width we can see the font-size goes down to 36px. Then if we increase it to a desktop width it maxes out at 48px. So that all looks good.

Let's go back to the design, to see what other h-tag styles we will need to add. In the 3-column Features section under the header, I think the title for each column can be set with h3 tags. So let's set those up as well.

First let's go to Figma and check the font sizes on desktop and mobile for these h3 tags. I'm going to select the header for the first 3-column feature, "AI-powered matching". It's 24px on desktop, and on mobile it's also 24px. Since they're the same, we don't need to use a clamp() function, which is kinda nice because it's less work for us.

In our typography.scss file, let's create a new selector for the h3 tag, and in it set the font-size to "u.rem(24)". Then we'll want to add more markup using the h3 tag so we can check that it's working.

In our index.html file, I'm going to select the section tag with the h2, duplicate it with Ctrl-D, then replace the h2 tag with an h3 tag. And for the header text, I'll go to the design and copy the "AI-powered matching" text and paste it in the h3 tag. Now let's check out the website.

If we inspect the h3 tag, we can see that the font-size is set to 1.5rem, and in the "Computed" tab it says 24px, which is what we want! So we should be all set for the header tag styles for now.
