# Double-checking styles

So, I know that the last thing you want to do, once you've built something, is to go back over and check things. But I do try to do this as much as possible, because I know that I'm not perfect and there's usually at least one thing that I've overlooked. And in a work environment, the less buggy the website is when you hand it off to get reviewed by either your internal team or your client, the better.

Let's start with the mobile design, and I'm going to check spacing and sizing from the top down. First is to see how much distance there is between the unicorn and the top of the hero section, right under the top navigation bar. Selecting the unicorn and holding down Alt and hovering above the unicorn, it looks like we have 30px above the unicorn.

Now I'm going to the website and I'm going to turn on the iPhone emulation. And I'm going to right-click the unicorn image and select `Inspect`. If I hover over the unicorn, the space isn't there, so I'll go outside to the `hero__wrapper`, and hovering over that shows us that there's padding at the top of the wrapper (the padding is purple and the margins are yellow).

Let's find out how much padding is set. I'm going to select the `hero__wrapper` and then go to the `Layout` tab, and hide any Flexbox or Grid stuff because we don't need that right now, and look in the `Box Model` panel. And it tells us that there's 30px of top padding, and 60px of bottom padding.

The top padding of 30px matches the design. Now let's go back to the design to check if 60px of bottom padding is correct. In Figma, I'm going to select all the `Hero content` layer and holding down Alt, hover below it, and yes we have 60px of bottom padding.

Next up let's check the size of the unicorn image. On mobile it's basically 200px. Going back to the design, if we inspect the unicorn image, it is 202.5px. So it's just 2 pixels over. If that's not a big deal you can leave it as is. If you have to have it exactly 200px, we can try to adjust the width, 53vw makes it 198px, so let's try 53.5vw, and it's just a tiny bit over 200px. That is a bit more accurate, so let's copy that 53.5vw and go into our code, and paste it in the `hero__image` width. And when we save and reload, the unicorn is 200px.

Next is the space under the unicorn, between it and the hero text. If I hover over the unicorn, the space isn't there in a margin or padding, and if I hover over the `hero__text` there's no margin or padding that would add space there either. However if we go outside and click the parent, we can see in the styles that it's the grid parent. And in the style rules we have a gap of 40px. That's probably what's causing the space, but if you want to confirm that, we can go to the `Layout` tab, and in the `Grid` panel select the `hero__wrapper` grid and we can see that the gap is creating space between the unicorn and the `hero__text`. So let's go to the design and see if there's 40px of space. In Figma I'll select the unicorn and hold down Alt, and yes, we have 40px of space. So that's good!

Now let's check out the text elements in the hero. I'm going to check the font styles of the main header first. If I select the layer, in the right sidebar it says it's Source Sans Pro, bold weight, font-size is 42px, and the line-height is the same which would be 1.

Let's check that in our website. I'm going to inspect the h1 tag, and in our styles we're using the `clamp()` function for font-size, so to see the final calculated size let's go to the `Computed` tab.

Here we can see the font-size is very close to 42px, and the line-height is 42px, and font-weight is 700, and checking the font-family it is "Source Sans Pro".

Let's check the space under the h1 tag. There's a margin-block-end style of 1.25rem. Let's see what pixel value that is in the `Layout` tab-- and it's 20px. So let's check the design for that space. In Figma, I have the header selected, so I'll hold down Alt and hover below it and yes, it's 20px of space between the header and the paragraph under it. So we're good there.

Now let's check the styles for the paragraph text. It's 24px and 31px of line-height. If we go to the website and inspect the paragraph, then go to the `Computed` tab, we can see the font-size is just a bit above 24px, and line-height is about 31px. I think that's close enough. And there's a `margin-block-end` of 40px. So let's see if we have that amount of space under the paragraph in the design. In Figma I'll hold down Alt with the paragraph text selected, and hover over the buttons, and yep, we have 40px of space between the paragraph and buttons.

Next up let's check out our button styles, starting with the teal button. The button text is 18px, with a line-height of 18px. There's also a 5% letter-spacing. Let's check those on our website first. I'm going to inspect the button, and in the `Computed` tab look for font-size, which is 18px, and line-height is also 18px. Then for letter-spacing it says 0.9px-- let's see what we put it in our styles as. In the `Rules` tab if we scroll down a bit in the `button` class styles we have `letter-spacing` of 0.05em, which is the same as 5%. So I think the text styles are all good.

Let's also check the amount of space around the button text. The `button` class styles has padding of 0.75rem and 1rem. In the `Layout` tab we can see the actual pixel values, 14px of padding on top and bottom, and 16px of padding on left and right. In the design, if I select the button text and hold down Alt and hover in the button just above the button text, it says there's 12px of space on top and bottom, and 16px of space on left and right. That is 2px different from our website, which is weird.

Let's also check the total button height. In Figma the button is 42px tall. But if we check our website, the button is 46px tall. My guess is that this might be different because the second button has a 2px border around it, which adds to the height. In the styles for the primary button, I changed the padding-block to 0.875rem, which is 14px-- and if we look at the styles, the default button styles have a top and bottom padding of 0.75rem.

If we inspect the secondary button, the `Layout` tells us that that is 12px of top and bottom padding. Also, the second button has a height of 46px, and a width of 108 or 109px. Let's see what the design says. In the design, the second button is 104px wide and 42px tall.

Ok, I think these differences are due to Figma seeing the `padding` differently from the website. In Figma, if I select the secondary button text and hold down Alt-- and I'm going to zoom in to see this better-- the 12px of space and 16px of space are measuring to the outside of the border line, which means that they are including the 2px of border when measuring the space.

But in the website, the secondary button, in the `Layout` tab, the 12px and 16px of padding only goes up to the border, it doesn't include it. So to truly get the website to be more accurate to the design, I think we need to reduce all button padding, on all sides, by 2px to take that border into account. Then I think the heights and widths will be the same.

So let's try that in our styles. Our button styles are in scss/globals/button.scss. And in the `button` class padding, I'm going to reduce both padding block and padding inline by 2. So instead of 12 and 16, we'll have 10 and 14. And in the primary button styles, we'll need 2px more padding on all sides. So I'm going to copy the `padding` rule from the default button styles, paste it instead of the `padding-block` rule, and then add 2px to each number so we have 12 and 16.

Let's save, and now check the button heights and widths on the website. The first button is 130 or 131 by 42px. And in the design it's 130 by 42. I'm not going to make a fuss about a 1 pixel difference, so I'm happy with that. Then the second button in Figma is 104 by 42. And in the website it's 104, almost 105, by 42. So again, that's close enough in my book. And I think we're good on the button styles!

We do need to check the space between the buttons. The primary button has a right margin-- and in the styles it has `margin-inline-end` of 20px. Going back to Figma, I'm going to select the first button and hold down Alt, and there is 20px of space between it and the second button. So that's great.

And I think that's good for the mobile hero styles, since we already checked the space at the top and bottom of the hero content.

Next up, let's check the desktop styles. I'm going to turn off the iPhone emulation, and go to a width where the wrapper is 1200px.

And I'm going to go to Figma, and in the desktop design start by checking the header text. It's bold, has 72px for the font-size, and the same line-height, and it has 20px of space under it to the paragraph text. Going to the website, I'm going to inspect the h1 tag, and go to the `Computed` tab to get the pixel values. The font-size is 72px, and the line-height is the same, and the font-weight is 700 which is bold. So that's all the same. And in the `Layout` tab there is 20px of bottom margin. So that seems good!

Next up, in the design, the paragraph text is 28px font-size, 36px line-height. And it has 40px of space under it to the buttons. In the website, if I inspect the paragraph and go to the `Computed` tab, the font-size is 28px, line-height is just a bit more than 36px, and I can also see `margin-block-end` of 40px. So that all seems the same. In the `Rules` tab the line-height is coming from our global typography styles for a line-height of 1.3. The line-height is slightly different but I don't think 0.4px is going to make that much of a difference.

Now let's check on the buttons. In the design, the buttons on desktop are actually the same size as we have on mobile. The first one is 130 by 42, and on mobile it's the same, 130 by 42. So since we already checked the button styles on mobile I think we are good on that point.

Let's also check the unicorn image size. On desktop it is 483 by 486 pixels. And on the website if we inspect the unicorn it is 483 by 486. So that's good.

And we also want to check the padding around the hero section. On the website the `hero__wrapper` in the `Layout` tab, has 40px of padding top and 80px of padding bottom. In Figma I'm going to select the `Hero Content` layer to select all the hero content, and holding down Alt, there's 40px of space on top and 80px of space on the bottom. So that's correct.

Last, let's check the layout of the hero text and hero image. I'm going to turn on the Layout grid, if you don't have it on already. I'll select the Desktop frame and then click the eye icon to show the grid. And the hero text is taking up 6 columns out of our 12-column layout grid, and the image is taking up 5 columns. And they are vertically centered to each other.

On the website, I'm going to inspect the `hero__wrapper` div, and in the styles we created a grid-template-column with `6fr` for the first column and `5fr` for the second column. And just eyeballing the hero text, it's 589px wide, and let's see what it is in Figma. In Figma it's 594px wide. So that's really close. The other thing I check is if the words break at the same point. So in the design the main headline is 2 lines, and has `unicorn` on the second line. And we have that on our website. Then on the website, the paragraph is 3 lines, and it breaks, with `startups` and `millions` as the first word on the 2nd and 3rd lines. In Figma, it's also 3 lines, and we have `startups` and `millions` as the first words. So that all looks good!

The last thing I want to do is check over the hero.scss file and remove any selectors or code that we don't need. In VS Code, we do have a bunch of commented out lines-- in a real project I would probably remove all of that. But I'm keeping in the file so you can have it for reference to see the flexbox styles. If we scroll down we do have some empty selectors, the `hero__title` and `hero__content`, and I'll go ahead and delete those since we don't need them. And then save our hero styles.

Cool. So at this point, in a real world website, I would feel comfortable enough that the website matches the design and would hand it off to get reviewed internally.

Now that we're done with the hero styles, let's create a new commit in GitHub Desktop with our changes. So just scanning the `Changes` tab to make sure everything we're including seems right. And in the `Summary` section I'm going to title this `Hero`, and commit the changes to main, and push to origin.

Next up we will be moving on to the 3-column feature section!
