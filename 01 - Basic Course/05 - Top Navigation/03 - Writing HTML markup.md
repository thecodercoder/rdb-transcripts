# Writing the HTML markup

Now, let's continue writing the markup for the top navigation, and go to our index.html file.

In the header tag, the first thing I want to do is add a visually hidden h2 tag that says "Header". If you remember, back in our design, we created an outline for all the H-tags. And we need to create a hidden H1 or H2 tag for screen readers, for both the Header and Footer.

And I forgot to add the "hidden" note to those, so let's adjust that in our outline.

Again, you could also set the "Header" as an h1 tag, but I know having multiple h1 tags has been viewed as a big no-no. So let's set it as an H2 tag.

Even though having an h2 tag in the header before the main h1 tag might not technically be good practice, screen readers will still be able to navigate using them. And I think that's the most important thing.

Using the Emmet shortcut, in the header tag, I'll type `h2 dot visually-hidden` and press Enter to create the h2 tag with the visually-hidden class. Then in the tag I'll write "Header".

And if we save and load the website, we can't see the "Header" text, but if we check the source code panel, and expand the header tag, we can see the hidden h2 tag, and it has the styles from our `visually-hidden` class.

Now let's start adding the other elements for our top navigation. I'm going to be giving the elements class names according to the BEM approach. The first thing we need to come up with in our BEM approach is the BEM block name. Since we're working with the top navigation, I'm going to name the block `topnav`.

Since all our top navigation markup will be in the header tag, let's add a class to the header called `topnav`. Then in the header, after the hidden h1 tag, I'm going to create a child div with the class `wrapper`. The reason I need a child div to be the wrapper instead of just putting the wrapper class in the header tag is because we want the top navigation to have that purple background color, all the way across.

If I put the wrapper class on the header tag, the entire header, including the purple background color, will have the wrapper class's max width of 1200px. So for screens wider than 1200px, the purple would have the default background color of white on either side. I'll show you what I mean by this after we add some more content to the header.

Let's refer back to the design. First, let's add that logo image. In our index.html, I'll add it inside the wrapper div. We want the logo to be a link, so that if you click it, it will load the homepage, which will be the root domain.

In the wrapper div, I'll add an anchor link by typing `a` and then give it a class by typing `dot topnav__homelink`. This is again using the BEM approach, with the BEM block name `topnav` followed by two underscores and the BEM element name, `homelink`.

In this link, I'll set the `href` attribute to a forward slash. This will make clicking the link load just the domain, for example Mythos.com as our hypothetical domain name. The domain is usually what you'd want to load as the homepage of a website.

In the logo anchor link, we want to load the logo image that we exported from Figma as an SVG. So I'll add an image tag by typing in `img` and then `dot` to give it a class, and then a class name of `topnav__logo` where we're again using the BEM approach for the block `topnav` and the element `logo`.

In the image tag, in the `src` or "source" attribute, we need to set the path to our logo image file. If we look in the Solution Explorer in the left sidebar, in the `img` folder we have the `logo-mythos.svg`. This location and filename is what we want to set the source path to.

In the source, I'll start typing forward slash which will again load the root directory of the website, and then VS Code will automatically load the folder and let you see what subfolders and files exist. So we can select the `image` folder, and then the `logo-mythos.svg` file, and then press Enter.

For the `alt` attribute, we want to add "alt text," describing what the image is. This is the logo for Mythos, but since it's also the link to the homepage, it would be most helpful to add that so screenreaders users will know right away that this will link to the homepage. So I'm going to set this to "Mythos homepage".

Since it's an SVG, instead of using an image tag, I could also paste in the actual SVG code so it's an inline SVG. In VS Code, if we double-click the SVG image file, it'll load what looks like sorta like HTML, with an SVG tag. SVGs are written in another markup language called XML, or "Extensible Markup Language".

In an SVG file, everything is in an SVG tag. You can see there's some info like width and height. In the SVG tag, there's a path tag. This is the actual vector shape of the Mythos logo, in code form. At the end of the path tag it says `fill=white`, which is what makes the logo white.

This is a pretty simple SVG, with just one shape's path, but SVGs can be very complex with multiple paths and shapes.

One cool thing about SVGs is that we could just copy the code here and paste it right in our HTML file instead of the image tag. This would be called an inline SVG.

I normally just use an img tag to load SVGs, because I find it easier. Also, if you load the SVG as an image tag, your browser can cache, or save a local copy of it on your computer. So if you load the webpage again, it won't have to download it from the web, which will help load the website faster and save on data usage.

You can't normally cache with inline SVGs. It's not a huge deal since this logo image has a very small file size, but if you're ever working with larger SVG files, this information might come in helpful.

However, if you wanted to do something like change the color of a path when you hover over the SVG, making the SVG inline in your HTML markup will make this easier to do. I'll show you how to do this later in the course, when we do the footer section. But for the logo, we'll keep it in an image tag.

After our homepage logo link, we also have our three navigation links. We'll use another semantic HTML tag, the nav tag, for this. Then in the nav tag I'm going to create an unordered list or ul tag to store the navigation links, and give it a class of `topnav__links`.

The reason that we want to make the links in a list is because they are a list of links. So again, we're trying to use semantic HTML tags whenever we can, so they will add more context for what type of content they contain.

In our unordered list will be the list items, with an `li` tag. I'm going to create the first one by typing `li` and then `dot` to give it a class, and then `topnav__item`. Then in the list item I'll add an anchor link by typing `a` and `dot` and give it a class of `topnav__link`.

In the real world, each link would go to another page in the website, and that URL would go in the `href` attribute. But since we only have the one homepage, I'm going to leave the `href` blank.

Now I'm going to select the list item and press Ctrl-D to duplicate it 2 times to get our 3 links. And I'll add the link text according to the design. If we check the design the first link is "Features," then "Pricing," then "About". So in the first anchor link I'll add the text "Features", then the second one will be "Pricing", and the last one "About".

And this is our markup for the Top Navigation! I know that it can be difficult to know what's considered best practice for things like what HTML tags to use. Believe it or not, I don't have all the knowledge of everything web development just sitting in my head. I always have to do a lot of research when I'm building websites and making tutorials-- and most web developers have to do that too, I'm pretty sure!

When I'm building a website and I'm not sure about what best practice is for something, one thing that can be really helpful is looking at big websites that you're pretty sure follow best practices, and see how they build their websites.

So the short list of websites that I tend to look at as examples of best practice are: CSS-Tricks.com, MDN or Mozilla Developer Network, and the Accessibility-Developer-Guide.com. So let's take a look at how they build their navigation.

CSS Tricks has a top navigation that is not sticky. And if we inspect their code, we can see that in their header, their links are put into a nav element and then an unordered list.

MDN has a fixed top nav, as well as a fixed left sidebar. And if we inspect their code, they also are using a header tag, and a nav tag for their navigation links-- also in an unordered list.

The Accessibility Developer Guide has a fixed left navigation sidebar which is using a nav tag and the links are again in an unordered list.

So I hope this helps-- I wanted to show you that you don't have to know everything off the top of your head, but you can do research and see what other websites are doing, and learn from them. Let's start setting up our styles for the Top Navigation.

One thing I'm going to do just for the sake of this video is add some space at the bottom of the website, so we can see the bottom content in the middle of the screen which I think will make it a little easier for you watching this video. You don't have to do this, of course.

I'm going to go into the boilerplate.scss file and in the body selector I'll add a rule saying `margin-block-end: 50vh` to add a space below the website that's 50% of the viewport height. And I'll add a comment after as a reminder that this is temporary and needs to be removed after the website is complete.

If you're not familiar with the `margin-block-end` it's totally ok! If your browser is using a left to right and top down direction, which most languages are, it's the same thing as `margin-bottom`. Using the `block` and `inline` and `start` and `end` words for margin and padding is part of a a newer set of what's called "logical properties", which let you control direction and positions based on the document flow.

If we go to our Developer Tools, in the "Layout" tab, for the body tag, we can see the margin-block-end or margin-bottom that we added. If your website content is going from left to right and top to bottom, then `margin-block-start` will be the top side, `margin-block-end` will be the bottom, `margin-inline-start` will be the left side, and `margin-inline-end` will be the right side.

I know these terms may seem weird or overcomplicated as opposed to top, bottom, left, and right, but they can be more flexible for if you have to change the direction of the website content, like for languages that might read from right to left. If you do have to change the direction, then using the `block` and `inline` start and end's will let your browser automatically change the sides based on that direction.

These are fairly new CSS features, and while modern browsers support them, some older browsers may not. You can still definitely use top, bottom, left and right if you want. I'm just trying to use these new features to use more modern CSS when I can.
