# Blog #5

## Date: 7/2/2020

### Finishing up the Minimum Viable Project

From last time, I need to finish up working on the reset button logic. After this, I should have a good minimum viable project to upload to GitHub as well as actually use. I think after I am done with this portion, I will also upload these blogs to the GitHub, and host the page on GitHub pages.

#### Reset Logic:

First, we know that the reset button will be displayed after the timer has started. So, let’s focus on getting the button to show up now. I actually just realized that the reset button can always be on so I will just remove the not-active class from it as well as any functions for now.

In order to get the reset button to work, I am going to add another data variable of isReset, and a new changeState value of 3 that will represent the starting state. I will use a condition in timer to check if isReset is true, if it is, then timer will call clearInterval, and changeState will be called with this new state I will make.

So, this mostly worked. I realized that I didn’t need to call changeState in timer, just when the button is clicked. I also had to add isReset to changeState so not very modular. The last thing I forgot was that I also need to reset the displayed time in timer when I check for isReset.

There was a delay in the timer when I called the displayTime function in timer since the time is getting updated every second. In order to ensure there wasn’t a weird delay, I instead put the call to displayTime when the reset button is clicked. (I also need to set phase to true so that it resets starting with the original timer).

There is a strange glitch that happens if you click reset then start too quickly, where it doesn’t clear the old timer and two times can be seen counting down. It only occurs if you do it very quickly, quicker than a second. I will leave this for now, but I will look into fixing this issue when I make future changes.

#### Conclusion:

I’m done for now!
