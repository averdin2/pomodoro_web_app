# Blog #2

## Date: 6/25/2020

### Creating the Dynamic Color Styles

I will be detailing my thought process for making the colors dynamic based on the timer state for my pomodoro timer. I feel that writing this information is important because I don’t see a lot of sources for new comers to coding and web development that teaches you how to think and break down problems. So, I thought I would give it my best shot. My goal here is to also learn as I do this so it is a win win.

#### First:

I know that I need to change my colors depending on if the timer is started, in a break, or finished. I have already made css classes to acct as those different color themes. I will need a variable (data value for vue) to keep track of my different states. I can’t have a simple Boolean since I have three different color themes and 3 different states. Let’s try using three new Boolean variables to represent if that color is chosen. Initially, all will be set to false.

#### Second:

We know that each button will be a unique state for our app at this moment, so, let us make three methods (one for each button) that will change our color state variables and link them to the buttons. This works, but seems very boilerplatey (repetitive work), so, let us try to make one method to handle the cases. It works well. I used values 0-2 to represent the three states. (These values are hard coded in so no need to worry about users changing this value). I then used a switch statement to set the values.

#### Third:

This effectively changes my data variables, but now we need the actual colors to change. We will use vue class style bindings compared with our data values to change the page’s color when the color button is clicked. This works. However, we may now notice that having all these variables for isBlue, isGreen, and isRed is very boilerplatey, and also not very modular should we add other color themes. This is where we need to make tradeoffs on more development time for better code, or move on to other tasks. I am going to decide to move on since I know I won’t add other color options and the time taken to make this better is not something I am going to focus on at this time. I will make comments in the code so that I can go back to this when I revisit and I will move on.
