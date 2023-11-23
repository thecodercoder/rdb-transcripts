# Layout with flexbox

Before getting into flexbox, I wanted to show you something that I had mentioned previously, about which element to add the "wrapper" class to for the Top Nav.

If we inspect the header, we have our header tag and then the wrapper class on a child div. If we select the wrapper div, in the "Rules" tab, this is where we've limited the width of the wrapper to be 1200px wide or 75rem.

In the website, if I zoom out, and turn on Responsive Design Mode, I'm going to set the viewport width to 1300 so it's greater than 1200px.

And if I hover over the wrapper div in the source code, you can see the margins on the left and right with the extra space.

However, if we put the "wrapper" class in the header tag, things won't look quite right. In the source code I'm going to double-click the "wrapper" class in the div, press Ctrl-X to cut it out, and then in the header tag I'm going to double-click the "topnav" class and then paste in the "wrapper" class name after it.

Now in the website, the purple background color that we set on the "topnav" class is getting limited to 1200px. And there's white space on either side. This is because we moved the wrapper class up to the header tag-- it's limiting the entire header to 1200px.

This is why I put the wrapper class which limits the width to a child element of the entire section. If I go back and cut the "wrapper" class out from the header, now its width is not getting limited. And when I paste it back in the div, now just the content in the header is getting limited to 1200px and centered, but the whole header with the purple background is going all the way across.

This might seem obvious to you, but it's something that did trip me up when I had to build website sections like this, with a full-width background color, but setting a max-width of the text content within the section.

Hopefully that's helpful to you. So now let's get into the flexbox layout.

In web design, layout means the visual arrangement of elements on the website-- where they are positioned on the page, and how they are aligned in relation to one another.

In CSS, we often control the layout using flexbox and grid. These two features are sometimes compared with one another in a "who's better" competition, but in my experience they are both great tools with different strengths.

With flexbox, you "turn on" flexbox by setting the `display: flex` rule on the parent element, and adding additional rules to control the alignment of the child elements. In our case, we want to style the logo and the navigation links.

In VS Code, the parent element is the wrapper class div inside the topnav header. And the flex child elements are the `topnav__homelink` and the nav element. For the wrapper div, that wrapper class will be reused in pretty much every section in the website.

So in order to be able to write some topnav-specific styles, I'm going to add another class to that div called `topnav__wrapper`. That way, it will have the shared styles from the wrapper class, but we can also set styles that we only want to affect the `topnav__wrapper`.

In our topnav.scss file, we'll need to add a selector for the wrapper div inside the topnav selector. In our block `topnav` selector I'll add a selector for `&__wrapper` which will target the `topnav__wrapper` class. Then in that selector, I'll add the rule `display: flex`.

And let's see what the website looks like when we just have that rule. If we look at the website, we can see that now instead of the links being under the logo, they are all next to the logo. If we inspect the website, this is because we made the flex parent the `topnav__wrapper` div, which will make the direct children the flex children. The direct children are the `topnav__homelink`, and the nav tag which contains the navigation links.

So we can see that just by adding that one rule of `display: flex` on the parent, it's made flexbox start to work, by default it will try to fit all the flex child elements on the same row. One cool feature is that in the source code, the `topnav__wrapper` div has a little "flex" label next to it. If you click that, Firefox will add lines to show you how flexbox is working in that element.

Firefox also has a Flex Inspector. If we go to the "Layout" tab and expand the "Flex Container" panel, we can see that the `div.wrapper.topnav__wrapper` element is displayed as a "Flex Container" and it has the flex inspector turned on. Let's set the color of the lines to be a bit more visible-- maybe a yellow orange color to contrast more with the purple background.

Now, we can see that in the wrapper flex parent element, there are two flex child items, `topnav__homelink` and the nav. And both child items are horizontally aligned to the far left. This is the default way that flexbox will horizontally align items if you don't add any additional rules.

However, what we want is to have the logo on the far left and the links on the far right. The links themselves are stacked instead of being side by side, which we'll get to in a little bit. But for now let's just focus on the logo and the group of links.

With flexbox, the default direction that the browser will display the flex child items is horizontal, in a row, going from left to right. This is because by default it has a property called "flex-direction" set to "row" which means from left to right since we are displaying content from left to right in our browser.

However, if you play around with the flex-direction property, it is also possible to change the direction of the flexbox items. Let me show you what else you can do. In the browser, in the `topnav__wrapper` selector, I'll add a new style with the "flex-direction" property.

If we set it to "column", the items will be displayed vertically from top to bottom, with each flex child on its own row. Setting it to "column-reverse" will order the flex children vertically from bottom to top.

If we set it to "row" which is the default value, the children will go back to displaying horizontally from left to right. And setting it to "row-reverse" will display them horizontally, from right to left. And I'll delete this style so it will go back to the default flex-direction of "row".

When you're working with flexbox, there are two axes that you are working with. There is a main axis along which the flex child items are arranged. If the flexbox direction is horizontal in a row, like we have now, the main axis is the horizontal axis.

And then there is a cross axis, which is perpendicular to the main axis. In our case, since the main axis is horizontal, the cross axis is vertical.

If the direction is column or column-reverse, the the main axis will be the vertical axis and the cross axis will be horizontal. It's important to remember what your main axis is when you're trying to align the flex content either horizontally or vertically. Because some flex properties will target either the main or the cross axis.

To control the alignment along the main axis, we can use the `justify-content` property. By default it's set to "flex-start" -- which will align the flex child items at the start of the flexbox parent, which in our case is the left side.

When I was first working with flexbox, and even still now, I would always open up a really great resource that CSS Tricks has. Let's go there now. I'm going to run a search for "css tricks flexbox" and the first result is the "A Complete Guide to Flexbox" article on CSS Tricks. This is super helpful because it has a visual reference for what each flexbox property does.

Let's scroll down to look at `justify-content`. We can see all the different possible values you can use for that property here. Now, in our design we wanted the logo at the far left, and the links at the far right. If we look at the examples, what we want to use is "space-between," because it will put the flex child items on the edges, with any remaining space in the middle between them.

Also, in this guide, all the properties on the left side of the article are meant to be put on the parent element, and the properties on the right are for the flex child items. `justify-content` is a parent flex element, so it needs to be added to the `topnav__wrapper` class div.

Let's go back to our code in topnav.scss and add that rule. Under the `display: flex` rule I'll add "justify-content: space-between" and save. And now when we look at the website, we can see that the logo is still on the far left, but the links are now all the way on the far right, with all the additional space between them. Which is what we want!

Now, we need to layout the navigation links themselves, so they're not stacked but are all in the same row. And we can use flexbox for this as well. Even though the links are in the `topnav__wrapper` flexbox container already, it's totally ok to have another flexbox container in an existing one.

Like we did before, we first need to identify what the flex parent and flex child items are. If you want, pause the video here and look at the HTML markup for the links, and identify to yourself which element should be the flex parent, and which should be the flex children.

[ pause ]

Ok! If we check out the HTML markup for the links, we want the parent to be the ul-tag with class `topnav__links`, and the flex child items will be the direct child elements of the parent, which are the li-tags with class `topnav__item`.

So, going back into our code, if we go to the `&__links` selector, that's the unordered list tag, and we can add a `display: flex` style rule to it. In terms of what order to put your style rules in, it doesn't matter too much. Usually I will put flexbox and grid styles first. I think everyone has a different way of ordering their style rules, but as long as it's reasonably organized, I think you can choose whatever order makes the most sense to you.

Now if we look at the website again we can see that the links are indeed side by side now! However there are a couple of issues where what we have isn't exactly what is in the design. For starters, it looks like the links are all vertically aligned to the top of the navigation bar.

But if we look at the design, the logo and the navigation links are centered vertically. Let's go back to the Flexbox guide to see how to do that. We used the `justify-content` property to align the header items horizontally, along our main axis. If we scroll down, the next property is `align-items` and it looks like that's what we need to align the flex child items vertically, on the cross axis. We probably want to set `align-items` to "center".

Now, the question is, which flex parent should we try to vertically align? Because we have two. Going back to our website, since the issue is with the nav links, let's first inspect the ul-tag `topnav__links`. If I just hover over the tag in the source code panel, we can see that it's height is just the height of the link text, and everything is aligned to the top.

Setting `align-items` will align the child items vertically within the parent container. But since the `topnav__links` parent height is less than the height of the purple top nav bar, it won't do anything. We can try, just to see. In the browser for the ul-tag `topnav__links`, I'll add `align-items: center`. And nothing happens. So I'm going to delete that rule.

If we hover over the ul-tag's parent, the nav tag, we can see that that height is the full height of the top navigation bar. And both the nav tag and the anchor link `topnav__homelink` are flex children of the `topnav__wrapper` div, which is the flex parent.

The reason that the nav tag is the same height as the `topnav__homelink` is because in flexbox, if we go back to the CSS Tricks Flexbox guide, the default value for the `align-items` property is `stretch`, which will stretch the child items vertically to fill all available space. This results in all the flex children having the same height, the height of the tallest item.

If we go back to our website, in our `topnav__wrapper`, the tallest flex child is our logo SVG. Then the nav tag, which based on its text content is shorter than the logo, will stretch to fill the space so that it's the same height as the logo.

This default vertical stretching of flex child items is good to remember-- it can often come in handy if you're working with something like cards and you want them all to be the same height. But it can cause unexpected issues like if one of your flex child items is a JPG image tag and it is getting stretched and skewed.

Thankfully, setting `align-items` to something other than the default "stretch" will fix problems like that, if you ever encounter them. And in our case, we want to use `align-items: center` to center the flex child items vertically.

Let's add it to our `topnav__wrapper`, just in the browser first. And it looks like everything is centered in the top navigation now! So let's add it to our code as well. In the `topnav__wrapper` I'll add `align-items: center` under the `justify-content` rule, and we'll save and see how the website looks. And now everything is vertically centered.
