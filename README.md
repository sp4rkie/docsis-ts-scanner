docsis-ts-scanner
=================

what is it
----------

- a small tool to display DOCSIS transport streams in a human readable way

required hardware
-----------------

- basically any linux machine with Linux DVB API (Version 3, Version 5.x) and DVB-C support is suitable
- to ease things further following components are recommended
    - Raspberry Pi (e.g. Pi 3 Model B, earlier B models may also work)
    - TV stick: Sundtek MediaTV Pro III (DVB-C/T/T2, FM-Radio, AnalogTV)

software installation
---------------------

- first install Raspbian on your RPi: [Download Raspbian for Raspberry Pi](https://www.raspberrypi.org/downloads/raspbian/)
- after this the following additional packages are required
        
        sudo apt install wget gawk dvbsnoop dvbtune dvb-tools tshark

- Sundtek MediaTV Pro driver installation

        wget http://www.sundtek.de/media/sundtek_installer_181220.135032.sh
        sudo sh sundtek_installer_181220.135032.sh -service -nolirc -noautostart

- finally install the transport stream scan tool

        wget https://raw.githubusercontent.com/sp4rkie/docsis-ts-scanner/master/ts-scanner.awklib
        wget https://raw.githubusercontent.com/sp4rkie/docsis-ts-scanner/master/ts-scanner
        chmod 755 ts-scanner

how to use it
-------------

- to execute the program simply type something like

        sh ts-scanner -m filtered -f 618:626:634:642

this will repeatedly scan primary-capable frequencies 618, 626, 634, 642 MHz for DOCSIS frames
according to the given filter rule (see filter definition in the tool).

Per default this will show all frames that are either

    - Type: Multipart Registration Response (45)
    - Type: MAC Domain Descriptor (33)
    - Type: Upstream Channel Descriptor Type (29)
    - Type: Privacy Key Management Response (13)

The filter rule 

        "docsis_mgmt.type == 45 || docsis_mgmt.type == 33 || docsis_mgmt.type == 29 || docsis_mgmt.type == 13"

Please see tshark/ wireshark for further information.

- command line options

        Usage: ts-scanner
          -h                    - print this help and exit
          -f [0-9]+(/[0-9]+)?(:[0-9]+(/[0-9]+)?)*
                                - acquired start frequencies in segment (in MHz)
          -c [0-9]              - select DVB-C tuner
          -m (filtered|full)    - select operation mode
          -v                    - increase logging verbosity

reference
---------

[CaptureSetup/DOCSIS - The Wireshark Wiki](https://wiki.wireshark.org/CaptureSetup/DOCSIS)

