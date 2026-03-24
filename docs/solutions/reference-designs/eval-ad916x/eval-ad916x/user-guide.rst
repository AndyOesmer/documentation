.. _eval-ad916x user-guide:

User guide
===============================================================================

This page summarizes the AD916x evaluation flow using the ADI HDL reference
design and links to the original board and project documentation.

Hardware guide
-------------------------------------------------------------------------------

General setup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The AD916x-FMC setup is validated on
:xilinx:`ZCU102 <products/boards-and-kits/ek-u1-zcu102-g.html>` through HPC0.
The evaluation board can be operated from the on-board clock generator or an
external clock source, depending on the JESD mode and lane-rate target.

.. IMAGE PLACEHOLDER: AD916x-FMC ZCU102 block diagram screenshot/export

Clock source selection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The HDL project documentation defines clock source jumper use for EVAL-AD916x:

.. list-table::
   :header-rows: 1

   * - Jumper
     - Position
     - Function
   * - J61
     - Mounted
     - Use on-board clock generator
   * - J61
     - Unmounted
     - Use external clock source

For example, AD9163 mode 2 builds at high lane rate may require external
clocking with J61 removed.

ZCU102 boot mode and connections
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For Linux bring-up on ZCU102:

#. Insert SD card in connector J100.
#. Connect EVAL-AD916X-FMCZ to ZCU102 HPC0.
#. Connect Micro-USB UART to J83.
#. Connect Ethernet to P12 for remote IIO.
#. Set SW6 for SD boot mode according to the ZCU102 board documentation and
  ADI quickstart references.
#. Apply 12V power to J52 and power on the board.

The ADI ZCU102 quickstarts are useful references for board-level setup order,
UART bring-up, and safe shutdown behavior.

SPI and control connectivity
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the AD916x HDL design on ZCU102, PS SPI0 is used to control these devices:

- AD9508
- ADF4355
- AD916x device

The HDL project also defines GPIO and interrupt mappings for ZCU102, including
DMA interrupt and JESD link interrupt paths.

Reference details are documented in the AD916x HDL project SPI section.

Supported DAC variants
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1

   * - Device
     - Resolution
     - Notes
   * - AD9161
     - 11-bit
     - RF DAC family member
   * - AD9162
     - 16-bit
     - RF DAC with digital upconversion support
   * - AD9163
     - 16-bit
     - RF DAC family member
   * - AD9164
     - 16-bit
     - RF DAC with direct digital synthesis support

.. HDL configuration guide
.. -------------------------------------------------------------------------------

.. Default build behavior
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. The AD916x project supports multiple JESD modes through make parameters.
.. A default build from `projects/ad916x_fmc/zcu102` targets AD9162 in mode 8.

.. .. code-block:: bash

..   cd hdl/projects/ad916x_fmc/zcu102
..   make

.. Configuration parameters
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. .. list-table::
..    :header-rows: 1

..    * - Parameter
..      - Description
..      - Typical values
..    * - `ADI_DAC_DEVICE`
..      - Select DAC device
..      - `AD9161`, `AD9162`, `AD9163`, `AD9164`
..    * - `ADI_DAC_MODE`
..      - Select predefined JESD mode
..      - `08` default, other modes by device support
..    * - `ADI_LANE_RATE`
..      - Select lane rate
..      - `12.5` (default), `4.16` and other supported values

.. Custom JESD parameter override
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. When needed, users can override JESD transport parameters in the build command,
.. including `M`, `L`, `S`, and `NP`, based on the selected DAC data-sheet limits.

.. .. code-block:: bash

..   cd hdl/projects/ad916x_fmc/zcu102
..   make ADI_LANE_RATE=12.5 ADI_DAC_DEVICE=AD9163 ADI_DAC_MODE=02

.. .. code-block:: bash

..   cd hdl/projects/ad916x_fmc/zcu102
..   make ADI_DAC_DEVICE=AD9164 ADI_LANE_RATE=12.5 M=1 L=8 S=4 NP=16

Schematic, PCB Layout, Bill of Materials
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Design files (schematics, PCB layout, and BOM) are available from the
respective product pages:

- :adi:`EVAL-AD9161-FMCZ`
- :adi:`EVAL-AD9162-FMCZ`
- :adi:`EVAL-AD9163-FMCZ`
- :adi:`EVAL-AD9164-FMCZ`

Software guide
-------------------------------------------------------------------------------

The evaluation boards are supported through the :ref:`libiio` library, which
is cross-platform (Windows, Linux, Mac) with bindings for C, C#, Python,
MATLAB, and others. Applications that interface via libiio include:

- :ref:`iio-oscilloscope` — graphical waveform and spectrum analyzer
- :external+scopy:doc:`Scopy <index>` v2.0 or later (requires the IIO plugin)
- :external+pyadi-iio:doc:`index` — Python interface

For a step-by-step walkthrough of connecting and using these tools with the
:adi:`EVAL-AD7768-1` / :adi:`EVAL-ADAQ7768-1` on the ZedBoard, see the
:ref:`ad77681 quickstart zed` guide.


.. Software resources
.. -------------------------------------------------------------------------------

.. Linux support
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. - :git-linux:`AD9162 IIO driver <drivers/iio/adc/ad9162.c>`
.. - AD916x Linux device trees for ZCU102 mode variants (AD9161/2/3/4)

.. Bench validation checkpoints
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. After boot and driver initialization, validate:

.. #. Device visibility with `iio_info`.
.. #. Clock lock and source selection status.
.. #. JESD link state transitions to DATA/no alignment errors.
.. #. DAC output frequency/power consistency on external RF instrumentation.

.. For JESD debug methodology, use :dokuwiki:`JESD status utility <resources/tools-software/linux-software/jesd_status>`.

.. HDL support
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. - :git-hdl:`AD916x-FMC HDL project source <projects/ad916x_fmc>`
.. - :external+hdl:doc:`AD916x-FMC HDL project page <projects/ad916x_fmc/index>`
.. - :external+hdl:doc:`Build an HDL project <user_guide/build_hdl>`

.. Board and documentation assets
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. - :adi:`EVAL-AD916X-FMCZ board page <EVAL-AD916X>`
.. - :adi:`UG-1526 AD916x user guide PDF <media/en/technical-documentation/user-guides/AD9161-9162-9163-9164-UG-1526.pdf>`
.. - :dokuwiki:`AD-FMCDAQ2 ZCU102 quickstart setup sequence <resources/eval/user-guides/ad-fmcdaq2-ebz/quickstart/zcu102>`
.. - :dokuwiki:`AD9081 ZCU102 quickstart validation sequence <resources/eval/user-guides/ad9081_fmca_ebz/quickstart/zynqmp>`
