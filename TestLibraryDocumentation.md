##Table of Contents
1. [Introduction](https://github.com/PSAScapstone2014/Documentation/blob/master/TestLibraryDocumentation.md#1-introduction)
2. [Robot Framework Test Table](https://github.com/PSAScapstone2014/Documentation/blob/master/TestLibraryDocumentation.md#2-robot-framework-test-table)
3. [Library Method Description](https://github.com/PSAScapstone2014/Documentation/blob/master/TestLibraryDocumentation.md#3-library-method-description)
4. [References](https://github.com/PSAScapstone2014/Documentation/blob/master/TestLibraryDocumentation.md#4-references)

##1. Introduction
####1.1 Purpose
The purpose of this document is to describe some of the files in the TestingFramework repository.

####1.2 Valgrind and Robot Framework
Valgrind can be run alongside the Robot Framework via the command line. To run Valgrind with the framework you can run the framework with the following arguments: <br>
pybot --variable ARGS:valgrind_./ --escape space:_ TEST_TABLE.tsv <br>
More on using variables with Robot Framework can be found here: http://robotframework.googlecode.com/svn/trunk/doc/userguide/RobotFrameworkUserGuide.html#setting-variables-in-command-line

##2. Robot Framework Test Table
This section will describe the testing table, located in [SendReceiveTest.tsv](https://github.com/PSAScapstone2014/TestingFramework/blob/master/serial_test_example/SendReceiveTest.tsv) file in the serial_test_example folder.

The Robot Framework uses a structure they call test tables, in order to automate testing. Each test table has up to four different sub tables that help define the test; these are the Setting, Variable, Test Case, and Keyword tables. The Keyword table is not used in this file.

####2.1 Setting Table

*Setting* | *Value*
--------- | -------
Library | SendReceiveLibrary.py

This tells the Robot Framework that we want it to use a Library of pre-defined keywords for testing. The SendReceiveLibrary.py file defines several methods that are used for testing. More libraries can be defined in the same method.

####2.2 Variables Table

*Variables* | *Value*
--- | ---
${ARGS} | ./
${APP} | ${ARGS}serialTest
@{DRIVERS} | SD1_IO
@{DATA_FILES} | SendReceiveData.tsv
${PORT} | 27000

This table lists different variables that can be used by the test in different actions. The ${NAME} represents a scalar variable for the test. The @{NAME} represents a list variable, a variable that can have multiple values assigned to it.

####2.3 Test Case Table

*Test Case* | *Action* | *Argument* | *Argument* | *Argument* | *Argument* | *Argument* |
----------- | -------- | ---------- | ---------- | ---------- | ---------- | ---------- |
Send and receive data from a ChibiOs serial app | ${ret}= | Send And Receive | ${PORT} | ${DRIVERS} | ${DATA_FILES} | ${APP}
 | Echo Test | ${ret} | SendReceiveData.tsv

The first row defines that this is the Test Cases table. It also indicates which columns are the action to be taken, and the arguments for that action. The second row defines the first (and only) test case and the first action to be taken for that test case. The test case is called "Send and receive data from a ChibiOS serial app." It then defines the first action to be taken on that test case, which is to save the return value from the Send And Receive keyword (A method located in the SendReceiveLibrary.py file) with the appropriate arguments. The second action defined is calling the Echo Test keyword (Another method defined in the SendReceiveLibrary.py file) with it's arguments, one of which is the return value from the previous action.

##3. Library Method Description
This section describes the methods in the [SendReceiveLibrary.py](https://github.com/PSAScapstone2014/TestingFramework/blob/master/serial_test_example/SendReceiveLibrary.py) file in the serial_test_example folder.

**Methods**

**Name** | **Description**
---- | -----------
send_to_driver(fileName, fileDesc, driver) | Reads data from a file and sends it over a port.
send_and_receive(self, simioPort, drivers, dataFiles, arguments) | This method receives data from a port and sends it to a specified driver.
send_and_receive_with_lwip(self, simioPort, drivers, dataFiles, lwipPort, lwipAddress, arguments) | This method sends data to a specified driver using lwip.
echo_test(self, data, fileName) | This method is an example of a user defined test.

**send_to_driver(fileName, fileDesc, driver)** <br>
This method reads a TSV file and sends the contents to a socket that represents the IO interface for a low-level driver. The data is what will be sent to the driver and the time is the time stamp of the data, the method will delay it's sends to the socket to simulate the time elapse represented by the difference of the time stamps.

**send_and_receive(self, simioPort, druvers, dataFiles, arguments)** <br>
This method represents a keyword that can be used in the test table. This keyword starts up a ChibiOS application, sends data to the app, receives data that the app outputs, and finally closes the app. The file in dataFiles must have the same index as the driver it needs to be sent to in drivers. 

**send_and_receive_with_lwip(self, simioPort, drivers, dataFiles, lwipPort, lwipAddress, arguments)** <br>
This method is the same as send_and_recieve except it collects data from an outgoing lwip connection as well as from the drivers.

**echo_test(self, data, fileName)** <br>
This method is an example of a user defined test. The keyword echo_test will take the dictionary returned from send_and_receive and check that the data sent from the serial driver matches the data in a provided TSV data file.


##4. References
Robot Framework User Guide - http://robotframework.googlecode.com/svn/trunk/doc/userguide/RobotFrameworkUserGuide.html <br>
TestingFramework Repository - https://github.com/PSAScapstone2014/TestingFramework <br>
Robot Framework and Command Line Variables - http://robotframework.googlecode.com/svn/trunk/doc/userguide/RobotFrameworkUserGuide.html#setting-variables-in-command-line
