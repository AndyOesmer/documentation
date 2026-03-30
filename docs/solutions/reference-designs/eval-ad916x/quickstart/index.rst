.. _eval-ad916x quickstart:

Quickstart
===============================================================================

This quickstart provides a baseline setup for the AD916x-FMC reference design
flow, aligned with the CN0540 quickstart structure.

.. toctree::

   ZCU102 <zcu102>

.. _eval-ad916x carriers:

Supported carriers
-------------------------------------------------------------------------------

The currently supported carrier is:

- :xilinx:`ZCU102 <products/boards-and-kits/ek-u1-zcu102-g.html>` on HPC0

Supported environments
-------------------------------------------------------------------------------

.. list-table::
   :header-rows: 1

   - - Board
     - HDL
     - Linux software
     - No-OS software
   - - :xilinx:`ZCU102 <products/boards-and-kits/ek-u1-zcu102-g.html>`
     - Yes
     - Yes
     - No

Hardware setup
-------------------------------------------------------------------------------

The :adi:`EVAL-AD916X` connects to the ZCU102 through the FMC connector (HPC0),
with UART and JTAG or Ethernet connections as needed by your software flow.

ZCU102 + EVAL-AD9164
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: ../images/ad9164fmc+zcu102.png
   :width: 800
