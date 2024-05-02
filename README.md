# XMCode: Extended Machine Code

XMCode (Extended Machine Code) is a next-generation machine control format designed to provide a flexible and extensible way to configure and control various types of machines, including CNC machines, 3D printers, laser cutters, and robotic arms. It aims to address the limitations of traditional gcode and offer a more structured and readable format for machine control.

## Project Overview

The XMCode project consists of two main components:

1. **Settings JSON**: A comprehensive machine configuration file that defines the machine's capabilities, limitations, and settings. It includes information about axes, tooling, custom commands, and various machine-specific parameters.

2. **XMCode JSON**: A machine control file that contains the actual commands and parameters for controlling the machine. It uses a human-readable format and supports advanced features like parameter validation and asynchronous command execution.

The goal of XMCode is to provide a standardized and extensible format that can be easily adapted to different machines and use cases. It aims to simplify the process of configuring and controlling machines, while also enabling more advanced functionality and flexibility compared to traditional gcode.

## Settings JSON

The settings JSON file is responsible for defining the machine's configuration and capabilities. It includes the following main sections:

1. **Axes**: Defines the properties and settings for each axis of the machine.
   - Motor type: Specifies the type of motor used for each axis (e.g., stepper, servo).
   - Drive type: Indicates the type of drive mechanism used for each axis (e.g., leadscrew, belt).
   - Range of motion: Defines the minimum and maximum limits for each axis, along with an enable/disable flag for hard limits.
   - Soft limits: Specifies the soft limits for each axis, which are used to restrict movement within a safer range, along with an enable/disable flag.
   - Homing direction: Indicates the direction of homing movement for each axis.
   - Homing speed: Specifies the speed at which homing is performed for each axis.
   - Limit switches: Defines the properties of limit switches for each axis, including enable/disable flag, triggered state, and last triggered time.

2. **Tooling**: Specifies the available tools and their associated settings.
   - Mill:
     - Maximum RPM: Defines the maximum rotational speed of the mill.
     - Horsepower: Specifies the power rating of the mill.
     - Commands: Defines the available commands for the mill, such as on, off, and adjust speed, along with parameter validation and async flag.
   - Laser:
     - Maximum power: Specifies the maximum power output of the laser.
     - Wavelength: Indicates the wavelength of the laser.
     - Commands: Defines the available commands for the laser, such as on, off, and set power, along with parameter validation and async flag.
   - 3D Printer:
     - Maximum temperature: Specifies the maximum temperature the 3D printer can reach.
     - Nozzle diameter: Defines the range of supported nozzle diameters.
     - Filament diameter: Indicates the diameter of the filament used.
     - Bed Leveling:
       - Enable/disable flag: Allows enabling or disabling bed leveling.
       - Grid size: Specifies the grid size used for bed leveling.
       - Last leveled time: Indicates the timestamp of the last bed leveling process.
       - Command: Defines the custom command for performing bed leveling.
     - Commands: Defines the available commands for the 3D printer, such as extrude, retract, and set temperature, along with parameter validation and async flag.

3. **Custom Commands**: Allows defining custom commands that are not specific to any tooling.
   - Command name: Specifies the name of the custom command.
   - Function: Defines the function to be executed when the command is called.
   - Parameters: Specifies the parameters required for the command, including their types and ranges.
   - Async flag: Indicates whether the command should be executed asynchronously.

4. **Power-on Setup**: Defines the initial setup routine when the machine is powered on.
   - Enable/disable flag: Allows enabling or disabling the power-on setup routine.
   - Homing sequence: Specifies the order in which axes should be homed during the power-on setup.

5. **User Settings**: Includes user-specific settings.
   - Timezone: Specifies the timezone settings for the user.

The settings JSON file serves as a configuration template for the machine and can be easily modified to accommodate different machine types and configurations.

## XMCode JSON

The XMCode JSON file contains the actual commands and parameters for controlling the machine. It follows a structured format and includes the following main sections:

1. **Axes**: Specifies the movement commands for each axis.
   - Target position: Defines the desired position for each axis.
   - Acceleration: Specifies the acceleration value for each axis movement.
   - Velocity: Indicates the velocity at which each axis should move.

2. **Tooling**: Defines the commands and parameters for the selected tooling.
   - Mill:
     - Command: Specifies the command to be executed, such as on, off, or adjust speed.
     - Parameters: Provides the necessary parameters for the command, such as RPM for adjust speed.
   - Laser:
     - Command: Specifies the command to be executed, such as on, off, or set power.
     - Parameters: Provides the necessary parameters for the command, such as power value for set power.
   - 3D Printer:
     - Command: Specifies the command to be executed, such as extrude, retract, or set temperature.
     - Parameters: Provides the necessary parameters for the command, such as length for extrude/retract or temperature for set temperature.

3. **Custom Commands**: Allows executing custom commands defined in the settings JSON file.
   - Command name: Specifies the name of the custom command to be executed.
   - Parameters: Provides the necessary parameters for the custom command.

4. **Async Flag**: Indicates whether the command should be executed asynchronously or not.

The XMCode JSON file is designed to be human-readable and easy to generate programmatically. It supports parameter validation and error handling based on the constraints defined in the settings JSON file.

## Usage

To use XMCode in your machine control project:

1. Create a settings JSON file that defines your machine's configuration and capabilities.

2. Generate XMCode JSON files containing the desired commands and parameters for controlling your machine.

3. Develop a machine control software that can parse the settings JSON and XMCode JSON files, validate the commands and parameters, and execute them on your machine.

4. Integrate the XMCode format into your existing workflow or use it as a foundation for building new machine control systems.

## Contributing

Contributions to the XMCode project are welcome! If you have any ideas, suggestions, or bug reports, please open an issue or submit a pull request on the project's GitHub repository.

## License

The XMCode project is released under the [GNU General Public License v3.0](LICENSE).
