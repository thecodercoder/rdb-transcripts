## Menu styles

We need to add selectors to our topnav styles for the new elements we created. So in VS Code, let's use the Quick Open menu and type in "topnav" and open topnav.scss.

And I'm going to have the index.html file on the top, and I'm going to right-click the styles and "Split Down". And in our styles we're going to start with the "topnav\_\_open" button which is after the logo, so after "&\_\_logo" and before the links, I'll add "&\_\_open", then "&\_\_menu", and then "&\_\_close".

And that should be it, so I'll close the duplicated tab.

And let's go back to the website to see what we want to work on first. Okay, so I'm thinking let's start by getting rid of the default styles for the open and close buttons.

If I hover over one of them in the markup view, it looks like there's padding, so let's go to the "Layout" tab. And it looks like we have padding and also a border, so we'll want to get rid of those and the background color too.

Back in our styles, I want to affect both buttons. So I'm going to create a compound selector, before the "&\_\_open" class, that is both "&\_\_open" then comma, then "&\_\_close".

Let's start getting rid of the background, with "background: none". And when we save, the buttons are now transparent, and you can see the default button border more clearly. Next we'll do the padding, and set "padding" to "0". And now all that we have left is the border, and we'll write "border: 0".

And now the buttons match the design better!

Next, let's work on the "topnav\_\_menu" div that we created for the open menu. Let's go into our styles, and in the "topnav\_\_menu" selector, I'm going to add a max-width media query with our breakpoint-down mixin, so that these styles will only apply on mobile.

That way on larger viewports, the top navigation links will look the way they should on the desktop design. And we're able to use the same markup for all devices, without having to have 2 versions of the navigation links.

For the open menu, we want to make it fixed to the top of the viewport, so I'm going to add "position: fixed". And to have it "stick" to the top and sides, I'm going to set "inset" to "0" for top, "0" for right, "auto" for bottom, because I don't want it to go all the way to the bottom, and then "0" for left.

The "inset" property is a shorthand so you can set top, right, bottom, and left all in one property, and I find it pretty handy.

And if we save, on the website, if I start scrolling down, you can see that the close button and links stay visible and fixed.

Now, let's add the background color to the menu. We want that blue-purple color that we're already using in the top nav. And yes, we have the "background-color" and it's set to "var(--header-bg)". And since we want the top nav and menu to have the same background color, I might just create a compound selector for both the "topnav" class and "topnav\_\_menu".

We can refer to the parent "topnav" class when we're nested by just writing an ampersand. So I'll write "&" comma, then "&\_\_menu". And I'l move that background color rule into it.

And now when we save, on the website the menu is covering up whatever parts of the regular website content it is over when we scroll down. So, we're getting there!

Next, let's get those text links to be in 1 column and centered. Let's look at the design, and this is what we want them to look like. If you want to try this on your own, you can pause the video, and see if you can write the styles to display the links in 1 column, and have them be centered. And if you want, set the spacing between the links to match the design. Don't worry right now about the spacing around the links, we'll get to that later.

Alright, pause now, and we'll see you in a little bit.

[ pause ]

Okay, so, going back to the index.html file, the links are in the unordered list "topnav\_\_links", so that's what we'll want to target.

In our styles for the "topnav\_\_links", we're using flexbox to layout them for desktop, so let's keep using flexbox for the mobile menu.

Under the large breakpoint, I'll add another "@include u.breakpoint-down(small)" and I want to change the "flex-direction" from its default value of "row", which is what was putting the links all in 1 row previously, and I want to set it to "column".

And if we save, now the links are in a column. To center them horizontally, we want to use "align-items", because we flipped the direction of the main axis of the flexbox container to now be vertical. So "justify-content", which we usually use to align flex children horizontally, will now align them vertically. Which we aren't trying to do.

We want to align them horizontally on the cross axis, so we want to write "align-items" and set it to "center". And there you go, it's centered.

Let's also make sure the space between the links is correct-- right now it looks like we have a gap of 20px for mobile, so let's go back to the design and see how that compares.

In the design, I'll hold down Ctrl (or Cmd on Macs) and select one of the links, and hold down Alt, and it tells us that there are 40px of space between the links now.

Back in our styles, we already are using 40px on desktop, and the 20px was just for mobile and tablet. So, I think we can make the gap always 40px. So let's change that 20 to 40, and now we can delete the large breakpoint since we don't need it anymore.

Now on our website we can see there's a lot more space between the links.

Okay, next up, the links seem a lot smaller now than on the design. In Figma, on desktop, the links are that small font-size with all caps, which we want to keep for larger viewports. But on the mobile design, they're not all caps anymore, and let's check the font-size.

It is 20px font-size now. Going back to our styles, let's see where we set the original text link styles. It looks like it's the "&\_\_link" selector, because I can see that "text-transform: uppercase" rule, and I'm pretty sure that's the only place we have all caps.

Right now, we have a large breakpoint, so the default styles outside that breakpoint media query are for mobile and tablet. And we want to use the new hamburger menu styles for only mobile, meaning we want the original styles for not just large, which is desktop, but also for tablet, which is medium in our breakpoint names.

So I'm first going to change that breakpoint to be "medium" instead of "large". And in this media query is where we want to start moving some of these styles that are not for the mobile menu styles. So for example, like the "text-transform" rule-- I'm going to move that over.

And also I think the letter-spacing is really just for that all caps style, so I'll move that too. And we want to change that font-size for mobile from 14px to now 20px. So I'll change that to "u.rem(20)".

Let's save, and on the website, the hamburger menu links are bigger, and no longer all caps which is good. And just to test the responsiveness, let's change to iPad view, and we can see the links go back to being smaller and all caps. So it looks like the responsiveness is good!

I'll go back to iPhone view. And next, let's move the close button all the way to the right. In our styles, that's in the "&\_\_close" selector, and in here we want to hide this by default, and only show it for medium and large. So I'm going to set "display: none", then I'm going to write another "@include u.breakpoint-down(small)", and in it we'll show it with "display: block".

And to get it all the way to the right, we're going to use my favorite trick of setting the left margin, or "margin-inline-start" to "auto". And there we go.

Now, you might be wondering why I'm all of a sudden using breakpoint-down to just target the small mobile styles, when I've been using the breakpoint mixin to target either medium and large or just large breakpoints.

I try to use whichever one will let me target just the more complicated design, meaning requiring more styles that I have to write. In most cases, the desktop styles are more complicated and the mobile styles are more simple. So I want to target the desktop styles to add on the additional style rules that we need.

But in this case, the mobile menu styles are more complicated and need additional style rules that we don't want on desktop, and in our case, tablet.

If I used the breakpoint mixin to create min-width media queries to target desktop, that means I'd be putting all these extra styles outside the media query, and they'd get applied to all viewports, so I'd have to cancel each one out inside the media query. So there would be a lot of extra, unnecessary style rules to cancel things out.

It's a lot more efficient to use the max-width media queries with our breakpoint-down mixin, so we can only add those styles for mobile.

Alright, back to our menu styles, the next thing we want to do is add spacing around the menu content, so let's check out the design.

The close button has 12px of space on top, and 24px on the right. So I'm going to add some padding to the "topnav\_\_menu" so it has 12px of space on the top and bottom, and 24px on the left and right.

In our styles, let's add that, under the "inset" I'll add "padding: 12px 24px". And now there's some more space. I think I might also add a temporary outline so we can see things a little better. So something like "outline: 2px solid yellow". And it's only on the bottom, I think the top and sides are off screen, but I think that's ok, I mainly just wanted to separate the menu from the rest of the website under it.

It kinda seems like there's a lot of space between the links, like I think more than the design. Let's inspect and see what's going on. If I h over over one of the links, it looks like there's extra space on the bottom below the text itself.

I think this is from the gradient underline that we added with the pseudo-element. In the "Rules" if I expand that "Pseudo-elements" panel, yeah, it's 3px tall and there's a margin-top of another 3px. So this is making each link 6px taller than it needs to be on mobile, because we don't have hover states on mobile, just desktop.

So I think we should hide that ::after pseudo-element on mobile and just show it on tablet and desktop.

Back in our styles, if I scroll down, eventually we hit the ::after pseudo-element for the topnav\_\_link selector. And I'll probably just add another "@include u.breakpoint-down(small)" mixin, and then set "display: none".

Ok, and now if we inspect a topnav link, it is 20px tall, which matches the font-size we set, so we are good.

Now that that's set, we need to add space between the close button and the top of the links. In the design if I select the group of links, it's 120px to the top and bottom of the menu, and then 84px below the close button.

I'm going to add 84px of margin-block-end to the close button to start. Let's try that, and the website looks pretty good. Now, as I've mentioned before, I like using margin to add space between sibling elements, but for space between a child element and the edge of the parent, I like using padding. That way you won't run into weird margin collapse issues.

So, I think we can adjust the "topnav\_\_menu" padding and make the padding-bottom or "padding-block-end" be 120px. In our "padding" rule, I'll add a third number and say 120px.

For the padding shorthand, if you use 4 numbers, it's top, right, bottom, left. If you use 3 numbers, it's going to be top, right, bottom, and it'll make the left number match whatever you put for the right.

The menu is looking good! Now, if we go back to the design, and look at the "Menu Open" design, the bottom edge of the menu is rounded, and it has a bit of a shadow, and there's a semi-transparent overlay covering the rest of the website.

Let's do the rounded corners first. I'm going to select that background, and get the border-radius. Up in the right sidebar on the top, after the width and height, we have "rotation" and then the corner-radius which says "Mixed". If I click on the icon on the right it pops up a menu where you can set each corner individually.

We have 20px of corner-radius, which is Figma's way of saying "border-radius", on the bottom left and bottom right corners. Let's add that to our styles for the menu. I'm going to write "border-radius" which is also a shorthand for the top, right, bottom, and left corners. And I'll set it to "0 0 20px 20px".

And when we save, we can see the rounded corners! Next up, let's check out that shadow.
