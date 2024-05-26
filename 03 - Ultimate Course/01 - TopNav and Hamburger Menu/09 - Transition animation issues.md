## Animation issues

And I'm noticing that this sometimes happens when we reload on mobile. Not all the time, but if I make the browser emulate a slower connection, by clicking "No throttling" and then selecting something like "Regular 3G", then you can see this happen.

I think the cause of this issue is that the "topnav\_\_menu" and "topnav\_\_overlay" both have an animation with a transition duration of 400ms.

If we're on mobile and then reload, the browser immediately begins running the slide up and the fade out animations.

This also happens when going from desktop back to mobile. Because when we cross that breakpoint, the mobile styles get loaded and the animations run again.

So basically, anytime the mobile styles get loaded this will happen. Since the transition animations are causing this issue, I think the best solution would be to not set the transition-duration of 400ms for the "topnav\_\_menu" and "topnav\_\_overlay" in our styles.

Then we can add it in with JavaScript when the website is loaded on mobile.

Let's go to VS Code. Going to topnav.scss, in the "topnav\_\_menu", I'm going to remove that "400ms" from the transition property, so it's now going to default to zero milliseconds, which means the animation will happen instantaneously, so we won't be able to see the motion.

And then let's go to the "topnav\_\_overlay" and do the same thing and remove the "400ms".

So when we save and reload, neither of the animations are visibly happening since they're running in zero milliseconds.

Then, in our JavaScript, we're going to add the transition-duration back to the menu and overlay only when we click to open the menu.

In the openMobileMenu() we can add the "transition-duration" back by adding some inline styles to the menu and the overlay.

Just at the bottom, we can add the inline style first for the "topnav\_\_menu" by writing "menuTopNav dot style". And I'm not sure why VS Code Intellisense doesn't detect "style" so you have to press Escape so it doesn't autocomplete to "computedStyleMap", then add another "dot" and then write the CSS property that you want to style.

I'm going to write "transitionDuration", in camelCase, with "duration" capitalized. We do need to use camelCase in order for this to work correctly.

This is what will create an inline style for the transition-duration property. And since it's inline, it will override the transition-duration of zero from our styles. I'm going to set this to "400ms", using quotes since it needs to be a string.

And we should remove our inline styles when the menu is closed. So in closeMobileMenu(), I'll remove it by writing "menuTopNav.removeAttribute('style')".

And we'll want to do the same thing for the "topnav\_\_overlay". We haven't loaded the overlay in our JavaScript, so let's do that now. First we need to add an ID to the overlay, in our index.html file. In the "topnav\_\_overlay" I'll create an ID attribute and set it to just "overlay".

Then in our JavaScript let's go to the "menuTopNav" line, duplicate it, and rename the const to "overlay". And update the ID to "overlay" also.

Then we'll again duplicate the "menuTopNav" code, so in our "breakpoint.matches" I'll duplicate the "transitionDuration" line and rename it to use "overlay". And in the "else" statement we'll do the same thing, duplicate the "removeAttribute('style')" line and rename it to "overlay".

Okay, let's save this and test on the website. Ideally what we're hoping to see is that the website will load on mobile without the menu sliding up or the overlay fading out.

On our website, let's reload, and it looks like neither of the animations are happening, which is good! Let's inspect, and when I click to open the menu, you can see the inline styles getting added, and animations seem to be working.

Let's try closing. And… [ click to open and close a few more times ]

It looks like the opening animations are working, but when we click to close, I think we're removing the inline styles with the transitions too quickly for the animations to actually run.

Fortunately, we can delay removing the inline styles a bit so the animations have enough time to run. In our JavaScript, in the closeMobileMenu() function, we can add a delay by adding a "setTimeout" function.

If I write "setTimeout" and select the "Set Timeout Function", VS Code will generate it for us. And the "timeout" variable is for the amount of time you want to delay, in milliseconds. So since our transition animations are 400ms long, let's delay just slightly more to give them time, so I'll set this to 500 milliseconds. And we just need the number, no units.

Then, we can move our code that we want to delay inside the curly brackets of the function. So the 2 "removeAttribute()" methods.

And let's save and try this out! And when we reload, then click to open, that's good. And let's close, and now the closing animation is working! And if we inspect, we can see when we open, the inline styles are getting added right away. Then when we close, they don't get added until after the menu finishes closing.

That's exactly what we want for mobile. Now let's check switching to desktop widths. When we hit that breakpoint, we go to the desktop design, and things look good, there's no weird animations.

And going back to mobile, things look good to. Awesome. I think that fixes the animation issues that we had with the menu.

And going back to a desktop width, we need to hide the hamburger button for tablet and desktop. And actually, we don't want that "Home" link either on desktop, since it's just for the mobile menu.

In our styles, the hamburger button is "topnav\_\_open", so if we scroll down to that. I'm going to add this style before the "aria-expanded" styles.

And I'm going to hide it for medium and up, so we'll use our regular breakpoint mixin with "@include u.breakpoint()" and set it to "medium". And in it I'll write "display: none". And now on the website the hamburger button is hidden on desktop, but if I change back to mobile it is visible.

Going back to desktop view, we want to hide that first "Home" link on tablet and desktop also. What selector do we want to target?

If I inspect it, it's the first "topnav\_\_item" list item in the "topnav\_\_links" unordered list. So I think we should be able to use the "first-child" pseudo-class selector for this.

In our styles, let's go down to the "topnav\_\_item", and it doesn't seem like we have any styles for it yet. So I'll create the new selector after the "&\_\_links" and before the "&\_\_link" selectors.

We'll add "&\_\_item" class and since there's no other styles, let's also put the "first-child" pseudo-class without nesting it. Then in the styles, I'll add another media query with "@include u.breakpoint(medium)" and in it I'll add "display: none".

Now if we save, on the website the "Home" link is not on desktop, and if we go to mobile and open the menu, we can see the "Home" link.
