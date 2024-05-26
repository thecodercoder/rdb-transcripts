# Unicorn image spacing

Before moving on to the buttons, I think we need to look at the spacing around the unicorn image-- meaning how much space there is above and below the unicorn. In Figma, in the mobile design, I'm going to select the unicorn and then hold down the Alt key and hover the mouse over the top navigation bar. It is 30px under the nav bar. And if we hover over the main header, it's 40px from the bottom of the unicorn to the h1 tag. So that's 30px of space above, and 40px of space below the image.

Going back to our hero.scss file, in the `hero__image` selector, I'll add `margin-block: 30px 40px` which is a shorthand property to add 30px of margin to the top and 40px of margin to the bottom of the image.

If we look at the website, there's now this weird white space above the hero! What's going on? If we inspect the unicorn image, in the `Layout` tab, we can see that the image has the margin-top of 30px and margin-bottom of 40px, which seems correct.

Then if we hover over it, it looks like the top margin is extending outside the purple hero area. And what's stranger, is that if we hover over its parent element, the `hero__wrapper` div, the top margin from the unicorn extends outside the bounds of the `hero__wrapper`, and if we keep going up the tree, it also is going outside the hero section tag, article tag, and main tag, all the way up until it hits the header tag. Pretty weird, right?

Well, what's happening is something called `margin collapse,` which we also saw in the intro to Sass section with our demo website. Margin collapse usually happens when the bottom margin of one element overlaps the top margin of the element below it-- this is an old feature from when websites were basic HTML that looked like Word documents.

And the intent was to not have too much space between elements if there were two sets of vertical margins between them. Unfortunately, even though today we don't really need that type of feature, the website will behave that way unless we force it not to happen.

What's happening to cause that space on top, is that the element on the website that comes before the hero and its ancestor elements all the way to the main tag, is the header tag. And so the top margin of the unicorn image tag keeps extending outside all its parent elements since we haven't forced it to not extend, to add that space between the hero itself and the top navigation.

That's why there's a white space on top. There's no white space under the unicorn image, because the next element is the `hero__text` div, which is still inside the hero with that purple background color.

So how do we force the top margin of the image tag to be inside the `hero__wrapper` parent div? There are a couple of style rules we can add to the `hero__wrapper` that will fix this problem. If we add a border of `1px solid` that will magically fix it. Or if you add padding of 1px that will too.

But it's a little hacky to add a border or 1px of padding when you don't really need to. Another style that fixes it is if we set `overflow: auto` or `overflow: hidden` to the `hero__wrapper`. But overflow is usually used to control if scrollbars appear or to clip content that goes outside the parent. So even though it works, it's also a bit hacky.

One newer solution that will fix the problem without any added side effects is setting the parent to `display: flow-root`. If you want to know the technical reason that this fixes the problem, it's that this style rule (and the other hacky style rules) creates a new `block formatting context` in the parent.

This is related to the box model that you can see in the developer tools in the Layout tab-- it's the content, padding, border, and margins of an element. Creating a new block formatting context in the `hero__wrapper` div forces the child elements, including any top and bottom margins, to be inside the parent box.

The other hacky fixes also create a new block formatting context, but as more of a side effect to their primary function of adding borders, padding, and so on. The `display: flow-root` rule only creates a new block formatting context and it does nothing else. So if you ever encounter weird whitespace that seems to be coming from margins, try setting `display: flow-root` on a parent element, and see if that fixes the issue.

However, what I consider a better solution to this situation is to use top and bottom padding on the parent `hero__wrapper` div to create that space between its top and bottom edges, and the children inside it.

This is why I use padding to add space between an element and the edge of its parent, which we also did in the Top Navigation wrapper, to add the space around the links. Padding is never collapsed, so it's better to use for those cases.

But I'll use margin to add space between elements that are on the same level in the markup, like the space between the h1 and the paragraph tag in the Hero.

So going back into our code, let's not set the margin-block-start, and only add a `margin-block-end` or `margin-bottom` of 40px to the unicorn. Going back to our website, the white space has disappeared since we took away the top margin.

And now, let's add space to the top and bottom sides of the `hero__wrapper` by using padding. Let's check Figma to see how much padding we need to add. I'm going to select the `Hero content` layer, which is all the image and text elements inside the hero. And holding down Alt, if I hover above the Hero content, it says there's 30px of space. And if I hover below the Hero content, there is 60px of space.

Let's do the same for the desktop design. If I select the Hero content, above it there is 40px of space, and below it is 80px. So it's 30px and 60px for mobile, and then 40px and 80px for desktop.

In our hero.scss file, we want to add the padding to the `hero__wrapper` selector. First let's add the mobile padding as our default styles. Since we're talking about top and bottom padding, we can use the `padding-block` property, which will set top and bottom padding, and not set left and right padding. And I'll set that to `30px 60px`.

And we also have to set up the desktop padding-block values. We could use the Fluid Typography Calculator to create a clamp() function for the padding values, but the padding changes aren't that much from mobile to desktop, so the benefits of fluidly changing 10 or 20 pixels between viewports isn't going to matter that much.

Honestly, I think it's just easier and quicker to add a media query and then set the padding-block to be 60px and 80px. So let's do that, using our breakpoint mixin. And if you want to try to do it yourself first, you can pause here.

[ pause ]

To load our mixin, under the `padding-block` rule let's type `@include u.breakpoint` to load our breakpoint mixin, and then in the parentheses add `large` as the parameter. And in curly brackets we'll update `padding-block` to be `40px` for the top padding, and `80px` for the bottom padding.

And now, let's save and check it out on the website. On our website I'm going to inspect the `hero__wrapper` div, and for desktop we can see the `padding-block` style rule in the desktop media query, and on the `Layout` tab we can see padding is 40px on top and 80px on bottom.

Now let's go to a mobile viewport width, and we can see that it has a padding-top of 30px and padding-bottom of 60px. So we have space above the unicorn image, and space below the links at the bottom of the hero. Looks good!

So I think we are good with the text styles, and we also got some spacing issues figured out. Next up, we'll be working on styling the buttons.
