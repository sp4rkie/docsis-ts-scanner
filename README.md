docsis-ts-scanner
=================

what is it
----------

- a small tool to display DOCSIS transport streams in a human readable way

how to use it
-------------

        Usage: ts-scanner
          -h                    - print this help and exit
          -f [0-9]+(/[0-9]+)?(:[0-9]+(/[0-9]+)?)*
                                - acquired start frequencies in segment (in MHz)
          -c [0-9]              - select DVB-T tuner
          -m (filtered|full)    - select operation mode
          -v                    - increase logging verbosity

reference
---------

[CaptureSetup/DOCSIS - The Wireshark Wiki](https://wiki.wireshark.org/CaptureSetup/DOCSIS)

