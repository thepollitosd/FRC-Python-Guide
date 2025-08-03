# Programming Models in Python (FRC Concepts, Simplified!)

Before we jump into robots, let’s learn what these models mean **without any robot code**.

---

## Timed-Based Programming (Think: Alarm Clock)

### What is it?

Imagine a **morning routine** where you do everything on a **fixed schedule**:

* 7:00 AM — Wake up
* 7:10 AM — Brush teeth
* 7:20 AM — Eat breakfast
* 7:30 AM — Leave for school

You just follow the routine, step by step. That’s what **Timed-Based Programming** is like—**you control every step manually**, and it runs on a loop.

### Python Example:

```python
import time

def morning_routine():
    start = time.time()
    while True:
        elapsed = time.time() - start

        if elapsed < 10:
            print("Brushing teeth...")
        elif elapsed < 20:
            print("Eating breakfast...")
        elif elapsed < 30:
            print("Leaving for school...")
        else:
            print("Done with routine!")
            break
        time.sleep(1)

morning_routine()
```

### Pros:

* Super straightforward
* Great for short routines
* Easy to write and test

### Cons:

* Gets messy if things overlap
* Hard to make changes later
* Not flexible if you want to multitask

---

## Command-Based Programming (Think: Teamwork with Roles)

### What is it?

Now imagine you’re running a **school club**. Instead of doing everything yourself, you **delegate**:

* One person handles breakfast
* Another drives to school
* Someone else checks the weather

Everyone has a **role** (Subsystem), and you tell them what to do (Command). You can **swap, combine, or schedule tasks** however you like!

### Python Example:

```python
class BreakfastMaker:
    def make(self):
        print("Making breakfast...")

class Driver:
    def drive(self):
        print("Driving to school...")

class WeatherChecker:
    def check(self):
        print("Checking the weather...")

# Command functions
def morning_command(breakfast, driver, weather):
    breakfast.make()
    weather.check()
    driver.drive()

# Run it
breakfast = BreakfastMaker()
driver = Driver()
weather = WeatherChecker()

morning_command(breakfast, driver, weather)
```

### Pros:

* Organized and modular
* Easy to test or change parts
* Can run multiple tasks together or in sequence
* Built for complex systems (like robots!)

### Cons:

* Requires understanding objects and classes
* Slightly more setup at the start
* Might feel like “too much” for small tasks

---

## In FRC Terms...

* **Timed-Based** = You drive the robot by hand-writing everything.
* **Command-Based** = You give commands like "drive forward" or "shoot ball" and let the system handle when and how.

---

## What’s the Takeaway?

Timed-Based is good for simple, small tasks but not ideal for complex, multitasking logic

Command-Based is good for organized, scalable projects but not ideal for quick experiments or one-offs

### Why do we use command based?

To ***organize*** and to ***scale***

# Project Code Completed

```python
# robot.py
import wpilib
from wpilib import TimedRobot, XboxController, Joystick, Encoder
from ctre import WPI_TalonSRX  # Use robotpy's CTRE bindings for TalonSRX
import helpers as h

# Hardware port assignments (replace with your actual wiring as needed)
gameControllerPort = 0
joystickOnePort = 1
joystickTwoPort = 2

encoderChannelA = 0
encoderChannelB = 1

LFMCPort = 1  # Left Front Motor Controller port (CAN ID)
LRMCPort = 2  # Left Rear Motor Controller port
RFMCPort = 3  # Right Front Motor Controller port
RRMCPort = 4  # Right Rear Motor Controller port

class MyRobot(TimedRobot):
    def robotInit(self):
        # Initialize controllers
        self.gameControllerOne = XboxController(gameControllerPort)
        self.joystickOne = Joystick(joystickOnePort)
        self.joystickTwo = Joystick(joystickTwoPort)

        # Initialize motors using robotpy's CTRE TalonSRX bindings
        self.leftFrontMotor = WPI_TalonSRX(LFMCPort)
        self.leftRearMotor = WPI_TalonSRX(LRMCPort)
        self.rightFrontMotor = WPI_TalonSRX(RFMCPort)
        self.rightRearMotor = WPI_TalonSRX(RRMCPort)

        # Initialize encoder
        self.encoder = Encoder(encoderChannelA, encoderChannelB)

        # Optionally invert right motors for correct drive direction
        self.leftFrontMotor.setInverted(False)
        self.leftRearMotor.setInverted(False)
        self.rightFrontMotor.setInverted(True)
        self.rightRearMotor.setInverted(True)

    def autonomousInit(self):
        self.encoder.reset()
        self.autoDone = False

    def autonomousPeriodic(self):
        h.calculateTicks(5,0.127,8192)
        
        # Simple autonomous: drive forward until encoder reaches calculated number of ticks
        if not self.autoDone:
            if self.encoder.get() < h.calculateTicks(5,0.127,8192):
                self.leftFrontMotor.set(0.5)
                self.leftRearMotor.set(0.5)
                self.rightFrontMotor.set(0.5)
                self.rightRearMotor.set(0.5)
            else:
                self.leftFrontMotor.set(0.0)
                self.leftRearMotor.set(0.0)
                self.rightFrontMotor.set(0.0)
                self.rightRearMotor.set(0.0)
                self.autoDone = True

    def teleopInit(self):
        pass

    def teleopPeriodic(self):
        # Tank drive: left joystick controls left motors, right joystick controls right motors
        leftSpeed = self.joystickOne.getY()
        rightSpeed = self.joystickTwo.getY()

        self.leftFrontMotor.set(leftSpeed)
        self.leftRearMotor.set(leftSpeed)
        self.rightFrontMotor.set(rightSpeed)
        self.rightRearMotor.set(rightSpeed)

    def testInit(self):
        pass

    def testPeriodic(self):
        pass

if __name__ == "__main__":
    wpilib.run(MyRobot)
```
```python
#helpers.py
def calculateTicks(autoDistance,wheelSize,ticksPerRevolution):
    return round((autoDistance/(wheelSize*3.1415))*ticksPerRevolution)
