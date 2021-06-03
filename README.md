### macOS&reg; User-Space Driver for CAN Leaf Interfaces from Kvaser

_Copyright &copy; 2020-2021  Uwe Vogt, UV Software, Berlin (info@mac-can.com)_

[![Build Status](https://travis-ci.com/mac-can/MacCAN-KvaserCAN.svg?branch=main)](https://travis-ci.com/mac-can/MacCAN-KvaserCAN)

# Running CAN on a Mac&reg;

_Running CAN on a Mac_ is the mission of the MacCAN project.
The macOS driver for CAN Leaf interfaces from [Kvaser](https://www.kvaser.com) is based on _MacCAN-Core_ which is an abstraction (or rather a wrapper) of Apple´s IOUsbKit to create USB user-space drivers for CAN interfaces from various vendors under macOS.

## MacCAN-KvaserCAN

This repo contains the source code for the _MacCAN-KvaserCAN_ driver and several alternatives to build dynamic libraries for macOS,
either as a C++ class library ([_libKvaserCAN_](#libKvaserCAN)),
or as a _CAN API V3_ driver library ([_libUVCANKVL_](#libUVCANKVL)),
as well as some C/C++ example programs
and my beloved CAN utilities [`can_moni`](can_moni-for-maccan-kvasercan)
and [`can_test`](can_test-for-maccan-kvasercan).

_CAN API V3_ is a wrapper specification to have a uniform CAN Interface API for various CAN interfaces from different vendors running under multiple operating systems.
See header file `CANAPI.h` for the CAN API V3 wrapper specification.

Note: _This project does not aim to implement Kvaser´s CANlib library on macOS._

### MacCAN-KvaserCAN API

```C++
/// \name   KvaserCAN API
/// \brief  MacCAN driver for Kvaser CAN Leaf interfaces
/// \note   See CMacCAN for a description of the overridden methods
/// \{
class CKvaserCAN : public CMacCAN {
public:
    // constructor / destructor
    CKvaserCAN();
    ~CKvaserCAN();

    // CMacCAN overrides
    static MacCAN_Return_t ProbeChannel(int32_t channel, MacCAN_OpMode_t opMode, const void *param, EChannelState &state);
    static MacCAN_Return_t ProbeChannel(int32_t channel, MacCAN_OpMode_t opMode, EChannelState &state);

    MacCAN_Return_t InitializeChannel(int32_t channel, MacCAN_OpMode_t opMode, const void *param = NULL);
    MacCAN_Return_t TeardownChannel();
    MacCAN_Return_t SignalChannel();

    MacCAN_Return_t StartController(MacCAN_Bitrate_t bitrate);
    MacCAN_Return_t ResetController();

    MacCAN_Return_t WriteMessage(MacCAN_Message_t message, uint16_t timeout = 0U);
    MacCAN_Return_t ReadMessage(MacCAN_Message_t &message, uint16_t timeout = CANREAD_INFINITE);

    MacCAN_Return_t GetStatus(MacCAN_Status_t &status);
    MacCAN_Return_t GetBusLoad(uint8_t &load);

    MacCAN_Return_t GetBitrate(MacCAN_Bitrate_t &bitrate);
    MacCAN_Return_t GetBusSpeed(MacCAN_BusSpeed_t &speed);

    MacCAN_Return_t GetProperty(uint16_t param, void *value, uint32_t nbyte);
    MacCAN_Return_t SetProperty(uint16_t param, const void *value, uint32_t nbyte);

    char *GetHardwareVersion();  // (for compatibility reasons)
    char *GetFirmwareVersion();  // (for compatibility reasons)
    static char *GetVersion();  // (for compatibility reasons)
};
/// \}
```

### Build Targets

_Important note_: To build any of the following build targets run the `build_no.sh` script to generate a pseudo build number.
```
uv-pc013mac:~ eris$ cd ~/Projects/MacCAN/KvaserCAN
uv-pc013mac:KvaserCAN eris$ ./build_no.sh
```
Repeat this step after each `git commit`, `git pull`, `git clone`, etc.

Then you can build all targets by typing the usual commands:
```
uv-pc013mac:~ eris$ cd ~/Projects/MacCAN/KvaserCAN
uv-pc013mac:KvaserCAN eris$ make clean
uv-pc013mac:KvaserCAN eris$ make all
uv-pc013mac:KvaserCAN eris$ sudo make install
uv-pc013mac:KvaserCAN eris$
```
_(The version number of the library can be adapted by editing the appropriated `Makefile` and changing the variable `VERSION` accordingly. Don´t forget to set the version number also in the source files.)_

#### libKvaserCAN

___libKvaserCAN___ is a dynamic library with a CAN API V3 compatible application programming interface for use in __C++__ applications.
See header file `KvaserCAN.h` for a description of all class members.

#### libUVCANKVL

___libUVCANKVL___ is a dynamic library with a CAN API V3 compatible application programming interface for use in __C__ applications.
See header file `can_api.h` for a description of all API functions.

#### can_moni

`can_moni` is a command line tool to view incoming CAN messages.
I hate this messing around with binary masks for identifier filtering.
So I wrote this little program to have an exclude list for single identifiers or identifier ranges (see program option `--exclude` or just `-x`). Precede the list with a `~` and you get an include list.

Type `can_moni --help` to display all program options.

#### can_test

`can_test` is a command line tool to test CAN communication.
Originally developed for electronic environmental tests on an embedded Linux system with SocketCAN, I´m using it for many years as a traffic generator for CAN stress-tests.

Type `can_test --help` to display all program options.

### Target Platform

- Apple´s macOS (x86_64)

### Development Environment

#### macOS Big Sur

- macOS Big Sur (11.4) on a MacBook Pro (2019)
- Apple clang version 12.0.5 (clang-1205.0.22.9)
- Xcode Version 12.5 (12E262)

#### macOS High Sierra

- macOS High Sierra (10.13.6) on a MacBook Pro (late 2011)
- Apple LLVM version 10.0.0 (clang-1000.11.45.5)
- Xcode Version 10.1 (10B61)

### CAN Hardware

- Kvaser Leaf Light v2 (EAN: 73-30130-00685-0)
- Kvaser Leaf Pro HS v2 (EAN: 73-30130-00843-4)

Note: _**Leaf Pro HS v2** devices can currently only be operated in **CAN 2.0 mode**!_

## Known Bugs and Caveats

- For a list of known bugs and caveats see tab [Issues](https://github.com/mac-can/MacCAN-KvaserCAN/issues) in the GitHub repo.

## This and That

### Wrapper Library for Windows&reg;

A CAN API V3 compatible Wrapper Library for Windows is also available.
It is build upon Kvaser´s CANlib DLL and can be downloaded from / cloned at [GitHub](https://github.com/uv-software/KvaserCAN-Wrapper).

### MacCAN-Core Repo

The MacCAN-Core sources are maintained in a SVN repo to synchronized them between the different MacCAN driver repos.

### Dual-License

This work is dual-licensed under the terms of the BSD 2-Clause "Simplified" License
and under the terms of the GNU General Public License v3.0 (or any later version).
You can choose between one of them if you use this work in whole or in part.

`SPDX-License-Identifier: BSD-2-Clause OR GPL-3.0-or-later`

### Trademarks

Mac and macOS are trademarks of Apple Inc., registered in the U.S. and other countries. \
Windows is a registered trademark of Microsoft Corporation in the United States and/or other countries. \
All other company, product and service names mentioned herein are trademarks, registered trademarks or service marks of their respective owners.

### Hazard Note

_If you connect your CAN device to a real CAN network when using this library, you might damage your application._

### Contact

E-Mail: mailto://info@mac.can.com \
Internet: https://www.mac-can.com

##### *Enjoy!*
