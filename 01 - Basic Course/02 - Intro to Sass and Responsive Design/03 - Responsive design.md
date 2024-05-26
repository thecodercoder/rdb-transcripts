# Responsive Design

To illustrate the other Sass concepts and also get into how responsive design works, we're going to build a demo website. It will be a 2-column layout with a main section and a sidebar.

Let's go into our index.html and make some changes to the code there.

I'm going to wrap the h1 tag and paragraph tag that we have in a "main" tag. This will be the main content. Then I'll add a new element using the "aside" tag.

In the aside element, I'll add an h2 tag and say "More Info" and then add another paragraph with some lorem ipsum text by typing in "p>lorem30" to add 30 words.

The main and aside tags are what's called semantic HTML tags, where the tags themselves have a meaning separate from any CSS rules that you might apply to it. The h1 tag is another example of a semantic HTML element-- the "H" stands for "headline." And the "p" or paragraph tag is yet another one.

The "main" tag means this is the main content on the website. And the "aside" tag means that the content in it is secondary. It's generally a good idea to use semantic tags when you can instead of putting everything in a div or span element. Using semantic HTML is good for SEO because it lets search engines more easily parse the information on your website. And it's good for accessibility because screen readers can likewise navigate a webpage more easily if semantic HTML tags are used.

Now, with this website layout, I'd like it to be two columns for desktop, with the main element on the left and sidebar on the right, and then have them stack to one-column for mobile, with the sidebar below the main content. At a foundational level, this is what responsive design means-- making the website design look different if it's loaded on different devices.

There are a few components that work together in order for responsive design to work in the browser. The first one is that you need a specific tag in your HTML head. If we go to VS Code and look in the head, it's the <meta> tag with the name "viewport." The viewport is the part of the website that you can see in your device. Most websites are longer or taller than your viewport, but you can scroll down the page to read what's further down. So the website content is usually taller than your viewport, but is the same width as your viewport, unless you have to scroll horizontally to see content that's off-screen initially.

The viewport meta tag is doing two things. First, it's setting the width of the website to the device width that is currently viewing it. So if you're loading the website with a phone that is 375px wide, the website will be 375 pixels wide. If you're loading it from a monitor that's 1920px wide, the website will be 1920 pixels wide also. Then the initial-scale set to 1.0 means that it will set the initial zoom at 100%.

We can view how a website will look on various devices with an emulator that's built into all browsers. I'm using Firefox. We can change the device by going into the Inspector and clicking on the icon that looks like a phone and tablet. Then we can select the specific device that we want to view the website as. I'll select an iPhone. And we can see that the website viewport is now the size of the iPhone. If we switch to an iPad view, the website will also adjust to that width.

Let's see what happens if we don't have that meta viewport tag. If I comment it out and then save, and go back to our browser, the text on the website is actually a bit smaller than it was before. If we change to the iPhone view again, this effect is even more obvious.

What's happening is that the width of the website is not getting set to the device width, so it wants to get a lot wider than 375px. Then in order to fit the whole width on the phone, it's making everything very small. This is not what we want for a user experience on a website, of course. And if you've ever loaded a website on your phone and it looked super zoomed out like this, it's probably because the website hasn't been optimized for responsive design and is missing that meta viewport tag.
