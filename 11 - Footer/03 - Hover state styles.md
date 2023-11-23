# Hover state styles

The basic text styles look pretty good. Maybe one more thing we can add is a hover state when hovering over either the logo or the text links. We can test out a few different styles in the browser and see what looks good.

In Firefox, I'm going to inspect one of the anchor links and with it selected in the source code, in the `Rules` tab I'll click the `hov` label to the right of the Filter textbox, and then check the `hover` pseudo-class checkbox, and then click the plus sign icon to the right of the `hov` label. What we've done is force the hover state on the first `About` link, and then any style we add in the rules will show up on the website even if we're not actually hovering.

Now we should have a selector that says `footer__link:hover`. In the selector, let's add the `color` property and then in the value we can get Firefox to load the CSS custom properties that we've created by typing `var(--)`.

Then in the pop-up of the different custom props that we have, we can press the down arrow to go through the different colors and kind of monitor the website on the right to see what might work here. The darker teal of the `button-primary-bg-hover` could work.

And if we exit out of the pop-up we need to clear out what's in the parentheses and retype the double dash to get it to pop up again. The `fullwidth-bg` magenta color also looks kinda cool. I think maybe the darker teal color is good, since we are using teal for some of the button colors so it keeps it a bit more consistent. So let's go back to `--button-primary-bg-hover`.

But I'm not sure if it's going to have enough contrast with the white background, so let's check that with Firefox's accessibility tool. I'm going to right-click the teal `About` link and select `Inspect Accessibility Properties.` You can also get here by clicking the double right angle bracket icon at the top and select `Accessibility`.

Now, let's check for issues of Contrast. And unfortunately it does look like the teal link for `About` is not a high enough contrast. The other one that shows up is the hidden `Header` h2 tag for screen readers, so I think it's ok to leave that one as is since the screen readers will read from the HTML code, not the visual website.

It's saying the contrast is 2.33 which is not enough for WCAG standards. If you want to learn more we can click that link. WCAG stands for `Web Content Accessibility Guidelines`. And for contrast, this table tells us that for body text the minimum level or AA contrast ratio needs to be 4.5, and if you want to go for the higher triple A rating, it needs to be 7.

I haven't done a ton of accessibility, but usually most tests for accessibility require the double A rating at minimum, and triple A if you want to go beyond that. It might differ based on the company or industry you're working in, but in my experience we've tried to hit at least double A. Going back to our teal link, 2.33 is quite a bit lower than 4.5.

To compare, let's inspect the accessibility properties for the dark gray text like the `Company` title. If we inspect that and then in the top panel expand the `heading Company` and click the `text leaf` then in the bottom panel it tells us that the contrast is 11.39 which is a lot more contrasty than even the higher triple A rating.

So we definitely want to make the text color darker. Let's try the magenta color because I think that was darker. Let's go back to the inspect the `Inspector` tools, in the `footer__link:hover` selector we added, I'm going to clear out the variable name in the parentheses, and then re-type the double dash to make the custom props pop up again.

And this time let's select the magenta `fullwidth-bg` color. And then go back to the `Accessibility` tool and if we select the text leaf for the `About` link then now it says that the contrast is 5.70 which is great. It doesn't meet the triple A rating, but I think double A is ok. So let's use that color.

Back in our styles, let's go to the colors.scss file. I think it's best to create a new custom property for the text link hover state-- we could use the `fullwidth-bg` custom prop and it would work now, but if we ever change the fullwidth background color in the future it will also change the text link hover color. So it's best to separate it out into a new one.

Let's make a new custom prop, maybe I'll call it `text-link-hover` and let's add it under the other text custom properties at the top. After `text-light` I'll add `--text-link-hover` and then copy the magenta color from `fullwidth-bg` and paste it in as the value. And let's copy the `text-link-hover` name, and go to the footer.scss file.

Here, we want to add the hover state pseudo-class selector to the footer links. That's going to be in `footer__link`, and I'll add the ampersand because it's the pseudo-class for the `footer__link` element itself, and then type `colon hover`. And in the curly brackets let's add `color` and then we want to load the custom prop so we need to type `var` and then in parentheses I'll paste in the `text-link-hover` custom prop name.

Now let's save and see if it works. Going back to the website, now when we hover over the footer links, the color changes to magenta. That looks good!

The last thing for hover states is adding one for the logo link. Let's see what we did for the top nav logo. If we go to the top and inspect the logo, and select the `topnav__homelink` in the source code, then click the `hov` label and check the `hover` checkbox, we can see the hover state style in the topnav.scss file. When hovering over the logo the opacity goes down to 0.9 or 90%. We can do a similar effect for the footer logo.

Let's check out the Top Nav styles, they are in scss/components/topnav.scss. And if we find the `homelink` selector, we can see the hover pseudo-class has the `opacity: 0.9` set. I'd like to use this for the footer logo too, but I don't want to duplicate code. So I'm going to create a new helper class that will have this hover state style. I'm going to select the entire hover state rule, press Ctrl-X to cut it and then save the file.

Then let's figure out where to put this style rule. I might just put it in the boilerplate.scss file since it is a shared style. We could also create an entirely new Sass partial for hover states, but I'm going to put it in boilerplate for now.

In the boilerplate.scss file, since we're going to create a new class, I'll add it to the end of the file after the `visually-hidden` class. And let's make the class descriptive so it's easier to understand what it does. I'm going to name it `hover-fade`, and then in the curly brackets I'll paste the style rule. And now, we need to add the `hover-fade` class to both the Top Nav and Footer logo anchor links.

I'm going to copy the class name without the dot so there aren't any typos, and then go to the index.html file, and first in the header we need to find that `topnav__homelink` anchor link, and I'll paste the class name after the `topnav__homelink`. And let's go down to the footer, and find that `footer__homelink` class and paste in `hover-fade` after it.

Now let's save, and check that it's working on the website. Let's inspect the Top Nav logo first, and making sure that we have the hover state selected, we can see that it does have the `hover-fade:hover` style rule and the opacity is changing. And let's go to the footer and inspect the logo there too, and with the hover state forced we can see that it also is working. Looks pretty good!

So I think that should be it for the basic text and spacing styles. Next thing is to add the markup for the other footer column links, and then work on the layout styles.
