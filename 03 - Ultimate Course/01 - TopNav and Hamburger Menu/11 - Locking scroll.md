## Locking the scroll

One other common design pattern with mobile menus that I've seen is to prevent scrolling on the main website content when the menu is open. Right now, we can scroll freely, which could potentially cause confusion if you accidentally scroll to a different part of the website.

On our website, you can still see quite a bit of the main site when the menu is open, but a lot of mobile menus will cover the entire viewport, so if you scrolled you wouldn't notice until you closed the menu and were suddenly in a different part of the website.

And even in our case, I think it would be a better user experience if you weren't able to scroll when the menu is open.

You can prevent scrolling by adding the style rule "overflow: hidden" on the body tag. By default, the "overflow" property, which controls how the website handles additional content that doesn't fit inside the element, is set to "visible".

On the body tag, this will result in having vertical scrollbars if the content in the body is bigger than the viewport, like we have. [ scroll ]

But, in the browser styles, if I go to the body tag and set "overflow" to "hidden", we are not able to scroll anymore, because all the additional content has been hidden.

This is the general approach to locking scrolling on the overall website. However, by itself it doesn't always work, especially with different browsers and mobile devices. So in this case, I think the best overall solution is to use an existing plugin that specializes in locking scrolling.

The plugin that I've found is called "body-scroll-lock". So if we search for "body scroll lock github" we should be able to go to the repo. And in the Readme, it has some of the reasons why this plugin will probably save you time and headache.

So, to install this on our website, let's scroll down to "Install" and then "Usage examples" until we get to the "Vanilla JS".

This tells us we need to load the JavaScript file in our head, and then it has code snippets that we can use. Let's get the file we need-- it says "/lib/bodyScrollLock.js".

And for those of you who are more advanced in JavaScript, you might prefer to install this in other ways like yarn or npm. But I'm going to be showing you a more beginner-friendly way of doing it.

If we go back up to the top of the page, we'll navigate to the file that they had in the example. So the "lib" folder, and then the file they showed us was "bodyScrollLock.js". If we click on it, you can see the contents of the file and all the code in it.

However, they also have a minified version-- if I click on the left sidebar on the "bodyScrollLock.min.js" file, it's the same code but it's been minimized, so just really condensed down to as few code as possible. This will help save the load on your server when loading the website.

So I'm going to download this minimized file. And in the gray bar, on the right side there is a "download" button. So let's click that to download the file.

And I'm going to go to the File Explorer, and in the Downloads folder, I'm going to copy that file, and then navigate to the project root, then let's put it in the "app/js" folder along with our script.js file. And paste it in.

Now that we have the file, we need to load it in our index.html. In VS Code, we'll go there, and up in the head tag, I'm going to duplicate the script tag that we have already, and in the first one I'll load the plugin, so that we load the plugin code before our own JavaScript file.

I'll delete the file name and the last forward slash, then re-type the slash to get the autocomplete, and select the bodyScrollLock.min.js file. And save.

Now we have the body scroll lock code getting loaded on our website, and we need to write the code to actually lock the body scroll. Let's go back to the plugin website, and let's find that example code that they had for Vanilla JS.

Okay, so in here, it says we want to target an element that we want to allow scrolling in. I think this is more for modal or pop-up windows, but I think we have to put something there, so we'll probably use the "topnav\_\_menu".

Then, to lock the body tag, we'll run this "bodyScrollLock . disableBodyScroll()" function, and in the parameter we'll have the "topnav\_\_menu".

Then to unlock it we do the same thing except using the "enableBodyScroll()" function. And those are the only two we need. We don't need that last one since it's for canceling multiple elements that have been locked.

I'm going to copy that "bodyScrollLock.disableBodyScroll" code, so we can paste it in our code.

And going back to our JavaScript file, we want to first disable the scrolling when we open the menu. So in "openMobileMenu()" I'll add this line, at the end. And I'll set its parameter to "menuTopNav" since that's the element that is visible when the menu is open.

Then, I'll copy that line and we'll do the reverse in the closeMobileMenu() function. I'll paste it in and then instead of "disableBodyScroll" I'll rename it to "enableBodyScroll" to unlock the body scroll.

Now let's save, and see if it works! Alright, so on our website initially we can scroll. And if I open the menu, and try to scroll, I am not able to scroll. But if I close the menu I'm able to scroll again!

So that worked really well, and I think is one good example of how using other people's code can save you time. I do recommend doing your due diligence before using other people's code-- check the GitHub Issues and even look for reviews of it to see if it works for people.
