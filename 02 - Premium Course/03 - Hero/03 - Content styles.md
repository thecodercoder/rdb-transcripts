## Hero content styles

If we go back to the index.html file, we can see that the unicorn image and "hero\_\_text" div are children of the "hero\_\_content fb-wrapper\_\_content" element. I'm going to target the "hero\_\_content" class to make this layout, since it's specific to the Hero section.

So, in our hero.scss styles, the "hero\_\_wrapper" class is what used to be the parent. And since that class doesn't exist anymore, I'm going to rename it to "hero\_\_content".

And let's use grid to build this layout. I'll add "display: grid", and then the 2-column layout is for desktop, so I'll add our breakpoint mixin with "@include u.breakpoint(large)".

And I'm going to add "grid-template-columns" and if you remember previously we'd set it to "6fr 5fr" since in the design the text is taking up 6 out of the 12 columns of the design, and the unicorn is taking up 5 columns.

So I'm going to set "grid-template-columns" to "6fr 5fr". And then for desktop, I'll adjust the order of the "hero\_\_image" and set it to "order: 2". And I want to align the unicorn all the way to the right, like we have in the design, so I'll also add "justify-self: end".

Okay, looks pretty good on the website. We still need to fine tune the padding in the hero, but let's get the mobile layout basically working first.

Let's go to iPhone view, and we have our 1-column layout. We do need to center the unicorn on mobile. So in our code, for the "hero\_\_image" I'll add "justify-self: center". And now it is centered.

Now let's start working on the spacing in the Hero section, starting with mobile. In the design, if we look at the mobile Hero, what we did before was add "padding-block" to add space inside the Hero section. However, it's a little trickier now that the hero-wave image is part of the grid parent.

If I select the "Hero content" plus the hero-wave image and hold down Alt, there's 40px of space at the top of the Hero section, but zero on the bottom since the wave is aligned flush to the bottom of the Hero section.

So we can use "padding-block-start: 40px" for the top space above the unicorn. But I think we'll have to add margin below the "hero\_\_content" to add space under the buttons. If I select just the "Hero content", it says there's 60px of space between it and the top of the hero-wave image.

Let's try adding that 40px of space to the top of the Hero, and 60px of space under the "hero\_\_content".

In our styles, I'm first going to add in the "hero" class, "padding-block-start: 40px". And I'm using pixels so that it won't scale up if the browser base font size increases, just so that space doesn't take up more real estate that we'd want the readable elements to have.

Okay, so we have the space on top. Now let's add, in the "hero\_\_content" selector, "margin-block-end: 60px". And we have space, but it looks a bit less than the design. Let's inspect that and see what's going on.

If highlight the "hero\_\_content" element, we can see that bottom margin in yellow, but it's going all the way to the bottom of the Hero section, and through the hero-wave image.

This is because we set the hero-wave image to overlap the same space in the grid that the "hero\_\_content" is containing. So we'll have to add the height of the hero-wave image to the margin.

In the website, the hero-wave image is about 20, almost 21px tall. Let's check the design to make sure it's the same, since we haven't added any styles to control the size of the hero-wave image yet. In the mobile design, the hero-wave image is 21 pixels tall.

Let's go back to our styles and add 21 pixels to the margin, so 81px total. And now there's more space, and it looks more similar to the mobile design.

We also need to add space under the unicorn. In the design, there's about 40px of space under it. For our website, let's add that space in the "gap" property of the "hero\_\_content" grid parent. I'll add it in our styles under the "display: grid" rule, to keep the grid styles together, and we'll set it to 40px.

Looks pretty good! However, if we zoom to 100%, the wave image looks a bit weird, there's a tiny bit of extra space on the left and right. I'm not sure exactly why this is happening, but I do know that if you want to stretch the SVG image and allow it to skew in order to fit, you have to add an attribute to the SVG code itself.

Let me show you what I mean. If I open the hero-wave.svg in VS Code, I'm going to add a new attribute called "preserveAspectRatio" and set it to "none". I mainly use this for decorative SVG images that I want to be able to stretch out of its original aspect ratio in order to fit the viewport.

And when we save, the wave looks a lot better, it's going all the way from left to right. For regular images like JPG photos, you don't want to skew the aspect ratio because the image will look weird. But it's fine for these decorative SVGs since they're just curvy lines.

Let's figure out the height of the hero-wave image as the viewport gets larger, because if the height gets larger, it will cut into that 81px of space that we added.

Changing to iPad view, things looks okay, but the hero-wave image is getting taller-- it's 45 pixels tall. It's getting taller according to the width and height attributes that we had set on the image tag itself.

And if we change to a Laptop view, the image tag is 80 pixels tall. And if we go even wider and change the viewport width to [XXX], then the image tag continues to get taller and is now [XXX].

Also for desktop, the unicorn isn't overlapping the wave, because of the margin-block-end that we added to the "hero\_\_content" for mobile. So we'll have to fix that later.

So, for the image, I think I'll need to use the Fluid Typography Calculator, and set that clamp() function to the height of the image. That way we can make it fluidly scale up, and also set a min and max height.

In the Fluid Typography Calculator, I'll set the Minimum to be the 21px height for mobile. Then the Max will be 80px for the height on desktop. And let's inspect the Result, and copy just the clamp() function since we're not using it for font-size.

And back in our styles, we actually need to add a selector for the "hero\_\_wave" class on the image. So I'll create it before "hero\_\_content", add "&\_\_wave" and set height and paste in the clamp() function.

Now, on the website, the "hero\_\_wave" image is 80px for the really large desktop. If we go to iPad, it's 52px tall, and on mobile it's 21px tall. Cool!

We also need to adjust the "margin-block-end" for the "hero\_\_content" div. Originally we had 60px of margin-block-end, and we added 21px because that was the height of the wave image. But since we're calculating the height fluidly now, we need to add that value to the 60px.

Instead of pasting the clamp() function in twice, I think what I'll do is create a CSS custom property just in the Hero section and set it to that clamp() function. Then we can use that custom prop for both the image height and the "hero\_\_content" margin-block-end.

So in the "hero" class I'll create a new local custom property called "--wave-height". And I'll cut that clamp() function and paste it in as the value. Then in the "hero\_\_wave" selector, I can set the height to be "var(--wave-height)". And copy that and for the "hero\_\_content" "margin-block-end" I'm need to add 60px to the clamp() function. We can do that in CSS with the calc() function which lets you do math with different units.

I'll write "calc()" then "60px plus" and paste in the "var(--wave-height)" custom property again. Now when we save, there's no Sass errors which is good. And let's check out the website.

On iPhone view, let's go into the "Layout" tab to see everything more easily. And the "hero\_\_wave" image is 21px tall, and the "hero\_\_content" margin-block-end is 81px. That's correct.

Let's go to iPad, and now the "hero\_\_wave" image is 52 pixels tall, and the margin-block-end is 112 pixels tall. And 52 plus 60 is 112 so that's right.

Now let's check out Laptop view, the image is 80px tall, and the margin-block-end for "hero\_\_content" is 140px tall. That's right too. And if we manually increase the viewport width, the "hero\_\_wave" stays at 80px which is what we want.

Let's now fix the unicorn not overlapping on desktop. In our code, we only want the "hero\_\_content" to have "margin-block-end" for tablet and mobile, not desktop. So I'm going to add in the large breakpoint, "margin-block-end" of 0.

And that looks good! We have the spacing set in the Hero section, and we have the unicorn overlapping the wave image.

Let's do a check to see how everything looks, starting from desktop widths. And that looks good. And as I slide the window over to reduce the viewport, things look pretty good as we go down to mobile.

However, I did notice that a little before tablet width, when we're still at the 2-column layout for the Hero content, it looks like the buttons are just starting to overlap the hero-wave image.

I think this is because at this viewport, the unicorn image is about the same height as the "hero\_\_text", so there's not a lot of room for the height of the wave.

What I might do is add some space to the top of the unicorn image, to push it down more, which will make the whole Hero content grid container taller, and hopefully push down the wave image so it's not so close to the buttons.

In our styles, we'll add that to the "hero\_\_image" selector, only for desktop, since we only want this space when the layout is 2-columns. I'll try just adding "padding-block-start: 20px". That looks better. Maybe a little more, I'll try 30px.

Ok, that looks pretty good. So now there is a bit more breathing room between the buttons and the wave, at those narrower desktop widths.

Great! Now we have added the wave image to the Hero section, and made it work on all viewports. So that's everything for the Hero section. I think now we can commit our code in the GitHub Desktop App.

For this commit, I'll write something like "Hero - add wave image". And then press the "Commit to main" button, and "Push to origin".

That's it for the Hero section, next up is going to be adding a new section, the Alternating Features.
