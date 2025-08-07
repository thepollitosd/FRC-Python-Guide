# FRC Python Onboarding — Slides

## Slide 1: What is Programming?

**Explain:**
- Programming = instructing computers to solve problems by writing code.
- Programming languages are the bridge between human logic and computer instructions.

---

## Slide 2: Python Indentation

**Explain:**
- Python uses indentation (spaces or tabs) to define code blocks, instead of curly braces.
- Consistent indentation is crucial—incorrect indentation will cause errors!

**Code:**
```python
def function():
    if True:
        print("Hello World")
        if False:
            print("This won't run")
    print("This will run")
```
*Incorrect indentation example (causes errors):*
```python
def function():
    if True:
        print("Hello World")
    if False:
        print("This won't run")
    print("This will run")
```

---

## Slide 3: Python Variables

**Explain:**
- Variables store data values.
- No command for declaring a variable; created on assignment.
- No need to specify a type—Python infers it from the value.

**Code:**
```python
x = 5        # Integer
y = "John"   # String
print(x)
print(y)
```

---

## Slide 4: Python Comments

**Explain:**
- Use `#` for comments.
- Comments help explain code or disable it temporarily.
- Python ignores anything after `#` on a line.

**Code:**
```python
# This is a comment
print("Hello, World!") # This is also a comment
```

---

## Slide 5: Python Data Types

**Explain:**
- Common Python data types:
  - Text: `str`
  - Numbers: `int`, `float`, `complex`
  - Sequence: `list`, `tuple`, `range`
  - Mapping: `dict`
  - Set: `set`, `frozenset`
  - Boolean: `bool`
  - Binary: `bytes`, `bytearray`, `memoryview`

**Code:**
```python
name = "Alice"         # str
age = 16               # int
height = 1.73          # float
scores = [90, 85, 92]  # list
info = {"team": "FRC"} # dict
is_robot = True        # bool
```

---

## Slide 6: Python Strings

**Explain:**
- Strings are surrounded by single `'` or double `"` quotes.
- Strings can be printed and manipulated easily.

**Code:**
```python
x = "Hello World"
y = 'Hello World'
print(x)
```

---

## Slide 7: Python Numbers

**Explain:**
- Supports integers and floating-point numbers.
- Scientific notation is also valid.

**Code:**
```python
x = 1                  # integer
y = 35656222554887711  # large integer
z = -3255522           # negative integer

a = 1.10               # float
b = 35e3               # scientific notation
c = -87.7e100          # large negative float
```

---

## Slide 8: Python Booleans

**Explain:**
- Booleans represent `True` or `False`.
- Used in conditions and logic.

**Code:**
```python
print(10 > 9)    # True
print(10 == 9)   # False
print(10 < 9)    # False
```

---

## Slide 9: Python Casting

**Explain:**
- Use casting functions to specify or change data types.

**Code:**
```python
x = str(3)    # '3' (string)
y = int(3)    # 3 (integer)
z = float(3)  # 3.0 (float)
```

---

## Slide 10: Getting the Type

**Explain:**
- Use `type()` to check what type a variable is.

**Code:**
```python
x = 5
y = "John"
print(type(x))   # <class 'int'>
print(type(y))   # <class 'str'>
```

---

## Slide 11: Setting the Specific Type

**Explain:**
- Use constructor functions to set a variable's type.

**Code:**
```python
x = str("s1") # 's1'
y = int(2)    # 2
z = float(3.0)# 3.0
```

---

## Slide 12: Electronics in FRC

**Explain:**
- Electronics are the hardware that makes robots move and sense the world.
- Two main types: analog and digital.
- FRC robots use motors, sensors, controllers, and more.

---

## Slide 13: Analog vs. Digital Electronics

**Explain:**
- **Analog:** Values change smoothly, not just on/off. Used for things like knobs, dials, and sensors that measure continuous data.
- **Digital:** Only two states—ON or OFF. Used for switches, buttons, and simple sensors.

| Analog Example     | Digital Example    |
|--------------------|-------------------|
| Volume knob        | Light switch      |
| Steering wheel     | Limit switch      |

---

## Slide 14: Examples of Analog Electronics

**Explain:**
- Analog devices control things using a continuous range of values.
- Useful for settings that aren’t just ON/OFF.

**List:**
- Volume control on a stereo
- Temperature control on a heater
- Steering wheel on a car
- Throttle on a motorcycle

---

## Slide 15: Examples of Digital Electronics

**Explain:**
- Digital devices are either ON or OFF; no in-between.
- Used for clear signals and simple logic.

**List:**
- Light switch
- Motion sensor
- Doorbell
- Limit switch on a machine
- OLED display

---

## Slide 16: Electronics Components in FRC

**Explain:**
- FRC robots use many types of electronics. Each has its own purpose!

**List & Description:**
- **Motors & Motor Controllers:** Move the robot and mechanisms.
- **Limit Switches & Buttons:** Detect position or user actions.
- **Pressure Sensors:** Measure air pressure (for pneumatics).
- **Cameras:** Vision processing or driver feedback.
- **Relays:** Switch high-current devices on/off.
- **Lights:** Status indicators or feedback signals.
- **Microcontrollers:** The robot's "brain" (runs code).
- **Encoders:** Measure rotation or movement for precise control.
- **Gyro/IMU:** Detect orientation and motion.
- **Power Distribution:** Safely route power to all devices.
- **Radio:** Wireless communication with the driver station.

---

## Slide 17: Programming Models in Python (FRC Concepts)

**Explain:**
- Timed-Based: You write every step, loop manually.
- Command-Based: You split tasks into "commands" and "subsystems," more modular.

---

## Slide 18: Timed-Based Programming (Think: Alarm Clock Routine)

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
- Pros/Cons: Easy, but not flexible.

---

## Slide 19: Command-Based Programming (Think: Teamwork & Roles)

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
- Pros/Cons: Organized, scalable, but more setup.

---

## Slide 20: FRC Model Comparison

**Explain:**
- Timed-Based = manually drive robot with code for each action.
- Command-Based = give high-level instructions and let system handle details.

---

## Slide 21: When to Use Which Model?

**Bullet Points:**
- Timed-Based: fast prototyping, simple robots.
- Command-Based: real matches, complex behaviors, teamwork, testing.

---

## Slide 22: Why Command-Based for FRC?

**Explain:**
- Makes complex robot logic easier to organize and scale.
- Easier to test different parts separately.

---

## Slide 23: Project Overview

**Explain:**
- Building a basic FRC robot program in Python.
- Features: tank drive, autonomous driving, encoder for distance.

---

## Slide 24: Step 1 — Project Configuration

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

## Slide 25: Step 2 — Imports and Setup

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

## Slide 26: Step 3 — Hardware Port Assignments

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

## Slide 27: Step 4 — Controller and Motor Initialization

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

## Slide 28: Step 5 — Helper Function for Encoder Ticks

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

## Slide 29: Step 6 — Autonomous Mode Logic

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

## Slide 30: Step 7 — Teleop Mode Logic

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

## Slide 31: Step 8 — Boilerplate & Entry Point

**Explain:**
- Every Python robot must have an entry point for `wpilib`.

**Code:**
```python
if __name__ == "__main__":
    wpilib.run(MyRobot)
```

---

## Slide 32: Full Project File Structure

**Explain:**
- Summarize all files and their purpose.

**List:**
- `robot.py`: main robot logic
- `helpers.py`: utility functions (distance conversion)
- `pyproject.toml`: project config and dependencies

---

## Slide 33: Recap & Takeaways

**Bullet Points:**
- Python makes robot code readable and flexible.
- Timed vs. Command-based: choose model to fit robot/team complexity.
- Step-by-step building ensures understanding and easier debugging.

