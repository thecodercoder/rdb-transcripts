# Flexbox mobile layout

To start building the layout of the hero section, let's go back to the design and see how the website looks compared to it, and figure out what we need to do.

So I have our mobile design open in Figma, and then on the right I have our website, with Responsive Design Mode loaded on iPhone view.

Looking at both of these, the biggest thing I'm noticing is that we need to center the unicorn image on mobile. Everything else looks pretty good and close to the design.

Now, for the desktop version. Let's look at the desktop design. And on our website, I'll go back to a desktop view and zoom out a bit to try to match how the design looks. For desktop we need to do more work to put the content into 2 columns, with the text on the left and image on the right.

To make the responsive layout, so that it's 1-column on mobile and 2-columns on desktop, we can use either flexbox or grid.

Let's do the flexbox layout first. And to start, let's look at the markup and figure out which element will be the flexbox parent, and which will be the flexbox children. In the hero section, we have the `hero__wrapper` div, and in that div is the `hero__image` image with the unicorn image, and then the `hero__text` div with the text and buttons.

We should make the `hero__wrapper` div the flexbox parent, and then the direct child elements will be the flexbox children-- the image tag and the `hero__text` div.

In our hero styles, we'll start with the `hero__wrapper` selector and adding `display: flex`. I usually add `display` and the flex or grid properties at the top of the style rules, but you can order yours however you want.

Now, before looking at the website, just by adding `display: flex` to the parent, what do you think the hero content will look like? Keep that in mind, then make sure you've saved your changes, and let's go to the website to see what happens!

Ok, and now we have the unicorn image and the hero text next to each other, on the same row. Just by turning on flexbox on the parent, the browser will automatically try to fit all the flex child elements on the same row, from left to right.

We do want to have a 2-column layout for desktop, but thinking about the mobile view first, let's use some flexbox properties to layout the hero content into 1 column. There are a couple of ways we could do this, but one way is to modify the `flex-direction` property.

If we select the flex parent `hero__wrapper` element and go to the `Computed` tab, check the `Browser Styles` box and then filter for `flex`. This will display the default flexbox properties that the browser sets on every element.

You might notice that the `display: flex` style has an arrow on the left side, and if we click to expand it, Firefox tells you where that style is coming from in the CSS file. The properties that don't have an arrow are ones that are coming from the browser defaults, not our own styles.

There are a couple of default flexbox styles that are affecting the layout right now. In particular, the `flex-direction` property is one for flex parents, and it defaults to row, which places the flex children in rows, from left to right.

Another property that's affecting the layout is the `flex-wrap` property, which is set to `nowrap`. This means that the flex parent will not wrap its children to multiple rows, but will keep them all in the same row.

The other default flex properties are for flex child elements-- and again, these are default values that are applied to every element. They just won't take effect if the element isn't a flex child element.

If we click on the `hero__image`, we can see that the default flex styles are the same as the `hero__wrapper`. However since this is a flex child, the flex parent rules like `flex-direction` and `flex-wrap` don't do anything.

But the flex child rules, `flex-basis`, `flex-grow`, and `flex-`shrink`do have an effect. Flex-basis sets the initial size of the element-- it defaults to`auto`, which will be the width or height that the element is based on other, non-flexbox style rules.

Then flex-grow is set to zero, which means it will not grow to fit available space in the flexbox container or parent. And flex-shrink is set to 1, which means it is allowed to shrink from its initial flex-basis size in order for the children to fit on the row.

Ok, so for our mobile layout we want the image and hero text to be stacked to 1 column. One way we can do that is by changing the `flex-direction` property. Right now it's at the default `row` value. But we can make it vertical by explicitly setting `flex-direction` to `column`.

Let's try that in the browser first. In the `hero__wrapper` browser styles, I'll add `flex-direction` and set it to column. Now the flexbox children will be ordered starting from the top, and moving down vertically. Let's look at some of the other possible values. We can also set it to `column-reverse`, and now it's still in 1 column, but the hero text is first and the image is on the bottom.

And if we set it to `row-reverse`, the content is all on one row, but starting from the right side instead of the left. And this is actually very close to what we'd like the 2-column desktop layout to be.

The HTML hasn't changed at all-- all the changes are happening just in CSS. One thing to keep in mind is that you don't want to change the order of HTML elements too drastically.

For screen readers or users who navigate the website with just a keyboard, they will follow the order of the actual HTML elements. So if you alter the visual order of elements on a website too much from the markup order, it can cause confusion and make it difficult to navigate the site.

For our mobile layout, I think the `flex-direction: column` is a good way to go. Let's put that in our styles. In the hero.scss file, in the `hero__wrapper` selector, under `display: flex` I'll add `flex-direction: column`. This is because we're making the mobile styles the default styles, and then we'll add a media query with our breakpoint mixin for the desktop styles.

Now, let's save, and in our website, I'm going to turn on Responsive Design Mode and select the iPhone so we can see more what it will look like on mobile. That looks pretty good-- one thing we do need to do is center the unicorn horizontally.

Do you remember the flexbox property to center the unicorn? If you want, you can pause here and do some experimenting. And you can always refer to the CSS Tricks Flexbox Guide if you need some extra help.

Alright, so this was a little bit of a trick question. Before, we used `justify-content` to center the flexbox children horizontally. However, if in the browser styles I go to the `hero__wrapper` and add `justify-content: center`, nothing happens.

The reason for this is because we changed the flex-direction of the flexbox container, so that its direction is `column` instead of the default `row`. This changes the main axis of the flexbox container to be vertical going down, instead of horizontal.

This means that `justify-content`, which aligns flexbox child items along the main axis, will be aligning the children along the vertical axis, not the horizontal one. The ability for flexbox to flip its main and cross axes is a great feature, but it also means that we need to remember when it's flipped.

The property that will align each child item along the cross axis is `align-items`. If we adjust our browser styles for the flex parent so that it says `align-items: center` instead, now we can see that the unicorn is centered.

You might be wondering why the text wasn't affected, since the `align-items` property is set on the parent, and supposedly affects all the flex children. Well, it actually is being applied to the `hero__text` too! But nothing has changed, because it will move the child item if there is extra space within the flex container.

If we turn on the Flexbox inspector to highlight the flex items, we can see that while there's extra space for the unicorn to move left or right, there's no extra space for the `hero__text` element. It doesn't control the alignment within the flex child item, only the flex child item within the parent container.

And if you didn't want to apply `align-items: center` to all the flex children, you could instead just go to the `hero__image` item and set `align-self: center` to just center itself.

I'll probably keep the `align-items: center` on the parent, so let's add that to our styles. I'll add it to the `hero__wrapper` selector after `flex-direction`, to keep the flexbox styles all together.

And if we save, now on the website the unicorn is centered, and things looks very close to the mobile design.
