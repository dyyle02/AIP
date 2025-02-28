### Assignment #3

### Intro
For assignment 3, I created a light box with a button on the top to change 5 different light settings. The concept at first was a lamp with 3 different light settings, but when making the physical object, a light box was easier to make than the lamp shown in the concept drawing and it still hides the cables "mostly" which is the most important part to me.

### State Diagram
The state diagram shown below has a start, digital input (button), and 5 different states. When the lightbox is first turned on by code, it enters **waiting mode** which is like the first state. This state is the starting position, staying a white color while waiting for the user to change states. From waiting mode, there are 2 different states you can go from here. The first one I will show is the main loop of states. By clicking the button once, the states of the lightbox changes to **red mode**. This state makes the light pulse a red color. By clicking the button once again, you can change states to the **green mode**. This state make the light flicker a green color. Clicking the button once more will change it to the **blue mode**. This state is the last state in the loop and it turns each LED blue one by one like a wave. All these states loop the effect until the button is pressed and when clicking the button once more, it comes back to the waiting mode. The final state is outside the loop of states and by holding down the button for 5 seconds, the final state will appear being **rainbow mode**. This state makes the light change colors constantly making a rainbow. by clicking the button once, you will go back to waiting state.

### Hardware
* LED Strip (The light)
* ATOMS3 (The processor that talks to the light)
* USB4 Cord (connects the Lightbox to the computer)

### Firmware
```python
    if in1.value() == 0:  # Button is pressed
        if in1_val_last == 1:  # Last state was unpressed
            button_press_time = current_time  # Record press time
            button_held = False  # Reset the hold flag
```
This part of the code tells the button to change states when pressed and records how long the press is when pushing down on the button

```python
if program_state == 'RED':
                program_state = 'GREEN'
            elif program_state == 'GREEN':
                program_state = 'BLUE'
            elif program_state == 'BLUE':
                program_state = 'WAITING'
                just_entered_waiting = True  # Set the flag to prevent immediate RED
            elif program_state == 'RAINBOW':
                program_state = 'WAITING'
                just_entered_waiting = True
                state_start_time = ticks_ms()

            print('program_state =', program_state)
```
This part of the code tells the button what state it should go to next when in each of the states

```python
 if ticks_ms() - button_press_time >= 5000:
            program_state = 'RAINBOW'
            button_held = True  # Mark as held to prevent short press logic
            just_entered_waiting = False  # Ensure we don't block re-entering RED later
            print('program_state =', program_state)
```
This part of the code tells the button how to enter the **rainbow mode** (by holding the button down for 5 secs)

```python
    else:  # Button is released
        if in1_val_last == 0:  # Last state was pressed
            # Only trigger RED if not held for 5 seconds AND we are in WAITING 
            # AND didn't just enter WAITING from BLUE
            if not button_held and program_state == 'WAITING' and not just_entered_waiting:
                program_state = 'RED'
                print('program_state =', program_state)
```
This part of the code tells what the button should do when in **waiting mode**. Waiting mode is treated differently than the other states because it has 2 different states to go to. Here the code is specifically telling the button to not instantly go to **red mode** when the button is pressed because it needs to record how long the press is to go to **rainbow mode**.

### Physical Components
All of the components when making the lightbox is made of paper and tape. There are 3 components to the lightbox which is the box, the button, and the cover.
  
- **Box**
  
The box holds all the hardware and the button.
  
- **Button**
  
The button consists of folded paper, a long cylinder made of paper, and 2 copper tape. The folded paper is used so that when you push down on the long cylinder that is attached to the folded paper, the 2 copper tape which is taped to both ends of the folded paper is pushed in together making a wire connection. This acts as a button for the lightbox.
  
- **Cover**
  
Lastl,y the cover is a circular top that covers the box with a hole on top for the button to come out of.


### Project Outcome
The lightbox came out a little different than the concept drawing, but it came out great. I managed to hide all the hardware within the lightbox except the USB4 cord of course and the code works most of the time. If I was able to work on this more, I would clean out the paperwork and also tweak the code a little to make the state changes more smooth.
