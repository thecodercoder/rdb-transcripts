# Setting up VS Code

Alright! Now that we've gone over what the course will cover, let's get started by looking at the different tools that we'll be using throughout this course.

When you're building a website, the very first things you need are a computer and a code editor. I've always used a PC, but you should be able to follow along even if you're on a Mac or Linux computer.
Now, for the code editor, I use VS Code. It's fast and free, and you can use custom themes and extensions to make your coding experience more efficient and fun.

I'll be showing you how to install VS Code, some of the basic commands, and the themes and extensions that I use.

## Download and install

To get VS Code, go to code.visualstudio.com, download the version for your operating system (Windows, Linux or Mac), then install the program on your computer.

And just to note, make sure you're using VS Code, not Visual Studio. Visual Studio is a much bigger program-- it's the IDE or integrated development environment used for C# and .NET programming. We don't need the full IDE for what we're doing in web development, and VS Code is a much lighter weight program for our needs.

Once it's installed, go ahead and run it.

# The main VS Code user interface

The VS Code user interface is made up of the top menu bar, the left activity bar which opens the left sidebar, the bottom status bar, the bottom panel, and the editor taking up the rest of the space.

In VS Code, you can open folders or individual files. When I'm coding, I will usually open the project folder that I'm working in. Let's say I want to make a new project. In Windows File Explorer I'm going to create a new folder on my Desktop called "sample-project."

Then in VS Code I'll open that folder. Select the Explorer tool. This is the first icon at the top of the Activity Bar, on the far left. Then I'll select "Open Folder" and choose the "sample-project" folder I just created.
You can also reach this command from the top menu bar, by navigating to File > Open Folder.

Once the project is open, usually you would see the project's files and folders in the left sidebar. Since the "sample-project" folder is empty, let's create some dummy files and folders.

If you hover over the sidebar area under the folder name, you'll see some icons appear. The icons are, going from left to right, Create New File, Create a New Folder, Refresh, and Collapse the Folders. Let's create a new file and call it "index.html." And we'll use the Emmet shortcut exclamation point to add some boilerplate HTML.

Then let's create a new folder in the project root called "app" and in that folder I'll create a "style.css" file and a "script.js" file.

Folders will have an arrow icon, and if you click the icon or folder name, it toggle the display to to hide or show the folder contents. Files will have various icons, depending on what file type they are, for example, HTML, CSS, and JavaScript. Your icons might look different from the ones I have. This is because I have custom icons installed, which I'll show you how to do later in this section.

If you double-click a file, it will open in the main panel of VS Code. And you may notice that each open file will also be listed in the left sidebar, in the "Open Editors" section.

And if you open multiple files, they will each have their own tab up at the top under the menu bar.

If you single-click a file that's not open, it'll let you preview the file in the editor and display the file name in italics in the tab. If you preview another file it will automatically close the first file.

But if you start writing code changes in a previewed file VS Code will keep that file as an opened file.

## Activity Bar: Explorer, Search, Git, Debug, Extensions

In the Activity Bar on the far left, under the Explorer tool is the Search tool. Typing a search term will give you search results in the project folder.

And you can do a Find and Replace from here as well.

Below the Search tool is the Source Control tool. VS Code has a GitHub integration that allows you to manage your GitHub repository changes right in VS Code, if you so desire.

Then, under the Source Control tool is the Debugging Tool. We're not going to be using this in our course, so you don't need to worry about it.

And the last icon is for Extensions which we will be using. Extensions are programs for VS Code that are written by other developers. They can be custom themes or plugins that do cool things.

Customizing your VS Code with themes is in my opinion, one of the most fun parts of using it. If you want to find a theme to use, in the Extensions menu click the filter icon, then select "Category" and "Themes." You can then browse and look for themes that you like.

Generally there are two types of themes: color themes, which control the colors of VS Code; and file icon themes, which are the tiny icons next to the file names in the Explorer sidebar.

If you see a theme you want to check out, select it, then click the "Install" button in the right panel. It will install and immediately load the new theme.

To change the current theme, go to File > Preferences > Color Theme, and use the arrow keys to navigate through all your installed themes. Then select the one you want.

I'm currently using a theme that I created, Coder Coder Dark. If you want to use it too, type in "Coder Coder" in the Extensions search bar and it should pop up near the top.

For icon themes, in the Extensions menu, filter for themes and try adding the word "icon" at the end of the search term to filter for icons. Again, once you see one you like click to install and load it.

If you want to try out new icon themes, one thing you can do is to have a project with files open in the Explorer sidebar, so that you can see the icons. Then go to File > Preferences > File Icon Theme, and you can navigate through your icons to see which one you like the best.

I'm currently using the Material Icon Theme for my file icons.
Now, let's move on to some other extensions that I like using.

Prettier is another really helpful extension that will automatically format all your code with the proper indentation and spacing. In the Extensions menu, search for "Prettier" and install it.

There are a few settings that I use for Prettier, so open up the settings again by going to File > Preferences > Settings. Then on the left side expand "Extensions" and click on "Prettier".

There are a couple settings that I use. So scroll down a while until you find the "Prettier: Single Quote" and check that box. This will convert any double quote in your code to single quotes, which I personally like better.

Under that, set "Prettier: Tab Width" to 2 spaces for each tab. Obviously you can change that to your own preference if you want, but this is what I normally use.

Lastly, I like to automatically run Prettier anytime I save a file. So in the settings, expand "Text Editor" and scroll down until you see the property "Default Formatter." Make sure this is set to "Prettier - Code formatter" and you should be all set!

Just as a quick demo, in the index.html file if I select all and then hit Shift-Tab a few times until everything is on the same level of indent, then save, you can see that Prettier will indent everything correctly.
And in the script.js file, if I write "console.log("test");" using double quotes, when I save it will automatically convert to single quotes.

The last extension that we'll be using in this course is simply called SVG, and it's authored by jock. Installing this will allow you to preview SVG files right in VS Code.

## Command Palette

One more tool in VS Code that I want to show you is the Command Palette. It's is a pretty handy tool that lets you search and run different commands.

To open the Command Palette, type in Ctrl-Shift-P (or Command-Shift-P on Macs). And you'll see the palette open, with a search box and a right angle bracket symbol.

There will also be a menu list of possible commands that you can run. Yours might look different from mine because the menu will automatically show you the recently run commands.

The main reason I use the Command Palette is to open the settings JSON file. If I type in "settings" then select "Preferences: Open User Settings (JSON)." This is where all your settings are stored when you make changes to your Settings.

So you can see the current color theme and icon theme that I'm using, and scrolling all the way down, we can see the Prettier single quote setting that we just put in.

So that's it for the VS Code setup and extensions configuration! In the next video we'll be looking at source control tools that are really important to know in the job: Git and Github.
