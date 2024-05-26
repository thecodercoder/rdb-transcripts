# VS Code Extensions

Alright, so this is the Beginner route for how to compile your Sass files to CSS using the Live Sass Compiler and Live Server VS Code extensions. I'll walk you through how to install them, configure them, and get them up and running.

First make sure you have VS Code open to your course project folder.

If you don't have the extensions installed yet, in the far left Activity Bar, click on the Extensions menu and search for "live sass compiler."

Now you might see more than one "Live Sass Compiler" extension, and this is because the original extension was authored by Ritwick Dey, which has recently been officially deprecated. And it tells you to use the other Live Sass Compiler extension, authored by Glenn Marks.

So when you select the extension to install, make sure you install Glenn's version, because it uses the newer Sass syntax, unlike the older extension.

So to install it, click the "Install" button, and once it's installed, there is some configuration that we'll have to do.

Open the command palette by pressing Ctrl-Shift-P (or Command-Shift-P for Macs), typing in "open settings" and selecting "Preferences: Open User Settings (JSON)."

Now in the settings.json file, we're going to add some lines of code to customize the Live Sass extension that we just installed. There's already a bunch of settings stored here. You can add yours anywhere you want in the file, as long as it's inside the curly brackets.

You can either go all the way at the end before the closing curly brackets. I sort of try to put my settings in alphabetical order, so I'm going to add it before the "markdown" settings I have and after the "liveServer".

Wherever you decide to add, hit enter to create a new line, and make sure that the line before it ends in a comma to keep it separate. If you're adding these settings at the end of your file you might need to add comma to what was formerly the last line. Otherwise it will cause an error.

On the new line, type in a double quotation mark and start typing "livesass," one word without a space. You should see the autocomplete pop up several "liveSassCompile" options.

Select the "liveSassCompile.settings.format" item, then click it or press Enter to select, and VS Code will generate a bunch of options. For the "savePath" option, set it to quotation mark, forward slash, "dist," and a closing quotation mark.

These quotation marks are important in order for string values to be considered valid in the JSON format. You might see a wavy underline when you add the slash "dist" value, but I think this is just a bug in VS Code sometimes and it's not going to cause an error.

This settings will ensure that the Live Sass Compiler will compile your Sass files and save the final CSS file in the "dist" folder in your project root. If you leave it at the default value of null, the CSS file will be saved in the same location as your main Sass file. I personally like having the "dist" folder for all my compiled files, so I use this setting.

If you want to minify the final CSS file, meaning to compress it to save space, you can change the "format" option. Delete the "expanded" value including the quotation marks. Then, when you start typing a new quotation mark, it will pop up autocomplete with what possible options you set for it. Setting format to "compressed" will minify the CSS file. This is optional, so you can either leave it at expanded or compress it if you want.

Once you're done with changing your settings, save the settings.json file, and you should be all set with the Live Sass Compiler!

You'll also want to install the Live Server extension, by Ritwick Dey. This extension hasn't been updated in a few years, but it still works fine.

What this does is that with one click it will run a local server to open your project in a browser window. And it has a live reload feature that will reload the site anytime you make a code change.

## Compiling Sass and running a local server

Once you have both extensions installed, you may need to reload your VS Code window in order for the extensions to get loaded correctly. You can do this by manually closing and reopening VS Code, and re-opening the project folder.

Or alternatively, in VS Code you can open the Command Palette with Ctrl-Shift-P, type in "reload" and select the "Developer: Reload Window" option, which will reload and reopen VS Code for you. I like this method because it will automatically re-open the folder you had loaded.

To compile your Sass files, look in the status bar at the very bottom of your window, and you should see a "Watch Sass" button. Click that button, and an integrated terminal should pop up saying "Live Sass Compile." The terminal output should say something like "Generated," with the CSS file and CSS sourcemap file getting generated in the dist folder. And then a "Watching" message.

You should be able to see in the dist folder, the style.css file and then the CSS map file. The CSS map file keeps track of which SCSS files all the final CSS style rules come from. This is something that you can see in the browser which helps with debugging, and we'll take a look at that in a little bit.

The extension will watch your Sass files, so anytime you make a code change it will recompile your Sass files. I'm going to press Ctrl-S to save the file, even though I haven't made any changes, and you can see in the output panel it detected the save and regenerated the CSS files.

Now, let's load a local website using the Live Server extension. In the bottom status bar, click the "Go Live" button. It will show a "Starting..." message and then "Port: 5500". Your browser will probably automatically pop up a window loading the local website.

If you click the Go Live button while you have the `index.html` file open and active, it will say `http://127.0.0.1:5500/index.html`. If you have another file open it will load `http://127.0.0.1:5500` without the actual file name.

Since we only have the one index.html file, both have the same end result. But if you are working with multiple HTML files, then you can have the specific file open that you want to view.

If you want to stop the local server from running, you can click the "stop symbol Port: 5500" button again. And if you want to stop watching your Sass files, click the "Watching…" button to stop.

Now let's turn both back on so we can look at our simple website. So in the Status Bar, I'll click "Watch Sass" and "Go Live" to restart both extensions.

In our local browser, let's open the code inspector. You can do this by right-clicking anywhere on the page and selecting "Inspect". I'm using Firefox, but whatever browser you're using should have a similar option and say either "Inspect" or "Inspect element." You can also use the shortcut Ctrl-Shift-I or F12.

Now, we can see the HTML markup that is in this page. Click on the `<body>` tag and we can see some style rules in the right panel. These should match the styles that we have in our `style.scss` file.

On the right side it says "style.scss:1". This tells us that this style rule for the body tag comes from the `style.scss` file, line 1. And if we go back to VS Code in the `style.scss` file, we can see that line 1 is where the "body" tag selector is.

This extra information is displayed because we generated a CSS sourcemap file. Otherwise it would only show the `style.css` file in the browser, and we wouldn't know exactly what line number the rule comes from.

This feature comes in handy when you have a bunch of styles in multiple different files. It just makes it a lot faster to locate where your styles came from when you're debugging.
