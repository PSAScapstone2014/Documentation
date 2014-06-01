PSAS Systems Testing Framework
==============================
Requirements Document
=====================
**_Authored by Capstone Team E (Spring 2014 – Summer 2014) at Portland State University_**

##1. Introduction##
This document serves as the compilation of requirements for the Systems testing framework being built for Portland State Aerospace Society (PSAS). 
It documents the purpose and scope for this project, stakeholders and target audiences. Then it goes on to define each requirement for the project.

##1.1. Purpose and Scope##

The purpose of this document is to describe the various requirements for the systems testing framework being built for PSAS rocket software by the 
authors of this document. PSAS is non-profit group with an open source codebase. Improving the existing PSAS rocket software creates additional technical 
capital for PSAS. Being able to show a potential donor that the rocket software system is well tested is an advantage for PSAS. Therefore, the creation of 
this systems testing framework will be an important goal.

The scope of the work will include all modules needed to launch a rocket.

##1.2. Terminology##

* PSAS – Portland State Aerospace Society
* ChibiOS - ChibiOS/RT is a complete, portable, open source, compact and extremely fast RTOS (Real-Time Operating System).
* lwIP - Light Weight IP which is a TCP/IP implementation that is currently used by PSAS. 

##2. Product Overview##

We are developing a test platform to validate functionality of embedded rocket systems. 
This section will provide information about the stakeholders, target demographics and use cases for the product.

###2.1. Stakeholders###

Primary stakeholder for this project is Theo Hill from PSAS. The other team members of PSAS are additional stakeholders. 

###2.2. Target Demographics###

The main target audience for this product are the members of PSAS. 

If the project goes on to make significant changes to ChibiOS, the maintainers for this operating system may also be an additional target audience.

###2.3. Use Cases###

####2.3.1 User will run a nightly automated build test. ####

*Primary Actor*: PSAS Member

*Scope*: PSAS Systems Testing Framework

*Brief*: The PSAS member will select the nightly automated build test option, then selects the tests they want to run. Next they will run the 
build tests which are automated.

*Success Guarantees*: When the user returns at the expected time to the screen, the result of the nightly build test will be displayed. 

*Triggers*: The PSAS Member wants to run a set of tests in an automated fashion overnight. 

*Basic Flow*: 

1. The framework will have options to select type of test run. 

2. Once the nightly build test option is selected, the member can select the tests that needed to be run and their frequency.

3. The program tell the user of an expected end time or will alert the user when the test ends. 

4. The user returns to the screen and obtains the result to analyze. 

####2.3.2 User will take the software and use it as a training tool. ####

*Primary Actor: New PSAS Member

*Scope*: PSAS Systems Testing Framework

*Brief*: The new PSAS member will acquaint themselves with the PSAS rocket software system by using the systems testing framework. 

*Success Guarantees*: The user should be able to go through the software and successfully understand the PSAS rocket software system. 
For example, the new user could learn how to turn on the systems by working through the test framework. 

*Triggers*: The new PSAS member wants to learn about the software. 

*Basic Flow*: 

1. The user will select what they want to learn. 

2. Then the appropriate simulation will be generated for the new PSAS member to work through. 

3. The member will work through the simulation and learn more about the system. 

####2.3.3 User will run Valgrind/other testing tool with testing framework. ####

*Primary Actor*: PSAS Member

*Scope*: PSAS Systems Testing Framework and Valgrind over the PSAS Rocket Software. 

*Brief*: The PSAS member will run the Valgrind tests and the PSAS Systems testing framework together to conduct tests for their software. 

*Success Guarantees*: Both programs should work together with no problems and output a result of the tests that were run.  

*Triggers*: Need to do a more complete systems test. 

*Basic Flow*: 

1. User will select the Valgrind tests and the PSAS Systems testing framework tests to run. 

2. Then they will run the tests.

3. Finally a result for the tests will be obtained from both Valgrind and PSAS Test Framework. 

####2.3.4 User will create a prototype of a new functionality.####

*Primary Actor*: PSAS Member

*Scope*: PSAS Systems Testing Framework and over the PSAS Rocket Software

*Brief*: The user can test a new functionality for the rocket using the PSAS systems testing framework.

*Success Guarantees*: The test framework must be able to create the prototype without errors and run the appropriate tests. 

*Triggers*: A new functionality must be added to the system. 

*Basic Flow*: 

1. The user will update Rocket software with new feature information. 

2. The systems testing framework will be used to create a prototype of the software with the new feature.  

3. Then the user will use the testing framework to test the new prototype once it is created. 

####2.3.5	User will attempt stochastic fault simulation.  ####

*Primary Actor*: PSAS Member

*Scope*: PSAS Systems Testing Framework and over the PSAS Rocket Software

*Brief*: The user will have the test software provide bad data to cause a fault and see how the system reacts.

*Success Guarantees*: The test framework will show if the system exited gracefully or crashed and will provide data to analyze the cause. 

*Triggers*: System is provided with bad data. 

*Basic Flow*:  

1. The user programs the test and requests bad data to be generated as input.

2. The test framework runs the tests on the system. 

3. The test will fail and will exit (may be gracefully or it may crash). 

####2.3.6	User will test various data formats for correctness. ####

*Primary Actor*: PSAS Member

*Scope*: PSAS Systems Testing Framework and over the PSAS Rocket Software

*Brief*: The user will check if the data format for the rocket software is correct with the systems testing framework. 

*Success Guarantees*: The test will output information to show if the rocket software contains accurate data format. 

*Triggers*: Any request or need to test the data format for the rocket system. 

*Basic Flow*:  

1. User will input a data file. 

2. Then they will run a test to check that the data format is as expected. 

3. At the end of the test, the result will show if the data format is proper. 

####2.3.7	User will test out a simulated version of the hardware using the test framework. ####

*Primary Actor*: PSAS Member

*Scope*: PSAS Systems Testing Framework and over the PSAS Rocket Software

*Brief*: The user can simulate hardware component and test it using the test framework. 

*Success Guarantees*: The framework will produce a software based hardware simulation and will run requested tests.

*Triggers*: Need to simulate a hardware component. 

*Basic Flow*: 

1. The test framework is used to model a hardware component to which the run tests on. 

2. User will select the tests to run. 

3. Then the framework will run the test. 

4. Test results will be outputted. 

##3. Requirements##

###3.1. Functional Requirements###

####3.1.1	There must be a way to decide what a test is.####

This means that the Capstone team will provide a well-defined way to describe what can be thought of as a test for the rocket software. 
A test should be thought of as a generic one that could be done across multiple devices or boards.

####3.1.2	There must be a way to describe the configurations of a test. ####

Once a test is selected, there should be a way to configure that test depending on a particular features of the device that is currently 
being tested. This includes (but it is not limited to) networking options, sensor types, hardware model, and compilation options. 
All of this would be linked to test harness that will aid in carrying out the tests. 

####3.1.3	The test framework should test all modules needed for launching a rocket.####

This requirement is here so that the capstone team will ensure that all necessary portions of the rocket software will be tested. 

####3.1.4	The test framework will run on a Linux based system. ####

The scenario here would be to clone the systems testing framework repository from GitHub, then build the system with the required options 
and then the tests would be run for the system. In this scenario, we must make sure that everything will work from one Linux based system. 

####3.1.5	ChibiOS should run as a process on a Linux based system. ####

This is related to requirement 3.1.4.

####3.1.6 Our work must not interfere with core ChibiOS functionality. ####

The user should have a way to specify that they want to build our modifications rather than using a normal build. 
This ties in with requirement 3.1.2 in that it should be possible to configure a test as needed. 

###3.2. Usability Requirements###

####3.2.1 The capstone team will provide a method of automatically running tests and summarizing results.####

This could mean using an appropriately licensed third-party testing framework or some scriptable method for 
scheduling tests that the capstone team will create. 

####3.2.2 The tests should be suited for automated nightly build testing.####

Automated testing is an important usability need in order to reduce the in person hours needed by the team members.
 
####3.2.3 It must be possible to use the test framework with other testing tools like Valgrind.  ####

####3.2.4 The users must be able to prototype a new functionality. ####

####3.2.5 The users should be able to simulate failure and to see how the system reacts. ####

####3.2.6 Users should be able to simulate embedded system with a non-embedded system.####

This is in conjunction with requirements 3.1.4 and 3.3.1. 

###3.3. Technical, Environmental and Interaction Requirements###

####3.3.1 The test framework must run on x64 Debian Linux system with GCC version 4.8. ####

####3.3.2 Our work will use the main ChibiOS 2.6.3 repository as a baseline. The PSAS fork of ChibiOS will only be consulted as needed. ####

Keeping with the main version of ChibiOS will allow for more stability in the long run.

####3.3.3 Testing framework will use parts from the general software but it should be a separate testing unit.####

The project will be built in a separate GitHub repository. When the tests need to be used, the repository will be compiled separately.

####3.3.4 A goal will be to merge our changes back into the ChibiOS mainline and, as such, the changes should be kept compartmentalized as 
much as possible.####

####3.3.5 Functional tests will be the primary motivator. Unit tests are not required.####

####3.3.6 Our modifications shall be GPL licensed. ####

####3.3.7 Documentation must exist in required format. 

There should be two types of documentation. One is User documentation, which should be written in Markdown. 
There should also be usage examples associated with this. 
Maintainer documentation is the third type, which will be notes in line with the code. 

###3.4. Assumptions###

The team has agreed upon a waterfall style work flow.

The project is not required to be finished by July 20th for Launch 11, but a barebones prototype of the systems testing framework is required. 
More information about the launch can be found here: [http://psas.pdx.edu/launch11/](http://psas.pdx.edu/launch11/)

###3.5. Constraints###

#####3.5.1. Ethernet Stack specification#####
* The Ethernet stack uses lwIP (Light Weight IP). Depending on the specification for this, lwIP stack may have to be ported to Linux as well. 
But the current design of the microcontrollers requires lwIP. This is more of a design factor that will have to be addressed in the design 
document after further analysis. 

##4. Deliverables##

A successful product is based on the following criteria.

* The final deliverable must be submitted as a Github project. 

* It must be able to produce a test binary using either Git-clone or make. This test binary should be able to run several tests in an automated fashion.  

* There must be documentation, possibly in the form of user instructions and written in Markdown.  

* Additionally, ChibiOS fork changes that may be delivered to the original project for this operating system should be prepared as a Github project.

The final capstone presentation is on August 25th. All matters related to this project will be complete by that date. 

##5. References##

1. ChibiOS Definition: [http://www.chibios.org/dokuwiki/doku.php](http://www.chibios.org/dokuwiki/doku.php "ChibiOS") 
2. lwIP Definition: [http://savannah.nongnu.org/projects/lwip/](http://savannah.nongnu.org/projects/lwip/)
