## Hiding elements accessibly

Alright, so right now, when you initially load the mobile site, the menu is visually hidden, and there's no way for you to access its content until you open the menu.

Then when you do open the menu, you only have access to the menu content, and not the rest of the website, until you close the menu again.

And we want to have a similar functionality for screen reader and keyboard users, so that they can interact with the menu in the same way.

Because right now, screen readers, which navigate websites through only the HTML markup, nothing visual through CSS, can still access the menu even if it's closed. We can see this if we inspect the Accessibility Properties, and in the tree, we can see the navigation, and the dialog that contains our links.

And for keyboard users, who may be navigating by using the tab key, they can also access the menu links even when they're closed. If we check the box that says "Show Tabbing Order", it starts at 1 with our skip link, then goes to 2 with the logo, and the hamburger button is 3.

The next link after it, 4, should be the next link in the page, which is the Free Trial button. But it's 9, and it's because of the "topnav\_\_menu" dialog and all the menu links.

If we click to open the menu, all the links are tabbable, 5 through 8. And we don't want them to be accessible if the menu is closed.

I hope that helps explain what we are going to be setting up now.

Also, I do want to mention that I am not an accessibility expert, but I have been trying to get better at making sure I'm building websites with accessibility in mind.

One of the places I've learned the most from is Sara Soueidan, who is an accessibility expert. She's written a lot of articles on her blog, and she also has a course that I've personally found really helpful and in-depth.

This isn't sponsored, I just recommend her as a great resource if you're trying to get better at accessibility too. I'll link to her stuff below and in the resources module.

Alright, back to what we're doing for this menu.

Like I mentioned, if you hide an element visually with CSS, they are still going to be accessible to screen readers and keyboards. But one way we can make those elements not accessible by those devices is to use an HTML attribute called "inert".

Making an element inert won't change anything visually, but the browser will effectively ignore the element.

What we want to do is if the website is loaded on mobile, the "topnav\_\_menu" will be inert. But if we load on desktop (or tablet), we don't want it to be inert, because on desktop the full top navigation is visible.

So, we're going to use JavaScript to detect if the website is on mobile or desktop. And if it's mobile we'll dynamically add the "inert" attribute, and if it's on desktop, we'll remove it.

And as a quick side note, when I say "desktop" in this section, just know that I also am including tablets in that. It's just easier to say "desktop" rather than "desktop and tablet" every single time.

Let's go into our JavaScript file. We're going to use a super helpful method called "window matchMedia()" which will let us target a media query condition, the same kind of media query that we use in our styles, but in JavaScript.

As in most cases, we are going to load this condition as a constant. So up at the top, under the "btnClose", I'll create a new constant. And I'll call it "breakpoint" since we're going to be testing if the device loading the website matches our breakpoint width.

Then I'm going to set it equal to "window dot matchMedia". Then in the parentheses, it takes a string as a parameter, so we need to add quotes. And in the quotes we can put in our media query that we want to target.

First let's figure out what number we want to put in here. We can't use our Sass function because this is in JavaScript, so I'm just going to manually put in the actual number. Let's refresh our memory and look at our breakpoints Sass file to see which one we want to use.

I'll use the Quick Open menu and type in "breakpoints" and go to the SCSS file. And in our breakpoints-up map, "medium" starts at 700px. So we can use that number. And I do want to use em units, not pixels, for accessibility.

So I'm going to calculate this manually since we only need the one number. And in the calculator we'll put in "700" divided by 16 to get to em units. And we have 43.75. So I'll select that and copy.

Then in our JavaScript, I'm going to write our media query condition. It's very important that this is enclosed in parentheses, because that's how the media query conditions appear, and the match won't work if it doesn't have the parentheses.

And, instead of the "min-width" media query I'm going to use the slightly newer syntax with "width" and then a "less than" symbol or left angle bracket, and then the number, "43.75em".

It is kind of nice being able to use this syntax because it's simpler and clearer, instead of writing "max-width colon 43.75em". But I wanted to show you both because most websites currently are still using the older "min-width" or "max-width" media queries.

They are totally fine and still work. So I think it's a good idea to know both ways of writing it.

Okay, now we have our "breakpoint" constant. This will return data about the current conditions loading the website in what's called a MediaQueryList object, which is a collection of data.

Let me show you what this looks like by testing it out. At the very bottom of the file, I'm going to create a console log message, and in it I'll add the "breakpoint" constant.

Let's save and test out the website. And let's make sure we're on iPhone, and then reload for good measure. And we can see in our Console that we have a "MediaQueryList" object. If we click that little arrow on the left, it expands the data in the object, and lists the different properties out in an easier to read format.

So in our MediaQueryList, it has a "media" property which is the value of the matchMedia() parameter we added in our JavaScript.

And then there's a "matches" property which is returning true. This means that the current conditions do match our width of less than 43.75em, so it is true. If we change the device to iPad and reload, then we can see that now "matches" is false, since we are greater than 43.75em or 700px.

Looks like that's all working, so let's delete our console log message since we don't need it anymore.

Now, we can write some code and if the breakpoint matches property is true, meaning we're on mobile, we will add the inert attribute to the "topnav\_\_menu" element. And if it's false, meaning we're on tablet or desktop, we will remove the inert attribute.

I'm going to create this before the button event listeners. And to do this, we'll create an "if" statement. If you haven't worked with if statements, here's how they look.

It starts with "if" and then in some parentheses, we'll write a condition that we want to check if it is true or not. And then in curly brackets, we'll write the code that we want to run if the condition is true.

In our parentheses, we want to check if the value of "breakpoint.matches" is true. We can write that with just "breakpoint.matches" since it's already going to be either true or false.

Then In the curly brackets, I'll write a console log message, saying "is mobile".

We also want to run some different code if the device is not mobile. So we can add to our If statement by adding "else" and then another set of curly brackets. And in it I'll write yet another console log message, this one saying "is tablet/desktop".

Let's save and test if this works. On our website, I'll make sure we have the iPhone selected, and then reload the website. And in the Console, we can see our message, "is mobile".

Let's also test the opposite, if it's not mobile. I'll change to iPad and reload again. And the message says "is tablet/desktop".

Awesome, so our If/Else statement is working. Now let's write our actual code that we want to run if the device is mobile. If we're on mobile, we want to make the "topnav\_\_menu" element inert, by adding an HTML attribute of "inert" to it.

Just like when we were running code on the open and close buttons, we need to first create a constant for the "topnav\_\_menu" element. So up at the top, I'll add this under the "btnClose" constant, I'll create a new constant with "const", and call it "menuTopNav".

And we'll set this equal to, "document.querySelector()" and add a hashtag for the ID. And let's go back to the HTML to check what ID we gave it. The "topnav\_\_menu" div has an ID of "menuTopNav", so I'll copy that, and paste it in.

So, in our "breakpoint.matches" condition, I'll leave the console log message for now, and under it I'll write "menuTopNav" then "dot", and then we're going to run a method called "setAttribute()".

This takes 2 parameters, the first is the name of the attribute we want to add or update. That will be "inert". And even though "inert" doesn't need to be set to anything, we do need to have a second parameter, and this will just be a blank string, which we can set with two quotes.

So that should be good for mobile. Now, we don't want the "topnav\_\_menu" to be inert on tablet or desktop. So we do also want to cover cases where we're switching from mobile to desktop. This will involve writing more code later to detect a switch.

But for now, let's add the opposite effect, of removing the "inert" attribute from the "topnav\_\_menu" if we're on tablet or desktop.

So in the "else" statement, I'll write "menuTopNav dot" and then the opposite of "setAttribute" is "removeAttribute". And that one only needs 1 parameter, of the attribute we're removing. So again it will be "inert".

Let's save, and check if the "inert" attribute is successfully getting added on mobile. In our website, make sure we're on mobile. And I'm going to inspect the hamburger menu, and in our Markup View, I'll select the "topnav\_\_menu" element, and it does look like the "inert" attribute got added!

Let's reload just to make sure. And it's been added again. And just to check, let's change to iPad and reload again. And it does not have the "inert" attribute this time, which is right.

We also want to remove the "inert" attribute from the "topnav\_\_menu" when the menu is opened on mobile. If we don't, then you won't be able to interact with the menu links or click the close button.

So, I'm going to copy the "menuTopNav.removeAttribute()" code from the tablet/desktop condition, and then paste it in the openMobileMenu() function.

That way, if we load on mobile, the menu will initially be set to inert, but if we click the open button, we will make the topnav\_\_menu no longer inert.

And, we should probably add the "inert" attribute back in when the menu is closed, so that it is no longer accessible for keyboards and screen readers if it is not visible. So I'll copy the setAttribute('inert') method, and add it to the closeMobileMenu() function.

Let's test this out. On our website we'll make sure we're loading the iPhone view, and in our Markup View, I'll make sure to select the "topnav\_\_menu" div so we can monitor it. And let's reload, and initially we have the menu set to "inert".

Then when we click the open button, the menu opens and the inert attribute gets removed. And then if we click the close button, the menu slides back up and we can see that the inert attribute is again there. That's great!
