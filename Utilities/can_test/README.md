__CAN Tester for Kvaser CAN Leaf Interfaces, Version 0.2.0__ \
Copyright &copy; 2007,2012-2022 by Uwe Vogt, UV Software, Berlin

```
Usage: can_test <interface> [<option>...]
Options for receiver test (default):
 -r, --receive                 count received messages until ^C is pressed
 -n, --number=<number>         check up-counting numbers starting with <number>
 -s, --stop                    stop on error (with option --number)
 -m, --mode=(2.0|FDF[+BSR])    CAN operation mode: CAN 2.0 or CAN FD format
     --shared                  shared CAN controller access (when supported)
     --listen-only             monitor mode (listen-only, transmitter is off)
     --error-frames            allow reception of error frames
     --no-remote-frames        suppress remote frames (RTR frames)
     --no-extended-frames      suppress extended frames (29-bit identifier)
 -b, --baudrate=<baudrate>     CAN bit timing in kbps (default=250)
     --bitrate=<bit-rate>      CAN bit rate settings (as a string)
 -v, --verbose                 show detailed bit rate settings
Options for transmitter test:
 -t, --transmit=<time>         send messages for the given time in seconds, or
 -f, --frames=<number>,        alternatively send the given number of messages,
     --random=<number>         optionally with random cycle time and data length
 -c, --cycle=<cycle>           cycle time in milliseconds (default=0) or
 -u, --usec=<cycle>            cycle time in microseconds (default=0)
 -d, --dlc=<length>            send messages of given length (default=8)
 -i, --id=<can-id>             use given identifier (default=100h)
 -n, --number=<number>         set first up-counting number (default=0)
 -m, --mode=(2.0|FDF[+BSR])    CAN operation mode: CAN 2.0 or CAN FD format
     --shared                  shared CAN controller access (when supported)
 -b, --baudrate=<baudrate>     CAN bit timing in kbps (default=250)
     --bitrate=<bit-rate>      CAN bit rate settings (as a string)
 -v, --verbose                 show detailed bit rate settings
Options:
 -L, --list-boards             list all supported CAN interfaces and exit
 -T, --test-boards             list all available CAN interfaces and exit
 -h, --help                    display this help screen and exit
     --version                 show version information and exit
Hazard note:
  If you connect your CAN device to a real CAN network when using this program,
  you might damage your application.
```

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
