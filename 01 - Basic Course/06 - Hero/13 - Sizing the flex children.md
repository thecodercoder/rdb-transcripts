# Sizing the flex children

So now we have the basic 1-column to 2-column responsive layout working with flexbox.

However, I wanted to take a bit of a deeper dive into how sizing works with flexbox, because sometimes you might size a flex child using the `flex` property, but it doesn't end up looking the way you were expecting.

One possible reason for this is because you can affect the width of flex children if you've also set width properties, like `width`, `max-width`, or `min-width`. Another possible reason is if you have an image tag as a flex child, the size may be affected by the actual size of the image file.

It can be confusing and frustrating when you're working with flexbox and the flex child items aren't the size that you are expecting-- I know that it tripped me up a lot and it still sometimes does. So I'm going to show you what's going on, and how you can make sure your flexbox children are sized the way you want.

Right now, I have the website with Responsive Design Mode turned on, and the viewport width is set to a desktop width of [XXX]. And we're kinda zoomed out so you can see the whole website.

Things look pretty close to the design. Now we're going to look at the unicorn image and see how the browser determines what size it should be. If we inspect the image, and in the `Layout` tab scroll down to `Box Model Properties`, it tells us that it is 483 pixels wide.

Now let's scroll up in the `Layout` tab to where it says `Flex Item of div hero__wrapper`. This inspects the flexbox properties and tells us how that size is determined. At the top of the `Flex Item` panel, make sure that you have the image tag with class `hero__image` selected. You can also click that dropdown to see the other flex child item of the `hero__wrapper`, the hero text-- but we want to look at the hero image.

There's a little diagram of the width, and beginning on the right side it says `basis`. This correlates to `Base Size` which we can see at the bottom, and it also tells us in parentheses that it has the `width` property set to 62%, which is what we have in our `Rules`-- we set the width to 62% for our mobile design.

Going back to the `Layout` tab, we can also see that `Base Size` is zero. It is a little confusing because it says `width 62%` but that 62% isn't actually setting the width of the Base Size.

This is because `Base Size` is set from the `flex-basis` property. Remember, the `flex` shorthand property is made up of `flex-grow`, `flex-shrink`, and `flex-basis`. And flex-basis is the initial size of the flex child item.

If we go back to the Rules, where we set the `flex` shorthand property to 5, if you click that little arrow to expand it, it tells us that the initial size, the flex-basis, was auto set to 0%. This is why the initial or base size of the hero image is 0.

Then, under the `Base Size`, it tells us that the image was set to grow, and it grew greater than its Base Size of zero, to by [XXX] pixels. The image was set to grow because, going back to the Rules, we set `flex` to 5, which sets `flex-grow` to 5. Since the number is greater than zero, that means the flex child is allowed to grow from its Base Size if necessary, to fit in the flex container.

We can also see in the Rules that since `flex-shrink` is 1, the flex child is allowed to shrink. In our case, it didn't need to, because there was enough room for both flex children to fit on one row without needing to shrink.

However, even though according to the flex-grow, the image could grow [XXX] pixels, the Final Size is less than that. It's 483px. This is indicated by that padlock icon in the diagram-- that tells us that the size was locked, or clamped, by some styles other than the flexbox properties.

What's happening is that there is a Maximum Size coming from when we set `max-width` to be 30.1875rem which, is 483 pixels. And we can see this in our styles in VS Code-- we set the `hero__image` to have `max-width` of `u.rem(483)`. That max-width is clamping, or limiting, the final width to not be greater than 483 pixels.

If we go into our Rules and uncheck the `max-width` rule, the unicorn image grows slightly, and its Final Size is now set from flexbox, with the flex-grow property.

This kind of makes sense-- we are using the `flex` property to size the unicorn image, but then the `max-width` property is overriding the flexbox styles to prevent the image from being greater than 483 pixels. And you can assume if you set a `max-width` you really don't want the element to be bigger than that max-width, even if it goes against what flexbox might be trying to do.

However, something weird happens when we start reducing the viewport. I'm going to zoom in a bit, and then manually set the viewport width to 900 pixels so that it's just at the large or desktop breakpoint that we set in our styles.

And this still looks relatively like the design-- the unicorn image is taking up less space than the hero text, which is expected since we set the hero text to be `flex: 6`, which is greater than the `flex: 5` that we set the hero image to be.

But, what if we hadn't set the `width` property of 62%? It's pretty possible that you might not set any width properties for a flex child that is an image, especially if you're assuming that flexbox will take care of all the sizing for you.

Check this out. If I go into the hero image style rules, and uncheck the `width: 62%` style rule too, the unicorn is suddenly really large. What's going on here? Shouldn't the `flex: 5` rule for the unicorn image mean that it should always be narrower than the text on desktop viewport widths?

You'd think so, but this weird, unexpected situation is happening because of the image itself. Let's take a look at the `Layout` tab again. Here, we can see that the `basis` is still zero. And it says `Content Size` instead of `Base Size`, I think because we unchecked the `width` properties.

Then in `Flexibility` it is still set to grow because we still have `flex` set to 5. But then under that, instead of the `Maximum Size` coming from our max-width property, it says `Minimum Size` and it's set to 483 px. And this is the `Final Size` too.

Going back up to the diagram, the purple area with the arrow indicates what the size of the image would have been just based on the flexbox style rules. But then there's a lot of extra space as you go left, and then the `final` size has that padlock again, which tells us that the final size is coming from something other than flexbox.

So what's the Minimum Size, and where is it coming from? Let's do a little detective work. In our case, we have an image tag that is a flexbox child item. And if we look up in the source code, we can see that we have that `width` attribute set to 483. So let's test and see if that's controlling the size.

In VS Code, I'm going to to go to the index.html file and delete both the `width` and `height` attributes. And also just for testing purposes, let's comment out the `width` and `max-width` style rules, in the hero.scss file. We're doing this so we can figure out what is causing the unicorn image to be so large.

Ok, so now in our website, if we inspect the hero image, in the `Layout` tab, we still have that `Minimum Size` of 483px. So it looks like the `width` attribute doesn't control this.

What's actually happening here is that the image file itself is what's setting the Minimum Size. Images have what's called `natural dimensions,` which means that they have a size unrelated to CSS.

You can see this if you click on the image tag and hover over the `source` attribute, Firefox will pop-up a preview of the image, and it also tells us that the image is 483 pixels wide.

So what happened was, if we remove any width related properties from our CSS for the hero image, it will take its minimum width from the natural width of the image file, which is 483 pixels. And min-width will override flexbox sizing, so if we look in the `Layout` tab, flexbox wants to size the image at [XXX] px in the `Flexibility` section, but it gets overridden as 483px which we can see in the `Minimum Size`.

So now that you know this, what can you do to fix it, so that the unicorn image is sized according to the flexbox rules of `flex: 5`? Let's reload the website to refresh from our saved styles.

One thing I often do when working with images is to set a default width for all images, globally. I set it to 100%, right on the global styles. So in VS Code, if we go to scss/globals/boilerplate.scss, in the image tag selector, I'm going to add `width: 100%`. And I usually put width before height, but it doesn't matter a ton.

So now in our website, the unicorn looks closer to the design, and in the `Layout` tab, we don't have that weird `Minimum Size` set to 483 pixels anymore. This is because the `width: 100%` style rule is overriding the natural width of the image file itself.

And let's also go back to the index.html file and I'm going to press Ctrl-Z here to undo and put back the `width` and `height` attributes. And when we save, the unicorn still looks the same, which is good.

And going back to the hero.scss file, I do want to put back the `width: 62%` and `max-width` of 483px, because we need those for our mobile styles so the unicorn image doesn't get too big.

Now that we have the image working, let's check the size of all the hero elements on desktop. In the desktop design, when the wrapper is maxed out at 1200px, the hero text element is [XXX]px wide, the gap between the text and unicorn is [XXX]px, and the unicorn is 483px. Let's see how close our website is to that.

On our website, I'm going to select the Laptop view in Responsive Design Mode and show the `Layout` tab, `Box Model` so we can see the size of everything listed.

On desktop widths, the `hero__wrapper` is at 1200px, the `hero__text` if we click on it is [XXX], the `hero__image` is 483px due to the max-width property. This is pretty close, although in the design the `hero__text`was a bit narrower, at [XXX]px. And also in the design the word`millions` is on the last line, but on our website because there's more space it's on the second line.

So let's make the `hero__text` a bit narrower by increasing the gap a little bit. In our website, just in the browser, I might try increasing the gap in the `hero__wrapper` a little, to 10%. So now the `hero__text`is [XXX]px which is closer to the width in the design, and the word`millions` is now on the last line.

I think that's pretty close, so in our styles in the hero.scss file, I'll adjust the gap to be 10%, and save. And on our website things look pretty good. Let's try dragging the right edge to go down to tablet and then mobile widths.

And things are looking pretty good! The text stays readable, and the unicorn image seems to be a good size, not too big or too small on the different viewports.
