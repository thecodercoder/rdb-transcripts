## Loading SCSS and JS files

Next, let's get the main.js file working for what we need. I'm going to delete all the code here except for that very first line loading the style.css file. And we want to change the import so that it's loading our main style.scss file.

In the import statement, the dot slash means it's loading the current directory-- the syntax is a bit different from the syntax we've used in our Sass statements, just be aware of that. Then, after the dot slash, we want to load the "app/scss" folder, and in that, make it load the style.scss file.

We also want to delete our "dist" folder to make sure that the Vite workflow is working and generating the CSS file, because otherwise it's just going to load the old style.css file.

And in our terminal and on the website we have an error saying that we need to install the "sass" package via npm. This will let Vite compile our Sass to CSS files. So in our terminal, we can stop the local server by pressing Ctrl or Cmd C, and then Y for yes to stop it.

Then when we're back on the command line, we can type in what the error message said: "npm install -D sass". This will install the sass package into the node_modules folder, and add it as a dependency in our package.json file.

Let's run that.

Now in our package.json file we can see the sass package is listed there. And if we open our node_modules folder, we can see there's a subfolder called "sass".

Okay, let's try running the local server again with "npm run dev".

And now it looks like our styles are getting loaded. Let's test and make a change in our styles to make sure that the compiling is working and it updates the website.

I'm going to load the globals folder and the colors.scss file. And let's change the hero-bg color to something different. I'll just click the color swatch and choose a random color.

Now let's save, and on our website, now the hero is a different color. If we inspect the styles, where the dev tools would normally tell you the original Sass file and line number where it came from, now it just says "inline".

This is one of the ways that Vite works-- instead of generating a final CSS file and us loading it in our HTML file with the link tag, Vite will load all the styles as an internal style sheet in the HTML. We can actually see this if we go up in the markup view in the head tag, there's a "style" tag, and if we expand it, we have all our styles right here.

However, going back to the styles being listed as inline versus the Sass file, I like knowing where in the Sass files the style rule came from, because it makes troubleshooting a lot easier. To do this, we'll need to tell Vite to generate a sourcemaps file when it's compiling our Sass files. A sourcemap file will literally map each Sass style rule back to the Sass partial file that it originated from.

To do this, we will need a bit of configuring. In the Vite website, in the left sidebar, I'm going to load the "Config Reference". So here it's telling us that we need to create a config file, "vite.config.js" in the project root.

So I'm going to copy the basic config file contents, and then in VS Code I'm going to right-click in the Solution Explorer and create a new file, and call it "vite.config.js". Then in the file I will paste in the starter config code.

Now, we need to find the right config settings to tell Vite to create a sourcemaps file when compiling our Sass. I'm going to click the Search, and type in "sourcemap". And there are other sourcemaps for other things, but at the bottom, the "css.devSourcemap" is probably what we need.

If I click that, then it tells us that we can set an option called "css.devSourcemap" and it is a boolean, meaning true/false, and the default value is false. This is why by default we didn't have a sourcemap.

If we scroll up a bit, we can see some example code for other CSS options. So in the config file, in the default object, we have a "css" object, and then in that we can add the options.

So we can use a similar format for our "css dot devSourcemap" option. In our config file, inside the default curly brackets, I'm going to copy what we have in the example and add a "css" object, colon, and curly brackets.

Then, inside the css object, instead of "preprocessorOptions", I'm going to add "devSourcemap". And the devSourcemap is just a boolean property, so we can add a colon and then set it to "true".

Okay, let's save, and then see if this is working on our website. And it looks like we still have the inline styles showing with no sourcemap, so I think we need to stop and restart the Vite local server if we make any config changes.

Back in VS Code, in the terminal, I'm going to stop the server with Ctrl or Cmd C, and then hit "Y" to stop the job. Then let's run "npm run dev" again. And a quick tip, in the command line, if you hit the up arrow, it will navigate back through all the previous commands that you've run, so if I hit it once, it'll load my last command, which was "npm run dev", and then I can hit enter to run it again.

So now, going back to the website, we can see in our styles we now have sourcemaps working so we can see which Sass partials the styles came from. So that looks good!

So let's revert the hero color-- in colors.scss I'm going to hit Ctrl Z to undo and go back to the original color. And when we save, now it's back to normal.

Okay, our styles are working, now we need to get our JavaScript to load also. Because right now if we go to the website, and load the mobile version, clicking on the hamburger menu doesn't do anything.

From what I understand of Vite, it needs to have that main.js file in the project root. So what I'm going to do is open our script.js file, select everything, copy it, and then in the main.js file, paste everything in after the styles.

Now when we save, when we click the hamburger menu, it does open and close. However, you can probably see this, but we're getting error messages saying it can't find "bodyScrollLock"-- because we removed the script tag from our index.html file.

What we need to do is load the body scroll lock plugin via the main.js file also. When we initially loaded the body scroll lock plugin, we copied the actual JS file and loaded it in our HTML.

However, most plugins are also packages on npm, and we can install the plugin that way. Let's go to the body scroll lock plugin on GitHub, I'll do a search for "body scroll lock" and then go to the GitHub page.

If we scroll down, in the "Install" section it has instructions on how to install with npm. So we want to do that-- I'm going to copy that command, and then back in VS Code, I'm going to stop the server again. And on the command line, paste in the command, and I'll add "dash D" at the end to add it as a dev dependency in our package.json file.

Let's run that, and now in the package.json file we can see "body scroll lock" and if we go to the node_modules folder, we can see the subfolder there too.

Now that we've installed the plugin in our project, we can import it in our main.js file. To figure out how to do that, we can go back to the website and we want to use the React/ES6 version, where it says "import" and then has the name of the functions.

So I'm going to copy just that line, and paste it in, and we also need to add at the end, a "from" and then in quotes, the name of the package, "body-scroll-lock".

Now we have the package imported into our script. We need to tweak how we reference the different functions. I'm going to search the page with Ctrl or Cmd F, and search for "bodyscroll". And there are two places in our code where we're using it.

Since we imported the actual function names from the package, we don't need to say "bodyScrollLock", we can just load the functions. So I'm going to delete the "bodyScrollLock" before both of the functions.

I think that should work. Now let's run our server again and see if there are any errors. So we'll run "npm run dev" and no errors in Vite, which is good.

And on the website it looks good too, if we click the Console tab, I don't see any errors. Let's click on the hamburger menu, and it opens, and I'm trying to scroll and it's locked, which is great.

Then let's close the menu and try to scroll, and we can scroll again. Great!

So I think we're pretty good, we do need to test out deploying to Netlify to make sure that works too. So I'd like to clean up and delete any other Vite starter files in our project that we don't need.

The "public" folder, then the counter.js file, javascript.svg, and then the style.css file.
