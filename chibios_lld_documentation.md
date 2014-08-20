# Installation

1. Clone the repo.

```bash
git clone https://github.com/PSAScapstone2014/stm32.git
```

2. Pull the ChibiOS submodule.

```bash
cd stm32
git submodule update --init
```

3. Unpack the lwIP package.

```bash
cd ChibiOS/ext
unzip unzip lwip-*_patched.zip
```

4. Test it.

```bash
cd ../testhal/Posix/PAL
make clean
make
./go
```

If you see the following output, congratulations! It works!

```
ChibiOS/RT simulator (Linux)

simio connected to 127.0.0.1:27000
[SIMIO] CONNECT
[PAL_IO] <- set IOPORT1 latch to 0x01 (was 0x00)
[PAL_IO] <- set IOPORT1 latch to 0x03 (was 0x01)
[PAL_IO] <- set IOPORT1 latch to 0x07 (was 0x03)
[PAL_IO] <- set IOPORT1 latch to 0x0f (was 0x07)
[PAL_IO] <- set IOPORT1 latch to 0x1f (was 0x0f)
```

# Capstone Components

## Overview

![ChibiOS Flow](chibios_lld_documentation.svg)

The flow chart shows a high level overview of how the various pieces fit together.

### Daemons

Starting at the top, we have the daemon processes. The daemons are executable programs representing ChibiOS. As ChibiOS is meant to be running as the operating system on embedded hardware, the daemons will almost always run until killed by the user. Daemons are divided into two groups: the unit tests and PSAS projects.

Unit tests were developed by the capstone team to test their low level drivers. Each behaves differently according to how the developer wanted to run their tests. More on this later.

The PSAS projects were developed by the PSAS team to run on the rocket. They are generally beyond the scope of this document.

### ChibiOS

Each of the unit tests makes use of the services provided by ChibiOS. They usually involve calls to initialize one or more hardware abstraction layer drivers and then invoke the needed API calls to test the driver's interface.

### Low Level Drivers

The capstone team developed a total of 10 low level drivers (llds) during their project. For the simulator, they will either invoke linux system calls or use the network interface api (called simio) to implement features such as getting the system time, handling virtual hardware interrupts, or read and write data from user applications.

### Applications

User applications should be written to interact with the llds in some way. The capstone team created a testing framework (documented elsewhere) along with a series of "go" scripts to enable unit testing. Each of the go scripts located under ChibiOS/testhal/Posix provides an example of what an application needs to do in order to interact with a running ChibiOS daemon via the llds.

Any particular go script will launch and begin listening on TCP port 27000 for incoming connections from the simio network interface. Once the daemon has been started and the lld has been asked to read or write data, the daemon will connect to the application. At this point it is possible to read and/or write data to any of the registered llds specified in ChibiOS/os/hal/platforms/Posix/simio.h.

The simio layer is described in more detail later.

## LLDs

### ADC

**INSERT ADC DOC**

### EXT

The EXTernal driver is used to issue callbacks when a specific hardware event like a button push is registered. Callback functions may be registered on different numeric channels by the ChibiOS daemon developer. An application developer will send a binary number representing the channel number to EXT_IO. At this point the callback function will be triggered.

The go script for the EXT unit test will emulate a button push on channel 0 every second. The expected response will be from the PAL driver indicating that a virtual LED has been toggled.

### GPT

**INSERT GPT DOC**

### I2C

**INSERT I2C DOC**

### PAL

The Pin Abstraction Layer driver is used to interface with various IO ports on real hardware. In the simulator, we simply output the state of an IO port and its value. We usually interpret this as an LED being toggled on or off.

The go script for the PAL unit test simply prints out the status of IO ports as the unit test runs. No input is sent to the lld.

### PWM

**INSERT PWM DOC**

### RTC

The Real Time Clock driver implements time and alarm related functions. The driver will provide system time and signal a function callback when an alarm has been set.

The go script for the RTC unit test outputs PAL pin changes as alarms are set and callbacks are invoked. No input is sent to the lld.

### SDC

The SD Card driver is responsible for reading and writing to SD cards. In our implementation, the lld forwards read and write requests over the simio network channel. It is left up to the application developer to implement storage facilities.

The SDC lld uses its own protocol-within-a-protocol for reads and writes. When a read is requested the following messages is sent.

```
cmd read startblk XXXXXXXX nblks YYYYYYYY
```

The startblk is indicated by a 32 bit hexadecimal address. nblks is a 32 bit hexadecimal length. A block is defined by the MMCSD_BLOCK_SIZE macro and is currently set to 512 bytes. The application should write nblks back to the driver starting with block startblk.

When the driver needs to do a write, two message are sent. The first message is of the following form.

```
cmd write startblk XXXXXXXX nblks YYYYYYYY
```

Startblk and nblks have identical meaning to the driver's read counterpart. The second message will contain the data to be written to storage.

The go script for the SDC unit test implements this protocol using a in-memory auto-expanding storage device. The unit test runs a badblocks-style read-write test on the virtual storage device. At the end of the test, the go script writes the memory contents to disk and uses hexdump to display its contents.

### SERIAL

The serial driver emulates a serial cable connection. The unit test reads in a buffer and echos it back to the sender. The unit test go script will take input from stdin, send it to the lld, and display the echo'd response.

### SPI

The Serial Peripheral Interface driver is responsible for reading and writing to the SPI bus. It's functionality is similar to that of the serial driver with one exception. The SPI driver is able to select differing slaves from which data is read or written.

**TODO PROTOCOL**

## SimIO

### Overview

The simio network layer is responsible for reading data into a lld and writing data to an application. It's interface is documented in ChibiOS/os/hal/platforms/Posix/simio.h.

The interface contains:

 * a call to allow an application to select the host and/or port in which to connect,
 * two calls to read data from an application (with and without a timeout),
 * two calls to write data to an application (raw data and formatted data),
 * and a rarely used call to disconnect an active session.

Upon calling one of the read or write API functions, the interface will attempt to connect to the configured host. By default, this is localhost:27000. If no connection can be made, an error is written to stderr.

### Protocol

Simio uses a fairly simple protocol for communications.

```
LLD_IO <tab> <hexadecimal encoded data> <newline>
```

LLD_IO is the name of the driver as seen in simio.h. The hexadecimal encoded data represents each byte with two hexadecimal characters. For example, to send the string "Hello, world!" to the first serial driver, the message would be

```
SD1_IO  48656c6c6f2c20776f726c6421
```

The serial driver unit test will decode and re-encode the message back to the application.

A more complex application will generally involve some sort of hardware emulation or forwarding service. An example of this can be found in the SDC go script; it emulates an in-memory auto-expanding SD card.

### LLD Usage

**TODO**

## lwIP

**TODO**

# Upstream Merge

**TODO**
