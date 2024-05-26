## Installing Vite

In this section, I wanted to show you all a more advanced and more "real world" way of compiling your Sass files to CSS.

So far, we've been using the VS Code Live Sass extension to compile, and then we include the compiled CSS files in our GitHub repo and deploy them directly to the server.

However, if you're working on a team, you usually will not be committing compiled files. These files are super long, and if you have multiple developers all working on different parts of the website, you will inevitably run into Git conflicts in the compiled files, because each dev is going to have a slightly different version of the final CSS file.

So to avoid the huge headache of Git conflicts, what teams usually will do is ignore the compiled files in Git so that they will not be included in the repository and will then not get deployed to the server. Then each developer will compile their files only on their own computer.

But you still need to get the compiled files onto the production server, somehow, right? In order to do that, you can get each server to compile the files just for itself, every time a new deploy happens.

And the best way to do that is to run a Node script. Node JS is a JavaScript run-time environment, which lets you run JavaScript on the server via your command line. This is something that we can do on our own computers, and also on the production server.

You do need to install it on your computer, so if you don't have it yet, you can go to NodeJS.org and click the Download button.

Then run the file that you downloaded and it will install Node and a tool called "npm" or "Node Package Manage" on your computer.

After installing, you might also need to close and restart VS Code.

Once you're back in VS Code, first thing we want to do is turn off the VS Code extensions if they're running. So if you're watching the Sass files, click to stop watching. And if you have the live server running, you can click that to stop it too.

We're going to need to use our Terminal so that we can run commands on our command line. To open the Terminal, you can go to View > Terminal, or use the keyboard shortcut Ctrl or Command and then backtick which is the same button the tilde is on.

[ bring terminal panel up so it doesn't get covered by subtitles ]

When you open the Terminal, it will show you the command line of your computer, and you'll be in the folder where your project root is located. The command line is sort of a text version of your computer. You can navigate to any folder on your computer and run different text commands there.

For our purposes, we're going to want to stay in our project root folder.

First, let's check and make sure that you have Node installed. You can do this by typing "node -v" and hitting Enter. If you do have Node, it should return "node" and then a version number.

And you can do the same thing to check if you have npm, you can type "npm -v" and if it's installed it will return the version number.

Once you have Node and npm on your computer, next we are going to install a some software called Vite into our project.

[ Show ViteJS.dev website ]

Vite is what's called a build tool. When you run it, it will run a local server and is helpful particularly if you are using a JavaScript framework like Vue or React. We're just going to be using Vite to compile our Sass to CSS and run the local server.

Now in order to add Vite to our project, we need to install it using npm. Npm is a huge library of pieces of software called "packages" that individuals and companies write and then make available via npm so that others can use it.

So if there's some code that someone wrote that you want to use in your own projects, instead of having to go to the person's website to download the files, you can install it on your computer via the command line.

Alright, let's install Vite. On the Vite website, you can find instructions to install it by clicking the "Get Started" button. Then if you scroll down a bit, under the "Scaffolding your first Vite project", we're going to follow instructions for npm.

We want to run "npm create vite@latest" but we're going to add a little bit more to it. Let me show you what I mean in VS Code.

In the command line, first make sure that you're in your project root-- for me that's the "responsive-design-beginners" folder. Normally, you'll be installing Vite before starting your project, into an empty folder.

But because we already have our project, we want to tell npm to install Vite into our current project folder. However, to avoid potentially overwriting our existing files, we need to rename our index.html file because Vite will generate one of its own.

So in our Solution Explorer, I'm going to right-click the index.html file and rename it to "index_original.html".

Next, in the command line I'm going to type "npm create vite@latest dot forward slash". This will tell npm that we want to create a new project of Vite in the latest version, in our current directory.

Then when it says "current directory is not empty", use the arrow keys to select "Ignore files and continue".

Then select "Vanilla", and then "JavaScript".

Then it installs the Vite starter files, and we have our new index.html file. It also says we need to run "npm install" and then "npm run dev" to run the local development server.

When you run "npm install", what happens is, npm will look in the "package.json" file to see what packages it needs to install in your project. So if we look at the package.json file, it has some info, and then there are 2 sections.

One is "scripts", which are commands you can run to run the site. So in our case there's a dev script, build script, and preview script. And you can run them by running "npm run" and then the name of the script: dev, build, or preview.

We'll come back to those scripts a little later.

Under the scripts is another section called "devDependencies". This is a list of packages that will be installed to your project folder when you run "npm install". So here we will be installing the "vite" package.

Now let's click back on the command line and run "npm install". And in our sidebar, there's a new folder now, called "node_modules". This is where all the files from the packages are installed, each in its own subfolder.

We can see that one "vite" package down at the bottom. In addition to that, there are a ton of other packages that get installed because the "vite" package is also going to install other npm packages that it needs. And those packages most often will also be using yet even more packages. That's the reason that your node_modules folder will have a ton of stuff in it.

That's a quick look at node_modules. Now let's go back to our command line and run the other command that the instructions mentioned, which is "npm run dev". And this will run the "vite" script.

Now it's telling us that Vite is running, and we can load the local website at the URL [xxx]. If I hold down Ctrl or Command on Macs, then our browser will load the website.

And here is the Vite starter website.

Let's go back to the index.html file and see how things are working. There's not much here-- we have a div with the ID of "app" and then it's loading the main.js file as a JavaScript module. This is similar to how we've been loading our regular, non-module script.js file, except it has the type set to module.

Very briefly, JavaScript modules let you load JavaScript functionality from other files into your current one, without having to literally have the other code in your own script file. This is really useful because then you can reuse the functionality from various files without needing to copy all the code manually.

This is very similar to what we've been doing in our Sass files, where we have our util Sass features that we can then load in other Sass partials by using the "@use" at-rule.

I do want to also say that I'm not at all a JavaScript expert, and am just using Vite to compile Sass and run the local server. But I know that Vite has a lot of functionality that is meant to make development faster and easier if you're doing a lot of JavaScript-heavy coding.

Ok, so in our Vite project, the index.html file is loading the main.js file, so let's take a look at that. First, up at the top, it's importing a bunch of stuff. One is the style.css file-- and we're going to use this same method in a little bit to import our Sass styles.

Then it's importing 2 SVG images, and below that a JavaScript file, counter.js. It's importing the images here because under the imports, it's using JavaScript to actually load the HTML markup in the "app" ID div, and loading the images in the markup as well.

Again, this is more functionality than what we're using Vite for, but I just wanted to show you a bit of what's going on.

Let's start integrating some of this functionality in our own code. I'm going to go to the Vite index.html file and copy the script tag loading the main.js file.

And let's paste it in our index_original.html file, up in the head tag, before the closing tag.

When you're loading a JavaScript module, it is automatically deferred, so we don't need to add the "defer" attribute like we have for the others.

And since we're going to be using the main.js file to load our styles, we can delete the link tag loading our compiled style.css file.

And we're also going to have to load our script.js and the body scroll lock plugin through our main.js file, so I'm also going to delete those two script tags.

And that's all the changes we need to add to our index.html file.

So now we don't need the Vite index.html file anymore, I'm going to delete it, and rename the index_original.html file back to index.html.
