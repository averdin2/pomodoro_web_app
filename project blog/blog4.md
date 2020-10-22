# Blog #4

## Date: 7/1/2020

### More Styling and State Logic

The first thing that I am doing to start off this coding session is to make more useful comments for data variables as well as the styling. The file length for Couter.vue is getting quite long so I just want to ensure that it is readable for someone first looking at the code.

#### Button Styling:

The next thing I am doing is adding a container for the buttons. I don’t want the buttons to be too cramped together, and they were also placed vertically rather than horizontally. Not all of the buttons will be displayed at a given time so I will also create styles to set display to hidden.

I ended up realizing that the buttons don’t need a wrap class, just another wrapper div so I got rid of the class I just created. Instead I gave each button a little bit of margin on the right and left.

I now realize that hovering over each button is a bit boring so I am going to add some styling to each button. I’m thinking of making the text and border become white with a bit of a transition delay on hover and focus. I also got rid of focus outline.

I ended up changing the color for each button by adding a third style depending on the state of the app. I am now going to make the concrete names for the different states reflect in the variable names. This should make it easier to understand myself and the functions of the colors going forwards. I am also going to add separate button hover styling for each button as well as a class for setting display off.

#### Changing Data Variable Names:

I need to change variable names to now better reflect the state of the app rather than color. These variables will also be key for changing color depending on if the timer is started, is on break, or is stopped.

#### Stop Logic and Color Change:

I am now going to work on the stop logic. My idea is to have a check in the timer for when the time reaches 0 (this is already implemented), but when the timer reaches 0, the condition will call the changeState function (this function was formerly the setColor function) with a variable of 2 to denote that the timer has stopped. I am also making the timer start when the start button is clicked so that I can see if the color changes properly as a result of the start click and the stop condition.

#### Break Logic and Color Change:

I now need to add the logic when a break occurs. Let’s think about what needs to happen when the break button is clicked before I code anything. When the break button is clicked, it will set the time that needs to be counted down to the break time. The color needs to change to green to reflect that the app is in the break time. Finally, the timer needs to be called with for the length of the break time. So, when this button is clicked all of these things need to happen. We can call changeState, then displayTime with timeInSeconds with breakLength as the argument to set the new breakLength, then we need to call timer with breakLength as the argument. (I just now ended up changing some names for the button classes to better reflect the purposes of the buttons.)

#### Start and Stop Logic:

I am going to work on more logic for the start condition of the app as well as what happens when the app stops after the state has been in the start condition. After working on this I will be done for the day.

First thing to note that needs to happen is that the only button that should be present when the app is first booted/mounted is that the only button that should be displayed is the blue start button. (For testing purposes, I am going to completely set the reset button to not active with no way to activate it at this time. I am also adding extra comments into the html section of the file to denote where certain components are. I suspect that the logic within the html is going to get more complicated so I want to make it easier to find the components I am looking for.) Then, the changeState needs to be called with a value of 0 (to denote the start state), and the timer function needs to be called with the timeLength.

The main thing I need to focus on here is getting the buttons to come and go. Since I know that this is going to be dynamic, I can’t just set the class to not-active for the break start button. I need it to use Vue’s class style binding to change the set-active class to when the timer has finished. This means that our current state will be in the stopped state. For now, I will focus on doing this. So, I will have the not-active set when not isStop.

This works, but I also realized that I also need the regular start to not appear as well. However, I need this to not appear as long as the start condition is true and the stop is not on the break rotation. It seems like I actually need another data variable to keep track of which rotation I am on (I could actually just do this with my changeState function, but I have used the fact that only one of the three variables is set to true to set the color theme of the page. If I change how this works, I will have to fix those other styles. I think I will stick with adding a new variable, but this will be a focus when it comes to revisiting my project when I make it more modular). I will create a new Boolean data variable called timer that is initialized to true. When timer is true, this will denote that we are in the regular timer or start state. When timer is false, this will denote that we are in the break phase. (I just want to note that the way this is implemented is honestly just god awful. It definitely needs to be changed to be more modular. I mean this variable name does not help suggest what is being done at all and I can’t for the life of me think of a better name for it with this implementation. I’m actually changing the name from timer to phase for now just so I don’t get confused working on this). Every time the timer stops, the phase variable will be toggled to true or false. Then, the comparison will be made to phase and stop. If stop is true and phase is true, then the start button will appear. If the stop is true and phase is false, break button will appear.

The ended up overcomplicating the logic here so here it is again:

For the start button: the button is not active when the start condition is met or when phase is false.

For the Break Start button: the button is not active when the break condition is true or when phase is true.

#### Conclusion:

For next time, I still need to have a toggle for the reset button and add the reset button logic. Once I do this, the minimum viable project should be met and I can then focus on the next stage for the project which is to make the code more modular.
