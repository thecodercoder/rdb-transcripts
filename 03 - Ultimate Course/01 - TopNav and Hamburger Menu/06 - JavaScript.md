## JavaScript

We're going to be using JavaScript to add some functionality to the different parts of the hamburger menu. Specifically, the open button, the menu itself, and the close button that's in the menu.

And we'll need a way to target each of these HTML elements in our JavaScript. To do so, it's considered best practice to use an ID for that, instead of targeting CSS classes. And I like doing this too, to keep things separate.

In our index.html file, let's go to the open button element, and I'm going to add an ID before the class attribute. The order doesn't matter, but I always put my ID's first.

I'll create an ID, and for this, set it to "btnOpen". Then, in the "topnav\_\_menu" div, we'll add an ID there and set it to "menuTopNav". And for the close button, we'll set its ID to "btnClose". And for each of these I am using camelCase, meaning the first word is written with a lowercase letter, then the next word begins with a capital letter.

Now that we've created our IDs, we'll need to start loading them in our JavaScript code. So in VS Code, I'm going to open the sidebar, and in the Explorer we want to go to the "app/js" folder and open the script.js file.

So far we just have our console log message, and I'm going to delete that since we know this is getting loaded in our website already.

Now, to work with the 3 elements in JavaScript, we need to load each of them in our file as a constant, which is a type of variable.

Let's start with the open button. In our JavaScript, we'll write "const" to signify that we are creating a new constant. And then we'll write the name of the constant. I'm going to make the name match the ID we gave the open button, so I'll add "btnOpen".

And now, we need to set the value of "btnOpen" with an equal sign. And we want to load the button element here. So to do this, we first need to write "document" to load the actual document object that is the entire web page, then a "dot" and then a method called "querySelector", and parentheses.

I like querySelector() a lot because in it, in quotes, you can write CSS selectors. So for the open button, I'll write "hashtag btnOpen" to load the element with an ID of "btnOpen". And that's all we need for this line.

Now, we want to do something when the open button is clicked. We can do this by adding what's called an "event listener" in JavaScript to the button. This means the browser will detect when the button is clicked.

To do this we want to start with the btnOpen constant, add a dot, then write the "addEventListener" method with parentheses. And in the parentheses, we need to say what type of event we are listening for. In our case, we want to listen for a click, so in quotes, we can write " 'click' ".

And, we want to run some additional code when the button is clicked. We can do this by creating a function, by typing "function" and then the name of the function, which I'll call "openMobileMenu".

Then we'll add some parentheses and curly brackets. The parentheses are needed because functions will sometimes need parameters, which are variables whose values can be used in the function code that gets run in the curly brackets.

We will be using some parameters later on, but we don't need any here, so we'll leave the parenthese blank.

Then in the curly brackets, we'll write the code we want to happen. For now, let's just add some test code, I'll write "console.log('openMobileMenu')" so we can test to make sure the button click and the function will work.

Okay, so we have our function, now we need to finish our event listener code so that it will run the openMobileMenu() function when it is clicked. So after "click", I'll add a comma, and then write the name of the function, "openMobileMenu".

Now we have our open button, and an event listener that will run function when the button is clicked. Let's save and test this out!

Alright, in our browser, I'm going to go to the "Console" tab, and it looks like we have an error. It says "Uncaught TypeError: btnOpen is null". I'm including this error in the course because it's super common to see.

The reason this is happening is because, if we go to VS Code and look at our index.html file, in the "head" tag is where we have our script tag to load our script.js file.

And the browser is going to load things from top to bottom, so it's loading the JavaScript before all the actual website content in the body.

So in our JavaScript file, it's trying to do things with the btnOpen element, before the element itself has been loaded in the browser. This is why it's throwing that error saying that "btnOpen" is null-- because it doesn't exist yet when the JavaScript is getting run.

The old way of solving this was to put the script tag not in the header, but right before the closing body tag. However, a more modern way of fixing this is to add the "defer" attribute to the script tag. This means that the JavaScript will download but it won't execute the JavaScript file until after the rest of the DOM, the "document object model" is loaded.

The DOM is basically how the browser loads the website. And I do want to say that I am not a JavaScript expert at all, so if you want to read up more about the DOM or anything JavaScript related, I highly recommend Flavio Copes' website-- he has a very long-running and in-depth blog, on FlavioCopes.com.

He also has a free online bootcamp that's also text-based tutorials on TheValleyOfCode.com. Both of those are really great, free references which I've also linked below and in the resources module at the beginning of the course.

[https://flaviocopes.com/javascript-async-defer](https://flaviocopes.com/javascript-async-defer)

[https://thevalleyofcode.com/dom](https://thevalleyofcode.com/dom)

Anyway, once we have the "defer" attribute in, let's save, and now on our website we are no longer seeing the error. And when we click on the hamburger button, we see our console message "openMobileMenu", which means that the click event is working and running that function, which is awesome.

Now we can write the real code that we want to run in our function.

Back in our styles, we had targeted the "topnav\_\_open" class with aria-expanded attribute being true, as what makes the "topnav\_\_menu" slide down onto the screen.

So, in our JavaScript, we need to change the "topnav\_\_open"s aria-expanded value from false to true when the button is clicked. Under the console log message, I'll write "btnOpen dot" and then "setAttribute".

SetAttribute is a method that we can use to add or update HTML attributes for elements. It takes 2 parameters, the first one is a string that is the name of the attribute that we want to either add or change. So for us, we'll write, in quotes, "aria-expanded".

Then we'll add a comma, and the second parameter is a string that contains the value that we want to set. So I'l write, again in quotes, "true".

Now, on the website, let's inspect the hamburger button, and initially it has "aria-expanded" equals "false". But when we click the hamburger button, it changes to "true", and the menu slides down. So the open functionality is working!

Now let's get the close button to close the menu, by doing the reverse of what we did with the open button. So looking back at our code, with the open button, we first loaded it as a constant using "document.querySelector()" to target the ID that we created.

Then we added an event listener so that when it is clicked, it runs the "openMobileMenu()" function. And in the function that we created, it is setting "aria-expanded" of the open button to "true". So there are 3 parts to getting the open button to work.

Alright, this might be a bit of a challenge, especially if you haven't worked with JavaScript much or at all, but I'm going to give you the chance to pause the video and see if you can set up the close button functionality.

It's going to be very similar to what we did with the open button, but setting "aria-expanded" to "false" instead of "true".

And you definitely don't have to try this yourself if you don't feel ready. But give it a shot if you want, and pause now.

[ pause ]

Okay! Let's set up this close button functionality.

Following what we did for the open button, we first need to load the close button as a constant. Since a lot of the syntax is the same, I'm going to duplicate the "btnOpen" constant line, and we'll put the close button on the second line.

First I'll rename the constant "btnClose", and then we'll need to also update the ID which I'm pretty sure is "btnClose" also.

Then we'll do the same thing for the openMobileMenu() function-- I'll select it and duplicate it. Then I'll rename the second one "closeMobileMenu". And in it, I'll update the console log message, and for this we want to still be updating the "btnOpen", but instead of "true" we want to set "aria-expanded" to "false".

Lastly, we need to put the event listener on the close button. So again, I'll duplicate the first one, then set the second one on "btnClose", and have it run the function closeMobileMenu() instead of openMobileMenu().

Alright, let's save, and see if this works!

So on the website, I'll click the hamburger button to open the menu, and that looks good. And now, we want clicking on the close button to close the menu.

And, looks like it's working! So we're pretty good on the basic functionality. Next up, we're going to also hide and show the menu for accessibility tools like screen readers and keyboard-only users.
