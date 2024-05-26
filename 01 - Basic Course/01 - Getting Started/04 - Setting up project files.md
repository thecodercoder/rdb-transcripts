# Setting up the project files

Ok! So we've gone through some of the tools that we're using in the course. Now in this section I'm going to walk you through setting up the project files for the actual website.

First off, create a new folder wherever you want to keep the project.

I'm creating a new folder on my Desktop called "responsive-design-beginners." If you have a different location on your computer where you usually keep your GitHub projects, feel free to set the project up there. It doesn't matter a ton exactly where it's located.

Now let's create a GitHub repository in this folder.

Open GitHub Desktop and navigate to "File" > "Add local repository" and then select the folder you just created. GitHub Desktop will ask if you would like to create a repository here instead, since one doesn't exist yet. Click the "create a repository" link, and then check that all the settings are the way you want. I'm going to check the "Initialize this repository with a README" box, and set the License to MIT license so that it's open source. When you're ready, click "Create repository."

When the repository is created, go ahead and open VS Code. In VS Code, navigate to "File" > "Open Folder" and select the project folder.

Let's start by creating our `index.html` file. In that file I'm going to type the Emmet shortcut "exclamation point" and press enter to add some boilerplate HTML to the file.

Let's change the title tag to say "Mythos," the name of our fictional agency. And then let's add a paragraph tag with some lorem ipsum placeholder text. We'll use an Emmet shortcut again by typing in `p>lorem50` and hitting enter when the "Emmet Abbreviation" dropdown pops up. This adds a paragraph tag and inside it, 50 words of lorem ipsum text.

Now let's add tags for our CSS and JavaScript files.

In the `<head>`, type in `link` and then in the dropdown select `:css` to add a link tag. Then set the `href` attribute to `/dist/style.css`. This folder and file don't exist yet, but we'll be creating them later when we compile our Sass styles.

Under the link tag, we'll load our JavaScript. Type in "script" and then in the dropdown select `script:src` and press enter. Then in the `src` attribute type in `/app/js/script.js`. We're not going to be processing our JavaScript file since we're not doing anything complex with it. So this will remain in the `app/js` folder.

One last thing to add is a `defer` property in the script tag. This will ensure that the script loading won't block the loading of the rest of the website.

In the `<body>` tag let's add an h1 tag that also says "Mythos". We'll change this later but for now we just want some text on the page for when we test it in the browser.

Save the `index.html` file and we are done with it for now.

Let's now create our Sass and JavaScript files.

In the left sidebar of our project, create a new folder called `app`. Then in the `app` folder, create a subfolder called `scss`. Then click on the `app` name and create another subfolder in it called `js`.

So now, in your project file structure, we have the `index.html` file and the `app` folder in the project root. And then the `app` folder has the `js` and `scss` subfolders.

Now let's create a Sass file.

In the `scss` folder, create a file called `style.scss`.

For now we're just going to put in some test styles. In the `body` selector, add `font-family: Arial, Helvetica, sans-serif;` and set the `background` to `hsl(0, 0%, 13%)` or whatever color you want. And then set the `color` property to `hsl(0, 0%, 87%)` or again whatever you want.

As a sidenote, you may have noticed that I'm using HSL format for my colors.The HSL stands for hue, saturation, and lightness. You might be more familiar with HEX colors like `#000000`.

However HSL colors are considered a bit better format because they make it a lot easier to darken, lighten, and adjust the saturation level. So I try to use HSL colors whenever I can, but you are welcome to use HEX or RGB if you like those better.

VS Code actually makes it easy to convert between formats. If you hover over the color swatch you'll see a color picker pop up. Then if you click the color bar on the top, it will rotate between the different color formats.

All right, back to the code. We're going to be deleting all this and reworking our Sass file later on in the course. These styles are just so we can test compiling Sass to CSS in the next section.

Now let's create a JavaScript file.

In the `js` folder, create a file called `script.js`. In the file create a `console.log` and have it say whatever you want, I'm going with the classic `hello world` message with a "wave" emoji and an "earth" emoji.

Ok, that is all the stuff we're going to start with. In the next section we're going to talk about Sass. What it is, and how to compile your Sass to CSS.
