## ARIA and animation

In order to handle the open and closed states of the menu, we're going to be adding some accessibility features that will be helpful for screen reader users, and which we can target in our styles, to visually hide and show the menu.

Specifically, we'll be adding ARIA roles and attributes to our markup, for accessibility.

ARIA stands for "Accessible Rich Internet Applications". And if you've ever looked at some existing website code, you may have seen ARIA attributes like "aria-label" or "aria-controls". There are a lot of ARIA attributes.

These features help users who may be visually impaired and are using screen readers to navigate websites. By adding these ARIA attributes to our HTML markup, it allows screen readers to read out and describe additional context that will help these users understand the website content.

For example, a visually impaired user may not be able to see that there is a hamburger button on the menu. But with ARIA, we can label the hamburger button and tell you that it is there for navigation purposes. And we can label the "topnav\_\_menu" as content that you can access with the hamburger button.

Let me show you what this would look like. Going to the index.html file, we're going to add some ARIA attributes to the "topnav\_\_open" button and the "topnav\_\_menu".

For the open button, I'm going to add a new attribute that says "aria-expanded" and set it to "false".

What we're doing here is telling screen readers that there is an element, the hamburger button, that they can interact with to access some content that is kept separate from the rest of the website. The "aria-expanded" attribute being set to "false" means that the content is currently hidden.

However, how do we tell the screen reader what content you can access by clicking the button? We can do this by labeling the button and giving it a name that screen readers can read to the user.

Since the hidden content contains navigation links, let's label it with the word "Navigation".

There are a few different ways of labeling elements so that screen readers can access them.

One easy way for buttons, is to put the text inside the button. So we could write "Navigation" inside the actual button element. And if I right-click the button, and select "Inspect Accessibility Properties", we go to the "Accessibility" tab in Firefox dev tools.

This shows you the accessibility tree of the document, and is kind of like a visual representation of the website and similar to how screen readers will navigate the page.

In the "navigation" node, we can see that the button is now given the name of "Navigation", which will be helpful for screen readers.

This does work, but as you can see, the word "navigation" is now being displayed. And unlike other buttons which have text, like in the Full-width CTA form, we don't want visible text in this one, so I don't think this is the best solution for the hamburger button. So I'm going to delete the text.

Another possible solution is to use the "aria-label" attribute and add it to the button element, and set it to "Navigation". Now, there's no visible text, and if we inspect the accessibility properties, the button does have the name "Navigation".

While aria-label does work, there are some issues with it that make it more of a good back-up rather than the optimal solution. One is that the text in aria-label attributes doesn't get detected if the user is translate the website to a different language.

Another is that if it's not implemented correctly, it can actually lead to confusion for the end user. So let's remove that aria-label.

So, I've shown you two ways to label the button, but they are not optimal for our current situation. So what can we use?

Well, the method that is considered optimal for labeling is to create a separate hidden element that contains the text for the label.

So, in the nav tag before the button, I'll create a new span, and in it write the name "Navigation". And now you can see the text. And if I inspect the accessibility properties, it shows up as a "text leaf" in the "navigation" node.

And, one super helpful feature of this tool is that it can check for accessibility issues, like the contrast of the text is not high enough to be readable, as you can also see. And the button is still not labeled.

First, let's go back to our code, and hide the span, by adding an attribute to the span of "hidden". And now, this is hidden visually, and if I inspect the accessibility properties of the button, the "Navigation" text leaf isn't there anymore.

This is sort of similar to how we have _visually_ hidden labels before, like our hidden h2 tags for sections that don't have a visible title. But this is different because we are hiding the label not just visually, but also from screen readers.

We don't want screen readers to read this span, because we're going to use it to label the button. Let's go back to our code and do that. To use the hidden span to label, we need to give it an ID. So in the span I'll add ID and set it to "nav-label".

And now we can copy that ID, and in the button, I'll add a new attribute called "aria-labelledby" and set it to "nav-label".

Now when we save, on the website if we inspect the accessibility properties again, we can see that the navigation button now has the proper name, "Navigation".

We're good on the hamburger open button for now. And we'll be using JavaScript later on to toggle the "aria-expanded" value.

So we have the button to open the menu, but what about the menu itself? We also need to add some accessibility attributes to the "topnav\_\_menu" div that contains the hamburger menu content.

In the "topnav\_\_menu", we'll add an attribute "role" and set it to "dialog". The dialog role indicates that the element contains the additional content that you can access by interacting with the open button.

Other than the hamburger menu, other examples of dialogs might be accordions and pop-up or modal windows.

Now, I did want to mention that there is a newer native HTML dialog element with an actual overlay, that was made available in 2022. We can see this if we do a search for "mdn dialog". And if scroll down, we have this little demo for a modal window.

However, from what I could tell from researching, it seems kinda tricky to animate the dialog's overlay, at least at this point in time, which we do want to do.

So I'm not going to be using the native dialog, because we can achieve the same thing accessibility-wise, by using that ARIA dialog role that we added to the "topnav\_\_menu".

I just wanted to mention this since you may have heard of the newer dialog element, and are wondering why we're not using it.

Alright, since we've added an ARIA role to the "topnav\_\_menu" div, we now need to label it just like we did with the button.

Since this is part of the navigation menu, I'd like to label it "Navigation" like we did with the open button. And the good thing is, since we used that hidden span to label the button, we can actually reuse the same span to label the "topnav\_\_menu". The reusability is another reason why the hidden span label is pretty useful.

What we can do is go to the open button, and copy that "aria-labelledby" attribute, and then paste it in the "topnav\_\_menu" div.

And when we save, and inspect the accessibility properties of the hamburger button, now we can see that in the navigation node, the "topnav\_\_menu" has changed from having a generic role to now having the dialog role, and it's name is "Navigation".

So, we now have our Navigation Button, and our Navigation Dialog. But how do we actually open and close the menu?

This is where we will utilize that "aria-expanded" attribute on the button, by targeting when it's "true" in our styles and then opening the menu.

Going back to the index.html file, the "aria-expanded" is on the button, which has the class "topnav\_\_open", so let's find that selector in our styles.

And in the "topnav\_\_open" styles, I'm going to nest a selector and set it to itself with ampersand, and then if it has the "aria-expanded" attribute. HTML attributes you can select for using square brackets, and then in it write the attribute, "aria-expanded", and then the equals sign, and in quotes, the state we're looking for, which is "true".

And if aria-expanded is true, we want the menu to be open and visible, so we'll want to make the "topnav\_\_menu" have a "translate" value of "zero zero" to bring it back on screen.

How do we do that? Let's refer back to our index.html file, and here's the open button, and the "topnav\_\_menu" is the element right after it, meaning it is a direct sibling.

In our styles, we can add the direct sibling selector, which is the plus sign. And if that direct sibling has the class ".topnav\_\_menu", then we'll set "translate" to "0 0".

Alright, let's test and see if this style works. So I'm going to save, and in our Markup View, I'm going to double-click and manually change the aria-expanded value from "false" to "true". And when we do that, the menu slides down onscreen.

And let's manually change it back to false. And the menu slides back up. So visually, this works!

Also, we need to add that overlay that goes under the menu. So we'll be doing that next.
