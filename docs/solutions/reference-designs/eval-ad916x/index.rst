.. _eval-ad916x:

EVAL-AD916X
===============================================================================

AD9161/AD9162/AD9163/AD9164 high speed RF DAC reference design.

Overview
-------------------------------------------------------------------------------

The :adi:`AD9161 <AD9161>`, :adi:`AD9162 <AD9162>`, :adi:`AD9163 <AD9163>`,
and :adi:`AD9164 <AD9164>` are high speed RF DACs intended for demanding
wideband transmitter applications. The AD916x-FMC HDL reference design provides
a validated path to evaluate JESD204 link bring-up, DAC data transport, and
clocking on supported FPGA carriers.

The HDL design supports configurable JESD operation modes, lane rates, and
device variants from a common build framework. For Linux bring-up, ADI Kuiper
images and ADI Linux device trees are available for supported ZynqMP platforms.

Features
-------------------------------------------------------------------------------

- Support for AD9161, AD9162, AD9163, and AD9164 devices
- JESD204B/C transmit path with configurable modes and lane rates
- Reference HDL flow on :xilinx:`ZCU102 <products/boards-and-kits/ek-u1-zcu102-g.html>`
- Integrated DMA/data-offload based data path in HDL reference design
- Linux software enablement through ADI kernel drivers and device trees
- IIO-based remote evaluation from a host PC

.. figure:: images/AD9164-FMCB-EBZTOP-web.png
   :align: center
   :width: 500

   EVAL-AD9164-1FMCZ

.. figure:: images/AD9164-FMCB-EBZBOTTOM-web.png
   :align: center
   :width: 500

   EVAL-AD9164-1FMCZ

.. toctree::
   :hidden:

   user-guide
   prerequisites
   iio-oscilloscope
   quickstart/index

Recommendations
-------------------------------------------------------------------------------

Follow the quickstart sequence before customizing JESD parameters. This gives a
known-good baseline for hardware setup, clocking, and software bring-up.

If questions come up, use the :ref:`EngineerZone support channels
<help-and-support>` after reviewing the links below.

Table of Contents
-------------------------------------------------------------------------------

#. :ref:`eval-ad916x user-guide`
#. :ref:`eval-ad916x prerequisites`
#. :ref:`eval-ad916x iio-oscilloscope`
#. :ref:`eval-ad916x quickstart`

Block Diagram
-------------------------------------------------------------------------------

The AD916x-FMC HDL documentation includes a complete block diagram and module
mapping for the ZCU102 design:

- :external+hdl:doc:`AD916x-FMC block design <projects/ad916x_fmc/index>`

.. More Information and Useful Links
.. -------------------------------------------------------------------------------

.. - :adi:`EVAL-AD916X-FMCZ product page <EVAL-AD916X>`
.. - :adi:`UG-1526 AD9161/AD9162/AD9163/AD9164 User Guide <media/en/technical-documentation/user-guides/AD9161-9162-9163-9164-UG-1526.pdf>`
.. - :git-hdl:`AD916x-FMC HDL source code <projects/ad916x_fmc>`
.. - :external+hdl:doc:`AD916x-FMC HDL project documentation <projects/ad916x_fmc/index>`
.. - :dokuwiki:`ZynqMP SD image workflow <resources/tools-software/linux-software/zynq_images>`

.. Software Projects and Platforms
.. -------------------------------------------------------------------------------

.. - :ref:`AD916x + ZCU102 quickstart <eval-ad916x quickstart zcu102>`
.. - :ref:`AD916x with IIO-Oscilloscope <eval-ad916x iio-oscilloscope>`
.. - :git-linux:`AD9162 Linux driver source <drivers/iio/adc/ad9162.c>`
.. - :git-linux:`AD9161 Linux DTSI (mode 8) <arch/arm64/boot/dts/xilinx/adi-ad9161-fmc-ebz.dtsi>`
.. - :git-linux:`AD9162 Linux DTSI (mode 8) <arch/arm64/boot/dts/xilinx/adi-ad9162-fmc-ebz.dtsi>`
.. - :git-linux:`AD9163 Linux DTSI (mode 8) <arch/arm64/boot/dts/xilinx/adi-ad9163-fmc-ebz.dtsi>`
.. - :git-linux:`AD9164 Linux DTSI (mode 8) <arch/arm64/boot/dts/xilinx/adi-ad9164-fmc-ebz.dtsi>`

Warning
-------------------------------------------------------------------------------

.. esd-warning::
