# Unicorn image

Let's start with the unicorn image, and make sure it's the right size for both mobile and desktop. In our mobile design, the unicorn is about 200px wide. On desktop it is 483px.

Let's go into VS Code and check what class the unicorn image is for our selector. The unicorn is in an image tag with a class `hero__image`. So in our styles, we'll be targeting the `&__image` selector.

We could do a classic responsive style approach with media queries here. So first we'd set the `width` property to the mobile width, 200px, using our rem() function. And then we can write a media query using our breakpoint mixin, with `@include u.breakpoint` and in the mixin use the `large` size for desktop. And then in that, we'll set the width to 483px, again using our rem() function.

Let's save and see how that looks. On desktop, we have the big image, and the width is 483px. Then let's slide over the developer tools panel to decrease the viewport width to a mobile width. The the unicorn gets smaller, which is great. However there's a ton of space on the top and bottom.

If we inspect the image, the width is 200px, which we set in the styles. But the height is 486px. And if we go back to a desktop width, the height of the unicorn is also 486px. So why is the height stuck to 486px?

Well, if you look at our styles, we only set the width, not the height. And in the HTML source code, the image tag has the width and height attributes set. And the height is set to 486, which means 486 pixels. That 483 width attribute will get overridden if you change it in the styles, but since we didn't set a height, it's using the height attribute value of 486.

In the top navigation section, we had to size the Mythos logo. And if you inspect the logo image, in the styles you'll see that we set the width to 4.375rem, and the height is set to auto. We also added `display: block` to get rid of that little space under the image for the descender letters, and we should probably add that to the unicorn image as well.

In fact, since I think most if not all the images we'll be working with will need `display: block`, it might be most efficient to add it as a global style for our image tags. So let's add that in our code. In VS Code, which Sass file should we add that style rule to? I'll give you a few seconds.

So, I think that I would add it to the globals/boilerplate.scss file. This is where we've been writing some global styles for different tags, other than the text tags that we have in typography.scss. So in our boilerplate styles, I'm going to add a new style under the body tag styles, and the selector is going to be the `img` tag. In there I'll add `display: block`.

And, since we have this here now, we don't need to add it manually to the logo image. If you don't remember where it is, you can run a search in VS Code to find any instances of `display: block`. In the Solution Explorer, right-click the `scss` folder and select `Find in Folder`. This will run the search in the scss and any subfolders.

In the search bar type in `display: block`, and you can see that there are results in topnav.scss and boilerplate.scss which we just added. So we want to remove that rule from the topnav.scss file. Double-click the `display: block` line under the topnav.scss file, and VS Code will go straight to the file and location.

And now we can remove that rule and save. And actually, we could also take that `height: auto` rule and move it into the boilerplate styles as well, since it looks like we'll be using that for most images. So select that rule and cut it, save the topnav.scss file. And then let's go back to the boilerplate.scss file and paste it in the image tag selector.

And we can go back to our hero styles and delete the `display: block` rule. Now, since we added those two rules for all image tags, we should check and make sure they are getting loaded correctly.

In our website, let's inspect the logo image, and see if those two rules show up in the style rules. Do you see them? In the styles, we can see that the logo is getting those two rules from the image tag, and it also tells us that the styles are coming from the boilerplate.scss file, which is right where we added them.

So the logo image looks good. Let's inspect the unicorn image, and again we can see that it's inheriting the those two styles from the boilerplate styles.

Ok, that was a slight tangent, but I think it was worth it to save time for future image styles. Let's now check the unicorn sizing. The desktop image looks good, and when we reduce the viewport width to mobile the width changes to 200px, and the height changes with it to keep the correct aspect ratio.

So now the unicorn is technically responsive-- it's changing size as the viewport width increases. But there's just 2 sizes, and if we go to Responsive Design Mode and select an iPad, the unicorn looks pretty small, and should probably be a bit bigger there since there's so much more room.

So instead of media queries, we can try to make the unicorn image responsive with a more fluid approach, using a relative unit that will change with the viewport width. Two good options for that are the percentage unit, and the viewport width unit.

Going back into our code, let's delete our existing responsive approach, and create a new style rule that sets the width to 50%. And let's see what that looks like on the website.

Now, the desktop version has a large unicorn image-- if we inspect it, it's 600px, and as we reduce the viewport width the unicorn fluidly scales down with it. Pretty nice, right? And this doesn't require media queries.

What percentage does is it sets the width of the element to 50% of the width of the parent. So at desktop widths where the wrapper maxes out at 1200px, the image is half of that, 600px. And if we use the Responsive Design Mode and set it to iPhone, the wrapper is 327px wide, and the image is about 163px.

The percentage is based off the actual content size of the parent-- if we inspect the wrapper div, the `Layout` tab tells us that there's 24px of margin on either side, and the actual content in the blue box is 327px. So any margin or padding will not count towards the parent's width.

If we turn off Responsive Design Mode and go back to the wide desktop width, this is why the unicorn doesn't get wider than 600px. Because we set the max-width of the wrapper to be 1200px.

Now, let's compare that with another relative unit, the viewport width unit, which we've used previously when setting our typography sizes using the clamp() function. In the browser, I'm going to change the width value to `50vw` instead of 50%. And the unicorn gets a lot bigger.

This is because the viewport width unit isn't based on the parent element's width, but on the entire viewport. So for really large desktop screens, the unicorn width would continue growing as it increases. That's one big difference between percentage and viewport width.

And if we turn on the iPhone emulation, the unicorn is 187px, which is bigger than it was with 50%. This is because again, the percentage width is based on the parent's width, and doesn't count margin or padding, only content. The viewport width is based on the entire viewport, which is wider than the wrapper div.

So which one should you use? Well, I think you could use either, to first get the image to the right width on mobile, and then set a max-width on the desktop side to prevent it from growing too large.

With percentage, we can increase it until the unicorn is around 200px, so about 61%. And if we go to desktop, the unicorn is larger than it is in the design. In the design, the unicorn is 483px. So in our styles we could add a max-width of 483px, to limit the width.

And you could do the same thing with viewport widths. On the iPhone, if we change the unit to `vw` instead of percentage, we can edit the number with the arrow keys, and if we hover over the image tag at the same time, we can monitor the width as it goes down until it hits 200px. So somewhere around 53 or 53vw. And going back to desktop mode, keeping that max-width will allow the unicorn to grow but not get bigger than 483px.

In this case, I think one of these approaches is shorter than using media queries. Either is fine. I'll just copy both style rules, and paste them in our `hero__image` styles. And replace the 483px with the rem() function so it's more accessible. I'll keep the commented out media query approach, just in case you'd like to keep it for reference.

And let's save and check the website. And the unicorn image looks good, we can see the style rules we added, and the unicorn scales up and down nicely as the viewport width changes!

Next, let's get our text styles working.
