## Switching viewport widths

It may not be super common for a user to switch between mobile and desktop viewport widths, but it could happen, for example switching from portrait to landscape mode.

So let's fix this now. To do this, we're going to add another event listener, this time on the "window.matchMedia()" breakpoint constant.

Let's create this under the open and close button event listeners. One thing I wanted to mention is that so far in our JavaScript, we've been using the older syntax when writing functions.

But with the newer ES6/ES2015 version of JavaScript, you can write a new type of function called "arrow functions", as opposed to the older type which is now called "regular" functions. In many, but not all cases, you can use either regular or arrow function syntax.

But as I mentioned before, I am not a JavaScript expert, so I'm not going to go into all the differences between regular and arrow functions and why and when you would use each. But I did want to at least show you examples of both types of syntax.

I'll write "breakpoint.addEventListener()" and in it, we're going to listen for a "change" event. This means anytime the viewport changes and crosses the 43.75em breakpoint, this event will fire.

And when this change event happens, we want to run some code. We can do this by adding a comma after the "change" event, then with the older syntax first, we can add a regular function by writing "function()" with parentheses, and then some curly brackets.

And in the curly brackets we're going to write yet another console log message, and I'll make this one say "breakpoint crossed". So hypothetically, anytime the viewport changes and crosses the 43.75em or 700 pixel breakpoint, this message should pop up in our console.

This is different from what we did with the open and close button event listeners, as for those when the event happens, we run the open and closeMobileMenu() functions which are kept separately.

Now, let me show you the newer syntax and make this regular function into an arrow function. We're going to get rid of the word "function" and then between the parentheses and the opening curly bracket we're going to add our arrow, with an equal sign and a right angle bracket. This is where arrow functions get their name.

And this will achieve the same thing as the regular function that we just had. Again, in a lot of cases you can use either type and there's no big difference.

Okay, let's test out this code, and see if changing the viewport fires this console message when we cross that 700px width point.

Alright, in our website, make sure we are on iPhone, and have the "Console" tab showing. And you can see in the console we have our initial "is mobile" message from when the website got loaded. Now let's change the viewport width by dragging out that right edge.

And when we crossed that 700 pixel mark, we have the "breakpoint crossed" message loading, which is great. So let's go back to a mobile width, and when it crossed 700 again, we got a second console log message. And because it was exactly the same as before, Firefox condenses things and just starts numbering the message, which is why it says "2" now.

And if I keep going back and forth you can see that number increasing by one each time. Alright, this looks like our breakpoint change event listener is indeed working.

Okay, going back to our code, in our breakpoint change event listener, we want to check if we're on mobile or desktop anytime the breakpoint is passed. And this is what we've already written up in our if/else statement.

Right now, it's checking if we're on mobile or not one time, on the initial page load. Because when you load or reload the page, all the code in our file gets executed one time.

But, we want to check if we're on mobile or not not just that first time, but anytime the viewport changes and we cross that breakpoint.

We could copy the if/else statement and paste a duplicate inside our event listener function, but you really don't want to have duplicate code.

What we can do is to move the if/else statement into a function, kind of like openMobileMenu() and closeMobileMenu(). And that way we can run the function once on page load, and then also have the function run in our change event listener.

Let me show you what I mean. Let's create a new function, under the closeMobileMenu() function. And like I mentioned earlier, we're going to try to use the newer syntax and make this an arrow function and not a regular function like the two other ones.

Arrow functions get created as constants. So instead of writing "function", we'll write "const". And let's give it a name, I'll call this "setupTopNav". And instead of writing parentheses right away, we add an equal sign to set it, and then the parentheses, which we'll leave blank right now. And then our arrow with equal sign, right angle bracket, and then our curly brackets.

If you compare how this looks with the regular function syntax above, it is definitely different, but there are similarities too.

Now, I'm going to select the entire if/else statement and move it inside the function. Now, before, the if/else statement code was running on page load because it wasn't in anything.

But now because it's inside this function, the code will only execute if we call the setupTopNav() function. Just creating a function will not automatically run the function.

So we can run the function by adding it-- maybe before the event listeners, I'll write "setupTopNav()". And, let's test to make sure the function will run on page load. I'm going to add a console log message inside the function, before the if statement.

I'll write "console.log('setupTopNav')" just to print that text out, it's not running anything since it is a string inside the quotes.

Let's save, and test our website! I will reload just for good measure, and we can see in our Console, the message "setupTopNav". So we know that it is getting executed once when the website is initially loaded.

That's working, now let's also run the function in our breakpoint change event listener. Under the console log message, I'll do the same thing, and run "setupTopNav()".

Now let's go back to our website, and let's start on iPhone size. And we see we have our initial "setupTopNav" message, and the "is mobile" message. Now, when I drag out that right edge to hit the 700 pixel breakpoint, we see the "breakpoint crossed" message, followed by the "setupTopNav" message, and "is tablet/desktop".

And if we go back down to mobile size, we again see "breakpoint crossed", "setupTopNav", and then back to "is mobile".

And we still have that menu appearing and sliding up, and the overlay visible and then fading out, when we go from desktop back down to mobile widths. So let's fix that now.
