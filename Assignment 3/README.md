### Assignment #3

### Intro
For assignment 3, I created a light box with a button on the top to change 5 different light settings. The concept at first was a lamp with 3 different light settings, but when making the physical object, a light box was easier to make than the lamp shown in the concept drawing and it still hides the cables "mostly" which is the most important part to me.

### State Diagram
The state diagram shown below has a start, digital input (button), and 5 different states. When the lightbox is first turned on by code, it enters waiting mode which is like the first state. This state is the starting position, staying a white color while waiting for the user to change states. From waiting mode, there are 2 different states you can go from here. The first one I will show is the main loop of states. By clicking the button once, the states of the lightbox changes to red mode. This state makes the light pulse a red color. By clicking the button once again, you can change states to the green mode. This state make the light flicker a green color. Clicking the button once more will change it to the blue mode. This state is the last state in the loop and it turns each LED blue one by one like a wave. All these states loop the effect until the button is pressed and when clicking the button once more, it comes back to the waiting mode. The final state is outside the loop of states and by holding down the button for 5 seconds, the final state will appear being rainbow mode. This state makes the light change colors constantly making a rainbow. by clicking the button once, you will go back to waiting state.

### Hardware
* LED Strip (The light)
* ATOMS3 (The processor that talks to the light)
* USB4 Cord (connects the Lightbox to the computer)

### Firmware

This part of the code
