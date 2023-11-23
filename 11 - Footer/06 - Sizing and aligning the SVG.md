# Sizing and aligning the SVG

Right now the SVG is just taking the same size as the `Twitter` text, which we will need to change. Let's first check the size of the social media icons in the design. In Figma, I'm going to zoom in on that `Follow` column so we can see everything better.

If I select the Twitter icon, it's 18px wide and 15 pixels tall. Let's check Facebook, and that icon is 18px wide also, and 18px tall. Then Instagram is again 18px wide, and about 18px tall. And YouTube is 18px wide and 12.66px tall.

They are all 18px wide, which was on purpose on my part in the design. You do want the icons to be the same width, so that it makes the text to the right all aligned the same way. If one of the icons was a different width then it could throw off the alignment.

Anyway, since they are all the same width, we can add that 18px width as a style rule for all the social media icons. Going to our styles, in `footer__social` I'm going to set `width` to `u.rem(18)`.

And unlike with the image tags, we don't actually need to set `height: auto` on the SVGs in order for them to have the correct aspect ratio. It's another interesting quirk of SVGs when they have a viewbox set-- the image itself will always maintain the correct aspect ratio, so if we change the width, the height will automatically adjust.

And now when we save and go back to the website, we still have the scaled up browser font size, so we have big text, and the Twitter icon is also now bigger, which is great. Let's change that font size back to the default of 16.

We also need to check on the alignment and spacing. I'm actually going to zoom in on the browser so it's a bit easier to see. If I hover over the SVG in the source code, with the grid lines we can see that the icon is a bit taller than the text, and it's kind of extending above the text. Ideally the icon and text should be vertically centered to one another.

Looking at the markup in the source code, the flex parent should be the `footer__link` anchor link, and the flex children will be the SVG and then the `Twitter` text.

Let's start writing our flexbox styles. In footer.scss, in the `footer__link` selector, I'll change `display: inline-block` to `display: inline-flex`. This is because if I set it to `display: flex`, the link will go all the way across and make not just the text clickable but also the empty space to the right. So inline-flex behaves pretty much the same as flex, except that it will only take up the amount of space as its content.

And under that, I'm going to add `align-items: center` to vertically center the flex children. The other thing is that we want to add some space between the icon and the text, and I think a great way to do that is with the `gap` property. So let's check the design to see how much space there is.

In Figma, if I select the Twitter icon and hold down Alt, there is 16 pixels of space between the icon and the text. Going back to our styles, still in the `footer__link`, I'll add `gap: u.rem(16)` to add the space.

Let's save that and see how things look on the website. It looks pretty good! We have the space between icon and text, and if I hover over the `footer__link`, they also seem vertically centered to one another. So that works using flexbox.

We can also do this with grid. Just in the browser I'm going to change the `display: inline-flex` to `display: inline-grid`. And inline-grid is the same as inline-flex, in that it behaves the same as `display: grid` but the grid container won't take up all the available horizontal space, it will only be as wide as the grid content.

And with grid, we do need to set `grid-template-columns`, otherwise like you see here, the grid children won't automatically be on the same row like you do have with flexbox. We can add `grid-template-columns` and to make it simple I'm going to use the repeat() function, set it to `2` for 2 columns, and set the width of each column to `auto` so that they will be the width of the content.

And now it matches the design-- we have the same gap as we did with the flexbox approach, and things are vertically centered. Again, you can use whichever approach you like the best-- in this case I think flexbox is easier because you don't have to write that additional line of code to set the grid template the same way you would with the CSS grid approach.

Let's refresh to go back to our saved styles using flexbox. I think we're pretty good with the social media icon styles, so let's update the markup to add the other icons. Going back to VS Code, we have the index.html file. And let's get the SVG code for the other icons, starting with Facebook.

I'm going to open the primary sidebar and in the img/social folder, we'll open the `facebook` SVG and then copy that code. And then I'm going to paste it inside the `footer__link` anchor link before the `Facebook` text.

The next one is for Instagram, so I'm going to open the instagram.svg file, copy the code, and paste it in before the text. And let's open the last one, for YouTube, copy the code, and again paste it in before the text.

We do need to add the `footer__social` and the `footer__social-path` classes to all the SVGs and paths too. I'm going to copy the whole `class=footer__social` from the Twitter SVG, and then paste it in after the `viewBox` for all the other SVGs. And then go back to the Twitter SVG path, copy the `class=footer__social-path` and then paste it in each of the other paths.

And now let's save, and on the website we can see we have all the social media icons loaded and if we hover over each `Follow` link they all have the magenta hover state. Ok, so the `Follow` column should be all set now.

Next up, let's get the layout working with CSS grid!
