# Blog #3

## Date: 6/25/2020

### In Depth Description of Progress on Project

I want to say that this is actually the first day I have decided to document this project and plan on adding these, “blog posts” I guess I should say, to my project when I upload on GitHub. I plan to have my initial post to GitHub very soon, I just want to finish the basic functionality of the website before I do. I suspect by that time I will have written a few of these already.

#### HTML:

As of this point in the project, there are a few decisions with the HTML I had to make. Let me start by detailing my thought process for the basic HTML structure for the Counter.vue file (the App.vue file is very basic and I already detailed what I did in the first post, so I won’t be saying much about it unless I decide to change it later down the road).

#### HTML Structure:

Given that I am using the Vue single page component structure for my code, the HTML is all in one file. There is a template tag that encapsulates all of my HTML. I have a div tag with no class that then encapsulates the rest of the HTML. I need this div because for the Vue template syntax to read properly, there must only be one overarching div to be added to the page. For example, this would give you an error in Vue:

```
<template>
  <div></div>
  <div></div>
</template>
```

Continuing on, I have a div to act as an overlay (I will explain this reasoning a bit later), I have a div to act as an overall container for the rest of the items, I have a h1 to display the name of the project, I have another div for the actual display of the timer, and I have three buttons with text blue, green, and red respectively. The basic structure (without attributes and text) looks as so:

```
<template>
  <div>
    <div></div>
    <div>
      <h1></h1>
      <div></div>
      <button></button>
      <button></button>
      <button></button>
    </div>
  </div>
</template>
```

Let’s now jump into the CSS so I can explain the different attributes for each HTML element, and also help explain my reasoning for this HTML structure.

#### CSS:

Let me start by giving you the same HTML structure, but this time I will add the class attributes.

```
<template>
  <div>
    <div class="overlay"></div>
    <div class="counter-container">
      <h1 class="header"></h1>
      <div class="timer"></div>
      <button class="btn"></button>
      <button class="btn"></button>
      <button class="btn"></button>
    </div>
  </div>
</template>
```

I think that perhaps the most interesting decision I had to make here was with the div with the class of “overlay”. When working through this project, I know that I wanted the entire page of my site to change color. Normally we can change the color of our background with some CSS like this:

```
body {
  background-color: red;
}
```

Changing the color of the body wouldn’t be a problem for me if I wasn’t trying to dynamically change the color of the page. I considered using CSS variables, but that still didn’t solve my problem as I needed the color of the background to be able to change as I need. I decided I would do this by making separate dedicated classes for my color styling, and use those class attributes as a way to change the color. However, as you can see with the layout of my HTML, there is no way for me to add attributes to the body element when I am using Vue template syntax. This is why I made a new div with the class overlay to essentially act as a cover for the body. For my styling of the overlay, it will be positioned absolutely to top and left the page so that it does not interfere with the positioning of any other elements. I also gave it a z-index of -1 so that it did not get in the way of the main elements of the page. I then gave it a height and width of 100 view height and width respectively so that it takes up all of the webpage dynamically.

The next div here is the “counter-container”. The purpose of this div is to contain and format the rest of the elements in an organized fashion. It is no surprise here that I gave this div a display of flex and aligned the items to center. I decided to set justify-content to space-between to give equal spacing to the elements depending on the screen they are displayed on. I then gave a height of 30vh so that all these elements will be contained within a small area and not too spread out throughout the height of the page.

The header and timer classes were mainly just to change font size so not much else to say there, but I will note that I used rem units in order to ensure proper font sizes at different screen sizes.

The generic btn class given to the buttons is relatively basic for button styling so I’ll just show it here:

```
.btn {
  border: 1.5px solid black;
  border-radius: 10px;
  padding: 10px 20px;
  background-color: transparent;
  font-family: "MuseoModerno", cursive;
  font-size: 1rem;
  cursor: pointer;
}
```

Just a few notes to say about some of my decisions here, I decided to make the border color black because I know that I would change it with my class specific color styling, but I still wanted it to show while testing out functionality. I also needed to make the background-color transparent because I knew that the web page’s background color would be changing and it made it so I didn’t have to add unnecessary color styling to the button.

Here is an example of the color styling classes I have for the different color themes I wanted for the page:

```
.blue-bg {
  background-color: lightblue;
}

.blue-color {
  color: dodgerblue;
}

.blue-btn {
  border: 1.5px solid dodgerblue;
  color: dodgerblue;
```

Note that I have three color styles: blue, green, and red. This code is the classes I needed to style for my blue theme. There are similarly named and styled classes for green and red respectively. The blue-bg style is for elements that need a blue background color. I applied this for the overlay div. The blue-color class is for all text that needs to be changed. This was applied to the header and timer elements. Note that this color is darker than the background color. This is the same aesthetic for the other color themes with text being darker than the background color. The blue-btn class is because I needed to style the border and text of the button depending on the color theme. How the color theme was chosen will be explained in the JavaScript section coming up.

#### JavaScript:

Given that this is an explanation of my thought process and not a tutorial, I am not going to explain how I did everything or how Vue works. Instead, I will just explain my thought process for different variables I have, and changes I made to code structure. I will explain the different functions I have and their use, but I will not explain how I coded them specifically.

Given the nature of Vue and how it works, I initially had my time value passed down as a prop from App.vue. I decided that I wanted my value of time for the timer was going to be a consistent value of 25 minutes for work timer, and 5 minutes for break. Thus, I decided that I did not need to pass down a value from the props and instead made a hard-coded data value for the times. (Note: As of this time, I do plan on moving these values back to being props as I finish my minimum viable project here and move on to making my code more modular).

I will now explain my data values (if you don’t know Vue that well, just think of these as basic global or state variables).

My first two variables are displayMinutes and displaySeconds, both of which are set initially to 0. These variables are specifically used to display the time for the timer. They are the values that are put into the text area for the timer div. These initial values are quickly changed and used often so I will refer to them again when explaining my other functions.

My next two variables are timeLength and breakLength. These are the values that will be used to calculate how long the timer will last. These are initially set to 25 (for 25 minutes) and 5 (for 5 minutes) respectively.

My next and last three variables are isBlue, isGreen, isRed. These variables are to determine the different class styling the will be added to the HTML elements to determine the color theme of the page. I know that these different variables are rather redundant and I plan to change them to one variable in the future. If I only had two color themes, it would be easy to have one Boolean variable.

Now onto my functions. The first function is a mounted function that sets the intial time displayed for the timer based on the timeLength variable. The mounted function relies on two other functions I have made in order to effectively display the time: displayTime and timeInSeconds. (displayTIme calls timeInSeconds with the timeLength as its input).

The timeInSeconds variable is quite explanatory, but I will still detail its reasoning and use. First of all, it is used to take in a time in minutes and convert it to seconds. The reason I have this function is because the given time variables timeLength and breakLength are given in minutes. In order to make calculating values easier for the other functions, it is best to convert those times to seconds.

The next function is displayTime. This function takes in a time t given in seconds and converts the values to minutes and seconds and displays these values by setting displayMinutes and displaySeconds. Another thing to note about this function is that it needs to format the time for minutes and seconds to ensure a leading 0 is present should the time be less than 10 seconds. This is to ensure that the display of the time looks like a typical digital clock.

The next function is the main timer function. It is rather explanatory but this is the function that counts down the time given a specific time in minutes. It uses the timeInSeconds function to convert to seconds and then uses a setInterval function to subtract that time by 1 every second until the timer reaches 0 then it clears the interval. It also uses the displayTime function to display the time on the screen every second.

The last function is a setColor function which takes in a numeric value. The numeric value is something that is hard coded so there is no need for a check of this value. This value is a number between 0 and 2 inclusive. Depending on the value passed to the function, it will change the different color variables to true or false depending on the number value. These values then determine which color class attribute to add to the HTML element. I will show you what I mean with the overlay element:

```
<div class="overlay" v-bind:class="{ 'blue-bg': isBlue, 'green-bg': isGreen, 'red-bg': isRed }"></div>
```

(Note: The v-bind:class is specific syntax to Vue so if you don’t know Vue don’t be too confused, it is just a way to choose class attributes). Notice that all different color options are being evaluated. The setColor function will only ever set one value of isBlue, isGreen, and isRed to true and the rest to false so only one of these classes will be chosen. These color values will be determined by which button is pressed. As of the moment of this writing, there are three buttons corresponding to the three colors respectively. Clicking on the respective button changes the color theme of the page by calling the setColor function with the corresponding value. The other HTML elements have similar syntax that decides their respective color style. I want to say that I know this is not a very modular way of making this work. I plan on fixing this when I finish my minimum viable project. The goal is to make one data variable that will help determine the color theme along with the setColor function. Names of these variables and functions are more than likely to change to reflect the actual functionality of these colors. I have only made them color names at first to make it very clear as to if clicking a button was changing the color of the page like I have outlined in post 2 of my blog here.

#### Conclusion:

Hopefully if you are reading this then my outline of everything I have done makes sense. In future updates, I will really be talking more specifically about what I am working at the time so it won’t be so long and cover as many details.
