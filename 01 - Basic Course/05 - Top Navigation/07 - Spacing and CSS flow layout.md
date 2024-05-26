# Spacing / CSS flow layout

Let's take another look at the design for the Top Navigation, and see what sticks out as something we need to change in the website.

One thing I notice is that we need to add some space on the top and bottom of the top nav elements. Right now the logo and links look really close to the top and bottom edges of the bar. If we look back at the design and select the logo, then hold down Alt, Figma tells us that there's 20px of space on the top and bottom of the logo.

To add space like this, where it's between an element and the edges of its parent, as opposed to space between two elements, I generally like to use padding. What I'm going to do is add padding to the parent element, the `topnav__wrapper` class div. I only want to add padding to the top and bottom, which we can do with a new-ish property called `padding-block`.

Let's go into our code, and for the `topnav__wrapper` I'm going to add the `padding-block` property and set it to `20px`. This is adding 20px of padding only on the top and bottom. And like with the `gap` that we added between the top nav text links, I'm going to use pixels so that the space won't get huge if the browser base font size is increased.

Now if we look at it on the website, we can see that there's more space between the top and bottom of the navigation bar. If we inspect the `topnav__wrapper` class div, in the "Layout" tab, "Box Model" panel, it tells us that there's 20px of padding on the top and bottom.

And it also shows us how much margin we have on the right and left. If we turn on "Responsive Design Mode" and set the viewport width to smaller than 1200px, like 900px, the margin on the sides goes down to 24px.

This is because of the width property that we set earlier where the width of the wrapper is 100% minus 3rems, and the extra space gets divided between left and right margins since we've centered the wrapper with `margin-inline: auto`.

And then the width gets maxed out at 75rem which is 1200px. So for viewport widths less than 1200px, we'll have that 24px of space on the left and right, and if we increase the viewport width to 1300px and zoom out so we can see everything, for viewports greater than 1200px the width of the wrapper will remain at 1200px and it will be centered on the page.

Now if we take a look at the navigation bar, this is pretty hard to see, but if you look at the logo there's actually a tiny bit more space below the logo than above it. So let's check that out. I'm hovering over the `topnav__homelink` anchor tag so you can see its box.

You can see that while on the top side the letter "h" goes all the way to that top edge, on the bottom side there's a tiny space under the bottom of the lowest letter, the letter "y". To make it easier to see, I'm going to go back into VS Code and add a style rule for `topnav__homelink` to say `outline: 1px solid`. This will add a white outline so we can see things better.

The reason that this small space is happening is because of the image tag and something called the CSS flow layout. We've talked a bit about default browser styles, and how some HTML tags have them.

Some of those default browser styles will determine how elements will be displayed on the page, even if you haven't written any CSS rules to control the layout. For example, right now the text elements in the content on the page under the purple Top Navigation bar, are all getting displayed according to some of these default rules.

And as I've mentioned previously, this was because back in the day before CSS really existed, we only had HTML tags. And so the browsers needed to have a set of rules guiding how HTML elements would get displayed.

On the web, the flow layout or normal flow, is how elements will get displayed on the page by default. There are two default ways that elements can be displayed-- block and inline.

You can think of block elements like paragraphs: they will take up the maximum width available from their parent, and if you have multiple block elements they will get displayed one after the other, like paragraphs.

Inline elements will by default take up only as much width as their actual content, and they will get displayed next to one another in the normal flow of the page. They will wrap to a new line only when all the space on the previous line gets filled up.

Most of the elements that we've been working with, like divs, h-tags, and paragraph tags, are block level elements. You can see this on our website so far, where the header tags and the paragraphs take up 100% of the available space.

One of the most common inline elements is the `span` tag, which is similar to the `div` tag in that it's a generic tag that doesn't have any visible styling attached to it.

We can test this out if we go to our index.html file and in the first paragraph, I'll enclose some of the text in the middle of it inside a span tag. And I'll add a second span tag right after the first one with some additional text inside it.

Now if we check out the website and open that first paragraph tag, if I highlight the span tags, you can see that they get displayed side by side, wrapping to a new line when the text content inside reaches the end of a line.

One important quirk to remember about inline elements is that margin and padding don't affect them the way you might think. In the browser, I'm going to select the first span, and then in the "Rules" tab, I'm going to add an `outline: 1px solid red`.

So now we have a red outline around this first span tag. You can see it starts next to the text that was inside the paragraph tag, and it just kind
of goes all the way out to the right.

But then when it runs out of space, it starts wrapping on the second line. And you can see where that ends. We can do the same thing to the second span tag.

So the second span tag, let's select that. And then down in the DevTools, I'll say outline, one pixel, solid, and let's say maybe blue. So we can see that the span tag, the second span tag in blue, is starting right after the first span tag in red ends.

Then I'm going to add `margin: 20px` which is supposed to add 20px of margin on all sides: top, right, bottom, and left. So now you can see that it changed a little bit. And let me uncheck the box and check it a couple of times just so you can see.

On the website, we can see that the margin is only adding space on the left and right sides. The margin on the left is creating actual space between the previous text. However the margin on the top and bottom are just overlapping the content above and below it, and not moving anything around.

And if we change this from `margin: 20px` to `padding: 20px` the same thing happens, the padding is showing up in purple. And only the padding on the left and right are actually doing anything. The top and bottom padding are overlapping with the other existing content on the site.

This is because with inline elements like spans, their `display` property is defaulting to `display: inline`. We can actually see this if we inspect the span, and in the "Computed" tab, check the "Browser Styles" checkbox to display all the default browser styles, then filter for `display`. We can see that it's set to `display: inline`.

Versus if I click on the paragraph tag itself, display is set to block by default. If I click on the h1 tag, it also defaults to display block. Let's go back to our span tag.

With inline elements, the browser is keeping the element in the normal flow vertically, which means that it won't be on its own line, but rather next to other elements. So this is why the vertical margin or padding won't have any effect.

Only horizontal margin and padding will take effect. There is a difference with padding-- if you add padding, the border or the outline in our case, will include the padding and be outside the padding.

Versus if we're using margin, margin will be added outside of the border or padding. So that's why they look a little different.

However, if we add a `display: block` rule to the span, you can see that things have changed a lot. it will then be in its own `block` which means it will take up 100% of the available horizontal space and be on its own line.

And we can see if we force the highlighting that the top and bottom margins are taking up space and kind of pushing the elements away.

There's also a hybrid of inline and block, called `inline-block`. And let's use that with the second span. I'm going to make the second span a bit shorter so it will be less than the entire line.

So let's save that. So now, and it's sort of reset all of our styles.

So now the first span, let's set it to display block and set a margin of 20 pixels and then our outline of one pixel solid red. So the first span is display block, so it's taking up the entire space, and it's on its own line.

The second span, I'm going to set this to first an outline of one pixel solid blue. And we'll set margin of 20 pixels there too. And let's set this to display inline block.

Right now, it's the default display inline. So display inline block. So you can see that things do look a bit different, right?

Before, when it was inline, it just had space on the left and the right, but the top and the bottom margins didn't really do anything. And it's displayed within the normal flow of a document, meaning next to elements that are next to it.

However, if we turn on the display inline block, now it's still displayed inline, meaning next to other elements, but it looks like the top and bottom margins are actually taking effect.

So you can see that it's a little bit of a hybrid, where inline block will be displayed inline in the content, but margin and padding are still going to have an effect on it.

We can see that if we change the margin to padding, it's still going to work. However, if we then change display inline block to just block, like the first span, now it's on taking up the entire width of the available space, and also the padding and margin will take effect.

So hopefully, this helps explain the different display values that elements can be on the page.

The reason we're talking about this is the logo image. If we go back up and inspect the logo image tag, the img tag is another element which by default will be display inline.

And it being display inline is the reason why there's a small space under the image itself. Inline elements are often text, and so with text most of the letters will be aligned to the bottom of what's called the baseline.

However, some letters have descenders which will extend below the baseline, like the lowercase letters "p," "q," "y," and others. So the browsers will automatically include a small space below the baseline to have room for descenders.

We can see this if we look at the h2 tag, the lowercase g partially extends below that baseline. Browsers will automatically leave some space at the bottom of inline elements to leave room for letters with descenders.

Since images are by default inline elements, the browsers will also make the image sit on the baseline. And then it still leaves space for descenders. If I highlight the image tag, its bottom edge matches up with the actual image. But if I highlight the parent, the anchor tag, you can see that little extra space that's been added below the letter Y.

What I usually do to get rid of the space is to set the img tag to `display: block` so that the browser will not use the baseline to align the image. And as a side note, if I ever have a situation where margin or padding don't seem to be working, I'll often try adding `display: block` to see if it fixes things, which oftentimes it will!

Now that we know how to get rid of that space, let's update our styles. The logo image tag has the class `topnav__logo.` So in our styles I'll add the `display: block` rule there. Now when we load the page we can see that the space below the letter "y" is gone!

And you do want to remove any empty selectors once you're done with the styles, because it's not considered valid CSS. And when we check out the website everything looks pretty good!

One other thing when working with image tags is that in addition to the alt text for accessibility, it's considered best practice to include `width` and `height` attributes in the img tag itself. This is so the browser knows how big the image is going to be even before it finishes downloading and loading the image.

Image tags are what's known as a "replaced element," where the content of the element is determined by an external object, like an image or video file that has the image or video loading from something outside the HTML file.

We're doing this with the logo image, because the image itself is getting loaded from someplace outside the index.html file itself, from our local image files. Iframes are another type of replaced element, if you've ever worked with those.

Since it usually takes time for the browser to download the image file, initially when you load the website the image will have zero width and zero height. You can actually see this if we go to the website and reload it a few times.

Every time the website loads, the navigation bar jumps in height, which causes all the website content to slightly move down. This is called a "layout shift" and it's not a great user experience, since if the shift happens while you're reading content on the website it can be jarring or confusing.

In order to avoid that movement, we need to set the actual size of the logo image in the HTML image tag. In the browser source code, if I hover over the `src` attribute of the image tag, it tells us that the image is 128 pixels wide and 36 pixels tall.

So let's go to our code and in the index.html file, in the img tag, add `width="128"` and `height="36"`. When adding the img width and height attributes, you don't need to add a unit as it's automatically pixels.

Just make sure that you have to do the equal sign and quotes since these are HTML attributes and not CSS rules.

Now, when we save and then go back to the website, if we reload a couple times the logo image will still blink as it's being loaded, but the navigation bar won't have that jump in size and push the content down.

This is because we've told the browser how big the image is, so it knows to leave that much room for the image for when it finishes loading.

Alright, that's it for the CSS flow layout and weird spacing issues like descenders.
