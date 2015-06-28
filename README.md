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

For using the Nucelo F334 you need at least version 0.9.0

#### GDB
* Debian Users: `sudo apt-get install gdb-arm-none-eabi`
* Mac users might want to use Mac Ports with `port install arm-none-eabi-gdb configure.compiler=gcc`

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

### Complete Templates

For some chips, the Eclipse Plugin provides template projects that configure everything for you. Go to `New > C Project > STM32XX...` and try your luck.

### Abstract Templates

If there is not a complete template for your chip, you can create your project based on the more general Cortex-M template. Select chup frequency and memory sizes and fill in your device name as `Vendor CMSIS name`

In this state, your project is still missing the device specify information (peripherals and some stuff that touches the cortex like interrupt vectors). This information is provided by vendors as header and source files. You should find them online (for STM for example, you'll find and overview [http://www.st.com/stonline/stappl/productcatalog/app?page=partNumberSearchPage&levelid=SC1169&parentid=2004&resourcetype=SW](here))

First look for CMSIS header and source files and copy them in the right place in your project directory. Provided you entered `stm32f3xx` as the device name in the project wizard:

`System > Include > CMSIS`
	system_stm32f3xx.h
	stm32f3xx.h
	complete_device_name.h
		
`System > Source > CMSIS > vectors_stm32f3xx.h`
	Here, you need to explicity paste the vector table in the correct format and create default interrupt handlers

`ldscripts > mem.ld`
	Something like this: 
		
    MEMORY
    {
    FLASH (rx)      : ORIGIN = 0x08000000, LENGTH = 64K
    RAM (xrw)       : ORIGIN = 0x20000000, LENGTH = 12K
    CCMRAM (rw)     : ORIGIN = 0x10000000, LENGTH = 4K
    }
    
To automatically choose the correct header files on build, add a define with your complete device name in the build settings. To test if things work, check if the correct header file is included from `stm32f3xx.h`

## Usage

You now upload the hex file by selecting the active project and then clicking on external tools or debug it by clicking on the debug button

Select device description files to be able to see peripheral registers when debugging:
`Project Properties > C/C++ Build > Settings > Devices`

