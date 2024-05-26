# Deploying to Netlify

Alright, in this video we're going to be deploying our website that we just built to Netlify, so that you can load your website from anywhere on the internet.

Netlify is a great platform for hosting static sites that are built with HTML, CSS and JavaScript, as opposed to what's called dynamic sites that are built with a traditional server-side language like PHP or C# and often have a database hosted on that server as well.

I'm choosing Netlify for this because it seems to be the most popular option right now, and it has a free tier for personal projects. Other than Netlify, you can also host a static website on Cloudflare Pages, GitHub Pages, or Vercel-- they all are either free or have free tiers for hobby or personal projects, which is perfect for this course.

Ok, to get started with Netlify, go to Netlify.com and click the "Sign Up" button. Then you can sign up with either email, or your source control login. I signed up with my GitHub login because it automatically connects your repositories to Netlify to make deploying easier.

Now, once you're signed up with Netlify and you've logged in, you should see a dashboard here. And here's where we're going to create the website that we want to host. So to do this on your dashboard, there's a sites panel down here, and you want to do the import an existing project.

So if we click that to import from Git, then we want to select GitHub since that's where we've hosted our repository. And then it should pop up a new window, prompting you to ask if you want to install Netlify and connect it to your GitHub account.

And you have a couple options here. You can click all repositories. And if you think you're going to be using Netlify a lot for multiple different repositories, then you might want to click all repositories.

You can also just select one repository or a few repositories. And I might do this just since I'm only going to select one repository for this. You want to select the repository.

Mine is called Responsive Design Beginners. And then now you can see it has selected the repository. So you can just read over the permissions that you're giving. So it looks pretty good.

And then I'm going to click the install button. And now we can see we're back in our Netlify dashboard. And we can see under here, we have the name of our repository, Responsive Design Beginners, showing up, which is pretty great. So once you see the repository in your dashboard, let's click on that.

And then we want to look at the different configurations. We want to check the team, CoderCoder's team. I think that's just a Netlify default. But you do want to make sure you're deploying the correct branch. I just have the one main branch, so I'm going to select that.

But if you have work on other branches that you want to use for your production deployment, you can select those branches. Then down in build settings, if you are using the Live Sass compiler to compile your SAS files, you basically want to keep everything blank.

So you don't want any of these. And it's going to install from the base directory, which is what we want. It's just your directory in the project. And you don't need to use any of these build commands, because you've already compiled your SAS files to CSS using the live SAS compiler.

All right, so once this is all set up, then the last thing for you to do is to click the Deploy Responsive Design Beginners button, and it'll start deploying. And this might take a minute or so to finish deploying.

All right, so once the deployment is finished, you should see a little pop-up message saying Deploy Success. And then it also has a nicely randomly generated name for your website. So if you want to check out the site deploy, you can click this button here.

And it'll give you some information about your deployment. 37 new files uploaded, et cetera. Everything looks pretty good. And then you can click the Preview button, and it'll actually load the website. So now you can see up in the URL bar, we have a randomly generated URL as a subdomain, and then a .netlify app.

So we can tell this is a real website, which is pretty cool. And the other way you can get to the website is, let's say you're back in the, let's see, let's go back to our main dashboard. So the other way you can access your website if you're coming from the main dashboard is you can see the sites here listed.

You can click on that, and then you can see there's a little card here with the name of the site, and you can click this URL to load the site in your browser.

All right, so that's it for the deployment to Netlify. Again, you can use whatever static website hosting platform you want. I just use Netlify because it seems to be the most popular right now.
