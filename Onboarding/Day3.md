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
# helpers.py
def calculateTicks(autoDistance,wheelSize,ticksPerRevolution):
    return round((autoDistance/(wheelSize*3.1415))*ticksPerRevolution)
```



```toml
# pyproject.toml
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
    "all",
    "apriltag",
    "commands2",
    "cscore",
    "navx",
    "pathplannerlib",
    "phoenix5",
    "phoenix6",
    "rev",
    "romi",
    "sim",
    "xrp",
]
requires = []

[tool.robotpy-build]
robotpy = true

[tool.robotpy]
main = "robot.py"
```