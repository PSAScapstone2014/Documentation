Documentation

##Table of Contents
1. Introduction
2. Robot Framework Test Table
2.1. Setting Table
2.2. Variables Table
2.3. Test Cases Table
3. Library Method Description
4. References

##1. Introduction
###1.1 Purpose
The purpose of this document is to describe some of the files in the TestingFramework repository.

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

Methods

Name | Description
---- | -----------
send_to_driver(self, fileName, fileDesc, driver) | Reads data from a file and sends it over a port.
send_and_receive(self, port, fileName, *apps) | This method receives data from a port and sends it to a specified driver.
echo_test(self, data, fileName) | This method defines a test.

**send_to_driver(self,fileName, fileDesc, driver)**

**send_and_receive(self, port, fileName, *apps)**
This method takes a port, fileName, and a list of applications as input. The port given specifies which port to open a connection to, used to send data to a specified driver. The data sent is contained in the file given by fileName. The method also starts any necessary applications before sending data over the port.

**echo_test(self, data, fileName)**
This method takes a set of data and a filename as input. It reads data from the file given by fileName and compares it to the data input. If they match, the test passes, otherwise the test fails.


##4. References
Robot Framework User Guide - http://robotframework.googlecode.com/svn/trunk/doc/userguide/RobotFrameworkUserGuide.html

TestingFramework Repository - https://github.com/PSAScapstone2014/TestingFramework
