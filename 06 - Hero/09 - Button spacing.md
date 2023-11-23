# Button spacing

Now let's also look at the spacing between the buttons, because right now they're right next to each other. Let's go to Figma, and then open the website next to it, and you can see that we need to add some space between them.

And actually, the buttons on the website look slightly longer than in our design. I think that's because of that 2px border again-- we had subtracted 2 pixels from the top and bottom padding so the height is correct, but I forgot to also subtract from the left and right padding. Because the border goes all the way around the button.

So in VS Code, I need to adjust the padding, and subtract 2 from our 16px of horizontal padding. So instead of `u.rem(16)` it should be `u.rem(14)`.

And now when we save and compare to the design, the buttons look like they're the same width.

Ok, going back to the space between the buttons, in the mobile design, I'm going to select the `Free Trial` button and then holding down Alt and hover over the `Pricing` button. And Figma is saying that there's 20px of space between the buttons. And if we check on the desktop design, it's the same, 20px.

Let's see what we have on the website right now. It actually looks like there's a couple pixels of space between the buttons-- let's see where that's coming from. If I inspect the `Free Trial` button, in the source code, Firefox actually tells me that there's `whitespace` between the two buttons. If I hover over the `whitespace` label, it's 3.2px wide.

(One note that at the time of recording, Chrome does not explicitly tell you the whitespace is there, but the space does exist in Chrome, which has definitely caused headaches for me in the past. Just another reason why I like using Firefox!)

Why is this whitespace happening? If we go to our index.html file, I've put the link tags on separate lines. And, since we set the button links to be `display: inline-block`, the browser is displaying the buttons side by side. And having the link tags on different lines results in a space getting added between them in the browser.

So, now that we know why the whitespace has been added, how do we get rid of it between the buttons? There are a few different solutions, some kind of hacky like adding a negative margin to one of the buttons to get rid of that space. But the one that I think is most effective is to put the buttons on the same line in the HTML with no space between them.

I'm going to put them on one line and also delete the test links. Now when I save, Prettier has put them on two lines, but the last closing right angle bracket of the first link is on that second line. This will also get rid of that space. Now when we check out the website, the whitespace is gone and we can see the buttons are right next to each other.

Doing this fix does make the markup look a bit weird, especially if you don't like the idea of having everything on one line or having that angle bracket split up. So honestly, unless the added whitespace is is causing a big issue, I would generally leave the links on two separate lines in the HTML, because at least in our case I don't think 3 extra pixels of space makes a huge difference that most people would notice.

Now, let's add that 20px of space between the buttons. There's a few different ways to go about this. We could add a new div to wrap around both buttons and make it a flex or grid parent, and add 20px of gap between the flex or grid child items.

But that seems like a lot of extra markup and styles to add. So I think I'm going to add 20px of margin-inline-end or margin-right to the first button. However, this is a more hero-specific thing, not a style I necessarily want to add to every teal button on the website, assuming more are added in the hypothetical future of this website.

Now, how should we target that first button in the hero section? Let's take a look at the index.html file. Can you come up with a selector that we can put in our hero.scss file that includes the `hero__button` class? If you want to try this yourself, you can pause here.

Ok, so when I look at the HTML, one way we could target that first button is by adding the `primary` class to the `hero__button` class selector-- and targeting an element that has both class names in its class.

Let's go to our hero.scss file. And in the `hero__button` selector, I'm going to nest a child selector in there, and make it `ampersand dot primary`. We need the ampersand so there's no space between the `hero__button` class and the `primary` class, so the selector will target an element that has both classes.

Without the ampersand, there would be a space between classes in the selector, and it would be targeting a child element that has the `primary` class and is contained within a parent element with the class `hero__button`. And that isn't what we're targeting in our HTML.

One way to test is to add a style rule of `outline: 2px solid red`. And then save, and check out our website. And it looks like that selector is correct-- the `Free Trial` button has a red outline! Now that we know our selector is correct, we can add the style rule to add 20px of space to the right of the first button. So I'll keep our red outline for a little longer, and add `margin-inline-end` which is the same thing as `margin-right` and set it to 20px. And now we can see that space to the right of the button.

I did want to show you one more way you can target this button, and that's by using a pseudo-class that will target the first `hero__button`. And this doesn't require using the `primary` class. In the browser, make sure you're inspecting the primary button, and then we'lre going to update that selector so instead of the `dot primary` we will add `colon first-of-type`. And make sure there's no space between the `hero__button` and the colon of the pseudo-class.

We can see that this selector does work to target the first button. What the `first-of-type` pseudo-class does is that in a group of sibling elements it will select the first element that has the `hero__button` class. So in the `hero__text` div, we have the h1 tag, paragraph tag, and then 2 `hero__button` anchor links. This rule will select the first one.

There is also a `last-of-type` pseudo-class that we can use-- if we change the selector to that, it will select the second `hero__button`. Going back to our styles, I think you could either use the `primary` helper class or the `first-of-type` pseudo-class to add that 20px of right margin. I might just stick with the `primary` class, and delete the red outline style since we don't need it anymore.

Great, we should be pretty set with the basic button styles now. In the next video, we'll be working on the hover state styles.
