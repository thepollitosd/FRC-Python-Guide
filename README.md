# FRC-Python-Guide (for Team 5025)

## Getting Started (A 10 Step Guide)

1. Install Python:
    1. Select the link for your OS: [Windows](https://www.python.org/downloads/windows/) | [MacOS](https://www.python.org/downloads/macos/) | [Linux](https://www.python.org/downloads/source/)
    2. Under Python Releases for `[Your Operating System]`, click `Latest Python 3 Release - Python 3.13.3`. Any new version will work.
    3. Open the file, and follow the setup instructions.
2. Open the shell/terminal by searching in your operating system's search bar. The name for Windows is Command Prompt, and the name for MacOS is Terminal. In Linux, you need to do the keyboard shortcut `ctr + alt + t`.
3. Install or Upgrade RobotPy

- If you don't have RobotPy, type in `py  -3  -m  pip  install  --upgrade  robotpy`.
- If you do have RobotPy, type in `py  -3  -m  pip  install  --upgrade  robotpy`.

4. To start a project, type in `mkdir [Your Project Name Here]` to create the folder
5. Next, type in `cd [Your Project Name Here]` to navigate to the folder
6. To create the necessary files, type in `py  -3  -m  robotpy  init`. This will create `robot.py` and `pyproject.toml` files. You will write most of the code in `robot.py`, but for now, we will use pyproject.toml.
7. Open pyproject.toml, and uncomment all requisites. Your code should look like this:

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

8. Copy this starter code, and paste it in `robot.py`:

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

9. We need to set some constants for our ports and we need to import some libraries. To do this, write this code below `import wpilib`:

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
