# Creating a skip link

Now, let's start writing the HTML markup for the top navigation. One thing that's good for accessibility is to add what's called a "skip link" to the top of the page. This will allow screen reader users and users who use only a keyboard to skip over the header and get right to the main content.

If there is no skip link, these users will need to manually go through every navigation link before they hit the main content of the website. We don't have a lot of links in our navigation, but for websites that have huge menus with lots of links, having to go through every single one would be really annoying to get through.

Let's go to VS Code and our index.html file. The skip link should be the first content on the website, so right inside the body tag I'm going to create a new anchor link and set the "href" value to "#main". This means that clicking this link will navigate the user to the element that has an ID of "main", which we'll be adding.

Then I'll make the link text say "Skip to main content". Then in the main tag, we need to add an ID value of "main". This will make clicking on the skip link completely skip the header and top navigation and go straight to the main tag. Sometimes skip links are also called "jump links".

Now if we look at the website, we can see the "Skip to main content" link up at the top. A couple more things we have to do is to visually hide this link so that screen readers can detect it, but it won't show up on the webpage. And, for keyboard users who might be pressing Tab to navigate the website, we also want to make it visible if it gets highlighted with Tab.

To accomplish this, we'll be using that "visually-hidden" class that we added earlier for the hidden headers. It's in the boilerplate.scss file. We'll also need to add some additional styles so that when the skip link has what's called "focus" in CSS, it will become visible.

First, let's add the "visually-hidden" class name to the a-tag. I'm going to copy the class name, and in the index.html file add a class to the link and paste in the class name.

I know I could also just type the "visually-hidden" class name manually, but if I type it out and happen to have a typo, then the class name in the HTML won't match the class selector in our Sass file, and the styles won't work.

So I often will copy and paste class names, especially if they're longer, just to make sure the names match. Or I'll try to check the class name after typing to make sure there's no typos.

Anyway, let's check out the website-- and now the link is hidden. If I inspect it, we can see that it has the "visually-hidden" class styles. Now, what we want to do is to make it visible when it has focus from the keyboard.

We can actually force this state in our developer tools so we can test what styles will work. If we select the link in the source code panel, then in the bottom panel we can click on the ":hov" and checking the ":focus" checkbox. Then if we click the "plus" symbol it will add a selector for the link with focus state, and we can add our rules there.

Let's figure out what style rules we want to add to this focus state, to cancel out our visually-hidden styles. First let's undo the left of negative 10,000 by adding "left: 0". Then I also want to cancel out the width and height of 1px, so I'll set the width and height to auto.

Ok! That seems to be working, we can see the skip link text. It is currently overlapping the main header text. And even after we build the rest of the design it may overlap something. So to help with readability, let's add a few more styles.

First, I'll add a background color of white to the focus state, so that you can read it over the header text. And maybe add some padding around it, let's try 0.5 rems.

And to help distinguish it from the other content around it, I'll also add a border of "1px solid". By not setting a border color, it will automatically take the border color from the text color, which is the purple visited link text color. So we'll leave that for now, and we can always tweak it later on.

You might notice that I'm using pixels for the border instead of rem units. I know I said previously that you shouldn't ever use pixels, but I think in some situations pixels is fine. It's most important to use rems for font-size because you definitely want the font-size to increase if the browser base font size changes.

But it's not as important for smaller sized properties like border or even padding, because it's really most important for the text to be readable, and if the border doesn't get thicker if you set your browser's font-size to something larger, it's not going to cause huge issues.

So I think you could go either way for border and padding, in terms of using pixels or rems-- it won't matter quite as much as font-size.

That looks pretty good! So let's copy just the rules we added, and not the selector. And then in our boilerplate Sass file I'll add a nested selector and write "ampersand colon focus" and then paste in the rules.

The colon indicates that it's a pseudo-class-- pseudo-classes help you select how an element looks when it's interacted with in a certain way or falls under specific conditions, called "states." Some common states are hover (when you hover your mouse over the element) and focus (when you use the tab key to navigate through each focusable element on the page).

Let's now test to see if the Skip Link focus state styles work! I'm going to reload the page and then hit the Tab key. And, the link appears! And if we hit "Enter" it will navigate to that link. You can see in the URL bar there's now a "hashtag main" added to the URL.

And, navigating to the main tag takes the focus off the skip link, so it has disappeared. We can also do a test without navigating to the link. If I remove the main ID from the URL and reload, then hit Tab to make the skip link appear, and hit Tab to navigate off of the skip link, it will lose focus and disappear. So we now have the skip link working!
