# Write wrapper styles

Another global style I like to set up is the wrapper styles. By "wrapper" I mean that if we look at the design, all the text and image content on the website is limited to a specific width, and won't go wider than that.

I mentioned this briefly in the intro to Figma section, but let's look at the wrapper in the design.

In Figma, if I select the entire "Desktop" frame, in the right sidebar in the "Design" tab, under the "Layout grid" panel, there's a "12 columns" and a "1 column" grid. If I click the closed eye icon on both to show them, we can see the 12 columns in that light green color, and then a thin orange outline for the 1-column grid.

And they both are limited to 1200px wide, as you can see the 1-column grid is 1200 pixels wide. Let's add this to our styles.

In VS Code, I'm going to create a new Sass partial in the scss/layout folder, and call it `_wrapper.scss`. And since I'm creating a new partial in the layout/\_index.scss file I'm going to add a new `@forward` rule for it. I'm putting this in the `layout` subfolder because the wrapper is going to control the size of elements on the website.

Then in the wrapper Sass file I'm going to add these styles to a class called `wrapper,` because with that BEM or block-element-modifier approach, we want to name the file the same name as the block.

Then in the wrapper class, I want to use some of the same style rules that we did earlier for the `grid` class in our demo website. So let's actually go to the grid.scss file. What I want to reuse is the width and the margin-inline style rules and paste them in the wrapper class selector.

And, since we're using the u.rem() function, we should also copy the `@use` util from the grid.scss file, and paste it in the wrapper.scss file, so the wrapper styles can access that function.

Now, looking at the width property again, we're using the min() CSS function. As a refresher, the min() function can take two parameters, and it will calculate which one is the smaller value and use that one. The first parameter, `100% - u.rem(40)` is saying that the width will be 100% of the width of the website minus 40px, converted to rem units.

This is mainly for mobile styles, so we have a bit of space around the website content on smaller viewports. And the `margin-inline: auto` rule will set left and right margins to `auto,` which will center the content on the page.

Since we initially used this for the demo website, let's go back to Figma and check the mobile design, to see how much space around the website content we need to add. In the Mobile frame, I'm going to double-click in the Hero section so that the "Hero content" layer group is selected.

Then holding down the Alt key and moving the mouse outside the selection, Figma tells us that we have 24 pixels of space on the left and right sides, so combined that's 48 pixels of space. Going back to our code, let's update that `u.rem(40)` to be `u.rem(48)` to match the design.

The second parameter, `u.rem(1000)`, is a static width of 1000px. Right now this will set the maximum width at 1000px. Since the design has 1200px as the maximum width, let's change that 1000 to a 1200.

Now that we have the wrapper styles set, I'm actually going to delete the `grid.scss` file because that was just for the demo website and we don't need it anymore. And we'll also need to go into the layout `index.scss` file and remove the `@forward 'grid'` rule since the file doesn't exist anymore.

Now, let me show you how it will look on the website when we actually use this class. Let's go back into the index.html file, and I'm going to remove all the markup inside the body tag that was from the demo website and we don't need anymore.

Now, starting from scratch, let's start plotting out the website content using semantic HTML tags. In our design we have 3 main parts: a header containing the top navigation, the main content of the website, and a footer at the bottom.

These parts actually have corresponding semantic HTML tags that we can use. So in the body tag, let's start by creating a header tag. We'll keep this blank for now, so it's just a placeholder. Then under the header, let's add a main tag. Then after the main tag, let's add a footer tag, and we'll keep that blank for now too.

Going back to the main tag, it contains the main content on the website, meaning everything that's not in the header or footer. In the main tag, I'm also going to create an article tag. The article tag is meant to contain content that can be standalone or syndicated.

You can think about like this: if you wanted to share a URL of a webpage, or print out a website, what content is most important to include? You wouldn't necessarily need the header and footer, but you'd need a title and then the main content.

So I'd want to create the article tag inside the main tag. And then all the main content will go inside the article tag.

Then in the article tag I'll create a section tag by typing "section" and give it a class of "wrapper" by typing "dot wrapper". And we'll add styles to the "wrapper" class so the width will be limited to 1200px and centered.

The section tag is a bit more generic tag that you can use to section off parts of the website. Ideally each section should have a header of some sort that helps describe what that section of the website is about.

Then, in that section tag I'll create an h1 tag, and in the tag let's copy over the headline from the design that says "Find that elusive unicorn." And under that let's add a paragraph tag with a bunch of lorem ipsum text so we can make the content take up as much horizontal space as possible. So using Emmet I'll write `p>lorem50` to add 50 words of lorem ipsum placeholder text, and then save.

And Prettier has wrapped the words in the paragraph onto multiple lines for better viewing in VS Code. It's ok to put text content on multiple lines in the editor, because the browser will ignore them and display all the text the same way as if it was on one really long line.

Now let's see what the website looks like in our browser. We see our h1 text and the paragraph. If we inspect and select the section tag with the wrapper class, we can see the width property has that min() function that we just set. And if we look in the computed tab, it tells us that the width is 1200px, which is what we want.

Let's decrease the width of the viewport. In the dev tools I'm going to click the "Responsive Design Mode" icon, and select iPhone. Then we can adjust the width of the viewport to whatever we want if we hover over the right edge it'll turn into the 2 arrows and we can resize.

Keep an eye on the width up at the top. As we drag the right side out, the width goes up, and the device name has changed from "iPhone" to "Responsive" since we're now working with a custom viewport. Let's go back to a mobile size width. We can see that there is that space on the left and right.

This is from the first parameter of the min() function, where we set the width to 100% minus 48px. Since the content is centered from our `margin-inline: auto` rule, the 48px gets divided equally so it is 24px on left and right. And if we click on that "Layout" tab and make sure the "grid" class div is selected up in the source code, we can see that there is indeed a margin of 24px on the left and on the right.

So that's how the wrapper class works. We're going to be using that class in basically all the different section of the website. This is one example of a utility class that has basically just one function, that you can reuse in multiple places, which will save time since we won't have to keep writing the same style rules.
