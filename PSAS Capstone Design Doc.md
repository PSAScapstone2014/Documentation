Capstone Team E – Spring/Summer 2014
PSAS PROJECT
Software Design Document

Date: (06/29/2014)

Software Design Document

#TABLE OF CONTENTS

1.	INTRODUCTION........................................1
2.	SYSTEM OVERVIEW.................................1
3.  SYSTEM ARCHITECTURE..........................3
4.	DATA DESIGN..........................................6
5. COMPONENT DESIGN...............................6
6.	REQUIREMENTS MATRIX...........................6
7. APPENDIX................................................9


##1.0	INTRODUCTION

###1.1	Purpose
PSAS, the Portland State Aerospace Society, is in search of a way to test their rocketry software without the need for hardware. They would like to simulate how the different software modules behave when controlling the flight of a rocket.

This document represents our most current design of the test system. It is designed as a reference and building block for an actual implementation of the desired software-testing framework. 
			
###1.2	Scope
The scope of this work is limited to creating a software testing framework and any necessary 
software to support the testing of PSAS software/firmware within that framework. This
project will not emulate any micro-controller.


##2.0. SYSTEM OVERVIEW

The system consists of a software testing framework (referred to from now on as just the framework)
capable of driving, coordinating, and running functional tests on the PSAS software, as well as
any auxiliary software needed to facilitate running any PSAS software. In particular, this auxiliary software will consist of the following: a port of the real-time operating system ChibiOS, software modules that substitute for hardware sensors, and a possible port for the lwIP stack.

###2.1	Constraints and Dependencies

•	No Unit Testing.  
•	The framework must be scriptable.  
•	The PSAS software modules will undergo functional testing only within the framework. This testing will be invoked at the end of the software build process.  
•	The Linux operating system must be a 64-bit flavor of Debian (Ubuntu for example).  
•	The minimum version of the gcc compiler used will be 4.8.  

###2.2	Resources
	•	PSAS subject matter experts Theo, Nathan and K. Wilson.  
	•	PSAS GitHub Repository.  
	•	Capstone GitHub Repository.  
	•	ChiobiOS forums and GitHub Repository  
	•	Capstone Team Members.  
	•	Meeting room in FAB-84.  
	•	Google hangout for team.  
	•	Team members and the computers they are using.  
	•	E-mail and phone numbers.  
	•	Requirements document  
	•	elderberry (the code generator)  
	•	telemetry viewer  

	
##3.0. SYSTEM ARCHITECTURE

###3.1	Architectural Design
		
This is a high-level description of the parts of the project.
	
####3.1.1		User Interface
		
The user interface is the terminal/shell command line in Linux. The chosen shell must support the running of the build process and the framework. The interface to the framework is a text editor run from a command line. Which text editor to use is up to the user. However, the text editor used must not inject additional characters for formatting.

####3.1.2		Framework 

At this writing, the basis for the framework has not been decided. While it is possible to write such a framework from scratch within the c language, an ‘off the shelf’ solution would simplify and speed up the development. An example of such a solution may be the scripting language Tcl (Tool Control Language).

Regardless of where the framework comes from, it must permit the PSAS user to decide, programmatically through a configuration file read by the framework, which components to test, and how to test them. Which configuration file to use is a command line argument to starting the framework.

While the framework can be run from the command line directly, it must also be able to be called from within a makefile.
			
####3.1.3		HAL Port
		
The ChibiOS part of the port appears to compile and run. But what is missing from the port is the HAL. Below is a list of HAL drivers that need to be supplied as a minimum. Additional drivers may be added as time allows.

#####3.1.3.1	PAL

#####3.1.3.2	SPI

#####3.1.3.3  	I2C

#####3.1.3.4	Serial


####3.1.4 		Sensors
		
While physical sensors will not be used for this project, we still need data sources that will mimic the data streams from such devices in order to effectively test those ChiobiOS  related modules. These data sources will be individual processes running on Linux. The framework will spawn these additional processes per the configuration file. These processes are expected to read from data files as the source of their data (files specified in the configuration file.)

####3.1.5		Data Logging/Reporting
		
In addition to capturing the results from functional testing, all data exchanges between software modules opened by the framework will be captured to text files for later review.

####3.1.6		lwIP Port
		
In keeping with the spirit of trying to maintain conditions the same as in the real world, we will attempt to port the light weight IP stack to Linux. The lwIP stack is used on the microcontrollers used by PSAS. There may be a port already for this. However, if we have issues with this port, we may end up using standard sockets. This port will become part of the chibiOS port.

###3.2	Decomposition Description

The diagram PSAS has of their system looks like this:


![<Display Name>](<Website URL>)

Current design of how the framework will operate. All nodes are expected to reside on a single Linux system.



![<Display Name>](<Website URL>)

Note that the following modules that are on the PSAS graph are not present on the testing framework design: Elderberry, Packet, and Telemetry.  These can be added to the framework if needed, but Elderberry and Packet are not (as far as indicated) used during the functional testing phase of the software – that is, they are not used during launch. Further, they don’t appear to have objective means for test. The Telemetry module, however, used to monitor data from the rocket in flight, can be added. It just isn’t explicitly asked for.

###3.3	Design Rationale

The design is constrained by the need to have a scriptable solution for the framework, and the need to have a framework that can function both as a straight command line application and a functional test that can be invoked as part of a make process. A configuration file that the framework reads will facilitate turning on and off components and setting parameters such as where to send or find data. Regarding the ChibiOS port, we have no options but to port ChibiOS given that the microcontrollers that the flight computer relies on run ChibiOS.  


##4.0. DATA DESIGN

###4.1	Data Description
		
Data logs are kept of all data sent from one software process to another for later review. The data will be kept in CSV text files. The filenames will at least contain the name of the type of data inside and the time stamp. This will fulfill the data collection part of Requirement 3.2.1.  The framework is responsible for creating these files prior to their use.
	
While the exact format of the file header is to be determined, it should include the name of the framework script used, the date and time, and the source of the data.

The body of the file should contain column headers and values in chronological order. There will be a separate log file for each process that participates and generates or receives information. As mentioned above, all data will be comma separated.


##5.0. COMPONENT DESIGN  
###5.1   The ChibiOS/HAL Port
Written in GCC C.

At this writing it appears that the ChibiOS portion of the port (the POSIX-GCC port) compiles and runs. What is missing is the HAL portion.

We need only supply the high-level drivers  and a means of holding the ‘data’ for subsequent use.  

The following drivers are needed for start. Their description is based on the data files in PSAS GitHub (Path: ChibiOS-RT / os / hal / src). Each driver is in a separate file for compilation purposes. (Complete description of what functions are needed can be found in the existing code, which I will copy here.)

####5.1.1	Name: HAL.c  
 		Description: HAL Subsystem Code  
#####	5.1.1.1	<insert explicit function list>	


####5.1.3	Name: I2C.c  
				Description: I2C driver code  
				5.1.3.1  [insert explicit function list]  

####5.1.3	I2C.c
				Description: I2C driver code  
				5.1.3.1  [insert explicit function list]


####5.1.4	Name: SPI.c  
				Description: SPI driver code  
#####5.1.4.1  [insert explicit function list]  
			

####5.1.5	Name: Serial.c  
				Description: Serial driver macros and strucutures  
				5.1.5.1 [insert explicit function list]  


The ChibiOS port must compile and run as a separate process under Linux 64-bit. Successful completion of the HAL is part of this.

Regarding Requirement 3.1.6, our port must not alter core ChibiOS functionality. 
That is, if the user were to swap our ChibiOS port for a real microcontroller, the system should not break. 

###5.2   Sensors
There are two categories of sensor failure: faulty data, or no output signal at all. Sensor data failure simulation is accomplished by supplying a file with a specific error. The sensor should be able to pass on faulty values without error unless a total ‘failure’ condition is met. In other words, we need to be able to configure a software sensor to go dark within some interval (zero to infinity seconds). 
				
Written in gcc C.

####5.2.1	Name: genericSensor.c
			Description:	  	generic sensor module code
			5.2.1.1	main function: requires data filename, optional sleep timer value
					optional timeout value
			5.2.1.2	void readfile(); //reads the sensor data 
			5.2.1.3	void writeOut();	 //Outputs the sensor data to a socket


####5.3	   The Framework  
Created by using a scripting language (possibly Robot).  
#####5.3.1	Definition of Test.  
######5.3.1.1   Definition of Success  
######5.3.1.2	Definition of Failure  
#####5.3.4	Component Data Inputs and Data Outputs  
######5.3.4.1	Flight Computer  	
######5.3.4.2	ChibiOS Modules  
#######5.3.4.2.1 Sensor Module  
#######5.3.4.2.2 Rocket Hub Module    
#######5.3.4.2.3 Servo Module  
######5.3.4.3 Sensors/GPS  
#####5.3.5 Component Operations  
######5.3.5.1	Flight Computer  
5.3.5.2 ChibiOS Modules  
5.3.5.2.1 Sensor Module  
5.3.5.2.2 Rocket Hub Module  
5.3.5.2.3 Servo Module  
5.3.5.3 Sensors/GPS  
5.3.6	System Operation

###5.4	LWIP
If a port is to be created, it will be created in gcc C. 
						
At the time of this writing, it is unclear if we must create our own port of the lwIP stack. It is possible that such a port exists. If we can’t find such a port, or port lwIP ourselves, we will fall back on using standard sockets.


##6.0. REQUIREMENTS MATRIX

The following table matches functional requirement to design component. The usability requirements section of the requirements document guide the functionality built into the framework.
		

| Design Component| Requirement  |
|---------------|----------------|
| Row1 Cell1    |   3.1.1   |
| Row2 Cell1    |   3.1.2   |
| Row1 Cell1    |   3.1.3   |
| Row2 Cell1    |   3.1.4   |
| Row1 Cell1    |   3.1.5   |
| Row1 Cell1    |   3.1.6   |
| Row1 Cell1    |   3.1.7|
Configuration File, 

Configuration File,

The Framework, Sensors

ChibiOS Port, Framework, Sensors

ChibiOS/HAL Port

ChibiOS/HAL Port

The Framework

##7.0 APPENDIX  
###7.1 	Configuration File
	
The framework uses a configuration file that details which processes are to be started, initial conditions for those processes, how those processes transmit data, how those processes receive data, and any helper processes.

A partial example of such a file might be:

The design and the layout of the configuration file will be based on the design and layout of configuration files that the PSAS team is already familiar with.

[Module]
	Process: ChibiOS
	name: Sensor	
InPort: XXXX
OutPort:YYYY
Helper1: Sensor
Helper1 Name: Temperature
Helper1 Data: C:/sensor data/temperature1.txt
Helper1 Arg1: 0  #comment: this is delay between readings
Helper1 Arg2: 1000 #comment: seconds before stop
Helper1 Input : xxxxx #Where on process chibios does the data go?
.
.
.
.
HelperN: Sensor
HelperN Name: Pressure
HelperN Data: C:/sensor data/pressure1.txt
HelperN Arg1: 0  #comment: this is delay between readings
HelperN Arg2: 1000 #comment: seconds before stop
HelperN Input : xxxxx #Where on process chibios does the data go?

[Module]
	Process: ChibiOS
	name: Servo	
InPort: XXXX
OutPort:YYYY
Helper1: N/A
Helper1 Name: N/A
Helper1 Data: N/A
Helper1 Arg1: N/A
Helper1 Arg2: N/A
Helper1 Input : N/A #
