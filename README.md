![image](images/microchip.jpg) 

## MCLV-48V-300W dsPIC33CK256MP508 AN1078

## 1. INTRODUCTION
<p style='text-align: justify;'>
This document describes the setup requirements for running the Sensorless FOC algorithm using a Sliding Mode Observer, which is referenced in AN1078 “Sensorless Field Oriented Control of a PMSM” using a MCLV-48V-300W Inverter Board and dsPIC33CK256MP508 Motor Control Dual In-line Module (DIM).</p>



## 2.	SUGGESTED DEMONSTRATION REQUIREMENTS

### 2.1 Motor Control Application Firmware Required for the Demonstration
To clone or download this application from Github, go to the [main page of this repository](https://github.com/microchip-pic-avr-solutions/mclv-48v-300w-an1078) and then click Clone button to clone this repository or download as zip file.
> **_NOTE:_**
>In this document, hereinafter this firmware package is referred as firmware.
### 2.2 Software Tools Used for Testing the firmware

- MPLAB® X IDE v5.50 
- MPLAB® XC16 Compiler v1.70
- MPLAB® X IDE Plugin: X2C-Scope v1.30 
- DFP: dsPIC33CK-MP_DFP v1.6.176
> **_NOTE:_**
>The software used for testing the firmware prior to release is listed above. It is recommended to use the version listed above or later versions for building the firmware.
### 2.3 Hardware Tools Required for the Demonstration
- MCLV-48V-300W Inverter Board (EV18H47A)
- 	dsPIC33CK256MP508 Motor Control DIM (EV62P66A)
- 24V Power Supply [(AC002013)](https://www.microchipdirect.com/dev-tools/AC002013)
- 24V 3-Phase Brushless DC Motor [(AC300020)](https://www.microchip.com/en-us/development-tool/AC300020)
  <br />
> **_NOTE:_**
> All items listed under the section Hardware Tools Required for the Demonstration are available at [microchip DIRECT](https://www.microchipdirect.com/)

## 3. HARDWARE SETUP
<p style='text-align: justify;'>This section describes hardware setup required for the demonstration.</p>

1. <p style='text-align: justify;'> Motor currents are amplified on the MCLV-48V-300W Inverter Board; it can also be amplified by the amplifiers internal to the dsPIC33CK256MP508 populated on the DIM. By default, the firmware and DIM are configured to sample and convert internal amplifier outputs ('internal op-amp configuration'), measuring the motor currents needed for implementing FOC.</p>

     <p style='text-align: justify;'> The Table-1 summarizes the resistors to be populated and removed to convert the DIM from internal op-amp configuration to external op-amp configuration or vice versa.</p>

<p align="left" >
 <img  src="images/Tableopamp.png"></p>




2. <p style='text-align: justify;'> Insert the dsPIC33CK256MP508 Motor Control DIM into the DIM Interface Connector J8 provided on the MCLV-48V-300W Inverter Board. Make sure the DIM is placed correctly and oriented before going ahead.</p>

    <p align="left">
    <img  src="images/dimconnected.PNG"></p>


3. <p style='text-align: justify;'> Connect the three phase wires from the motor to PHA, PHB, and PHC terminals of connector J14(there is no specific order) provided on the MCLV-48V-300W Inverter Board.</p>
    <p align="left">
      <img  src="images/motorconnection.png"></p>

4. <p style='text-align: justify;'>	Plug in the 24V power supply to connector J1 provided on the MCLV-48V-300W Inverter Board. Alternatively, the Inverter Board can also be powered through Connector J3.</p>
      <p align="left">
      <img  src="images/mclvpower.png"></p>
 

 5.	<p style='text-align: justify;'>The board has an onboard programmer ‘PICkit™ On Board (PKoB4)’ , which can be used for programming or debugging the dsPIC33CK256MP508. To use an on-board programmer, connect a micro-USB cable between Host PC and Connector J16 provided on the MCLV-48V-300W Inverter Board.</p>


      <p align="left">
     <img  src="images/mclvpkob4.png"></p>

 6.	<p style='text-align: justify;'>Alternatively, the device can also be programmed using the programmer/debugger (MPLAB® PICkit™ 4 In-Circuit Debugger - PG164140) by interfacing it through connector J9 of the MCLV-48V-300W Inverter Board as shown below. Ensure that the programmer is oriented correctly before proceeding.</p> 

      <p align="left">
       <img  src="images/mclvprogramming.PNG"></p>
 
<br />

## 4. SOFTWARE SETUP AND RUN
### 4.1 Setup: MPLAB X IDE and MPLAB XC16 Compiler

Install MPLAB X IDE and MPLAB XC16 Compiler versions that support the device dsPIC33CK256MP508 and PKoBv4. The MPLAB X IDE, MPLAB XC16 Compiler, and X2C-Scope plug-in used for testing the firmware are mentioned in the [Motor Control Application Firmware Required for the Demonstration](#21-motor-control-application-firmware-required-for-the-demonstration) section. To get help on  

- MPLAB X IDE installation, refer [link](https://microchipdeveloper.com/mplabx:installation)
- MPLAB XC16 Compiler installation steps, refer [link](https://microchipdeveloper.com/xc16:installation)

<p style='text-align: justify;'>If MPLAB IDE v8 or earlier is already installed on your computer, then run the MPLAB driver switcher (It is installed when MPLAB®X IDE is installed) to switch from MPLAB IDE v8 drivers to MPLAB X IDE drivers. If you have Windows 7 or 8, you must run MPLAB driver switcher in ‘Administrator Mode’. To run the Device Driver Switcher GUI application as administrator, right click on the executable (or desktop icon) and select ‘Run as Administrator’. For additional details refer MPLAB X IDE help topic <i>“Before You Begin: Install the USB Device Drivers (For Hardware Tools): USB Driver Installation for Windows Operating Systems”</i>. </p>

### 4.2  X2C-Scope
<p style='text-align: justify;'>
X2C-Scope is a MPLAB X IDE plugin that allows a developer to interact with an application while the application program is running. X2C-Scope enables you to read, write, and plot global variables (for motor control) in real time. It communicates with the target using the UART. To use X2C-Scope, the plugin must be installed:</p>

- In MPLAB X IDE, select <i>Tools>Plugins</i> and click on the Available Plugins tab.
- Select X2C-Scope plug-in by checking its check box, and then click Install.
- Look for tool X2C-Scope under <i>Tools>Embedded.</i>

<p align="left">
  <img  src="images/x2cscopeconfiguration.png"></p>
 
<br />

## 5.  BASIC DEMONSTRATION
### 5.1 Firmware Description

The firmware version needed for the demonstration is mentioned under the [Motor Control Application Firmware Required for the Demonstration](#21-motor-control-application-firmware-required-for-the-demonstration) section.
<p style='text-align: justify;'>
This firmware is implemented to work on Microchip’s 16-bit Digital signal controller (dsPIC® DSC) dsPIC33CK256MP508. 
For more information, see the dsPIC33CK256MP508 Family datasheet (DS70005349).</p>
<p style='text-align: justify;'>
The Motor Control Demo application uses push button to start or stop the motor and potentiometer to vary speed of the motor.This Motor Control Demo Application configures and uses peripherals like PWM, ADC, UART etc.</p>

<p style='text-align: justify;'>

For more details refer Microchip Application note AN1078 “Sensorless Field Oriented Control of a PMSM” and AN1299 “Single-Shunt Three-Phase Current Reconstruction Algorithm for Sensorless FOC of a PMSM” available at [Microchip web site](https://www.microchip.com/). </p>

> **_NOTE:_**
> The project may not build correctly in Windows OS if Maximum path length of any source file in the project is more than 260 characters. In case absolute path is exceeding or nearing maximum length, do any (or both) of the following:
> - Shorten the directory name containing the firmware used in this demonstration. If you renamed the directory, consider the new name while reading the instructions provided in the upcoming sections of the document.
> - Place firmware in a location, such that absolute path length of each file included in the projects does not exceed the Maximum Path length specified. 
Refer to MPLAB X IDE help topic <i>“Path, File, and Folder Name Restrictions”</i> for details.

### 5.2 Basic Demonstration
<p style='text-align: justify;'>
Follow below instructions step by step to setup and run the motor control demo application:</p>

1. <p style='text-align: leftjustify;'> Start MPLAB X IDE and open<span style="font-family:Courier New; font-size:;"> (File>Open Project)</span> the project <span style="font-family:Courier New; font-size:;">pmsm.X</span> with device selection dsPIC33CK256MP508.</p>
    <p align="left">
       <img  src="images/idedeviceselection.png"></p>
  

2. <p style='text-align: leftjustify;'> Set the project <span style="font-family:Courier New; font-size:;">pmsm.X </span>as main project by right clicking on the project name and selecting “Set as Main Project” as shown. The project <b>“pmsm”</b> will then appear in bold.</p>
    <p align="left">
     <img  src="images/ideprojectsetup.png"></p>
 

	
3. <p style='text-align: leftjustify;'> Open <span style="font-family:Courier New; font-size:;">userparams.h </span>(under<span style="font-family:Courier New; font-size:;"> pmsm.X -> headerfiles)</span> in the project <span style="font-family:Courier New; font-size:;">pmsm.X</span> </p>
     <p style='text-align: leftjustify;'>
- Ensure that <span style="font-family:Courier New; font-size:;">TUNING, OPEN_LOOP_FUNCTIONING, and TORQUE_MODE </span>are not defined.
      <p align="left"><img  src="images/configParam.png"></p>
- When internal amplifiers are used for current amplification (referred as <b>‘internal op amp configuration’</b>) then<b> define</b> <span style="font-family:Courier New; font-size:;">INTERNAL_OPAMP_CONFIG</span>.
        <p align="left"> <img  src="images/internalopampconfig.png"></p>
       Otherwise if external amplifiers are used for current amplification (referred as <b>‘external op amp Configuration’</b>) then <b>undefine </b>the macro <span style="font-family:Courier New; font-size:;">INTERNAL_OPAMP_CONFIG</span> in <span style="font-family:Courier New; font-size:;"> userparams.h.</span></p>
        <p align="left">
      <img  src="images/externalopampconfig.png"></p>
      
      
   
   
> **_NOTE:_**
>The motor phase currents can be reconstructed from the DC Bus current by appropriately sampling it during the PWM switching period, called a single-shunt reconstruction algorithm. The firmware can be configured to demonstrate the single shunt reconstruction algorithm by defining the macro<span style="font-family:Courier New; font-size:;">‘SINGLE_SHUNT’</span> in the header file <span style="font-family:Courier New; font-size:;"> userparams.h </span><br>
>For additional information, refer to Microchip application note <b>AN1299, “Single-Shunt Three-Phase Current Reconstruction Algorithm for Sensorless FOC of a PMSM.”</b> <br>
>By default, the firmware uses phase currents measured across the phase shunt resistors on two of the half-bridges of the three-phase inverter (‘dual shunt configuration’) to implement FOC.


4. Right click on the project <i>pmsm.X</i> and select “Properties”  to open its Project Properties Dialog.Click the “Conf: [default]” category to reveal the general project configuration information. The development tools used for testing the firmware are listed in the section [2.2 Software Tools Used for Testing the firmware](#22-software-tools-used-for-testing-the-firmware).
   <p style='text-align: justify;'>
    In the <b><i>‘Conf: [default]’</i></b> category window: 
    <p style='text-align: justify;'>

 - Select the specific Compiler Toolchain from the available list of compilers. Please ensure MPLAB® XC16 Compiler supports the device dsPIC33CK256MP508.In this case, “XC16(v1.70)” is selected.
      <p style='text-align: justify;'>
 - Select the Hardware Tool to be used for programming and debugging. 
       <p style='text-align: justify;'>
-	Select the specific Device Family Pack (DFP) from the available list of Packs. In this case, “dsPIC33CK-MP_DFP 1.6.176” is selected.     
 -   After selecting Hardware Tool and Compiler Toolchain, click button <b>Apply</b>
        <p align="left">
        <img  src="images/projectpropertiessettings.png"></p>

5. <p style='text-align: justify;'> Ensure that the checkbox <b>“Load symbols when programming or building for production (slows process)”</b> is checked, which is under the “Loading” category of the Project Properties window.</p>        
        
      <p align="left">
      <img  src="images/loadvariables.png"></p>

6. <p style='text-align: justify;'>	 To build the project (in this case pmsm.X) and program the device dsPIC33CK256MP508, click <b>“Make and Program Device Main project”</b> on the toolbar.</p>
    <p align="left">
    <img  src="images/deviceprogramming.png"></p>
  
7. <p style='text-align: justify;'>	 	If the device is successfully programmed, <b>LD2 (‘LED1’)</b>  will be turned ON, indicating that the dsPIC® DSC is enabled. </p> 
    <p align="left">
     <img  src="images/led.png"></p>


8. <p style='text-align: justify;'> 	Run or stop the motor by pressing the push button <b>SW1</b>. The motor should start spinning smoothly in one direction in the ‘Normal Speed Range.’ Ensure that the motor is spinning smoothly without any vibration. The LED LD2 (‘LED1’) is turned ON to show the button is pressed to start the motor </p>
     <p align="left">
     <img  src="images/pushbuttons.png"></p>
 

9.  <p style='text-align: justify;'> The motor speed can be varied using the potentiometer (labeled “POT1”).</p>
    <p align="left">
    <img  src="images/potentiometer.png"></p>

 
10.	<p style='text-align: justify;'>To enter the extended speed range (NOMINAL_SPEED_RPM to MAXIMUM_SPEED_RPM) press the push button <b>SW2</b>. Press the push button <b>SW2</b> again to revert the speed of the motor to its normal speed (END_SPEED_RPM to NOMINAL_SPEED_RPM) range. </p>
      <p align="left">
     <img  src="images/stopButton.png"></p>
  

11. <p style='text-align: justify;'>	Press the push button <b>SW1</b> to stop the motor.</p>


>**_NOTE:_**
>The macro definitions END_SPEED_RPM, NOMINAL_SPEED_RPM, and MAXIMUM_SPEED_RPM are specified in userparms.h file included in the project pmsm.X. The definitions NOMINAL_SPEED_RPM, and MAXIMUM_SPEED_RPM are defined as per the specification provided by the Motor manufacturer. Exceeding manufacture specification may lead to damage of the motor or(and) the board. 

## 5.3  Data visualization through X2C-Scope Plug-in of MPLABX
<p style='text-align: justify;'>
 X2C-Scope is a third-party plug-in for MPLAB X, which helps in real-time diagnostics. The application firmware comes with the initialization needed to interface controller with the host PC to enable data visualization through X2C-Scope plug-in.</p>

1. Ensure X2C-Scope Plug-in is installed. For additional information on how to set up a plug-in refer [https://microchipdeveloper.com/mplabx:tools-plugins-available](https://microchipdeveloper.com/mplabx:tools-plugins-available)
 
2.	To establish serial communication with the host PC, connect a micro-USB cable between the host PC and the MCLV-48V-300W Inverter Board (connector J16). This interface is also used for programming.


3. Ensure application is configured and running as described under Section [Basic Demonstration](#5-basic-demonstration   ) by following steps 1 through 11.

 

4. Open the X2C-Scope window by selecting <span style="font-family:Courier New; font-size:;">Tools>Embedded>X2CScope.</span></p>
      <p align="left">
       <img  src="images/x2cselection.png"></p>
 

5. Open the X2C-Scope Configuration window and in <b>“Select project”</b> menu, select <b>pmsm</b> project as shown.
    <p align="left">
    <img  src="images/x2cprojectselection.png"></p>

6.	Serial communication needs to be set up, as shown in the following figure. Ensure the communication baud rate is set to 115200 as configured in the application firmware. The COM port used depends on the system settings. The <span style="font-family:Courier New; font-size:;">refresh button</span> lists the available COM Ports. Select the COM Port as per the connection.

    <p align="left">
     <img  src="images/x2cconnectionsetup.png"></p>
 


7. Once the COM port is detected, click on “Disconnected” and turn to “Connected”, to establish a serial communication between Host PC and the board.
     <p align="left">
    <img  src="images/x2cconnectionbutton.png"></p>


8. Set the “Project Setup” as shown below and click “Set Values”. Set Scope sample time as interval at which <span style="font-family:Courier New; font-size:1;">X2CScopeUpdate()</span> is called. In this application it is every 50µs.
      <p align="left">
      <img  src="images/x2cprojectsetup.png"></p>


9. When the setup is established, click on open scope View (under sub window “Data Views”), this opens 'Scope Window'.
     <p align="left">
      <img  src="images/x2cdataview.png"></p>
    	     

10. In this window, select the variables that needs to be monitored. To do this, click on the source against each channel, a window Select Variables opens upon the screen. From the available list, the required variable can be chosen. Ensure check boxes Enable & Visible are checked for the variables to be plotted.<br>
To view data plots continuously, uncheck<span style="font-family:Courier New; font-size:1;"> Single-shot</span>. When <span style="font-family:Courier New; font-size:1;">Single-shot</span> is checked it captures the data once and stops. The Sample time factor value multiplied with Sample time determines the time difference between any two consecutive data points on the plot.
    <p align="left">
    <img  src="images/x2cdatapointselection.png"></p>

11.	Click on SAMPLE, then X2C-Scope window shows variables in real time, which is updated automatically.
     <p align="left">
     <img  src="images/x2csample.png"></p>
 

12.	Click on ABORT to stop.
     <p align="left">
     <img  src="images/x2cabort.png"></p>
 
 ## 6. REFERENCES:
For additional information, refer following documents or links.
1. AN1078 Application Note “Sensorless Field Oriented Control of a PMSM”
2. AN1299 Application Note “Single-Shunt Three-Phase Current Reconstruction Algorithm for Sensorless FOC of a PMSM”
3. MCLV-48V-300W Inverter Board User’s Guide 
4. dsPIC33CK256MP508 Family datasheet (DS70005349).
5. Family Reference manuals (FRM) of dsPIC33CK256MP508 family
6. MPLAB® X IDE User’s Guide (DS50002027) or MPLAB® X IDE help
7. [MPLAB® X IDE installation](http://microchipdeveloper.com/mplabx:installation)
8. [MPLAB® XC16 Compiler installation](http://microchipdeveloper.com/xc16:installation)







