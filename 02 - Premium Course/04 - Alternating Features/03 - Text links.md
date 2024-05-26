## Text link styles

Let's now add the text link styles. In Figma, let's check what that magenta color is. I'm going to select one of the paragraphs that has the magenta link, and in the right sidebar under the panel that says "Selection colors" it lists the colors used in the text group. So we have the dark gray "383A4A" color, and then the magenta "BF1085" color.

I want to first check if we've already saved the magenta color in our colors.scss file, so we need to get the HSL value of the color here and then compare it to our colors.scss file. If I click on the color swatch, and in the pop-up change the format to HSL, it is "320, 85, 41".

Now let's go back to VS Code and have Figma open on the right so we can see the color numbers. In VS Code I'm going to use the Quick Open menu and load colors.scss. And it looks like we do have some magenta colors, near the top is "text-link-hover" which we used for the Footer text links. And that one does say "320, 85, 41"!

So it's the same color as the Footer links, except that in the Footer, the links are gray, and they turn magenta when you hover, hence the "hover" in the name. I think it might be nice to use the same CSS property for both the Footer and Alternating Features links, just because they are both links.

I might change the name and just have it be called "text-link" since there aren't any other text link properties. And since I did change the name, I'll have to change it in the footer styles.

Just to be safe, let's run a search in our project files for "text-link-hover" to make sure we're changing it in each place. We can do this by opening the search sidebar by pressing Ctrl-Shift-F or Cmd-Shift-F for Macs. And I'll type in "text-link-hover".

And in the results, it's in the footer.scss file, in two places, and in the final style.css file, which we don't have to worry about since it's the compiled CSS file and it'll get updated anyway. So I'm going to double-click one of the results and it will open the footer.scss file. Now let's just close the sidebar with Ctrl-B or Cmd-B.

If I scroll down the file I can see that "text-link-hover" property in the two places. So let's change both those to be just "text-link". And let's save and check out the website to make sure the Footer links still turn magenta on hover.

And it looks like the footer links are good! So, going back to the colors.scss file, we can now use the "text-link" property for the links in the Alternating Features section.

We need to figure out where to put these styles. Do we want it to just be in the Alternating Features section, or do we think that they should be a global style for all text links on the website?

Looking back at Figma and kinda scrolling through the website, the magenta text links only are in that Alternating Features section. However, I can imagine that if this was a real website with multiple pages, there could very well be links in text blocks in other places in the future. So it might be more efficient if we made this a style that could affect future text links.

Let's just try writing some global styles and see what happens. These links are in anchor tags, and we've already set some of those styles in our typography styles. So I'll Quick Open and go to the typography.scss file.

And if we scroll down, after the paragraph styles we have anchor tag styles that is removing that default underline with "text-decoration: none". This compound selector is for anchor tags, visited links, and active links meaning when you click on them.

I'm going to try adding the link color in this same selector. I'll write "color: var(--text-link)". Let's save and check out the website. And immediately we can see that this has affected the Footer links, and scrolling up, the links in the Alternating Features, and the Top Navigation links too.

Obviously we don't want to affect the Top Nav and Footer links. Let's start by figuring out why this typography style is affecting link styles in different sections, because I'm assuming we had set the link colors for the Top Nav and Footer using our BEM class names.

I'm going to inspect one of the Top Nav links, and in the "Rules" tab let's check out the style rules getting applied. So in the rules, they are ordered in order of specificity with more specific starting at the top.

For the topnav\_\_link, we did set the color to "text-light" on the "topnav\_\_link" class, but it's getting overridden by the magenta color we just added on the compound anchor tag, visited, and active anchor tags.

So is this happening?

Well, specificity in CSS is calculated using 3 different categories of selectors: ID, class, and type.

The ID selector has the most weight, specificity wise, then class, which also includes pseudo-class selectors like ":hover", is less than ID, and then type meaning the tag or element, or pseudo-element, has the least amount of specificity weight.

When specificity calculation is discussed, it's often written with 3 numbers corresponding to each category, separated by dashes. Like "zero dash one dash zero".

So let's first get the specificity of the ".topnav\_\_link" class, and see why the anchor tag rule is overriding it. The "topnav\_\_link" class is just one class.

So there's no ID, there's no tag selector either. So this means that the specificity of this is 0, 1, 0.

Because it just has one class, which is the middle number

Now, if we compare that with the compound anchor tag selector, we have to look at each one individually, because it's a compound selector, and there are multiple ones.

The first one is just the anchor tag, so the specificity for this first one is going to be 0-0-1, for the 1 tag.

And this will not override the "topnav\_\_link" class, because the class has more weight than the tag.

And another thing to note is that even if we added more tags to this selector, if there are no classes, it will never override the class selector just with tags. So we know that the first anchor tag selector is not what's overriding the "topnav\_\_link" class.

Now, the second selector is "a:visited" selector, and that contains no ID, but it does have the ":visited" pseudo-class, and then it has the a-tag, which is the tag. So the specificity number for this is 0-1-1.

Now because both the "a:visited" and the "topnav\_\_link" selectors contain 1 class, that makes them equal in terms of class. However, breaking the tie is the anchor tag, which is on the a:visited selector.

So this will make the a:visited selector win out over the .topnav\_\_link class, and that's why the Top Nav links are magenta.

If I added the anchor tag to the ".topnav\_\_link" selector, then it would also have 1 tag and 1 class selector, which is the same specificity level as the "a:visited" selector. But since the topnav.scss styles are getting loaded after the typography.scss styles in our final CSS file, this makes the CSS cascade come into play. And the later styles of the same specificity will override earlier styles.

This is just to explain the cascade-- I don't think adding an anchor tag selector to the ".topnav\_\_link" class is a good solution. For one thing, if we go to the topnav.scss file, there's no real way to add that anchor tag to the "topnav\_\_link" class selector.

So to fix the issue, I think we should change the typography.scss style to reduce its specificity, so that the section-specific class selectors can override it. In the file, I'm going to select that "color: var(--text-link)" rule, cut it, and then below I'm going to create a new selector just for the anchor tag, and paste it in.

Because the compound selector is just to remove the default underline from all links. We don't want to create confusion like we did by also setting the color on all of those. So now, the magenta color is on a selector that's just 1 element, which is less than the class selector rules for the Top Nav and Footer links.

Now when we save, the Top Nav links are back to white, and if we scroll down to the Alternating Features section, the link in the text is magenta like it should be, and down in the Footer, the links are back to gray, and hovering will turn them to magenta.

Cool, so I think this is good for the text links.
