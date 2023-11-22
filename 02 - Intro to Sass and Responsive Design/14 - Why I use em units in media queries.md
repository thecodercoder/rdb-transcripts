# Why I use em units in media queries

Now that we have our font-size and other sizing properties updated to use rems, I'm going to show you why I use em units in my media queries instead of pixels. I mention this just because I've seen that pixels in media queries seem to be the most common unit used by websites and even front-end frameworks that otherwise follow accessible practices.

For this demo, we'll go back into our "util/\_breakpoints.scss" file and I'm going to duplicate each of the Sass maps that we created earlier and comment them out, just to keep the final code that we want. Then I'll set all the breakpoint values to pixels without the function.

So we'll save that, and then load the website.

So far things look totally fine. If we inspect the "grid" class element we can see that 700px breakpoint kicks in at the right time and the website content goes from 1 column on mobile to 2 columns for tablet and desktop.

The problem happens if we change the browser's base font size in our settings. I'm going to double the font size to be 32 instead of 16, and reload the website. Now everything like the text has been scaled up since we're using rem units in our font sizes, which is good! But if we make the viewport narrower, the 2 columns get really narrow, and with the larger text it makes things look cramped. And this is not a great user experience.

The reason this is happening is because the media queries are set to pixels. If we inspect the grid class element, we see that it's still changing to 2 columns at 700px wide. And since pixels are an absolute unit, they are not affected by changing the base font size. So essentially you have the layout going from 1 to 2 columns at a narrower viewport than we really want, in order to keep the design.

We doubled the font size from 16 to 32, so ideally we'd want that breakpoint of 700px to also double to 1400px, so that the layout won't change to 2 columns until the viewport is much wider.

Let's fix this problem by going back into our `_breakpoints.scss` file and deleting the pixel Sass maps and uncommenting the em Sass maps. Once we do that, if we go back to our website to look at the iPad view, the layout is in one column now. And if we slide over the inspector panel, it will go to 2 columns at around 1400px and wider. And the columns have more breathing room now, which makes for a better user experience.

I hope that helps explain why it's best to use em units in media queries. You can use rem units, as they are also a relative unit. But unfortunately at the time of this recording there's a weird bug in Safari if you zoom in on your browser that makes the breakpoint hit at a different viewport. It doesn't have the cramped content issue that using pixels does, but I would stick with em units for now.

So now, we have all the building blocks that we need in order to build a responsive website. We have our media query breakpoints set up with Sass maps and mixins, we have our font sizes scaling up nicely using the CSS clamp function, and we're keeping things accessible by using our rem() and em() functions to convert from pixels.

The last part of this section is going to be building out this demo website a little bit more and delving a bit deeper into BEM.
