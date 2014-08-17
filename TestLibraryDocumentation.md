Documentation

##Table of Contents
1. Robot Framework Test Table
2. Library Method Description
3. References

##1. Robot Framework Test Table
The Robot Framework uses a structure they call test tables, in order to automate testing. Each test table has up to four different sub tables that help define the test; these are the Setting, Variable, Test Case, and Keyword tables.
Setting Table
This table has the following format:
*Setting* | *Value*
--------- | -------
Library | SendReceiveLibrary.py

This tells the Robot Framework that we want it to use a Library of pre-defined keywords for testing. The SendReceiveLibrary.py file defines several methods that are used for testing.

Test Case Table

*Test Case* | *Action* | *Argument* | *Argument* | *Argument* | *Argument* | *Argument* |
----------- | -------- | ---------- | ---------- | ---------- | ---------- | ---------- |
Send and receive data from a ChibiOs serial app | ${ret}= | Send And Receive | 27000 | dataToDriver.tsv | ./serial_test | ./fakeApp
 | Echo Test | ${ret} | SendAndReceive.tsv

The first row defines that this is the Test Cases table. The second row defines the first test case and the first action to be taken for that test case. The first test case is called "Send and receive data from a ChibiOS serial app." It then defines the first action to be taken for that test case, which is to call the Send And Receive keyword, which is a method located in the file SendReceiveLibrary.py, with the appropriate arguments and then saves the value that method returns in the variable ${ret}. The third row defines the second action to be taken for the test case, which is to call the Echo Test keyword with the appropriate arguments. This keyword is also a method located in the file SendReceiveLibrary.py.


##2. Library Method Description
Methods
Name | Description
---- | -----------
sim_format(self, lld, data) | THIS FUNCTION NEEDS A PROPER DESCRIPTION
send_to_driver(self, fileName, fileDesc, driver) | Reads data from a file and sends it over a port.
send_and_receive(self, port, fileName, *apps) | This method receives data from a port and sends it to a specified driver.
echo_test(self, data, fileName) | This method defines a test.

**sim_format(self, lld, data)**

**send_to_driver(self,fileName, fileDesc, driver)**

**send_and_receive(self, port, fileName, *apps)**

This method takes a port, fileName, and a list of applications as input. The port given specifies which port to open a connection to, used to send data to a specified driver. The data sent is contained in the file given by fileName. The method also starts any necessary applications before sending data over the port.

**echo_test(self, data, fileName)**

This method takes a set of data and a filename as input. It reads data from the file given by fileName and compares it to the data input. If they match, the test passes, otherwise the test fails.


##3. References
Robot Framework User Guide - http://robotframework.googlecode.com/svn/trunk/doc/userguide/RobotFrameworkUserGuide.html
