.. figure :: docs/source/slink_logo_white.png
  :align:    center

S-Link
======
Chiplets require an efficient and lightweight interface to an FPGA for testing, validation, and prototyping. 
S-Link is a simple, scalable, and flexible link controller protocol geared towards chiplets and chip-to-chip 
communication. S-Link defines the link layer, and gives freedom for various application and physical layers. 
The ultimate goal of S-Link is to provide a simple alternative for chiplet communication compared to other protocols.

S-Link supports the following features:

* Mult-lane support (provisions for upto 128+ lanes with asymmetric lane support, **up to 8lanes currently supported**)
* 128b/130b encoding
* Parameterizable Applicaiton Data Widths
* Configurable Attributes for fine tuning link controls and/or active link managemnet
* Low Power (P states) for power savings
* ECC/CRC for error checking of packet headers and payload data
* Parameterizable pipeline stages to optimze for frequency and/or power

Documentation
-------------
`S-Link Documentation <https://s-link.readthedocs.io>`__ is hosted on ReadTheDocs.

Tools Required
--------------
Iverilog and Gtkwave are the main tools you would need to try out some simulations. Those can be installed using the following
steps (or just visit their repos/websites for more info).

iverilog
++++++++
::

  sudo apt-get install bison flex gperf autoconf g++ zlib1g-dev  (zlib for saving in lx2 format)

  git clone git://github.com/steveicarus/iverilog.git
  cd iverilog
  sh autoconf.sh (if compiling from git)
  ./configure
  make
  sudo make install

  which iverilog


gtkwave
+++++++
::

  sudo apt-get install -y tcl-dev tk-dev libbz2-dev liblzma-dev
  sudo apt-get install gtk2.0   # you may or may not want this
  
  git clone https://github.com/gtkwave/gtkwave.git
  cd gtkwave/gtkwave3 # pick your version

  ./configure
  sudo make install
  
  which gtkwave


.. note ::

  Verilator may be supported later, but due to serdes models it is unlikely.

Additional
++++++++++++++++
This is primarily for building docs with ReadTheDocs. It is not required to run sims.

::

  sudo apt-get install -y python3-pip python3-testresouces
  cd S-Link
  pip3 install -r requirements.txt

Run your first sim
------------------
Ensure that iverilog and gtkwave are installed.

:: 

  cd verif/slink/run
  ./simulate.sh

This will run ``sanity_test`` which just sends a few packets from one side of S-Link to the other.

Synthesis/PnR
-------------
S-Link has been synthesized with Cadence Genus, PnR'ed with Mentor Aprisa. Previous versions have been compatible with Yosys and OpenROAD (newer versions have not been tested). For an example area/timing estimate, a 1-Lane, 8bit phy data width, with an AXI/APB/Interrupt application channel was roughly 0.02mm^2 in GF12LP+ (with flops synthesized, no memories for applicaiton layers). The application layer ran at 38.4MHz and the link clock was set to 1GHz. Higher frequencies are possible, these frequencies were set based on system architecture.

S-Link has also been implemented in Xilinx FPGAs (XC7Z020) for communication over 1.8V CMOS and LVDS. As an example, a 4lane-8bit phy data width implementation could sucessfully send traffic off-chip at 100MHz (400Mbps total bandwidth each direction) between two S-Link implemenations. This was with minimal effort given to timing closure, so higher frequencies are possible on higher performance FPGAs.


Using S-Link
------------
Want to use S-Link? Download and integrate! You are free to use in commercial projects. If you do choose to use S-Link, I do ask that you
let me know with some (minor) details about the use case just so I can see how it's being used. Also, please star the repo if you don't mind.


Want to Support S-Link?
-----------------------
Try it out! Offer suggestions for improvement! I have tried to create S-Link using only open source tools, and would like to continue support
for those. That being said, it would be nice to have a commercial simulator and synthesis/PnR tools in order to check compatibility. Larger FPGAs
and accompanying licenses would also be nice to have to try out various PHY types. If you or your oranization wish to help in any of these regards, 
please contact me.
