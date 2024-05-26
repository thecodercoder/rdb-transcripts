# Mobile styles

So we've gotten our desktop styles down, but there are a couple small changes that we'll need to make for mobile. I do usually build my mobile styles first, before desktop styles, since the mobile design is usually more basic.

And it's often easier to start of building your HTML and CSS with the more basic version as the default styles, then add on the more complicated desktop design in your media queries.

But in this case the two designs are very similar so I built the desktop version first. Let's go to Figma and see what changes we need to add for mobile. In the design, they look very similar. They both have the logo and then 3 navigation links.

One thing I can see is that there's less space between the links on mobile. On the mobile design we have 20px of space between them, and on desktop it's 40px. Other than that, they are both vertically centered, and on mobile the text links are aligned to the far right like we have on desktop, and then any available horizontal space will be between the logo and the text links.

Let's go into our styles and adjust that spacing between text links for mobile. The text links styles are in the `topnav__links` selector, and we have that 40px space for desktop. Since everything else is the same, what I'm going to do is make the gap value 20px first, then add a media query to change to the bigger 40px gap for desktop.

To add the media query, I'm going to use our breakpoint mixin and target the desktop styles.

If you want to pause the video, see if you can remember how to write a desktop breakpoint using our mixin. And if you don't remember, you can always look in other Sass files to see how it was done before. Ok, pause now, and we'll be back in a second!

Ok, ready? So to add our media query, we want to use our breakpoint mixin. If you don't quite remember, you can look in the scss/util folder and the breakpoints.scss file. The breakpoint we want to use is the `breakpoint` one, which loads the sizes from the Sass map `$breakpoints-up`. And we want to target desktop styles, so we should use the `large` size in the Sass map, which targets viewports larger than 900px.

Going back into the Top Nav styles, let's add our media query within the `topnav__links` selector. Under our existing styles, I'll load the breakpoint mixin by writing `@include` and then the name of the mixin. If we look back up at the top, we loaded the util styles with the `u` namespace, so for the name of the mixin we need to write `u dot breakpoint`.

Then the breakpoint will take a parameter, in parentheses, and in that we type the size that we wanted to use from that Sass map in the breakpoints.scss file. In our case we want to target `large`, so we'll write `large` in the parentheses, without any quotes. Then we'll add a set of curly braces, and in them write our desktop styles.

I'm going to copy that `gap: 40px` rule from up above, and paste it in the breakpoint. Then back up I'm going to change that 40px to 20px, so that by default the gap will be 20px for mobile, then once the viewport hits 900px and above it will change to 40px.

Let's save this, and check out our website! First, on the desktop view, if we inspect the `topnav__links`, we can see the `gap: 40px` style rule that's within a media query. So desktop styles look good. Then let's slide over that developer tools panel to get the viewport width more of a mobile size. And now the `topnav__links` has a gap of 20px. Cool!

Let's look back at the design and compare with our website to see what other changes we might need to do. It also looks like there's less space around the Top Nav content on mobile than we have on desktop. On desktop if we select the logo, it has 20px of space on the top and bottom. On mobile, we have 12px of space.

Looking back at the website, let's figure out where we added that space. If we hover over the header elements, we can see that there is padding on the `topnav__wrapper`. And in the "Rules" tab, it has `padding-block` set to 20px. So we'll need to change this to 12px for mobile.

In the `&__wrapper` selector, with the ampersand symbol standing in for the parent selector, the `topnav` class. So the full selector for this is the `topnav__wrapper` class.

And in here, we're going to follow a similar approach as last time, where we'll add a desktop breakpoint with our mixin, put the desktop style for padding-block in the mixin, and update the padding-block before the breakpoint with the mobile value.

First let's add the breakpoint mixin after the style rules in `topnav__wrapper`, before the nested `nav` tag. I'll do this by writing `@include u.breakpoint(large)` and then in curly brackets, I'll add the desktop style rule, `padding-block: 20px;`.

Then outside our breakpoint, we need to go back and change the initial `padding-block` value to the mobile value, which is 12px. And let's save, and see how it looks! Now, in the website, on mobile viewports, if we select the `topnav__wrapper`, we can see `padding-block: 12px` which is what we want on mobile.

Let's increase the viewport width by taking that bottom right corner of the mobile viewport and dragging it to the right, and as it increases, we can see the spacing change. And in the styles for `topnav__wrapper`, we can see that it's in a media query and the padding-block is now 20px. So that looks good, and matches the design.

Let's go back to the mobile design, and compare it with our website on a mobile viewport. Another difference I see is that the logo image is quite a bit smaller on mobile. It's 70px by 20px on mobile, and on desktop, it's 128px by 36px.

Currently, if we look at our website, the logo image tag is sized based on the width and height attributes that we added in our index.html file. We set it to 128 width and 36 height. And if we hover over the image tag, it does say "128 by 36". But we'll need to add styles to change the size between mobile and desktop viewports.

However, as I mentioned earlier, it's still important to keep the 128 width and 36 height attributes in our HTML so the browser knows what aspect ratio the image is, and how much vertical space to leave while the image loads so we avoid that weird jump in content after it loads.

The image tag has a class of `topnav__logo`, so we can add our styles there. And checking the design one more time, for mobile, the logo is 70px wide. And then it is 128px wide for desktop. And I'm just going to show you this because there are a couple new things when dealing with images.

In VS Code, in the `topnav.scss` file, we're going to put these image styles in the `topnav__logo` selector. Again, we're going to need a media query for desktop styles, so I'll add our mixin in here with `@include u.breakpoint(large)` and curly brackets.

Now, let's write our mobile styles before our media query. The mobile logo is 70px wide, so I'll write `width: u.rem(70)`. And I'm using our rem() function to size this because we do want it to get bigger if the browser base font size gets bigger. Now, for the height, instead of setting it to a static size, I'm going to write `height: auto`.

This is useful for responsive images because it lets the browser calculate the height that it needs to be for the current width, so you don't have to set height every time the width changes. Usually when I'm loading images, I'll do something like this where I set the width to an actual size, and then set the height to auto.

Then, in our large breakpoint, I'll change the width to the desktop size, and write `width: u.rem(128)`. And for desktop, the height will still be `auto`, so the browser will automatically set the proper height for this width.

Let's save this and check it out on the website! Now on our mobile viewport, we have a smaller logo image. And as we increase the viewport width, at our 900px breakpoint it will change and be the larger size. And the height has changed along with our new width. We can see in the "Rules" tab, the media query with the desktop width for the `topnav__logo`. So the logo size looks good.

Now let's compare the mobile view of the website with our mobile design to see if there's anything else. And they look pretty identical, so I think we are good with the Top Navigation section! Nice!

Since we finished this section, we should commit our changes in GitHub. In the GitHub Desktop app, in the Changes tab, just eyeball all the files changed and make sure there's nothing there that we don't want to commit. And I think that looks fine.

And then in the bottom left, in the "Summary" I'll write our commit message of "Top Navigation", and click the "Commit to main" button to commit our changes. And it's also probably a good idea to push our changes up to GitHub, so on the top right, click the "Push to origin" button to do that.

Ok awesome! So next up, we'll be building the hero section.
