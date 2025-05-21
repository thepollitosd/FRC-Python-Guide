# FRC-Python-Guide
## Getting Started
1. Install [Python for Windows](https://www.python.org/downloads/windows/)
2. Install or Upgrade RobotPy
- If you don't have RobotPy:
	```shell
	py  -3  -m  pip  install  robotpy
	```
- If you do have RobotPy:
	```shell
	py  -3  -m  pip  install  --upgrade  robotpy
	```
3. To start a project, type in `mkdir [Your Project Name Here]` to create the folder
4. Next, type in `cd [Your Project Name Here]` to navigate to the folder
5. To create the necessary files, type in `py  -3  -m  robotpy  init`. This will create `robot.py` and `pyproject.toml` files. You will write most of the code in `robot.py`, but for now, we will use pyproject.toml.
6. Open pyproject.toml, and uncomment all requisites. Your code should look like this
```toml
[tool.robotpy]
# Version of robotpy this project depends on
robotpy_version = "2025.3.2.1"
# Which extra RobotPy components should be installed
# -> equivalent to `pip install robotpy[extra1, ...]
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
# Other pip packages to install
requires = []
```
7. Copy this starter code, and paste it in `robot.py`:
```python
#!/usr/bin/env python3
#
# Copyright (c) FIRST and other WPILib contributors.
# Open Source Software; you can modify and/or share it under the terms of
# the WPILib BSD license file in the root directory of this project.
#

import wpilib

class MyRobot(wpilib.TimedRobot):
    def robotInit(self):
        pass

    def autonomousInit(self):
        pass

    def autonomousPeriodic(self):
        pass

    def teleopInit(self):
        pass

    def teleopPeriodic(self):
        pass

    def testInit(self):
        pass
    def testPeriodic(self):
        pass


if __name__ == "__main__":
    wpilib.run(MyRobot)
```
8. We need to set some constants for our ports and we need to import some libraries. To do this, write this code below `import wpilib`:
```python
import phoenix5
import commands2
from commands2 import Command
from commands2 import Subsystem

gameControllerPort = None
joystickOnePort = None
joystickOnePort = None

gameControllerOne = None
joystickOne = None
joystickTwo = None

encoder = None
encoderChannelA = None
encoderChannelB = None

LFMCPort = None
LRMCPort = None
RFMCPort = None
RRMCPort = None

leftFrontMotor = None
leftRearMotor = None
rightFrontMotor = None
rightRearMotor = None
```
9. **Finished Code**:
```python
#!/usr/bin/env python3
#
# Copyright (c) FIRST and other WPILib contributors.
# Open Source Software; you can modify and/or share it under the terms of
# the WPILib BSD license file in the root directory of this project.
#

import wpilib
import phoenix5
import commands2
from commands2 import Command
from commands2 import Subsystem

gameControllerPort = None
joystickOnePort = None
joystickOnePort = None

gameControllerOne = None
joystickOne = None
joystickTwo = None

encoder = None
encoderChannelA = None
encoderChannelB = None

LFMCPort = None
LRMCPort = None
RFMCPort = None
RRMCPort = None

leftFrontMotor = None
leftRearMotor = None
rightFrontMotor = None
rightRearMotor = None

class MyRobot(wpilib.TimedRobot):
    def robotInit(self):
        pass

    def autonomousInit(self):
        pass

    def autonomousPeriodic(self):
        pass

    def teleopInit(self):
        pass

    def teleopPeriodic(self):
        pass

    def testInit(self):
        pass
    def testPeriodic(self):
        pass


if __name__ == "__main__":
    wpilib.run(MyRobot)
``` 
10. You are all caught up!
