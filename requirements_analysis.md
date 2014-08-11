PSAS Systems Testing Framework
==============================
Requirements Document Analysis
==============================
**_Authored by Capstone Team E (Spring 2014 – Summer 2014) at Portland State University_**

###Table of Contents###

1. [Introduction](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#1-introduction) <br>
1.1. [Purpose and Scope](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#11-purpose-and-scope) <br>
1.2. [Terminology](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#12-terminology) <br>
2. [Product Overview](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#2-product-overview) <br>
3. [Requirements](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#3-requirements) <br>
2.1. [Functional Requirements](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#31-functional-requirements) <br>
2.2. [Usability Requirements](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#32-usability-requirements) <br>
2.3. [Technical, Environmental and Interaction Requirements](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#33-technical-environmental-and-interaction-requirements) <br>
2.4. [Assumptions](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#34-assumptions) <br>
2.5. [Constraints](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#35-constraints) <br>
3. [Deliverables](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#4-deliverables) <br>
4. [References](https://github.com/PSAScapstone2014/Documentation/blob/master/requirements_analysis.md#5-references) <br>

##1. Introduction##
This document serves as the line by line review of requirements for the Systems testing framework built for Portland State Aerospace Society (PSAS). It references the original requirements list and has a line by line description of how each requirement has been met or if they have not been met.  

##1.1. Purpose and Scope##

The purpose of this document is to check if the authors have met the previously outlined requirements for the systems testing framework built for PSAS rocket software. PSAS is non-profit group with an open source codebase. Improving the existing PSAS rocket software creates additional technical capital for PSAS. Being able to show a potential donor that the rocket software system is well tested is an advantage for PSAS. Therefore, the creation of this systems testing framework will be an important goal. Going through the requirements is important so that there is a good description for both the capstone team and the sponsor about what they were able to achieve within the duration of the project. It is also a way to understand what is left to do later on. 

The scope of the work should include all modules needed to launch a rocket as mentioned previously in the requirements.

##1.2. Terminology##

* PSAS – Portland State Aerospace Society
* ChibiOS - ChibiOS/RT is a complete, portable, open source, compact and extremely fast RTOS (Real-Time Operating System).
* lwIP - Light Weight IP which is a TCP/IP implementation that is currently used by PSAS. 
* Robot Framework: a generic test automation framework for acceptance testing and acceptance test-driven development (ATDD). This was chosen by the team as the basis for the test framework. 

##2. Product Overview##

We are developing a test platform to validate functionality of embedded rocket systems. 
Primary stakeholder for this project is Theo Hill from PSAS. The other team members of PSAS are additional stakeholders. The main target audience for this product are the members of PSAS. If the project goes on to make significant changes to ChibiOS, the maintainers for this operating system may also be an additional target audience.

##3. Requirements##
**_Total Requirements that were met: 11/19_** 

###3.1. Functional Requirements###
**Total Requirements met: 7/7**

####3.1.1	There must be a way to decide what a test is.####

This means that the Capstone team will provide a well-defined way to describe what can be thought of as a test for the rocket software. 
A test should be thought of as a generic one that could be done across multiple devices or boards.
_This requirement is met via the Robot Testing Framework. The user can define a test using this framework using a python script._

####3.1.2	There must be a way to describe the configurations of a test. ####

Once a test is selected, there should be a way to configure that test depending on a particular features of the device that is currently 
being tested. This includes (but it is not limited to) networking options, sensor types, hardware model, and compilation options. 
All of this would be linked to test harness that will aid in carrying out the tests. 
_This requirement is met through the implementation of the Robot Testing Framework as well. Python scripts can define the configuration of each of the tests that need to be done. A TSV file can also be used set up different tests._

####3.1.3	The test framework should test all modules needed for launching a rocket.####

This requirement is here so that the capstone team will ensure that all necessary portions of the rocket software will be tested. 
_This requirement is also met implictly via the Robot Test Framework setup._

####3.1.4	The test framework will run on a Linux based system. ####

The scenario here would be to clone the systems testing framework repository from GitHub, then build the system with the required options 
and then the tests would be run for the system. In this scenario, we must make sure that everything will work from one Linux based system.
_This requirement is met as the testing framewok runs on Linux machines._

####3.1.5	ChibiOS should run as a process on a Linux based system. ####

This is related to requirement 3.1.4.
_This requirement has been met._
 
####3.1.6 Our work must not interfere with core ChibiOS functionality. ####

The user should have a way to specify that they want to build our modifications rather than using a normal build. 
This ties in with requirement 3.1.2 in that it should be possible to configure a test as needed. 
_This requirement is met._

####3.1.7 Functional tests will be the primary motivator. Unit tests are not required.####
_This requirement is met._

###3.2. Usability Requirements###
**Total Requirements met: 1/6**

####3.2.1 The capstone team will provide a method of automatically running tests and summarizing results.####

This could mean using an appropriately licensed third-party testing framework or some scriptable method for 
scheduling tests that the capstone team will create. 
_This requirement has been met. The result summarization has been met via the HTML based results display. Since Robot Framework can automate tests, it meets the automatic running portion as well. The tests are define using python._ 

####3.2.2 The tests should be suited for automated nightly build testing.####

Automated testing is an important usability need in order to reduce the in person hours needed by the team members.
 
####3.2.3 It must be possible to use the test framework with other testing tools like Valgrind.  ####

####3.2.4 The users must be able to prototype a new functionality. ####

####3.2.5 The users should be able to simulate failure and to see how the system reacts. ####

####3.2.6 Users should be able to simulate embedded system with a non-embedded system.####

This is in conjunction with requirements 3.1.4 and 3.3.1. 

###3.3. Technical, Environmental and Interaction Requirements###
**Total Requirments met: 3/6**

####3.3.1 The test framework must run on x64 Debian Linux system with GCC version 4.8. ####
_Need to discuss this._

####3.3.2 Our work will use the main ChibiOS 2.6.3 repository as a baseline. The PSAS fork of ChibiOS will only be consulted as needed. ####

Keeping with the main version of ChibiOS will allow for more stability in the long run.
_This has been met._ 

####3.3.3 Testing framework will use parts from the general software but it should be a separate testing unit.####

The project will be built in a separate GitHub repository. When the tests need to be used, the repository will be compiled separately.
_This has been met._

####3.3.4 A goal will be to merge our changes back into the ChibiOS mainline and, as such, the changes should be kept compartmentalized as much as possible.####
_This is in the discussion but may not happen by the end of the capstone._

####3.3.5 Our modifications shall be GPL licensed. ####
_This has been met._

####3.3.6 Documentation must exist in required format. 

There should be two types of documentation. One is User documentation, which should be written in Markdown. 
There should also be usage examples associated with this. 
Maintainer documentation is the third type, which will be notes in line with the code. 
_There is some documentation available, but its not consolidated yet._ 

###3.4. Assumptions###

The team has agreed upon a modified agile workflow style with some waterfall elements to it.
_This is not a requirement. Its just a description of our workflow style._ 

The project is not required to be finished by July 20th for Launch 11, but a barebones prototype of the systems testing framework is required. 
More information about the launch can be found here: [http://psas.pdx.edu/launch11/](http://psas.pdx.edu/launch11/)
_We did not meet this as our framework was not used on the Launch, but we did have our first prototype before the Launch happened._

HAL Timing/ Latency/ Platform-Difference Issues were determined to be beyond the scope of this project.
_This was a previous agreement we have held on to._

###3.5. Constraints###

#####3.5.1. Ethernet Stack specification#####
* The Ethernet stack uses lwIP (Light Weight IP). Depending on the specification for this, lwIP stack may have to be ported to Linux as well. 
But the current design of the microcontrollers requires lwIP. This is more of a design factor that will have to be addressed in the design document after further analysis. 
_We have done some work to simulate network ports._

##4. Deliverables##
**_This is partially done._**

A successful product is based on the following criteria.

* The final deliverable must be submitted as a Github project. _This already exists._

* It must be able to produce a test binary using either Git-clone or make. This test binary should be able to run several tests in an automated fashion.  _This is in the works._ 

* There must be documentation, possibly in the form of user instructions and written in Markdown. _This is in the works._

* Additionally, ChibiOS fork changes that may be delivered to the original project for this operating system should be prepared as a Github project. _This is in the works._

The final capstone presentation is on August 25th. All matters related to this project will be complete by that date. _This may not be the case if the ChibiOS mainline task goes through._

##5. References##

1. ChibiOS Definition: [http://www.chibios.org/dokuwiki/doku.php](http://www.chibios.org/dokuwiki/doku.php) 
2. lwIP Definition: [http://savannah.nongnu.org/projects/lwip/](http://savannah.nongnu.org/projects/lwip/)
3. Robot Framework Definition: [http://robotframework.org/](http://robotframework.org/)
