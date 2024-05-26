# Add styles for h-tags

**Note: since recording this video, the Google Font "Source Sans Pro" has been renamed to "Source Sans 3".**

Let's also take a look at the typography styles. I'm going to inspect the top h1 tag, and click into the "Computed" tab. Then in our browser I'm going to switch the device to iPhone. And as we increase the viewport in our browser the h1 font-size also increases.

If we go to the "Rules" tab, we can see that the font-size is being set using the CSS clamp() function, which was from our demo website styles.

However, we need to make sure that the font sizes are matching what we have in the design, since I just kinda used a random font-family and font-size numbers for the demo website.

Back in Figma, I'm going to select the "Desktop" frame and hide both layout grids so we can just focus on the website content. Let's check the font-family first. If I select the main heading, in the right sidebar it says the font-family is "Source Sans Pro" and the font-weight is "Bold."

And if I select the subheading it's the same font family, with the font-weight set to "Regular." The top nav font is also "Source Sans Pro" bold.

When you have a design it's generally a good idea to check the text styles to see what font-families and font-weights are being used throughout the design, since that's what you need to know when getting the font from Google Fonts.

First we'll need to go to Google Fonts, so I'll open a new tab and search for "Google Fonts" and then go to the site. In Google Fonts, we can search for "Source Sans Pro" and then select it. And in the different styles we need Regular 400, and Bold 700. And we're not using any Italic styles.

With fonts, you do want to be careful about not using too many different font families and font weights, because each one needs its own separate font file, and whether you're loading them via Google Fonts or with local font files, the more you have the more users will need to download when loading the website.

I've tried to keep it very minimal with just the one font family and two weights, but if your design has a ton of different weights across multiple font families you might need to check with the designer to see if there's a way to reduce the amount of variations on the website.

Back to our fonts, to load them we will need to copy the code snippet under "Use on the web" and then go to VS Code in the index.html file. We have some existing Google Fonts code from our demo website, so let's delete those-- it's the 3 link tags that load "googleapis" or "fonts.gstatic.com" things. And then paste in the new code, checking that it's loading "Source Sans Pro", with 400 and 700 font-weights.

Once we have our HTML code for Google Fonts, we'll want to update our CSS styles with the "Source Sans Pro" font-family. To make sure we have it right, we can go back to the Google Fonts page and in the right it will say "CSS rules to specify families" and I'm going to copy the style rule.

Then back in VS Code, we need to check where we set the font-family-- it should be in `globals/boilerplate.scss`, and set on the body tag. And it is set to the "u.$font" variable, so to find where we set that, we know it's in the util folder since we have that "u" namespace, and in the util folder is a fonts.scss file.

So here we can paste in the new font-family, and just make sure to delete the `font-family:` part since we only want the font family name. And it should say `'Source Sans Pro', sans-serif`.

And that should be it for our font family styles, for now!
