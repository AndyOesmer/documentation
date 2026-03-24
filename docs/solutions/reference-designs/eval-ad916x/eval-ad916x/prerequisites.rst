.. _eval-ad916x prerequisites:

Prerequisites
===============================================================================

The required setup depends on whether you run HDL-only bring-up, Linux-based
bring-up, or no-OS software control. As a minimum, start with the items below.

Hardware prerequisites
-------------------------------------------------------------------------------

#. :adi:`EVAL-AD916X-FMCZ <EVAL-AD916X>` evaluation board
#. A supported FPGA carrier platform, currently
   :xilinx:`ZCU102 <products/boards-and-kits/ek-u1-zcu102-g.html>`
   on HPC0
#. A method to interact with the platform:

   #. For Linux/no-OS on ZCU102:

      - USB-UART cable (115200 baud, 8N1)
      - JTAG connection for programming/debug as needed
      - Ethernet connection for Linux network access
      - Optional DisplayPort monitor + keyboard/mouse for local desktop flow

#. A stable power source for the carrier and bench setup
#. Optional external clock source for JESD modes that require external clocking
   (J61 unmounted)
#. RF measurement equipment for validation:

   - Spectrum analyzer or RF signal analyzer
   - Coaxial SMA cables and attenuators as needed

Software prerequisites
-------------------------------------------------------------------------------

#. HDL build environment for ADI reference designs:

   - Vivado version supported by the active ADI HDL branch/release
   - GNU Make and a Linux/Cygwin/WSL shell environment

#. ADI HDL source tree with AD916x project:

   - :git-hdl:`projects/ad916x_fmc <projects/ad916x_fmc>`

#. One of the software control paths:

   - ADI Linux/Kuiper image workflow for runtime bring-up
   - no-OS workflow for direct control and test

#. Optional host tools:

   - Serial terminal application for UART logs
   - :git-iio-oscilloscope:`IIO-Oscilloscope <releases>`
   - Spectrum analyzer or RF measurement instrument for DAC output validation

#. SD card setup for Linux flow:

   - 8 GB minimum, 16 GB recommended
   - Prepared using :dokuwiki:`ZynqMP SD image instructions <resources/tools-software/linux-software/zynq_images>`

Reference links
-------------------------------------------------------------------------------

- :external+hdl:doc:`AD916x-FMC HDL project page <projects/ad916x_fmc/index>`
- :external+hdl:doc:`Build an HDL project <user_guide/build_hdl>`
- :adi:`UG-1526 AD916x user guide <media/en/technical-documentation/user-guides/AD9161-9162-9163-9164-UG-1526.pdf>`
- :dokuwiki:`AD-FMCDAQ2 ZCU102 hardware setup reference <resources/eval/user-guides/ad-fmcdaq2-ebz/quickstart/zcu102>`
- :dokuwiki:`AD9081 ZynqMP/ZCU102 setup and validation reference <resources/eval/user-guides/ad9081_fmca_ebz/quickstart/zynqmp>`

.. note::

   Validate your selected JESD mode, DAC device, and lane-rate combination
   before hardware bring-up, and ensure the clocking setup matches the
   configuration.
