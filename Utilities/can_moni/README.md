__CAN Monitor for Kvaser CAN Leaf Interfaces, Version 0.2.0__ \
Copyright &copy; 2007,2012-2022 by Uwe Vogt, UV Software, Berlin

```
Usage: can_moni <interface> [<option>...]
Options:
 -t, --time=(ZERO|ABS|REL)     absolute or relative time (default=0)
 -i  --id=(HEX|DEC|OCT)        display mode of CAN-IDs (default=HEX)
 -d, --data=(HEX|DEC|OCT)      display mode of data bytes (default=HEX)
 -a, --ascii=(ON|OFF)          display data bytes in ASCII (default=ON)
 -w, --wrap=(NO|8|10|16|32|64) wraparound after n data bytes (default=NO)
 -x, --exclude=[~]<id-list>    exclude CAN-IDs: <id>[-<id>]{,<id>[-<id>]}
 -m, --mode=(2.0|FDF[+BSR])    CAN operation mode: CAN 2.0 or CAN FD format
     --shared                  shared CAN controller access (when supported)
     --listen-only             monitor mode (listen-only, transmitter is off)
     --error-frames            allow reception of error frames
     --no-remote-frames        suppress remote frames (RTR frames)
     --no-extended-frames      suppress extended frames (29-bit identifier)
 -b, --baudrate=<baudrate>     CAN bit timing in kbps (default=250)
     --bitrate=<bit-rate>      CAN bit rate settings (as a string)
 -v, --verbose                 show detailed bit rate settings
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
