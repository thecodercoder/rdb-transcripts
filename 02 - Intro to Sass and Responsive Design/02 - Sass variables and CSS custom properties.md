# Variables and CSS custom properties

Next up, let's talk about variables. You may have heard variables being used when talking about programming languages like JavaScript. Without getting super technical, variables are ways that you can store bits of information and label them with a name. This name is generally descriptive so it makes it easier to both remember and understand what the information is. They're called variables because the information associated with the name can change.

Sass and now CSS both have variables. In CSS, variables are officially called "CSS custom properties" but people often refer to them simply as CSS variables.

Why do we want to use variables in our styles? Well, using variables to refer to things like color values, font styles, spacing, and so on, make it easier if we need to change those styles later on down the line. You define the variable and its value in one place, and then every style rule that needs to use that value can simply refer to the variable instead of the actual style value.

Also, it's just easier to remember the name "dark gray" when you're writing code, instead of the HEX or HSL color value.

Let me show you what I mean in our project. In VS Code, in the boilerplate Sass file, the body selector has the background-color and color properties being set to a color in HSL. Now imagine that we want to use both those background color and text colors elsewhere in our styles, so if we didn't use variables, we'd have to copy and paste those HSL colors in every place that we want to use them. Then if those colors need to change at some point, we'd have to do a Find and Replace to find every single instance and change them. This can be very time-consuming depending on how big your codebase is, and there's a decent chance for making an error when changing things manually.

So, let's move these color values into some CSS custom properties.

In the globals folder, create a new file called "underscore colors.scss." And in the index.scss file in globals, add a new @forward rule to load "colors." Back in the colors.scss file, we're going to set our CSS custom properties.

Generally when creating new CSS variables that may be used anywhere else on the website, you want to set them on the root selector, using "colon root." Some people also set them on the HTML or body selector, and that's fine too. Root will override the HTML and body selectors, so it's more of a "global" variable in this case.

And, you can also set the CSS variable in any selector. So if you wanted to save the spacing of a card element in a variable to be used for only cards, you could set the variable in the .card selector. How you use them is up to you. I've noticed a lot of people setting all the variables in the :root globally, but it also makes sense for organizational purposes if you wanted to have some "local" variables set only in the selectors where they will be used.

Going back to the colors that we want to move into variables, let's copy that first background-color value, HSL Zero Zero 11. And in the colors.scss file, in the root selector, we need to give it a name, like "background color." When you're creating CSS variables, the names must begin with a double hyphen. So this would be called "hyphen hyphen background dash color." Then add a colon and the HSL color value.

```
:root {
  --background-color: hsl(0, 0%, 11%);
}
```

And let's do the same thing for the color property. We'll copy the HSL value, and create a new custom property called "--text-color." And set the HSL value.

```
:root {
  --background-color: hsl(0, 0%, 11%);
  --text-color: hsl(0, 0%, 100%);
}
```

Now, let's load those variables in the body styles. In the boilerplate.scss file, we can call the background-color variable by typing in "var(--background-color)" in place of the HSL color. And for the color property, we can set the value to "var(--text-color)."

Now, let's check our local websites and see if everything worked.

Looks like the colors are loading. In the inspector, if we look at the body selector, we can see now that the background-color and color properties are using the variables that we created! So they say "var background-color" and "text color," and if we scroll down a bit we can see the root selector, with the actual color values of the variables. And they're displayed in HEX colors because the browser will ultimately translate the HSL colors into HEX on the website.

Sass also has variables, and they are similar to, but different from CSS custom properties. With Sass variables, your compiler will convert any Sass variables to the final CSS value. CSS custom properties are newer, and since they're native to CSS you can get the benefit of using variables without having to use Sass if you don't want to.

In addition, one big benefit that Sass variables don't have is that you can use JavaScript to change the value of a CSS custom property after the website has loaded. People use this for things like dark/light modes on a website, as you can use JavaScript to update the colors on the fly.

In general, it seems like people are replacing Sass variables with CSS variables, but I'm still going to show you how Sass variables work because if you're working as a developer in the field, there's a pretty good chance that you might have to work on some legacy code at some point. Not every company stays up to date with the cutting edge, so a lot of places will use tools and technologies that are considered "out of date" because they still work.

So we stored our colors in CSS custom properties. I'm going to use Sass variables to store font information. Let's go to Google Fonts and I'm going to look for Open Sans. Then let's select the weights we want-- I'm going to get regular 400 and bold 700. Then copy the link tags. And back in VS Code, in our index.html file, we'll paste those in the head of the document, before we load our stylesheet.

Now, since we're using Sass variables, and we want to be able to load the font values in any other Sass file, we need use something called Sass modules to make the Sass variables accessible from our other Sass files. This may sound a bit confusing right now, but let me show you what I mean.

Instead of adding another Sass partial in our globals, I'm going to create a new subfolder in scss called "util." And since we have a new subfolder, we want to create a new underscore index.scss partial. Then I'll create another partial in util called "\_fonts.scss." And we'll forward the fonts partial in the \_index.scss file by writing "@forward 'fonts';" And again, we can just write fonts without needing to type out the underscore or SCSS file extension.

Then, in \_fonts.scss, we'll create a Sass variable to store the font-family. I'm going to call this "$font." The dollar sign in front of the word signifies that it is a Sass variable. Now going back to Google Fonts, I'm going to copy the "Open Sans, sans-serif" text. And then I'll set the $font variable to this value. Now that we've created the variable, let's use it. Going back to the \_boilerplate.scss file, I'm going to update the body font-family to use that Sass variable.

However, when we save, we get an error in our compiler. It's saying that "$font" is an "undefined variable." What this error means is that it doesn't know what the $font variable is. This is because the variable is in a different Sass partial, util/\_fonts.scss. So we need to load that Sass partial as a Sass module in our boilerplate Sass file in order for us to be able to call that variable in our boilerplate styles.

This is similar to what you may have seen in JavaScript and other programming languages, where you load or "use" other code files in order to use functions and other things from those files. What we want to do is load all the "util" Sass files as a module. Right now there's just the fonts Sass file there, but we will be adding more as we continue.

The way to load another Sass partial as a module is to go to the target Sass file, which in our case is "\_boilerplate.scss" and at the top of the file, use a Sass at-rule called "@use." Then we need to add the file path from boilerplate to the util subfolder. We're starting in the "globals" folder, so we need to get out of that and go one level up-- we can do that with a double-dot to go navigate up to the scss folder. Then we want to go to util, so add a slash and "util."

We don't need to explicitly say "\_index.scss" in the util folder because Sass will automatically look for an index file. If we save, the Sass compiler is still giving us the same "undefined" error. This is because we need to use a namespace whenever we're loading a Sass module. By default Sass will give it a namespace that matches the name. So if we add a "util." in front of the "$font" variable, then save, everything loads with no error.

The namespace is to help keep things separate. Before Sass modules existed, you had to make very sure that you weren't using the same variable name, and things could get confusing and overwritten. Having namespaces means that we could have another $font variable in a different Sass partial from the utils. Since they would be loaded with different namespaces, it wouldn't cause a conflict.

And you can also set Sass modules to any namespace you want. So I could load util as just the letter "u" if I add an "as u" to the @use at-rule. Then when using the $font variable we could just write "u.$font". Lastly, if you don't want to use namespaces, you do have that option. We can @use util as a wildcard or asterisk. And then we don't need to use any namespace when using the $font variable. But then you will open yourself up to the problem of possible name conflicts, so I personally think it's safer to use the namespaces in some form.

And if we check the browser and inspect the body element, we can see the font-family has been set to "Open Sans." And we can see here the difference in how Sass variables and CSS custom properties behave in the browser. The font-family value of "Open Sans" you wouldn't know that it was loaded using a Sass variable, because the Sass compiler will convert it to the final value in the CSS file. The background-color and color properties are using CSS custom properties, which continue to exist in the browser itself since, again, they are native to CSS.

One last thing to note since we've used Google Fonts here. At the time of recording, Google Fonts has been found by a court in Germany to violate the GDPR regulations, because they can track the IP address of users who load your website when they load the Google font files from Google. I'm not sure how this will resolve, but if this is a concern for you, you can download the Google font files and host them on your own website's server instead of Google's servers.

Loading the fonts locally is a bit outside the scope of what I think this course is, but I just wanted to mention it that so you know what is currently the case with Google Fonts, since so many people use them.
