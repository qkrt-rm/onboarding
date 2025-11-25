- [Introduction](#introduction)
- [Cloning Starter Code](#cloning-starter-code)
- [Step 1: Flywheel Motors](#step-1-flywheel-motors)
  - [flywheel\_subsystem.hpp](#flywheel_subsystemhpp)
  - [flywheel\_subsystem.cpp](#flywheel_subsystemcpp)
- [Step 2: Flywheel On](#step-2-flywheel-on)
  - [flywheel\_on\_command.hpp](#flywheel_on_commandhpp)
  - [flywheel\_on\_command.cpp](#flywheel_on_commandcpp)
- [Step 3:](#step-3)
  - [ControlOperatorInterface](#controloperatorinterface)




## Introduction
By this point, you should have already completed the Tank Drive tutorial and gained a basic understanding of how the Taproot framework works. The purpose of this flywheel tutorial is to give new members a clear, practical understanding of how our robot’s flywheel system works and how to operate it effectively. Flywheels rely on stored rotational energy to launch projectiles with speed and consistency, and their performance depends heavily on motor control, tuning, and mechanical setup. In this guide, we’ll break down the core concepts, explain the hardware and software involved, and walk through the steps needed to configure, test, and refine a reliable flywheel system for competition.

## Cloning Starter Code

Please clone the following code:
```bash
mkdir FlyWheels
cd FlyWheels

git clone --recursive https://github.com/qkrt-rm/qkrt-mcb-2024.git
```

After your project has finished downloading, we’ll use Git to switch to the correct branch.
```bash
cd qkrt-mcb-2024
```

The git branch command shows which branch you're currently on.
The git switch command below will create a new branch based on the blank starter code and switch you to it.
Make sure to replace YOUR_INITIALS with your own initials..

```bash
git branch -a
git switch -c flywheel_tut_YOUR_INITALS flywheel_tut_blank
```

Change directory into tank-drive and open Visual Studio Code using the following commands:
```bash
code .
```



## Step 1: Flywheel Motors
Get the motors which use the PWM (Pulse Width Modulation)


### flywheel_subsystem.hpp
```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#pragma once

#include "tap/control/subsystem.hpp"
#include "tap/util_macros.hpp"

#include "tap/communication/gpio/pwm.hpp"

class Drivers;

namespace control
{
namespace flywheel
{

class FlywheelSubsystem : public tap::control::Subsystem
{
public:
    FlywheelSubsystem(Drivers& drivers);
        
    ~FlywheelSubsystem() = default;

    void initialize() override;

    void setDesiredOutput(float output);

    void refresh() override;

private:
    // Use gpio to access the pwm connectors
    static constexpr float MAX_SNAIL_OUTPUT = 0.50f;    
    static constexpr float MIN_SNAIL_OUTPUT = 0.25f;    

};

}  
}  
```


<details>
<summary>Solution</summary>

flywheel_subsystem.hpp

```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#pragma once

#include "tap/control/subsystem.hpp"
#include "tap/util_macros.hpp"

#include "tap/communication/gpio/pwm.hpp"

class Drivers;

namespace control
{
namespace flywheel
{

class FlywheelSubsystem : public tap::control::Subsystem
{
public:
    FlywheelSubsystem(Drivers& drivers);
        
    ~FlywheelSubsystem() = default;

    void initialize() override;

    void setDesiredOutput(float output);

    void refresh() override;

private:
    static constexpr tap::gpio::Pwm::Pin FLYWHEEL_MOTOR_PIN1 = tap::gpio::Pwm::C1;
    static constexpr tap::gpio::Pwm::Pin FLYWHEEL_MOTOR_PIN2 = tap::gpio::Pwm::C2;
    static constexpr tap::gpio::Pwm::Pin FLYWHEEL_MOTOR_PIN3 = tap::gpio::Pwm::C3;
    static constexpr tap::gpio::Pwm::Pin FLYWHEEL_MOTOR_PIN4 = tap::gpio::Pwm::C4;
    static constexpr float MAX_SNAIL_OUTPUT = 0.50f;    
    static constexpr float MIN_SNAIL_OUTPUT = 0.25f;    

};

}  
}  
```

</details>


### flywheel_subsystem.cpp

flywheel_subsystem.cpp
```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#include "flywheel_subsystem.hpp"

#include "tap/communication/serial/remote.hpp"
#include "drivers.hpp"

namespace control::flywheel
{
FlywheelSubsystem::FlywheelSubsystem(Drivers& drivers)
    : tap::control::Subsystem(&drivers)
{
}
        
//Make the FlywheelSubsystem initialize, refresh, and setDesiredOutput functions




}  // control
```


<details>
<summary> Solution: </summary>

```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#include "flywheel_subsystem.hpp"

#include "tap/communication/serial/remote.hpp"
#include "drivers.hpp"

namespace control::flywheel
{
FlywheelSubsystem::FlywheelSubsystem(Drivers& drivers)
    : tap::control::Subsystem(&drivers)
{
}
        
void FlywheelSubsystem::initialize() { 
    drivers->pwm.write(0.25f, FLYWHEEL_MOTOR_PIN1);
    drivers->pwm.write(0.25f, FLYWHEEL_MOTOR_PIN2);
    drivers->pwm.write(0.25f, FLYWHEEL_MOTOR_PIN3);
    drivers->pwm.write(0.25f, FLYWHEEL_MOTOR_PIN4);
}

void FlywheelSubsystem::refresh() {}

void FlywheelSubsystem::setDesiredOutput(float output) {
    drivers->pwm.write(output, FLYWHEEL_MOTOR_PIN1);
    drivers->pwm.write(output, FLYWHEEL_MOTOR_PIN2);
    drivers->pwm.write(output, FLYWHEEL_MOTOR_PIN3);
    drivers->pwm.write(output, FLYWHEEL_MOTOR_PIN4);
    drivers->leds.set(tap::gpio::Leds::Green, true);
}

}  // control
```

</details>


## Step 2: Flywheel On
### flywheel_on_command.hpp
```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#pragma once

#include "tap/control/command.hpp"

#include "flywheel_subsystem.hpp"

namespace control
{
class ControlOperatorInterface;
}

namespace control
{
namespace flywheel
{
class FlywheelOnCommand : public tap::control::Command
{
public:
    FlywheelOnCommand(FlywheelSubsystem *sub, ControlOperatorInterface &operatorInterface, float flywheel_speed)
        : flywheel(sub), operatorInterface(operatorInterface)
    {
        addSubsystemRequirement(sub);
        spinning_pwm = flywheel_speed;
    }

    void initialize() override;

    void execute() override;

    void end(bool interrupted) override;

    bool isFinished() const override;

    const char *getName() const override { return "flywheel on command"; }

private:
    FlywheelSubsystem *flywheel;
    ControlOperatorInterface& operatorInterface;
    float spinning_pwm;
    static constexpr float OFF_PWM = 0.25f;

};  // class FlywheelOnCommand
}  // namespace flywheel
}  // namespace control
```


### flywheel_on_command.cpp
```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#include "flywheel_on_command.hpp"

#include "tap/control/command.hpp"

#include "flywheel_subsystem.hpp"

#include "tap/communication/gpio/leds.hpp"

#include "control/control_operator_interface.hpp"

namespace control
{
namespace flywheel
{

// Add code here
//For initialize, execute, and end functions


}  // namespace flywheel
}  // namespace control
```




<details>
<summary>Solution</summary>

```cpp
/*
 * Copyright (c) 2020-2021 Queen's Knights Robotics Team
 *
 * This file is part of qkrt-mcb.
 *
 * qkrt-mcb is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * qkrt-mcb is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with qkrt-mcb.  If not, see <https://www.gnu.org/licenses/>.
 */

#include "flywheel_on_command.hpp"

#include "tap/control/command.hpp"

#include "flywheel_subsystem.hpp"

#include "tap/communication/gpio/leds.hpp"

#include "control/control_operator_interface.hpp"

namespace control
{
namespace flywheel
{
void FlywheelOnCommand::initialize() {}

void FlywheelOnCommand::execute() 
{    
    operatorInterface.pollInputDevices();

    if (operatorInterface.getFlyWheelInput())
        flywheel->setDesiredOutput(spinning_pwm);
    else
        flywheel->setDesiredOutput(OFF_PWM); 
}

void FlywheelOnCommand::end(bool) { flywheel->setDesiredOutput(0.25f); }

bool FlywheelOnCommand::isFinished() const { return false; }
}  // namespace flywheel
}  // namespace control
```
</details>

## Step 3: 
### ControlOperatorInterface
As you remember from the tank drive tutorial, we need need to add the flywheel controls to ControlOperatorInterface.hpp and ControlOperatorInterface.cpp.


