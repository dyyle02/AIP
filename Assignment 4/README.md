### Assignment #4

### Intro
For assignment 4, I created a bracelet that tracks how many steps you take. When you wear the bracelet and start walking, it will count the steps you take and display them on a digital screen. If you take enough steps, then it will display how many miles you traveled based on the amount of steps. the bracelet will also light up green or blue which represents a step u took. If you traveled 0.5 miles, then the bracelet will light up red indicating you reach the half mile.
  
<img src="state diagram.jpg" width="500">
  
### State Diagram
<img src="state diagram assignment 3.jpg">  

The state diagram at first looks complex, but using the device is quite simple. When you start it, it will first turn blue or green depending on where you hand is. How it works is that when the bracelet detects one side that is pointing to the ground, it trigger 2 things, first it will add 1 to the step counter, then it will turn blue or green and vise versa for the other side of the bracelet. This will happen each time you move your arm either in front of you or behind you. The step counter will be in the background adding up. Once it hits 20 steps, it will calculate that many steps as 0.1 miles and will add that to the mile counter. This will happen forever, but when you hit 0.5 miles, the bracelet will then turn red. Moving to the digital side, the hidden data of steps and miles will appear on the app. The app will also show the color of the bracelet when its green or blue.

### Hardware
* LED Strip
* ATOMS3
* USB4 Cord
* imu PRO Unit (For collecting movement data)
<img src="IMG_6752.JPG" width="500">

### Firmware
```python
    # setting values for previous inputs
    prev_stepcounter = stepcounter
    prev_milecounter = milecounter
```
This part of the code gives me the variables to be able to calculate the step and mile counter without it continuously counting

```python
    # code for when the arm is moving clockwise
    if imu_x > -1 and imu_x < -0.8 :
        
        # if the previous imu_x value was out of the threshold, add to step counter
        if boolen_stuff == False :
            stepcounter += 1
            
        boolen_stuff = True
            
        # change color to green within threshold
        for i in range(NUM_PIXEL) :
            np[i] = (r, g, b)
            b = 255
        np.write()
        sleep_ms(50)
        print('stepcounter||'+str(stepcounter))
        print('b')
```
This part of the code tells me when the x-axis of the imu pro unit reaches between -0.8 and -1, the bracelet will turn blue. This is also when the code would add 1 to the step counter. There is also a boolean value for when the x-axis bounces around the edge of the threshold, the step counter won't count unless the x-axis was in the previous threshold before

```python
  # code to calculate for every 20 steps, add 0.1 to mile counter
  if stepcounter != 0 and stepcounter % 20 == 0 :
    if prev_stepcounter % 20 != 0 :
      milecounter +=0.1
      print('mile||'+str(milecounter))
```
This part of the code calculates for every 20 steps, add 0.1 to the mile counter.

```python
    # code to calculate for every 0.5 miles, turn red 
    if milecounter !=0 and milecounter % 0.5 == 0 :
        if prev_milecounter % 0.5 != 0 :
            print('you ran half a mile!')
            for i in range (NUM_PIXEL):
                np[i] = (r,0,0)
                r = 255
            np.write()
            sleep_ms(50)
```
This part of the code calculates when the mile counter hits 0.5, the bracelet will turn red indicating you ran half a mile.

### Physical Components
The bracelet is made of paper and tape. There is only 1 physical component which is the bracelet. It holds all the hardware.

### Digital Components
There is an app that talks to the bracelet since you can't see how many steps you take on the bracelet.

### Project Outcome
The bracelet was surprisingly a little more difficult than the light box, but overall came out fine. The coding, even though it was shorter, was more complex and I took more time to figure it out. As for the physical object, it was relatively easy since it was made of paper. If I was able to put more work into it, I would change how the app looks and use better material for the bracelet than paper.

<img src="IMG_6747.JPG">

**Video**
https://drive.google.com/file/d/1E2hmnnzSuAAQhJjo_V_JV9wVQgR2nl_e/view?usp=drive_link
