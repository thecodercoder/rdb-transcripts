## Overlay

Going back to Figma, we can see that the overlay is under the menu when it's open, but it is covering the rest of the website. And it is semi-transparent.

If we select the "overlay" element, in the right sidebar in the "Fill" panel, we can see that it's #383A4A, which I believe is the dark gray text color, and it's at 40% opacity.

Let's go back to VS Code and figure out where we want to put this. Now, for the "topnav\_\_menu", we're utilizing the "aria-expanded" state of the open button to trigger the animation in our styles, and to make that work we have the "topnav\_\_menu" as a direct sibling to the open button.

I'd like to use the same approach for the overlay, so that means we want to have the overlay div be a direct sibling or at least a sibling of the open button.

Also, in terms of stacking, I'm going to put the overlay before the other hamburger menu elements, so that the latter elements will be layered on top of the overlay.

Latter elements being put on top of earlier elements is the default way browsers will stack elements, and when possible, I like using this default stacking order to my advantage so I hopefully don't have to manually place things with z-index.

All that said, let's add our overlay right before the open button. I'm going to create a new line before it, and create a div with a class and I'll name this "topnav\_\_overlay".

And this is just going to be a blank div with no content or anything. Now, let's go to our styles, and I'm going to create a new selector before the open and close button styles. So we'll add "&\_\_overlay".

Similar to the "topnav\_\_menu", I'm going to first put all the styles in a "breakpoint-down" mixin because we only want this overlay on mobile, and I don't want to cause any potential issues on desktop. So let's copy that mixin from the "topnav\_\_menu" and paste it in the "topnav\_\_overlay" selector.

Then, I'm going to make this a fixed element with "position: fixed", and I'll set "inset" to "0" so that it sticks to all four sides of the viewport. And let's add that background color.

I'm going to create a new CSS custom property for this, so let's go to colors.scss, and I'll add the overlay with the header and menu properties that we have, maybe under the "menu-shadow" prop.

Let's call this "--menu-overlay", and it's the same color as the "text-dark", so I'm going to copy that HSL and paste it in. But we need to add opacity, which is an optional fourth parameter. So after that "25%" I'll add a comma and then add the opacity percentage from Figma, which was 40%.

And I'll add the "a" after HSL so it says HSLA. It's not mandatory, because the browser can read it either way, but we'll just be more explicit about it having the alpha or opacity value.

Now, let's copy that property name, and then for our "background-color" we'll set it to "var()" and then paste in the property name.

Let's save and check out the website now. And it looks like the overlay is loading, and it seems to be covering the whole website, which is good. Now obviously, we don't always want it to be visible like this, only when the menu is open.

Before adding any more styles, we need to figure how we want the overlay to behave. So initially it should not be visible, but when we open the menu, we want it to maybe fade in while the menu slides down. And then fade out when we close the menu.

To make the overlay not visible, we could set it to "display: none" first, and then make it "display: block" to show it. But from my experience, while this is possible, it makes trying to animate it in a much bigger hassle, because the "display" property is not one that you can animate. So it will just suddenly appear and disappear.

What I usually like to do is use "opacity" and have it be zero initially so it's not visible, and then animate it to "1" to fade it in. And that works really well. Let's try that.

In our styles for the overlay, I'm going to add "opacity: 0". Now when we save, and go to the website, the overlay is not visible. However there is one problem with using just opacity to hide elements.

They still exist on the page. So if I try to click anything, like the logo link, nothing happens. And that's because the overlay is on top of the rest of the website since it has its position fixed. And it's blocking the rest of the website.

This is one reason why a lot of people will use "display: none" in situations like this with overlays, because "display: none" will basically make the element not exist on the page at all, so it won't block anything.

But, fortunately, we can prevent the blocking without needing "display: none" by allowing you to click through the overlay with the "pointer-events" property. Back in our styles, I'm going to add "pointer-events: none".

What this is does is it prevents you from clicking on the overlay itself, which in essence lets you click _through_ the overlay and click on elements that normally would be blocked by it.

Now, on the website, we can click the logo or the hero buttons again.

Next, let's change the opacity when the menu is open. Going back into our styles, we need to figure out the selector for when the open button has "aria-expanded true".

Looking at what we did for the "topnav\_\_menu", we used the "topnav\_\_open" class with "aria-expanded true" attribute with the direct sibling selector, "plus", then the "topnav\_\_menu" class.

However, because the overlay is before the open button, we can't use the sibling selector, because the sibling selector only works to target siblings after the element.

So if we tried writing something in the "topnav\_\_overlay" selector, like "plus .topnav\_\_open[aria-expanded='true']", those styles would be applied to the open button, not the overlay.

What we need is a previous sibling selector, which very fortunately we now have with the new ":has" pseudo-class selector. Now we can write "ampersand :has and then parentheses. And inside the parentheses we'll write "plus .topnav\_\_open[aria-expanded='true']". And then curly brackets.

What this is selecting is if the "topnav\_\_overlay" HAS a direct sibling with the class "topnav\_\_open" and attribute "aria-expanded true", then these styles will get applied to the "topnav\_\_overlay" element. This is a super useful selector that has fixed a pretty big pain point that we've been having in CSS for a very long time.

Let's try this out. In the curly brackets, we want to change the overlay's opacity from zero to 1. So I'll set "opacity: 1". And we want to animate the opacity too.

If you want, you can try this yourself first-- figure out where to animate the opacity of the overlay. And if you need some guidance, you can look at how we did the animation for the "topnav\_\_menu".

Alright ready? You can pause the video now.

[ pause ]

Okay! So we want to animate the opacity property. So we want to add this in the "topnav\_\_overlay" selector. I'm going to just copy what we did before, the "transition" property from the "topnav\_\_menu, and paste it in for our overlay. And then I'll change the transition-property from "translate" to "opacity".

Let's save, and check out the website! And in our Markup View, in the open button, let's manually change that "aria-expanded='false'" to "true".

And the menu opens and we can see that overlay fading in. And if I change it back to "false", the menu slides back up and the overlay fades out. Awesome!

One other thing I want to add is that when the menu is open and overlay is visible, I don't want you to be able to click through the overlay and like click the buttons or other links on the rest of the website. We want the overlay to block other elements when it is visible.

We can do this by in our ":has()" selector, adding "pointer-events: all". This means you are able to click on the overlay, so it will block clicking through it.

Now, on the website, if we open the menu, we can click on the menu links, but if I go to the hero buttons, you can't click on them.

Now, what we need to do is use JavaScript to change that aria-expanded value from false to true when the open button is clicked.

And for accessibility, we will also need add a few more attributes so screen readers can tell when the "topnav\_\_menu" is either hidden or visible.

We'll be doing that and more in the next part, where we start getting into the JavaScript.
