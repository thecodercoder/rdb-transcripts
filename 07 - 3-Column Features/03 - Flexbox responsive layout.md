# Flexbox responsive layout

First we're going to build a flexbox layout, using a responsive approach with media queries.

To start, in our website let's turn on the iPhone emulator to view the website for mobile. And right now, the Features content is stacked to 1 column, which is what we actually need for mobile. One thing I like to do is when I know I'll need flexbox or grid for multi-column desktop layouts, I still use it on mobile, because I can use the `gap` property to add space between the items. This is what we did for the hero section earlier.

Let's go to Figma, and looking at the mobile design, if I select one of the features, there's 40px of space between items. So we'll want to add flexbox to our styles, and set a gap of 40px between items. Looking at our markup, we want each feature in `features__item` to be a flexbox child item, which will make their direct parent, the `features__wrapper` div to be the flexbox parent.

Going to VS Code, in the features.scss file, we'll add flexbox by going to the parent selector, the `features__wrapper` class, and add `display: flex`. Now, if we go to the website, we have all the features squished together on the same line. This is because by default, the flex-direction will be set to `row`, and flex-wrap will be set to `nowrap`.

To put the flex children one after another, we could set `flex-direction` to `column` like we did in the hero section. If we put this in the browser styles you can see that it does work. But, another solution I wanted to show you is to set `flex-wrap` to `wrap` instead of the default `nowrap`, like this. This will put flex child items on a new row if their width is greater than the flex container.

Let's inspect the first `features__item` elements. Then in the `Layout` tab we can see that it says the base size of the content is almost 1000px. This is because with text, if you don't explicitly set a width, it will be as wide as possible, to fit all the text content on one line. But the browser will automatically wrap it to fit on the website.

We can actually see this in action if we go to the `Rules` tab, and making sure the `features__item` div is selected in the source code, click the `plus` icon to add a new selector for the class, and set `flex-shrink` to zero, instead of the default `1`. Now all the paragraph text is on 1 line, and it's super long, causing horizontal scrolling. Let's delete that rule, to make the `features__item` able to shrink in order to fit in the flex container.

What I want to do is use `flex-wrap: wrap` to stack the Features content to 1 column. Going to our styles, I'll add that under the `display: flex` rule. And while we're here, let's add that `gap` and set it to `40px`. And I'm going to use pixels not rems, because if the gap doesn't scale up as the browser base font size increases, it won't negatively affect readability. And now when we save and check out the website, it has that gap between Features items.

One thing we also need to do is add padding on the top and bottom of the wrapper, similar to what we did in the hero section. If I inspect the `hero__wrapper`, you can see we have that `padding-block` rule. Let's check the design and see what we would need to add for the `features__wrapper`. In the mobile design, if I select all the Features content, there is 60px of space on the top and bottom. And on desktop, if I do the same thing, we have 80px.

Let's see what the hero section had-- because if the padding is the same, then we might want to move those padding-block rules into the `wrapper` styles, not just the `hero__wrapper`, so other sections can use it too. On mobile, the Hero content has 30px on top and 60px on the bottom, so that's different. And then on desktop the Hero content has 40px on the top and 80px on the bottom. So the Hero section has slightly different padding, probably so there's less space from the top of the unicorn to the Top Navigation bar.

But let's also check the section after the 3-column Features, because that might have similar padding and then they can share styles. This is the magenta Fullwidth features section. And it's 60px on top and bottom on mobile, and on desktop it's 80px on top and bottom.

So I think since those 2 sections have the same padding, we can add those style rules to the global `wrapper` class. And then the `hero__wrapper` can override it with its own padding. Let me show you what I mean in VS Code.

Sometimes I forget exactly what file the style rule that I'm looking for is in. So I'll search in our Sass files. If you right-click the `scss` folder and select `Find in Folder`, then type in `dot wrapper` and here is our global wrapper style. And in the breadcrumbs under the file tabs we can see that it's in the scss/layout folder.

Let's add in those padding-block styles. In the `wrapper` selector, I'll add `padding-block` and then `40px`, and that will add 40px of top and bottom padding. Then for desktop we'll need to add our breakpoint mixin, so below those rules I'll add `@include u.breakpoint(large)` and in the curly brackets add the desktop padding rule, `padding-block: 80px`, to change the padding to 80px on top and bottom.

Let's save that and see how it looks, and hopefully it didn't mess up the padding on the hero and top navigation sections. In the website, the 3-column Features looks good. If I inspect it and select the `features__wrapper` div, in the `Rules` we can see the `padding-block` rule, so we know our change went through.

And the hero section also looks basically the same as it did before, which is good. Let's inspect that `hero__wrapper`. We can see in the `Rules` that it's getting its padding from the `hero__wrapper` padding-block rule. And below that in the `wrapper` class styles, we can see that `padding-block` rule but it's crossed out because it's getting overridden by the `hero__wrapper` styles. And the same in the `topnav__wrapper`-- it's overriding the `wrapper` class padding with its own padding rule of 12px.

One thing to note, in Firefox it will order the styles in specificity order, with the most specific at the top and then less specific below. You might be wondering, if both the `wrapper` and `topnav__wrapper` rules are class rules, those are the same specificity level, since they're both classes. So what determines the `topnav__wrapper` overriding the `wrapper` styles?

That is because of the cascade in CSS, where styles that come later on will override previous style rules if they are both on the same level of specificity. Let me show you this in VS Code. The wrapper styles that we just added are in the `layout` folder. And the topnav and hero styles are in the `components` folder.

And if we go to our main Sass file, style.scss, we've first loaded the global styles, then the layout styles, and last, the component styles. This means that when we compile all our Sass styles to our final style.css file, the component styles will come after the first two styles. And this order is on purpose, because we want the component styles, like in the top nav or hero sections, to be able to override the more global styles from the globals and layout folders.

So if I move the `@forward layout` rule AFTER the components, and save, we can see on our website that the top nav and hero sections padding has changed. And if we look at the `topnav__wrapper` styles, now the `wrapper` class styles are at the top, meaning they are overriding any identical style properties from the `topnav.scss` file.

This is one reason why order is very important when you're writing your styles. Let's change back the order in our main Sass file now, and save. And going back to the website, the padding is back to normal.

Ok, now that we've gotten the padding set, let's work on the 3-column desktop layout. In the website I'll go to the Laptop viewport width. And, for desktop we do want the 3 features to be side-by-side on the same row. So let's turn off the wrapping in our styles. The `flex-wrap: wrap` rule is what put each feature on a new row, so I'm going to cancel that out for desktop.

In the `features__wrapper` selector, we'll create a new large breakpoint by writing `@include u.breakpoint(large)` and then in it write `flex-wrap: nowrap`. And now when we go back to the website, the features are all on the same row, but if we slide over the dev tools panel, it goes back to a 1-column layout.

However, if we look at each of the features, they are actually different widths. Let's see what's going on here. In the source code, I'm going to click the `flex` label to turn on the flexbox highlighting, and then change the color to something more contrasty.

Let's select the first `features__item` and in the `Layout` tab Firefox is saying that basis, meaning the `flex-basis`, of the item is its content size, [XXX], and then it's shrinking to fit. And again, this is because if you don't set flex-basis, it will default to `auto`, which in this case is the size of the content itself. And the paragraph text is initially going to try to fit everything on one line, which is why it's so large.

Then let's click on the second `features__item`, and this one has a larger flex-basis size, because it looks like it has more text than the first one. And the last one has the smallest flex-basis size, because it has the least amount of text.

So, for our website design, I want the 3 columns to be the same width, instead of having different flex-basis values based on the amount of content they have. One quick way that you can do this is by setting `flex: 1` for all the flex child items. Let's do this in our code.

In features.scss, in the `features__item` class selector, we'll want to add these flexbox styles in a large breakpoint. So I'll write `@include u.breakpoint(large)` and in it add the `flex: 1` style rule. Using an integer, meaning a number without a unit like px or percent, will make the `1` be assigned to flex-grow. Then flex-shrink will automatically be set to 1, and flex-basis will automatically be set to 0%. This will make the base size of each child the same, zero, and then they will grow the same amount since they all have flex-grow set to 1, making their final size the same.

Now when we save and check out the website, the 3 columns look more equal in width. Let's confirm that they're exactly the same in the `Layout` tab, and select the first `features__item` element in the source code. It says the final size is [XXX]. Now click on the second `features__item` and it looks like it's the same width. And if we click on the third item, it also has the same Final Size. So they're the same!

And let's test things out by reducing the viewport width. The 3-column layout looks good, we have space between the items, and as we narrow the viewport width the `display: flex` rule isn't applied anymore, making the content go to 1 column.

Let's look back at the design and see what else we need to change. On desktop, if we compare the design with the website, I think we need a bit more space between the features. Right now, we have a gap of 40px, which is what we needed for mobile. But on the design, we have 80px of space between items.

Let's change the gap for desktop. In our features.scss file, we're going to go to the flex parent selector, `features__wrapper`, where we set `gap`, and in the large breakpoint I'll add `gap: 80px`. And let's save and see how this looks. On viewports where the wrapper maxes out at 1200px, it looks good, and as we get narrower, it's not too bad, but right before the mobile breakpoint where it stacks to 1 column, the features content does look a bit narrow.

I might try making the gap a bit more responsive by using percentage instead of always being 80px. Since the gap is 80px when the wrapper is 1200px, if I use my calculator and divide 80 by 1200, it's about 6.67%. Let's try adding that just in the browser first. And it does help a bit! The title on the second feature is still breaking to 2 lines, so if that's an issue for you, you could try reducing the gap a bit more. I'm ok with the 6.67% because the title breaking is only happening on a very narrow range of viewport widths.

So I'm going to go back into my styles and adjust the 80px gap to be 6.67%. And, I'm using percentage instead of viewport width units because they are based on the parent's width. So as the viewport width gets larger, once the wrapper maxes out at 1200px, the gap will also max out at around 80px. If we used vw units the gap would continue to increase as the viewport increases, which wouldn't be desirable.

I think we're pretty good on the desktop version, let's now use the iPhone emulator to look at our mobile site. The biggest thing I can see is that in the design, all the content in each feature is centered-- both the icon image and the text.

You can center text by adding `text-align: center`, so let's do that in our styles. I think I'm going to center the text in the `features__item` selector, and since we want it centered on mobile, I'll add it in the initial styles, not in the large breakpoint mixin. We could also write this style rule in the `features__wrapper` selector, as any child element would inherit the style. But I think I'd rather keep it in the `features__item` selector, just in case in the future we add a features item that we don't want to be centered. But honestly, either place will work just fine.

Let's save that and see how things look. Going back to the website, we can immediately see that the text in the features is centered, but the icon image is not. What's going on here?

The reason the icons aren't centered is that-- if we select one of the image tags in the source code-- we set them to `display: block` so that they wouldn't have the extra space at the bottom for the descender letters. If I uncheck the `display: block` rule in the browser, the image tags go back to their default setting of `display: inline` like the text, which lets them get centered from the `text-align` rule. You can also see that the text content gets moved down slightly due to the space for letters with descenders getting added below each image.

If we check the `display: block` rule again, there is a way to center block elements, if we add `margin-inline: auto`. This is the same way we centered the `wrapper` class content in the page, since it's also a block element. So in VS Code, in the `features__icon` selector, I'll add `margin-inline: auto`.

Now we have the mobile styles working. But when we increase the viewport to desktop everything is still centered. What we need to do is override or cancel out the styles centering content for desktop viewports. For the `features__item` we can override it by in our large breakpoint mixin, adding `text-align: left` or `start`. They're the same thing when the writing direction on the browser is left to write, and both work, but I am trying to use more of the logical properties like we have with padding and margin.

And when we check the website, we can see that the text is left aligned on desktop, and when the layout breaks to the 1-column layout it goes back to being centered.

For the icon image, in the `features__icon` selector we'll have to add our breakpoint mixin by typing `@include u.breakpoint(large)` and then setting `margin-inline` to zero. If you really want to minimize the lines of code, let me comment out the mixin, and then we could add a `breakpoint-down` mixin with `@include u.breakpoint-down(medium)` so that anything smaller than desktop widths will be centered. And you won't have to cancel out the mobile styles on desktop. Both approaches work, so you can use whichever one you like better.

Now, in the website our icon images are centered on mobile, and going to desktop widths they are left aligned along with the text.

And as I'm decreasing the viewport width, I'm noticing that right when it breaks to 1 column the lines of paragraph text are pretty wide, probably wider than is optimal for readability. And also the last `Protected Payments` feature is shifted to the left a bit. I think we can fix the horizontal alignment by centering the flex items with `justify-content: center`. And that looks better, so let's add that in our styles, in the flex parent, `features__wrapper` selector.

And now on the mobile website the features are all centered. And if we check the desktop version, this didn't mess anything up alignment wise, because the features items are all the maximum width allowed, so other than the gap that we set, there's no available space to align the items inside. If we for some reason limited the width of the flex items-- like if I set the `features__item` desktop styles to be `flex: 0 0 200px` so that they will be stuck at 200px and can't grow or shrink, then if I turn on the flexbox highlighter you can see the items are now centered with the extra space on the left and right side. But we don't need to worry about that since if we uncheck the rule the flex child items will grow to take up all available space aside from our gap.

Now, let's go back to the wide 1-column viewport width, and try to limit the length of the paragraph lines. Let's inspect one of the paragraphs, and in the `features__description` selector, I'm going to add a max-width property and set it to 50ch. The `ch` unit is short for `character`, and it measures the number of characters of text in a line. So we're not letting the paragraph get any wider than 50 characters. This is nice for controlling text width because the final pixel width will change based on the font-family and font-size.

I think that looks pretty good, so I'm going to copy that rule and paste it in the `feaures__description` selector. And when we save, now on the website the features items are bit more readable instead of being really long lines. Cool, so now if we look at the Features section on both mobile and desktop widths, things look pretty good!

So that's how I personally would build the 3-column features layout, using a responsive flexbox approach with media queries.

However, I did want to offer an alternative way of building this using a more intrinsic flexbox approach that doesn't use media queries.

This is optional, you don't have to go through it. But if you're curious how it compares to this one, it's up in the next video.

If you don't want to go through it, that's totally fine, just make sure to go into GitHub Desktop and commit your changes for this section. I would use a commit message saying `3-column Features`. And then commit to the `main` branch, and push to origin.
