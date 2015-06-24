# Bastl-ARM-Tools

## Install Tools

### Eclipse
* You will need a Version > 4.3 (Juno, Kepler, Luna...)
* Mac Users: Download and install [Binaries](http://eclipse.org/downloads/packages/eclipse-ide-cc-developers/lunasr2)
* Debian Users: `sudo apt-get install eclipse-cdt`

### Toolchain
* Mac Users: Follow the installation instructions on the [Official Website](http://gnuarmeclipse.livius.net/blog/toolchain-install/#OS_X)
* Debian Users: `sudo apt-get install gcc-arm-none-eabi`

### Debugger

#### OpenOCD
* Mac Users: Download and install the latest OpenOCD binary from [Sourceforge](http://sourceforge.net/projects/gnuarmeclipse/files/OpenOCD/OS%20X/)
* Debian Users: `sudo apt-get install openocd`

#### GDB
* Debian Users: `sudo apt-get install gdb-arm-none-eabi`

### Eclipse Plug-in
* Open Eclipse and select `Help > Install New Software`
* Paste `http://gnuarmeclipse.sourceforge.net/updates` and hit enter
* Uncheck `Contact all Update sites during install`
* Follow the further instructions to install the plugin

## Setup Eclipse

Start Eclipse and select the workspace you want to work in

### Save before build
`Window > Preferences > General > Workspace`

### Build shortcuts
`Window > Preferences > General > Keys`
`Ctrl + Alt + B` Build All
`Ctrl + B` Build Project

### Showing Peripheral Registers in Debug Perspective
* Set up path where you want to store the downloaded hardware description files in `Windows > Preferences > C/C++ > Packages`
* Switch to Packs-View and refresh
* Install latest version of STM32F429IDISCO

### Remember last Debug configuration
Set `Always launch the previously launched configuration` at `Window > Preferences > Run/Debug > Launching`

## Clone Repository

The content of this repository need to be placed inside your workspace in a folder called `Bastl-ARM-Tools`

## Create your project

Select the Wizard: `New > C Project > STM32XX...` and follow the instructions
You now upload the hex file by selecting the active project and then clicking on external tools or debug it by clicking on the debug button

Select device description files to be able to see peripheral registers when debugging:
`Project Properties > C/C++ Build > Settings > Devices`

