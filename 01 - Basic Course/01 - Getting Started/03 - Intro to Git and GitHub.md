# Intro to Git and GitHub

Alright, so we've covered how to use VS Code, and now I'm going to show you how to use Git and GitHub. These tools are a must-know for any web developer. They'll make your coding life much easier, and they'll look good on your resume as well.

## What is Git?

To start off: what is Git? Git is a type of software called a version control system, which tracks changes to files.

What this means is that it will detect all your code changes, and you can use it to record different versions of your files at different points in time.

This is super helpful for developers for a number of reasons. First off, having Git is kind of like having a giant set of save points. If you make a code change that you realize later on was a huge mistake, you can revert back to an older version of that file.

Git also makes working on a team a lot easier. Each developer can work on a copy of the project on their own computer. This copy is stored in a folder connected to Git, which is called a local repository. The developers can then send their code changes up to the main remote repository which is stored online, and get code changes made by other developers.

## Setting up GitHub and the GitHub Desktop app

The most popular place to store your remote repository is GitHub, which is owned by Microsoft and is free to use.

If you don't have a GitHub account yet, you can go to GitHub.com and sign up for a new account.

Once you're signed up, we're going to use the GitHub Desktop app to run GitHub on our computer. To download it, go to desktop.github.com and download and install the program.

Now I just want to take a minute to explain the differences between Git, GitHub, and GitHub Desktop, cause it can get kind of confusing!

To compare, Git is the actual version control software. It was originally meant to run on the command line, and a lot of developers run Git this way.
GitHub Desktop is a program that runs Git on your computer and allows you to do most of the Git command line commands, just through a more visual program interface.

A quick note: I know a lot of people like using the command line to run Git commands. But for beginners, I've always felt that it's a little easier to use a tool like GitHub Desktop. If you're already familiar with Git and GitHub, you can of course use whichever tool you prefer.

And lastly, GitHub is a website where you can host your Git repositories, collaborate with other users, and discover other open source repositories.
Ok, back to the GitHub Desktop app. Once you've installed the app, go ahead and run it.

The first thing you'll want to do in GitHub Desktop is to sign in to your GitHub account. Go to File > Options, and in the "Accounts" tab, click the "Sign in" button. It will prompt you to sign in using your browser, so go ahead and click "Continue with browser."

Your default browser on your computer will try to log in to your GitHub account. Log in to GitHub if it's prompting you to. And, if you get a pop-up window that says "Choose an application to open the x-github-desktop-auth link," make sure GitHubDesktop is selected.

Once you're signed in, your computer should go back to Github Desktop. And to make sure everything worked, go back to File > Options > Accounts, and you should see your GitHub username and profile picture on the right side.

Now, we want to set our Global Git configuration. In the Options, go to the "Git" tab and you should see your GitHub username listed under Name, and a users.noreply.github.com email under Email. And under "Default branch" select either main or master. Master used to be the default branch on Git, but currently GitHub and other places are using "main" as the default, and it's what I use as well.

Once your settings are set, make sure to click the "Save" button, even if you didn't make any changes on this screen. GitHub Desktop automatically populated these fields when you logged in, but you still need to manually save them.

Now, we're going to walk through the basics of a Git workflow with a test project. Feel free to follow along!

## Basic Git workflow

### Creating a repository

First off, we want to create our repository. Go to File > New repository, and then in the Name field write the name of your test project. GitHub repos need to be named a string without spaces. So usually you would use hyphens between words, for example, I'll be naming this "test-repo."

The Description field will let people who see your repository on GitHub know what it's about.

The Local path is the folder where you want to create your repository. I use Windows, and generally put my repos in the "Documents/GitHub" folder, but you can choose another location if you prefer.

Then, check the box asking if you want to initialize this repository with a README file. This file lets you write a more detailed description about your project that will show up on GitHub, and you can always edit it later. This is optional but in general it's a pretty good idea to have one.

The Git ignore field lets you select types of files that you don't want to add to the repository. I usually leave this at "None" and then ignore files later on while I'm coding-- we'll get to that later in this video.

The License field tells people what they are allowed to do with your code in the repository. Since a lot of open source exists on GitHub, most people select the MIT License which allows people to copy, distribute, and modify your code. If you leave it blank, your project will be licensed with standard copyright. You can read more about open source licensing at ChooseALicense.com (https://choosealicense.com/).

Once all your options are selected, click "Create repository." It may take a few seconds, but GitHub Desktop should create and automatically load the repository.

### GitHub Desktop UI

Let's take a look at the Desktop app. At the top under the menu bar, you'll see another bar with information about your repository. On the left is the current repository that's open. Next to it is what branch you're currently on. We'll talk a bit more later about working with branches, but for now, just know that a branch is one version of the codebase, and you can have multiple branches.

Then at the end is it tells you that you can publish this repository to GitHub, which we will do a little later on.

Under the repository bar is the main panel which has a left sidebar. The sidebar has two tabs, the first is the Changes tab. This is currently blank since we haven't added any files or made any code changes yet. And the history tab which has an "initial commit" with the files generated by GitHub Desktop when we created this repo.

If you have the "Changes" tab selected, at the very bottom of the sidebar is the commits panel. A commit is the "save point" that you can create during development that includes a set of code changes that you want to track.

Let's start by making some code changes to see what happens in Git. In your VS Code, go to File > Open Folder and select the location where you created your GitHub repository.

If you see an alert message from VS Code saying "Git not found," this is asking if you want to download the original version of Git that runs on the command line. You can either dismiss the alert, or if you think you might use Git on the command line at some point, you can click the "Download Git" button to download and install it.

If you do decide to download and install Git for the command line, I'm going to show you the settings I use for Git. For most of the settings I will go with whatever is pre-selected. But most importantly, for the default editor used by Git, I set that to VS Code instead of Vim because I like VS Code. And the other settings is for the name of the initial branch when you're making a new repo, I want to override the default branch name and use "main." And for everything else I just hit the "Next" button and then finish installing.

Now let's create a new file. Click the "New file" icon in the left sidebar and create an index.html file. In the file, type in an exclamation point and tab to use Emmet to create boilerplate HTML markup, and save.

If you go back to GitHub Desktop, you'll see that in the left sidebar under the "Changes" tab will be the index.html file. And there's a green plus icon on the other side of the filename. This means that Git has detected a new file, and wants to add it to your repository and track any future changes.

And on the right panel you'll see the actual code changes that you made in the index.html file. Right now we've added new code, which is why the lines of code are highlighted in green.

You'll also see a checked checkbox to the left of the filename. Checking this box will "stage" the file, which means that you want to include this file change in your next commit.

Now let's create our commit to add the index.html file to the repository. In the bottom commit section, there is a field where you can add what we call a commit message describing what the change is. GitHub Desktop has automatically populated the field with text saying "Create index.html". You can keep this as your commit message, or write your own. There's also a larger description field under it, where you can optionally write a longer description.

At the bottom is a button saying "Commit to main". This means that clicking it will create a commit on your main branch. This matches the "current branch" up at the top of the main panel. Click the button to create the commit.

After we commit, the "Changes" tab is empty. And if we click on the "History" tab in the left sidebar, we'll see that commit that we just made, along with the code changes from that commit.

### Publish repository on GitHub

You may have noticed up at the top on the right a panel that says "Publish this repository to GitHub." Since we created this repository locally, it won't exist on GitHub until we publish it.

Click the button to publish it. A window will pop up, with the name of the repository and the description. And there's a checkbox for if you want to keep the repo private. I'm just going to keep this private since it's not for any real code. Then click "Publish repository" and it will get published to your GitHub account.

Let's go to the GitHub website and see how our repository looks. If you go to GitHub.com, login if it prompts you to. Then click on your avatar in the top right and navigate to "Your repositories." When you see the "test-repo" repository click on that and it will load.

Let me point out a few things that are good to get familiar with. In the top left is your username, followed by a slash, then "test-repo." This tells you what repository you're currently in, and it will also be listed in the URL.

In the main part of the webpage GitHub will load the most recent commit message which should be "Create index.html." And it has a 7-digit string that is the first part of the hash for that specific commit. Every time you create a commit, Git will automatically create a hash, which is a long string of letters and numbers, that serves as the unique ID for that commit. If you click on the 7 digit code, it will load that commit, and you can see the really long string in the URL and on the right side.

Going back to the test-repo repository, next to the hash is how long ago the commit was made, and then at the end is the total number of commits.

Under the top bar GitHub will also display the files currently in the repository, which right now is only the index.html file. As we add more files you'll see then all in this area. And if you click on the filename, GitHub will load the actual code in that file. You can even edit and delete the file right in GitHub. I wouldn't actually recommend doing this since it's better to manage your code in VS Code. But it's nice that the access is there.

We'll look at a few more things in GitHub in a little bit, but for now let's go back to VS Code.

### Ignoring files

So far we've added files to our repository. But there might be files and folders that you create that you actually don't want Git to track. Let's say you're keeping some notes or something in a text file called random.txt that's in your project. You want those notes there but you don't want them to be public in your repository.

Then in GitHub Desktop, what you can do is uncheck that box. That will make sure that the file won't be included in any commits.

But, it can be kind of annoying to keep seeing that filename all the time. So you can actually have Git ignore files and folders. If you right-click the file and select "Ignore file (add to .gitignore)" you'll see that random.txt has disappeared. And there's a new file that Git has detected and wants to add to the repository: .gitignore. And in the right panel we can see that it contains "random.txt".

And if we look in VS Code and open the .gitignore file, we'll see the "random.txt" line. In gitignore files, you can ignore individual files and folders by adding each one on a separate line. Let's test this out.

In the gitignore file, add another line that says "random123.txt" and save it. Then in VS Code create a file with that exact file name.
Going back to GitHub Desktop, it has not added the random123.txt file since we ignored it.

As you might imagine, it can get a bit tedious to have to manually write each file name in the gitignore file. One thing that can help with that is that you can use the wildcard when writing the filename. So let's go back to the gitignore file and delete everything that's there. Then add "\*.txt" to ignore all text files.

Now in GitHub Desktop we don't have either of the text files showing up, and we can see the wildcard in the gitignore file. Just be very careful when using the wildcard to ignore file types, in case you might want to include a file of that type in the future sometime.

Let's make a new commit with a commit message that says "Ignore text files". Then double-check to make sure the .gitignore file is checked, and click "Commit to main."

In the top on the right we can see the panel saying "Push origin." What "origin" is, is it refers to the remote repository that we published on GitHub. So when we push commits in our local repo to origin, they will get pushed to the origin repository which is on GitHub.

Let's click "Push origin" and it usually takes a few seconds.

Now let's go back to GitHub and the main "test-repo" repository page. We can see that it looks a bit different now!

The most recent commit is the "Ignore text files" one, and it has a new hash. And the total number of commits has gone up. And we can see the .gitignore file is now on GitHub too.

### Modifying files

We've covered adding new files to the Git repository. Another thing Git will keep track of is changes made to existing files. Let's see how this looks.

In VS Code, open the index.html file and let's add some content to the body:

```
<h1>Hello here is our website</h1>
<p>Here is some cool new content!</p>
```

I'm adding an h1 tag with some text, "Hello here is our website" and a paragraph tag saying "Here is some cool new content!"

Save it, and let's see what this looks like in GitHub Desktop.

Now, in the left sidebar the index.html file is showing up, and instead of that green plus icon that we saw when adding new files, there's a yellow dot icon. This signifies that Git has detected modifications in that file.

Then in the right panel we can see the new text that we just added. And it's highlighted in green, meaning that it's code that has been added.

So let's make a commit. I'll make the commit message something like "Added content to index.html." Now we'll commit it to the main branch, and push to origin.

And if we look in GitHub, we'll see that commit we just made, and clicking on it will show us again, the green highlighted code we added to index.html.

One thing to note about Git is that it tracks changes on each line of code. We added X lines of code to index.html, and we can see each line listed.

If we click on the "History" tab we can see the 4 commits that we have in this repo, with the most recent on top.

And if we go back to GitHub.com to the repository page, we can see the same history up there if we click on the "4 commits" link on the right side, again with the newest commits on top, and the oldest ones on the bottom.

### Deleting and reverting

Git will also track if you delete files. Let's test this out. In VS Code, go ahead and delete the index.html file!

Now, going back to GitHub Desktop, we see the index.html file is showing up under "Changes." It has a red minus symbol icon to indicate that this file has been deleted. And in the right panel all the code in the file is highlighted in red, meaning it's been removed.

Let's make a commit, with the commit message saying that we deleted index.html. Commit it, and then push to origin. And if we check out GitHub, it'll show that most recent commit, and clicking on the commit, it tells us that the file was indeed deleted.

But what if we realize that we really need that index.html file?! Not to worry, this is one of the ways that Git can really save your life.

In GitHub Desktop, in the "History" tab, right-click the commit where we deleted index.html. And select "Revert changes in commit." Now we see that Git has automatically created a new commit saying that it has reverted the previous commit.

And looking at more details in the right panel, it tells us the hash of the commit that was reverted, and it's added back the index.html file and all 16 lines of code. Whew!

Now if we click the "Push origin" button, everything will be back to normal. In VS Code, the index.html file will be back. And in GitHub if we refresh, we can see the commit reverting it, and the index.html file is also back where it belongs.

### Branching and merging

Now there is one more area in Git that I'd like to cover. And that is branching. In Git a branch is one version of the codebase, and a repo can have multiple branches going at the same time.

So far, all the work that we've done in Git, and all the commits that we've made have been on the one main branch. If you're just working by yourself you can probably get away with doing everything on main.

But if you're on a team with multiple developers all working on the same codebase, it would be quite chaotic to have everyone working on the same branch, especially if more than one person makes changes to the same file.
So most teams will separate work into different branches.

You might have one developer fixing a bug on the homepage working in a branch called homepage-bug. Then there might be another developer building a new feature on the careers page working in another branch called careers.

Each of those branches will be created off the main branch, so they will have the most up to date code from main. Then they'll each work on their own branches locally.

When the developers are done with their work, they will merge their branch back into the main branch. This type of workflow is considered best practice when you're working on a team.

So even though in this course we can do all our work on the main branch, I wanted to show you a little bit of what working with different branches looks like.

In GitHub Desktop, in the top menu, navigate to Branch > New branch. Let's give it a name of "feature-1". And you'll notice under the Name field is a note saying that the new branch will be based on the current branch, which is main. Then click "Create branch".

Now up at the top GitHub Desktop has the feature-1 branch listed as our current branch.

Let's make some demo code changes in this branch. In VS Code, create a new file called "feature1.html" to keep things simple. And in the file hit exclamation point and enter to use the Emmet shortcut to add boilerplate HTML. Then save the file.

And back in GitHub Desktop, we want to add feature1.html to our repo. In the commit panel at the bottom we'll just leave that default commit message of "Create feature1.html" and hit the button to commit this change to the feature-1 branch.

Now, in GitHub Desktop, let's switch our current branch back to the main branch. If we go back to VS Code, the feature1.html file won't exist. This is because it was created in the feature-1 branch, and so it doesn't exist yet on the main branch. Git will keep the codebase files updated depending on what you are loading.

So let's pretend that we've now finished all the development work on the feature-1 branch, and we want to deploy it to our website. We need to add our changes from the feature-1 branch to the main branch in what's called a merge in Git.

To merge feature-1 into main, in GitHub Desktop, first make sure that you are currently in the main branch. Then in the top menu, navigate to Branch > Merge into current branch. And select the feature-1 branch. So what this is saying is that we will merge all the commits from the feature-1 branch into the main branch.

And click the button saying "Create a merge commit". This will merge in the code from feature-1 into main, and the change will be automatically put into a new commit on the main branch.

Now if we load the History tab, we can see the "Create feature1.html" commit message listed as the most recent commit on the main branch. Now click the "Push origin" button up at the top to update GitHub.

In GitHub, if we load the repository page, we can now see that the commit creating feature1.html is the most recent commit, and the file exists on the main branch.

One last thing to note, if you're working on a team that uses GitHub, new branches are typically merged into the main branch through a feature on GitHub called pull requests. This allows other people on the team to check the code changes and approve them before merging them into main. This helps to prevent any mistakes from being added.

So what you would do is make your code changes and commit onto the feature-1 branch. Then instead of merging feature-1 into main in GitHub Desktop like we did last time, you would publish the feature-1 branch up to GitHub.

Then on GitHub you would create the pull request for other people on your team to review and either approve or suggest code changes. If the changes are approved, your team member can then merge your changes into main.

Again, this is mainly if you're on a team. We're not going to be working with multiple branches or pull requests in this course. But I wanted to make sure that you know that they exist because they're common practice when you're working on a team.

Next up, we'll be setting up our project files for the actual course! I'll be showing you how to set it up from a blank folder and create a new Git repo for it, so you won't be needing this test-repo one anymore.
