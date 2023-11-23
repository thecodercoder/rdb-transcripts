# Prep and HTML markup

In this section we're going to be building out the last section of the beginner level website-- the footer. As usual, before we start building, let's look at the design and see what we need to do.

In Figma, let's take a look at the desktop design first. I'm also going to turn on the layout grid-- if you select the "Desktop - 1440" frame, then in the right sidebar, in the "Layout grid" panel, make sure the "12 columns" grid is showing with the open eye icon.

Ok, now, in the footer, we have 2 rows of content. The first row has the logo and copyright information. Then in the second row, we have 4 columns of footer links. And it looks like each column is taking up 3 columns, or 25% of the wrapper.

Then, in each column, the content is mainly text links. But the "Follow" column also has social media icons along with the text. Also, everything seems to be aligned to the left, nothing is centered.

Ok, let's check out the mobile design. It's pretty similar to the desktop one, where we have the logo and copyright info first, then the 4 groups of footer links. But here, instead of having 1 row with 4 columns, the links are in 2 rows with 2 columns each per row.

For the images, we'll need the logo image-- but instead of re-exporting from Figma, I'm going to show you how we can make a dark gray version from the existing logo image from the Top Navigation. For the social media icons, I originally got all the social icons from Font Awesome, so I'm actually going to show you how to download them from Font Awesome directly instead of exporting them from Figma.

The reason is that Font Awesome includes some comments in the SVG code that gives them attribution, and exporting the social images from Figma strips that out for some reason. So, since I don't want any of us to potentially get in trouble, let's go to the browser and go to FontAwesome.com.

Then on the site, click on "Icons". And we're going to scroll down all the way until we see a section called "Brands Icons". Click on "View All Brand Icons" and now we can see their whole collection.

Let's start with Facebook, since it's first. Click on the icon, and then in the top right corner there's a down arrow "download" button. And if we click that it'll download an SVG. Next up is Twitter. Click on the icon, and then click to download. The next one we need is Instagram, so do the same thing for them. And the last one is YouTube.

I personally like to just download the individual icons I need from Font Awesome, but if your website is using a ton of them, you can also load some or all of their library via a CDN or even hosting them locally on your own server.

If you click up in the top, the "Start" link, you'll be able to learn how to do that. I'm not going to cover setting those up in this course, but wanted to mention it in case you need to use that approach in the future.

Once you have all the icons downloaded, go to where they are in your File Explorer, and copy or move them into your "img" folder. I'm going to try to organize a bit since we do have quite a few files. I'm going to create another folder in the image folder called "social" and then I'll paste in the SVG files there.

So we are good with the social media icons-- next up, let's go into VS Code and I'll show you how we'll get the dark gray Mythos logo image. In VS Code, in the Solution Explorer, scroll down until you hit the image folder. Then we need to find the "logo-mythos.svg" file and make a copy of it-- you can do this either by right-clicking and selecting "Copy", or using the shortcut Ctrl-C.

Then paste in the same location by either right-clicking the "img" folder and selecting "Paste", or using the shortcut Ctrl-V. After pasting, you should see a file called "logo-mythos copy.svg". Let's rename this. Right-click the file and select "Rename" or press F2. Then rename it to "logo-mythos-dark.svg", and open the file.

In the SVG file I'm going to wrap the lines by pressing Alt-Z, which toggles wrapping. Then all the way at the end of the path tag you should be able to see a "fill" attribute, currently set to "white." This is what's making the logo up in the top navigation that solid white color.

For the footer, we need the logo to be the dark gray text color. Since this is the same color as the dark gray for the text, we can grab that color from our `scss/globals/colors.scss` file. In our colors, the one we want is the "text-dark" color. So I'm going to copy that hsla() color and paste in the "fill" attribute in the SVG file, so it should say "fill equals" and then in quotation marks, the hsla() color.

Hex colors are what you normally will see in SVGs, but other color formats like RGB, HSL or HSLA should all work. Ok, now, we have our logo image. So let's start writing the markup in our index.html file.

Most of the website content has been in section tags in the main tag. We can see this if we fold up all the section tags-- they're all contained in the main tag. And before the main tag, all the Top Navigation content was put in the header tag.

So in a similar way, we're going to put all the footer content in a `footer` tag which comes after the `main` tag.

Again, we're just trying to use semantic tags whenever possible, and organize them in a way that is better for accessibility. Also I think it makes it easier to go back and find things in your HTML. If everything was nested in several layers of div tags then it would be a bit harder to look through the file.

Alright, let's start writing our footer markup. After the closing main tag, in the footer tag, let's give it a class of `footer` so that we can target that class in our styles. And `footer` is going to be our BEM block name.

Let's go back to look at the design. The footer doesn't have a title saying `footer`. Let's check our outline that we created back at the beginning for the h-tags. Ok, so like we've done in other sections that also don't have titles, we need to add a visually-hidden h2 tag that says `Footer` so that screen readers can more easily navigate the page.

Going back to VS Code, in case you don't remember exactly what you need to add, since you know we've done this in the past, we can do a Ctrl-F to search for `hidden`, to look for those `visually hidden` h2 tags.

The first one is in the header, so we can copy that tag, then go to the footer tag and paste it in there. Then make sure to change the text to say `Footer` instead of `Header`. Now, let's start adding the rest of the footer content after the hidden h2 tag.

As we've done in previous sections, in the footer tag I'm going to add a wrapper div. I'll type `dot` to start writing the classes, and then write `footer__wrapper dot wrapper` without any spaces between them. Then press Tab or Enter to generate the div with those classes. It doesn't matter if you have `footer__wrapper` or `wrapper` first in the HTML, it will all be the same when it comes to the CSS.

In the wrapper div, we will put the logo and copyright section, and then the four sets of footer links. I think I'm going to put each of those groups in their own section tag. So starting with the logo section of the footer, in the wrapper div I'll add a section tag by typing `section` and then give it a class with `dot` and then the class name, let's use `footer__logo`.

Then in this section tag we want the logo to be a link to load the homepage, similar to what we have up the Top Navigation. Since the 2 logo images are the same size, to save time I'm going to scroll up to the Top Nav and copy that anchor link `topnav__homelink` that includes the logo SVG. And then paste it in the `footer__logo` section.

Then we'll need to update the class names. So instead of `topnav__homelink` let's use `footer__homelink`, and in the image tag itself, let's make the class `footer__logo-image` since we're already using `footer__logo` for the section tag. We also need to update the file name to use `logo-mythos-dark.svg`.

After the logo image is the copyright text. I'm going to put this in a paragraph tag, so I'll type `p dot footer__copyright`. Then press Enter, and in the p tag we need to get that copyright text. So let's go back to Figma, select that layer, and copy, and then go back and paste it in the paragraph tag. And that should be it for the `footer__logo` section.

The next section is going to be the first links column. So after the closing section tag for the `footer__logo` section, I'll go to a new line and create a new section tag by typing `section`, `dot`, and since these columns look pretty much the same stylewise, I'm going to create a class that they can all have, like `footer__column`. And if later on we need some column-specific styles, we can always add more classes then.

In the `footer__column` section, let's refer back to Figma to see what we have here. Looking at the design, each column has a header, and then a set of links. Since we already have an h2 tag for the footer, these column header should follow the hierarchy and be h3 tags.

And then, we want to put the links in an unordered list because they are technically a list of links. So each column will have its own unordered list, with the text links. The first column is `Company` so I'm going to select actually the whole `Company` section also including all the text links.

Then back in VS Code, I'll paste it in the `footer__column`. This way we have all the text content and won't have to keep flipping back and forth to copy each little item. First, let's create our h3 tag. Then I'm going to select the `Company` text and press Ctrl-X to cut, and in the h3 tag, I'll press Ctrl-V to paste it in.

Now, for our text links, what we want is to create an unordered list-- again, we're trying to use semantic tags when we can. And since the footer links are essentially a list of links, I think it's best to use the HTML unordered list tags for them, instead of having a bunch of paragraph tags or something.

And I'll want the unordered list to have a class of `footer__links` using the plural term `links` to indicate that it's a group of links. And in that unordered list, we need to add 4 list items, with a class of `footer__item`, and in each list item we need an anchor tag for the links, with a class of `footer__link`.

Now, just for fun, let's try to create the entire markup using Emmet. Remember that you can use the right angle bracket to indicate a child element, and the asterisk symbol to create multiple numbers of tags.

If you'd like to try it yourself before watching me, you can pause here and try.

Alright, to add the unordered list, I'll write `ul` and give it a class with `dot` and the class name, `footer__links`. Then I need to add 4 list items as children of this unordered list. To add children to the tag, we need to write right angle bracket, and I'm going to first add 1 list item with `li dot footer__item`. And, each list item needs to contain a link, so I'll write another right angle bracket and then write `a dot` and the class name `footer__link`.

If I pressed enter now, it would generate an unordered list with 1 list item that has 1 link. But since we want 4 list items, each with their own link, what we can do is add parentheses around the li-tag and its anchor link, to indicate that those are what we want to multiply. And then after the close parentheses, add an asterisk or star and the number 4.

Now, press Enter or Tab to run Emmet, and it should generate the unordered list with the class name `footer__links`, and in it are 4 list items with the class `footer__item`, and in each list item is an anchor link with class `footer__link`.

Now let's move our text into the markup. I'm going to select the `About` text, Ctrl-X to cut, and then in the first anchor link press Ctrl-V to paste. Make sure you've pasted it between the opening and closing anchor tags.

In VS Code instead of cutting and pasting, you can also drag selected text to where you want. So I'm going to select `News & Press`, then click and hold on the highlighted text, and then drag it up to inside the second anchor link. And we can do the same for `Careers`, and `Contact`.

And we'll just leave the `href` attributes in the anchor links blank since for our course they won't actually go anywhere. In real life, the href attributes would go to the URLs of the web pages of each of these links.

Let's save, which will trigger Prettier to format the HTML. And do a quick check of all the markup to make sure each anchor link is inside the list item. And now let's check out the website, just to see how it looks. Ok, the h3 tag has most of the styling it needs from the global h3 tag styles, but we'll check and see if it needs any tweaking for the Footer header styles.

And the links, since they're in an unordered list, have the default bullets. And if we inspect the ul-tag itself, we can see the margin and padding that it has from the default styles. This is similar to the Top Navigation, where in the ul-tag we canceled out the default styles with the `list-style-type: none` and then zeroing out the margin and padding.

One thing we could do is move those 3 style rules from the `topnav__links` ul-tag to something that we can use for both Top Nav and Footer links. We could move them to a helper class, then add that helper class to both ul-tags.

Or, we could target any unordered list tag that's inside the header or footer tag, since it's very unlikely that we'd want bulleted lists in either the header or footer. That actually might be a good solution, so that we don't have to add a helper class to the HTML.

Let's do that now. In VS Code, I need to go to the topnav.scss file, so in scss/components, it's the topnav.scss file. And in the `topnav__links` selector, we'll select those three styles, list-style-type, margin, and padding. And I'll press Ctrl-X to cut.

And, since this will be a global style since it's used in different parts of the website, let's put them in the scss/globals/boilerplate.scss file. And I'm going to add them before the `visually-hidden` class since I'm kind of keeping all the tag or element styles together for organizational purposes.

So let's add our selector. I'm going to create a compound selector to first target any unordered list in the header tag-- and we'll add that with `header space ul` so that any descendent ul-tag in the header tag will be targeted. We want just a space between them, not the right angle bracket, because that would only target the direct children of the header tag.

Then add a comma, and we'll do the same for the footer tag with `footer space ul`. And then add curly brackets, and in them we'll press Ctrl-V to paste the style rules.

Now, let's save and see if it worked on our website. In our Top Nav the links look the same, and if we inspect the `topnav__links` ul-tag, we can see that boilerplate style that's targeting both footer and header. And if we go to the footer, we can see that the bullet points and the extra spacing are now gone. And if we inspect the unordered list, it also has those boilerplate styles. So looks good!

Now let's work on adding the basic styles for text and spacing to the footer links that we have so far. Then once we are confident that those styles are working, I'll duplicate the `footer__column` markup to make the other columns.
