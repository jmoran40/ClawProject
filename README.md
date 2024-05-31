# THE CLAW (but on a school budget)
## Marini - Moran - Tactical Block Repostioner Planning Document, Engineering 3 2023/24
### Scope
The assigned task for this project is to model, code, and assemble a robotic arm that can interact with objects to complete a specific task. Our goal is to make a device that can recognize an object's color, pick it up, and move it to a designated sorting area similarly to a claw machine found in an arcade. The creation process can be broken down into the four main steps of Onshape Design, Coding, Assembling. The details of these steps are provided in the schedule section below. This project will be considered a success if the device is able to differentiate between different colors and place them in the proper sorting areas without exploding.

### Schedule
Task - DD/MM/YY Completed - Description of task

Project Planning Completed - 3/8/24 - The Github planning repository will be completed

Onshape finished for the Arm  - 3/19/24 - We will create the Onshape model for the arm

Onshape assembly done - 3/22/24 - We will have all parts of the arm correctly assembled (in Onshape)

Onshape Done - 3/22/24 - Wrapping up work on Onshape and making sure everything is working correctly

Split up the work. Jude will write the code, Asher will assemble the physical pieces of the arm and the wiring

Code Done - 4/12/24 - Have functional code written and tested

Project Assembled - 5/8/24 - Have the pieces of the arm printed, assembled, wired, and tested

Documentaion Done - 5/10-5/20 - Document the process with pictures, videos, and reflections

Everything Done - 5/10-5/20 - Self explanitory (Make sure everything is done)

### Diagrams, Pictures, and Sketches
![Screenshot (1)](https://github.com/amarini3722/Arm-Project/assets/143545265/a18b16c4-6f5d-4104-ad55-d157b127942b)
![Assembly 1 (1)](https://github.com/amarini3722/Arm-Project/assets/143545265/a562679d-d38a-48d2-8694-47ebcd8786b4)

### Bill Of Materials
Acrylic

Motors

Screws, Nuts, and Bolts

3d-Printed Parts

Wires

M4 Metro

Ir Sensor

### Pseudocode
```python
Check if block is at postion
If block is at postion:
  Move to next postion
If no block is at postion
  Record "current postion"
  Move to block holder postion
  Grab block
  Move back to "current postion"
  Drop Block
  Move to next postion
```
### Scrapped Designs
![Screenshot (3)](https://github.com/amarini3722/Arm-Project/assets/143545030/1b790b21-cfbb-4532-b0a2-31491a096eb2)

RGB Color Sorter - Originally, the robot arm would detect the color of objects and sort them accordingly. This idea was scrapped partway through the coding process due to diffculties coding the RGB sensor.

Circular Box Pattern - Originally, there were four block holders arranged in a circular pattern. This was later changed to five boxes arranged in a 0/45/90/135/180 degree pattern.



# Robot Arm Project Documentation

### Project Planning
All project planning can be viewed in the doucment above. This includes the scope of the project, a schedule including precise timeframes, Diagrams/Pictures/Sketches of the original project design, a bill of materials, pseudocode, and scrapped design ideas represented through images and short sentances.

### Bill of Materials
Acrylic

Motors

Screws, Nuts, and Bolts

3d-printed Parts

Wires

M4 Metro

Ir Sensor

### Wiring Diagram
![Screenshot (21)](https://github.com/amarini3722/Arm-Project/assets/143545030/21a7e278-4e8d-431a-9ca5-622d6a61cc69)

### Project Code
```python
# Importing Libraries
import time
import board
import pwmio
import digitalio
from adafruit_motor import servo

# Component Set-Up
pwm = pwmio.PWMOut(board.D4, frequency=50)
pwm2 = pwmio.PWMOut(board.D5, frequency=50)
pwm3 = pwmio.PWMOut(board.D6, duty_cycle=2**15, frequency=50)
servo1 = servo.ContinuousServo(pwm)
servo2 = servo.ContinuousServo(pwm2)
servo3 = servo.Servo(pwm3)
Rotation = 0
ir_sensor = digitalio.DigitalInOut(board.D1)
ir_sensor.direction = digitalio.Direction.INPUT
ir_sensor.pull = digitalio.Pull.UP
now = time.monotonic()
CurrentPostion = 0



while True:
    # If IR Sensor Detects Block
    if ir_sensor.value == False:
        print("Block Sighted")
        servo1.throttle = 0
        servo2.throttle = 0
        # Move To Next Postion
        Rotation = Rotation+45
        if Rotation > 180:
            Rotation = 0
        servo3.angle = Rotation
    # IF IR Sensor Doesn't Detect Block
    if ir_sensor.value == True:
        print("NO BLOCK PANIC PANIC")
        # Remember Current Postion
        CurrentPostion = Rotation
        # Return To Block Holder
        servo3.angle = 0
        # Grab Block
        time.sleep(1)
        servo1.throttle = 1
        time.sleep(1)
        servo1.throttle = 0
        servo2.throttle = 1
        time.sleep(1)
        servo2.throttle = 0
        # Return To Remembered Postion
        servo3.angle = CurrentPostion
        # Drop Block
        time.sleep(1)
        servo1.throttle = 1
        time.sleep(1)
        servo1.throttle = 0
        servo2.throttle = 1
        time.sleep(1)
        servo2.throttle = 0
        # Resume Scanning Mode
    time.sleep(0.5)
```
### Onshape Model Pictures

### Photo/Video Evidence

### Design and Creation Timeframe (Schedule)
Warning: This is an estimation starting from when we finished the planning document

April 14th - Planning Document Finished And Submitted

Week 1 (April 15th - April 19th) - Working on Onshape models, ideas scrapped, designs modified

Week 2 (April 22nd - April 26th) - Team Split Up: Asher continues to work on Onshape models, Jude begins work on code and wiring

Week 3 (April 29th - May 3rd) - Asher works on Onshape models, Jude finishes project pieces and begins working on complete project code, Wiring is completed

Week 4 (May 6th - May 10th) - Plans are altered to include IR Sensor in place of RGB Sensor, Asher works on updated Onshape models, Jude works on updated code, Wiring is updated

Week 5 (May 13th - May 17th) - AP WEEK (Productivity Impacted), Plans are altered to include three motors (Final design change), Asher works on Onshape models, Jude updates and finishes code, Wiring is updated

Week 6 (May 20th - May 24th) - Asher works on Onshape models, Jude begins documentation and irons out coding bugs

Week 7 (May 27th - May 31st) - Asher works on Onshape models, Documentation is completed, Project is submitted

## Project Reflections

### Jude Moran
Any project in any class can be broken down into stages and this is especially true in Engineering. This project can be broken down into six. The Initial Ideas, The Actual Planning, The First Work Phase, The Reworking Phase, The Second Work Phase, and The Documentation. This list of stages is not a list held to any standard procedure. This is a refledction, a writing dedicated to looking back and sharing my view of how things went, of what I learned, of what was good, of what was bad, and most importantly of what my personal thoughts are on this project. As such, the stages I have devised and designated as the crucial phases of this project are strongly subject to my own opinion. Put simply, I see them as the most distinct parts of the project and now I shall reflect upon them. Once again, the stages are: Initial Ideas, Actual Planning, First Work Phase, Reworking Phase, Second Work Phase, and Documentation.

The Inital Ideas stage is the start of the project. As the name implies, its when the criteria for the project is recieved and the first ideas are dreamed up. Due to the large influx of creativity that always comes with the start of a new project, dozens fo various plans and designs are considered and sadly, many poor innocent ideas perish at this stage, never making it off the figurative and in most cases literal drawing board. Both Asher and I had several ideas to start this project with and after much consideration and several plans and designs sent to the big engineering farm in the sky, the idea we landed upon was a motor-powered claw that could sort small objects by color. Looking back, maybe we should have thought about the color recognition part of the plan a bit more before we fully invested into it but hindsight is 2020 and the design we ended up switching to later on didn't require too many adjustments so overall i'm happy with the choice we made.

I don't have a lot to say about The Actual Planning Phase if i'm being honest. The Actual Planning Phase occured after we had landed on an idea before we began working on the project itself. Basically, The Actual Planning Phase was the creation of the planning document. Truth be told, I'm proud of my handiwork and I hope you approve of our planning document. I also thank Asher for his help with the planning document and while we are at it let it be known that I greatly appreciate his contribution to the project. I'm certain the motivation and effort he put into this assignment is only matched by that of his well written reflection of which you shall be able to view below my own.

The first work phase was all the intial work done before the inevitable period of small changes and minor redesigns. Initally both Asher and I worked on Onshape, both working on a model to fit our design plans. The model went through several different iterations as we ourselves went through several different discussions over what we wanted to create. Eventually, we decided that the best course of action was for Asher to be the designated Onshape modeler and part assembler (when all the physical parts were ready) while I focused all my efforts on coding and wiring. The wiring was rather easy as at this point I already knew how to code and wire all of the essential parts of our project. For the coding aspect the hard part came not within making the parts work, but making them work in unison and in the unique ways the project criteria demanded. All was going well until one simple problem came up: A don't know how to use an RGB sensor and neither did the internet (In any way I could interperet). When even Mr. Miller couldn't help me I knew it time to change the design plans.

The Reworking phase. The period in which every problem with your original design rears its ugly head. Thankfully in our plans nothing needed a major rework with the biggest changes being a swap from an RGB sensor, a tool I had made no progress with, and a shift in the positioning and number of our sorting pods. Oh yeah, and we had to completely change the scope of the project from being a color based object sorter to a distance-detecting object mover. On second thought, maybe there was a major rework during this stage. It just didn't feel that noticable on my end due to how little work was necessary to make the change.

The second work phase was everything up until Documentation began and there isn't much else to say about it. I finished the wiring with minimal effort and a few quick hotfixes. The code took much longer and I did have some unproductive days but in end I completed it all with plenty of time to spare. Everytime I asked Asher how he was doing, he said he said he was doing good so I can only assume things were going well on his end. This was simply an extended period of time involving constant work.

### Asher Marini
Sample text

### Obituary
This project sadly was not completed within the preset amount of time provided. If I was to pick this project back up, I would start by finishing the Onshape models. The main reason our project failed was because our Onshape models were not done in time to even be 3d printed. Knowing this going forward would allow me to understand the importance of making sure a great deal of effort would be but towards the completion of those ever-important digital designs as without them the physical aspect of the project amounts to a jumble of circuits and wires. After the models would be completed, I would then focus all of my efforts on the 3d printing, laser cutting, and overall physical assembly of the actual parts of the project. Once those pieces were united, it would be time to test the finished project and make necessary adjustments until the device would be in complete working order. At that point the project would then be complete and I would be free to bask in the personal satasfaction of a job well done (after the documentation had been updated to account for the finished product of course).

### Credits
Planning Document (Diagrams) - Asher Marini

Planning Document (Everything Else) - Jude Moran

Onshape Models - Asher Marini

Wiring - Jude Moran

Project Code - Jude Moran

Documentation - Jude Moran

Project Reflection - Jude Moran & Asher Marini (Seperate Reflections)

Project Obituary - Jude Moran

Pain, Sweat, and Tears - Jude Moran

Credits - Jude Moran

### Conclusion
This concludes the documentation of our 2023-2024 Engineering 3 project

Thank you for reading - Jude Moran
