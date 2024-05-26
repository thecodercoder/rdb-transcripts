## Troubleshooting

Let's check things over and compare to the design. If I go to Figma to eyeball everything, it matches.

Let's now test the website with decreasing the viewport width from desktop down to mobile, to see if there are any points where this new set of styles looks weird.

I'm going to use Responsive Design mode, and drag the right edge over to decrease the width. And it looks ok until we hit about over 1000px. And now the quotation marks are going off screen, and we have horizontal overflow. And it's like that until we hit our large breakpoint at 900px and switch to the mobile design without position absolute.

We also probably want to hide that second quotation mark except for desktop widths. Let's do that since it's one quick thing we can fix. In our styles, I think I'm going to use our breakpoint-down() mixin so we can target widths at and below tablet.

This is just for the last-child one, so I think before our large breakpoint, I'll nest a selector for "ampersand colon last-child", then in it add "@include u.breakpoint-down(medium)" and in that set "display: none". Now when we save, the second quotation mark isn't there, and if we increase the viewport, it appears at the same time as the design changes.

That's good. Let's get back to our original problem of how to make this design not break at around 1000 pixels. If I inspect, the code, one thing that we could change is making the "testimonial\_\_wrapper" less wide. So right now it's set to a max-width of 50rem. Just in the browser, let's try reducing that by 10 to 40rem.

Looks better, let's drag over that viewport to decrease it, and right at 900px when the design is going to change, everything is still onscreen, which is great. I might even tweak it a little more narrow, like 38rem, so there's a bit more breathing space around the quotation marks.

This does work and it's pretty quick. However, you might not always be able to adjust the width of the content. You might sometimes need to create a new breakpoint-- if we do that here, we can get the Testimonial section to switch to the mobile design sooner than 900px which is our "large" breakpoint.

If I go to the breakpoints.scss file, looking at our breakpoint Sass map, there is a pretty big difference between 900 and 1440 pixels. I think that I might try this solution in our code, just because it might be good in the future to have another breakpoint between 900 and 1440, so I could see this benefitting future code.

Let's do that. I'm going to duplicate the "large" breakpoint, and let's set the second one to xlarge and maybe 1100 pixels. Then we will have to rename the original "xlarge" to "xxlarge".

And since we renamed it let's see if we have used the old "xlarge" breakpoint in our styles, because that will have to be changed too. I'm going to press Ctrl-Shift-F or Cmd-Shift-F for Macs, to open the project search, and I'll type in "xlarge". And the only results are in the breakpoints.scss file, which means we haven't used it yet. So we're good on that.

And we should also create a corresponding breakpoint for the "breakpoints-down" map. So I'll duplicate the "medium" one, name the second one to "large" and change the number to "1099.98" so it's just under the "1100" size of the "breakpoints-up" size.

And let's check the project to see where we've used the "breakpoint-down" mixin, to see if we need to change any of those names. I'll press Ctrl-Shift-F again, and search for the mixin name, "breakpoint-down". And it looks like we've only used "medium" and "xsmall". We never used "large" which is the one that is now "xlarge". So we're good.

Now, with our new breakpoint name all set, let's go back to our Testimonial styles, and change the name of the "large" breakpoint to be one size bigger with "xlarge". And change the "breakpoint-down" name to be also one size bigger, from "medium" to "large".

Now let's test. I'm going to put the website browser window to be full size. And let's move the right edge down to the mobile design. And then drag it out. So at 900px it is still using the mobile design, and when we hit 1100px, that's when we change to the two absolutely positioned quotation marks.

That looks good! And I think this was a good solution that is also making how we set up our breakpoints a little better for the future.

Cool! So that's pretty much it for the Testimonial section. Let's go to GitHub Desktop and commit our code. As usual, let's eyeball the files in the Changes tab, and everything looks like this is what we want to commit. So I'll add a message, "Updated Testimonial". And I'll press "Commit to main" and "Push to origin".
