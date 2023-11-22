# Sass partials

Sass partials are one of my favorite parts of working with Sass. Instead of having to search through a giant long CSS file, you can split your styles up into multiple files, and even keep them organized in subfolders. This allows you to keep different parts of the website separated into different files, making it easier to locate a particular style rule when you're debugging.

It also allows developers to work on the styles at the same time with a lower chance of more than one person altering the same file and potentially creating a code conflict in your version control.

In our project, the first partial that we'll be creating is for some boilerplate styles. These are some general styles that I use on every website that I work on. These boilerplate styles are what I consider "global" styles, and I'll also be creating more global styles in other partials, so I want to keep them all in one folder.

In the app/scss folder, I'm going to create a subfolder called "globals." And in that folder I'm going to make a new file, "underscore boilerplate.scss." Then in that folder, I'll add some boilerplate styles:

```
html {
  box-sizing: border-box;
  font-size: 100%;
}
```

First, in our HTML selector, I'm going to set the font-size to 100%. This is for accessibility purposes, so that the default font size on the website will match whatever the use has set in their browser settings. This defaults to 16px.

Then, I'm adding "box-sizing: border-box," which ensures that any padding and borders added to an element on the website will be included when the final width is calculated. Meaning, if I set a box to be 300px wide and add 20 pixels of padding on all sides, the final width will still be 300px. If I don't set box-sizing: border-box, the 20px of padding on all sides will increase the width of the element to 340px, which generally is not desirable. We want any widths that we set to stay at those widths, even if we add padding. And the same is true if we add borders.

```
*, *::before, *::after {
  box-sizing: inherit;
}
```

Then, we want every element to have that same box-sizing: border-box rule, so we'll use the wildcard selector plus the pseudo-elements before and after to inherit the rule from the HTML element.

```
body {
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
  background-color: hsl(0, 0%, 11%);
  color: hsl(0, 0%, 100%);
}
```

Lastly, I'll add a body selector and reset the margins and padding to zero. These resets are helpful because browsers will usually have some default styles that they'll add to any website if they are not reset. And they will vary between browsers. So it's often helpful to add reset rules like this to your website.

I'm also going to go into style.scss and copy those test style rules and put them in the boilerplate.scss file. I'm going to clear out style.scss so it's empty, because we will be using it for other purposes now that we have multiple Sass files.

That's all that we'll be adding to our boilerplate styles for now. I'm also going to create another partial here in globals called "underscore typography.scss." In this file I'll be adding some styles related to text elements.

```
h1,
h2,
h3 {
  font-weight: 700;
  line-height: 1.1;
  margin-top: 0;
}
```

First off, I want to style our headline or H tags. So the first selector will be a compound selector. It will be for h1, h2, and h3 tags, separated by a comma, and they will have some shared styles. The H tags also have default styles that browsers will set, so I want to set these rules to make sure that they look the same across browsers.

First, I want them to all be bold, so I'll set font-weight to 700. Then I am setting the line-height to 1.1, which is like a percentage, 1.1 is like 110% of whatever the font size is for each of those H tags. Then lastly I want to remove the top margin that browsers always add, so set margin-top to 0;

```
p {
  margin-top: 0;
}
```

After the H tags, I'm going to add a rule for p or paragraph tags, also setting the margin-top to 0. This is just a personal preference for me-- by default the browser will generally add space on both top and bottom using margins. I like having space only at the bottom.

```
a,
a:visited,
a:active {
  text-decoration: none;
}
```

Lastly, I want to remove the default underline that gets added to text links. I'll do this by creating a style rule covering all A or anchor links, including both visited links and active links. So I'll set all of them to have text-decoration: none.

Now, we have our two global Sass partials and our main style.scss file. You might be wondering how we load the styles from the partials since they're in their own files and not in style.scss.

One way that we can do this involves creating another partial in globals called "underscore index.scss." I generally like to keep one index file in each Sass subfolder-- this helps with organization. In this index.scss file, I'm going to load the other two Sass partials that we created.

```
@forward 'boilerplate';
@forward 'typography';
```

What we're doing is using a Sass at-rule called forward to load the styles from boilerplate.scss and typography.scss. You might notice that even though the filenames start with an underscore and end in ".scss," we only have to write the words boilerplate and typography. You could write the whole filename out, but Sass will detect if you just have the same name without the underscore or SCSS file extension. So it's a little less to type, which is nice.

What forward does is pretty much just take those style rules in those partials and forward them on to get loaded. So the index.scss file is taking those styles to forward them on. And when we create more Sass partials in the globals folder, each one needs to get forwarded in this index.scss file too.

Then we want to forward all the global styles from index.scss to our main style.scss file. So in style.scss, I'm going to add "@forward 'globals';" Sass will see that globals name and be able to match it to the globals folder. And it will automatically look for this "underscore index.scss" file.

Ok, so we have our Sass files saved, let's go and check out compiler, and we did that it did detect different changes that we made. And if we go all the way down to the bottom, it says "Watching" and it doesn't have any error messages.

And if you hit Save again, I'm pressing Ctrl-S to save, you can see that it'll automatically run the compiler again, and it has that little success message. So that's a good indicator to know that everything is ok with your Sass compiling.

Let's also check the local server to make sure it's loading the styles correctly without errors too.

Ok, in the browser let's open the Developer Inspector. You can do this by hitting F12, or Ctrl-Shift-I, or right-click and look for an option that says "Inspect" or "Inspect Element." And it looks like we do have some errors here. So let's click on that to display the errors.

And, this error is pretty common. It says "localhost port 3000 app script.js was blocked due to MIME type (text/html) mismatch." So I decided to leave this error in the video because it's very common. I get asked this a lot and I figured I might as well let my mistake be a teaching moment.

If you see this error, it is most likely because the file you are trying to load, in this case, script.js, is in a different file path in your files than the link where you're loading it in your index.html file. The reason it's a type mismatch and getting loaded as an HTML file is because, if we click on that link, it loads an HTML error page saying it can't GET or find the file.

So to fix this, let's go back to VS Code and check out index.html.

And in the head, we can see our script tag loading "app/script.js." But in our actual files, the script.js file lives in app/js/script.js. So I forgot to add the "js" subfolder to the file path in our script tag. Adding that back in, let's check out the local site again. And it looks like that error was fixed! I am still getting an error for not having a favicon, which is the little icon image that would load in the browser tab. But that's not a serious problem and we'll fix that later on.
