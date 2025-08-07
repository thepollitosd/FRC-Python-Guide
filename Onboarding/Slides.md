# FRC Python Onboarding — Slide Guide

## Slide 1: What is Programming?

**Explain:**
- Programming = instructing computers to solve problems by writing code.
- Programming languages are the bridge between human logic and computer instructions.

---

## Slide 2: Python Syntax Basics

**Explain:**
- Indentation matters (no curly braces!)
- Variables: store data.
- Comments: `#` for human notes.
- Data types: str, int, float, bool, etc.

**Code:**
```python
# Indentation example
def greet():
    if True:
        print("Hello World")
# Variables and comments
x = 5       # An integer
y = "John"  # A string
# Data types
is_active = True
```

---

## Slide 3: Electronics in FRC

**Explain:**
- Analog vs. Digital (continuous vs. on/off)
- Common FRC hardware: motors, sensors, encoders, controllers

---

## Slide 4: Programming Models in Python (FRC Concepts)

**Explain:**
- Timed-Based: You write every step, loop manually.
- Command-Based: You split tasks into "commands" and "subsystems," more modular.

---

## Slide 5: Timed-Based Programming (Think: Alarm Clock Routine)

**Explain:**
- Each step happens at a set time, like a morning routine.
- Good for simple, linear tasks.

**Code:**
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
- Pros/Cons slide: Easy, but not flexible.

---

## Slide 6: Command-Based Programming (Think: Teamwork & Roles)

**Explain:**
- Tasks are delegated to roles (objects/classes).
- Can run, swap, and combine tasks.

**Code:**
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

def morning_command(breakfast, driver, weather):
    breakfast.make()
    weather.check()
    driver.drive()

breakfast = BreakfastMaker()
driver = Driver()
weather = WeatherChecker()
morning_command(breakfast, driver, weather)
```
- Pros/Cons slide: Organized, scalable, but more setup.

---

## Slide 7: FRC Model Comparison

**Explain:**
- Timed-Based = manually drive robot with code for each action.
- Command-Based = give high-level instructions and let system handle details.

---

## Slide 8: When to Use Which Model?

**Bullet Points:**
- Timed-Based: fast prototyping, simple robots.
- Command-Based: real matches, complex behaviors, teamwork, testing.

---

## Slide 9: Why Command-Based for FRC?

**Explain:**
- Makes complex robot logic easier to organize and scale.
- Easier to test different parts separately.

---

## Slide 10: Project Overview

**Explain:**
- Building a basic FRC robot program in Python.
- Features: tank drive, autonomous driving, encoder for distance.

---

## Slide 11: Step 1 — Project Configuration

**Explain:**
- `pyproject.toml` defines project settings, dependencies, and RobotPy extras.

**Code (`pyproject.toml`):**
```toml
[project]
name = "frc0-robot"
version = "0.1.0"
description = "FRC robot code using RobotPy and CTRE TalonSRX motor controllers"
authors = [
    { name = "thepollitosd" }
]
dependencies = [
    # Add any non-RobotPy Python dependencies here if needed
]

[tool.robotpy]
robotpy_version = "2025.3.2.1"
robotpy_extras = [
    "all", "apriltag", "commands2", "cscore", "navx",
    "pathplannerlib", "phoenix5", "phoenix6", "rev",
    "romi", "sim", "xrp",
]
requires = []

[tool.robotpy-build]
robotpy = true

[tool.robotpy]
main = "robot.py"
```

---

## Slide 12: Step 2 — Imports and Setup

**Explain:**
- Why imports matter (libraries for robot hardware, controllers, math, etc.)
- Overview of files (`robot.py`, `helpers.py`, `pyproject.toml`).

**Code:**
```python
# robot.py
import wpilib
from wpilib import TimedRobot, XboxController, Joystick, Encoder
from ctre import WPI_TalonSRX  # CTRE TalonSRX motor controller support
import helpers as h            # Custom helper functions
```

---

## Slide 13: Step 3 — Hardware Port Assignments

**Explain:**
- Assign each hardware device to a port (wiring matches code).

**Code:**
```python
# Port numbers for controllers and motors
gameControllerPort = 0
joystickOnePort = 1
joystickTwoPort = 2

encoderChannelA = 0
encoderChannelB = 1

LFMCPort = 1  # Left Front Motor Controller port
LRMCPort = 2  # Left Rear Motor Controller port
RFMCPort = 3  # Right Front Motor Controller port
RRMCPort = 4  # Right Rear Motor Controller port
```

---

## Slide 14: Step 4 — Controller and Motor Initialization

**Explain:**
- Create controller/motor objects.
- Set up inversion for correct drive direction.

**Code:**
```python
class MyRobot(TimedRobot):
    def robotInit(self):
        self.gameControllerOne = XboxController(gameControllerPort)
        self.joystickOne = Joystick(joystickOnePort)
        self.joystickTwo = Joystick(joystickTwoPort)

        self.leftFrontMotor = WPI_TalonSRX(LFMCPort)
        self.leftRearMotor = WPI_TalonSRX(LRMCPort)
        self.rightFrontMotor = WPI_TalonSRX(RFMCPort)
        self.rightRearMotor = WPI_TalonSRX(RRMCPort)

        # Encoder setup
        self.encoder = Encoder(encoderChannelA, encoderChannelB)

        # Motor inversion for correct direction
        self.leftFrontMotor.setInverted(False)
        self.leftRearMotor.setInverted(False)
        self.rightFrontMotor.setInverted(True)
        self.rightRearMotor.setInverted(True)
```

---

## Slide 15: Step 5 — Helper Function for Encoder Ticks

**Explain:**
- Converts distance to encoder ticks (important for autonomous).

**Code (`helpers.py`):**
```python
def calculateTicks(autoDistance, wheelSize, ticksPerRevolution):
    # autoDistance: meters to travel
    # wheelSize: wheel diameter in meters
    # ticksPerRevolution: encoder ticks per full wheel turn
    return round((autoDistance/(wheelSize*3.1415))*ticksPerRevolution)
```

---

## Slide 16: Step 6 — Autonomous Mode Logic

**Explain:**
- Reset encoder, drive forward for a set distance using helper function.

**Code:**
```python
    def autonomousInit(self):
        self.encoder.reset()
        self.autoDone = False

    def autonomousPeriodic(self):
        # Drive until encoder reaches the target ticks
        if not self.autoDone:
            if self.encoder.get() < h.calculateTicks(5, 0.127, 8192):
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
```
- **Key point:** Use encoder ticks to measure distance.

---

## Slide 17: Step 7 — Teleop Mode Logic

**Explain:**
- Tank drive: left joystick for left motors, right for right.

**Code:**
```python
    def teleopPeriodic(self):
        leftSpeed = self.joystickOne.getY()
        rightSpeed = self.joystickTwo.getY()

        self.leftFrontMotor.set(leftSpeed)
        self.leftRearMotor.set(leftSpeed)
        self.rightFrontMotor.set(rightSpeed)
        self.rightRearMotor.set(rightSpeed)
```

---

## Slide 18: Step 8 — Boilerplate & Entry Point

**Explain:**
- Every Python robot must have an entry point for `wpilib`.

**Code:**
```python
if __name__ == "__main__":
    wpilib.run(MyRobot)
```

---

## Slide 19: Full Project File Structure

**Explain:**
- Summarize all files and their purpose.

**List:**
- `robot.py`: main robot logic
- `helpers.py`: utility functions (distance conversion)
- `pyproject.toml`: project config and dependencies

---

## Slide 20: Recap & Takeaways

**Bullet Points:**
- Python makes robot code readable and flexible.
- Timed vs. Command-based: choose model to fit robot/team complexity.
- Step-by-step building ensures understanding and easier debugging.

