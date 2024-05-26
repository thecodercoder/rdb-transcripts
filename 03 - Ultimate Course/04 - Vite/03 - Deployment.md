## Testing Deployment

Before we added Vite to our website, we had included the compiled CSS files in our GitHub repository. But now, that we don't have it, we need to compile our Sass files on the production server.

And we can do that by adding a build command to our Netlify deployment. This will run whatever command we want on the command line of the production server.

What command do we want to run on production? In the package.json file, in the scripts, we have the dev script which we ran on our local machine to run the website locally. But that's not going to work on the production server. What we want to run there is the build script.

I'm going to run it locally just to show you what will happen on the production server. This isn't something that you would normally do.

In our terminal, I'm going to stop our dev script from running, and then run "npm run build".

What happened is that the build script created a "dist" folder, and in it we have an index.html file and an "assets" folder that contains the images, the compiled JavaScript file, and the compiled CSS file.

We need to run "npm run build" on Netlify, so we need to go there to adjust the deployment configuration.

We want to go to Netlify.com, and then login, and we are logging in with GitHub.

Then in our dashboard, if we click the "Build and deploy" we should be able to configure the Build settings. In our build settings, we want to add the command to the "Build command". So I'm going to add "npm run build".

And we also need to add the "Publish directory" and set it as "dist" because this is the folder that Vite creates when you run the build command. So you want to tell Netlify that this is the location that the final website is in that has everything compiled.

And we can save that.

Now, let's commit our changes in GitHub Desktop. In the Changes tab, let's look at the changes happening. Vite added a gitignore file which we do want-- in this file you can add files, folders, even just file types and Git will ignore those files in your project so that they won't get added to the repository.

One big one is you always want to ignore the node_modules folder, because it's really huge and takes up a lot of space. And you don't need it because you can run "npm install" on the production server to generate all the node_modules files and folders that the project needs. So you should always ignore that. The other changes look pretty good.

So let's add a commit message, I'll say "Vite setup". And click commit to main, and push to origin.

And on our Dashboard, we want to click on our site, which should be this one. And on the site page, under "Production deploys", the latest deploy has failed. So let's do some troubleshooting and see what's going on.

I'm going to click on the failed deploy, and in the Deploy log, it failed in the "Building" stage, so let's click to expand that, and scroll down until we see the error. So here it says "Error: Cannot find module @rollup/rollup-linux-x64-gnu", and it suggests to re-run "npm i" which is the same thing as "npm install".

Also, I don't know if this message popped up for you, but at the top Netlify has an AI-powered troubleshooter, so let's just see what it says. Okay, so nothing too exciting here, it's saying the same thing, it can't find the module @rollup linux.

By "module" they are talking about installed Node modules which are installed in the node_modules folder. And the website was working correctly locally, so I'm going to see if we have this module on our local machine.

In VS Code, let's look in our Solution Explorer in the node_modules folder, and here look for "rollup". Up at the top some of the subfolders have a name that starts with the "at" symbol. This means it's the name of the organization that has authored multiple packages under this organization name.

If we expand the "@rollup" folder, it had a subfolder called "rollup-win32-x64'msvc". And the missing module had the name "linux" in it. So my guess is that when you install the rollup package, it needs to be installed for whatever operating system you're using. I'm using Windows, so it installed the Windows version.

And on Netlify, I'm assuming it runs on linux, so we need to install the linux version on our production server. But how do we do this?

So when I get an error message and I don't know the solution, the first thing I usually do is search for the error message. So let's see if we can do this. Back in the Netlify website, I'm going to go to that error message and select the whole thing.

Then in Firefox let's open a new tab and paste in the search term. And I'm going to add "netlify" at the beginning to help filter our search. And let's just start looking at the results.

The first one is on Stackoverflow. They're using Docker, which we are not, but the error message is the same one we had, and they're talking about some fixes they tried which did not work. And there doesn't seem to be a solution for this.

Let's go back and look at the other results. This second one is on Netlify.com, and it mentions Vite, so let's check that one out. The post seems exactly what we're doing-- the Vite site works locally, but fails when you deploy and it builds on Netlify. And the error message looks the same like what we're getting.

It looks like this is solved in post 4, so let's click on that. They installed the module as a dev dependency and deployed.

Then the person below them says they are on Windows which I am too. And below that, someone has some code where you add it as an optional dependency. So that might be what we need to try.

So let's copy that, and go back to VS Code. Since the problem is related to installing the correct module, this means that we need to put this code snippet in our package.json file.

Let's open that up, and we already have a "dev Dependencies" section, so this will be a new section, so after the closing curly brackets, we need to add a comma, and then below that, paste in the code snippet for the optional dependencies. And get rid of the last comma, since you only want commas between items.

Alright, let's try this. So to trigger a deploy with the updated files, we need to create a new commit in GitHub Desktop and then push. So in GitHub Desktop, we'll commit our changes to the package.json files, and I'll add the message "add rollup as optional dependency".

And let's commit, and push to origin.

And now on Netlify, if we go back to the "Deploys" section we can see the new deploy in process, so let's click on that to see how it goes.

Okay, it went through without failing, awesome!
