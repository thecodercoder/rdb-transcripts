## More optimizations

Alright, so there are a few more optimizations that we're going to be making for the menu.

We had made the "topnav\_\_menu" inert initially when the menu is closed, so that screen readers and keyboard users don't mistakenly access the hidden content. And then we remove the inert attribute when the menu is opened.

We want to do a similar thing for the main content of the website, just the reverse. So initially, when the menu is closed, the user can access all the rest of the website. But when the menu is opened, visually it's covering up and blocking the rest of the website so you can't interact with it if you're using a mouse.

We should do the same thing for screen readers and keyboard users, so that when the menu is open, the parts of the website other than the top navigation is inaccessible by making them inert, and then when the menu is closed we will make them not inert.

If we look at the Markup View, and I fold up the header tag, the rest of the website content is the main tag, and also the footer tag. Like before, we can do this in our JavaScript file.

We'll first need to load the main and footer tags as constants. I might add them at the top of the group since they are sort of major tags on the page.

I'm going to duplicate the first "btnOpen" constant twice. And for the first one, let's make that the main tag. So I'll rename the constant to "main", and update the querySelector() as just "main" so it'll load the main tag. And for the second one we'll make that the footer, so let's rename it to "footer" and update the querySelector() to "footer" for the footer tag.

Now, we want to set both main and footer tags to be inert when the menu is opened. So in the openMobileMenu() function, I'll try to group them with the line removing the "inert" attribute from the "topnav\_\_menu".

Before that, I'll add a new line and write "main.setAttribute('inert', '') " to add the "inert" attribute and set it to a blank value. Since we're doing the same thing for the footer tag, I'll duplicate that line and then rename it to use the "footer" constant.

And then we'll want to do the opposite, and remove the "inert" attribute from the main and footer tags when we close the menu. So in the closeMobileMenu() function, before the "menuTopNav.setAttribute()" method, I'll create a new line and write "main.removeAttribute('inert')".

Then we'll duplicate that line and change the constant to "footer".

Now let's save, and test on the website. So initially, the "topnav\_\_menu" is inert. And the main and footer tags are not.

Then when we click to open the menu, the menu is no longer inert, and the main and footer tags are inert.

What this is doing is making the main and footer content not able to be accessed by screen readers or keyboards when the menu is open. We can actually see this in action in the accessibility tree.

Let's reload the site, and in our dev tools go to the "Accessibility" tab. In the tree, we have the main document, which is the entire website. And under it we have the "banner" node which is the header tag, and after that is the main node which is the main tag, and then a "contentinfo" node, which is the footer tag.

Now let's see how the accessibility tree looks when the menu is open. Firefox is a little buggy with this, and it won't update the accessibility tree automatically. So I have to reload the entire page, so that we only see the "document" node, and don't expand it yet.

I have to click to open the menu, and THEN I can expand the "document" node. And now we have the banner which has the header and navigation content, but the main and contentinfo nodes are no longer there. So the "inert" attribute is successfully working.

Then if we go back to the "Inspector" tab and close the menu, we can see that the main and footer tags have the "inert" attribute removed now.

Alright, that seems to be good.

Another nice feature we can add for keyboard users is that if we use the tab key to navigate to the hamburger menu, and then hit Enter to open the menu, it's considered a best practice to have the Close button automatically focused.

This lets the user know where they are focused on the site, and they can also quickly close the menu again by pressing Enter. Then when the menu is closed, we will automatically focus on the hamburger button.

In our JavaScript, let's add some code to focus on the close button when the menu is opened. In the openMobileMenu() function, at the end, I'll write "btnClose.focus()".

And similarly, in the closeMobileMenu() function, we can focus on the open button after the menu is closed by adding "btnOpen.focus()".

Let's save, and reload the website. And now I'm going to use the Tab key until the hamburger button is focused and has that outline highlight. And then I'll press Enter to open the menu, and we can see that the close button has focus now.

And if I press Enter again to close, the hamburger button has focus. So that works, and it will make navigating the menu a little more intuitive for keyboard users.

And the last optimization we're going to be doing is for users who don't want to see motion based animations. Some people experience vertigo and other really unpleasant things when they see certain moving animations, like elements moving back and forth or scaling up or down.

And they may have turned off animations in their Windows or Mac settings. We can detect this with a "prefers-reduced-motion" media query, and use that to change or remove the animation itself from the website.

On our website, opening and closing the menu uses a sliding animation, which could trigger a negative motion-based effect in some people. So, we're going to change that to a fade animation if the user has selected to reduce motion.

In our styles for the "topnav\_\_menu", in the breakpoint-down mixin, I'm going to add a media query and write "@media (prefers-reduced-motion)".

Then in the media query, I'm going to cancel out our default "translate" value of "0 -106%", by writing "translate: 0".

Then I'm going to make the menu faded out by default, similar to the overlay, by writing "opacity: 0". So initially the menu will have 0% opacity.

And, we also need to update our "transition" style. I'm fine keeping the duration and the timing-function, so I'm only going to update the property that we are animating by writing "transition-property" and setting it to "opacity". That way the other two values will remain the same.

That's good for our initial menu styles, to hide it with opacity.

Now we need to fade the menu in when the open button is clicked. So above, in the "open aria-expanded true" style, I'm again going to nest a media query in there, and write "@media (prefers-reduced-motion)". And in it I'll change the "opacity" to "1".

That should be everything we need, stylewise. So let's save, and test this out. On our website, I'm not going to reduce motion animations yet, so we can test and make sure we didn't mess anything up with the sliding animations.

On our site, I'll reload just to refresh again. And click the open button, and the menu slides down. And closing it makes the menu slide back up. Awesome, so that is working!

Okay, now I'm going to go into my Windows Settings which I already have open-- you can get here by using the Windows menu and searching for "animation effects" which is this setting here that we have.

So right now we have animation effects turned on. I'm going to toggle this off. And then back on the website, let's open the menu again. And now the menu is fading in! And if we close, the menu fades out.

Alright! So that's all the features we're going to be adding to the menu. Let's do one final check on the different viewports. First let's check iPhone, and if we scroll all the way down the sticky nav is working. And clicking the open button opens the menu, and scrolling is locked. Then clicking the close button closes the menu, and we can scroll again.

Let's try iPad now-- and instead of the hamburger menu, we have the Top Navigation links. And scrolling down, the top nav is sticky. So that's good.

And let's quit out of the dev tools and load a desktop view. And we have our top nav links, and scrolling down the nav is sticky. So yeah, I think we're are all good with the menu!

Code-wise, one last thing I will do before deploying is go back to the JavaScript file, and I'm going to comment out all our console log messages. You usually want to either delete or comment them out so they don't go up to your production server.

So I'm going to do a Find and anywhere where we have "console.log", we want to comment it out with Ctrl+forward slash. I am going to keep them in a comment-- you can delete them if you would prefer to.

Now, let's deploy our changes! In GitHub Desktop, in the "Changes" tab, we'll do our usually thing and eyeball everything. And we have a line endings warning on the bodyScrollLock file-- this is because of the difference between how Windows and Mac machines handle line endings.

I'm just going to ignore the warning. You might have to deal with this if you're working on a team that has people with both Windows and Mac computers. But for projects by yourself it doesn't really matter.

Other than that, things are looking pretty good. So in the commit panel I'll add a commit message of "Top Navigation - hamburger menu". And then click "Commit" and "Push to origin".
