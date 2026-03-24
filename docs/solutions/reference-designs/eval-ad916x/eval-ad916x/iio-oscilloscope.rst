.. _eval-ad916x iio-oscilloscope:

Using the System with IIO-Oscilloscope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section describes how to connect to the AD916x target and validate signal
bring-up using IIO-Oscilloscope.

Before starting, ensure quickstart steps are complete:

#. Linux/no-OS stack is booted successfully.
#. UART console is available.
#. JESD and clocking are configured for your selected mode.

Connection modes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Local IIO-Oscilloscope
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Use local mode when the target platform runs a desktop environment.

#. Connect DisplayPort monitor, keyboard, and mouse to ZCU102.
#. Launch IIO-Oscilloscope on target.
#. Select local ADI IIO context and open capture/controls.

Remote IIO-Oscilloscope
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Use remote mode when IIO-Oscilloscope is running on a host PC.

#. Connect UART over J83 and login on serial console.
#. Check the target network address:

   .. code-block:: bash

      ip addr

#. Start IIO-Oscilloscope on host PC.
#. Go to connection settings and select remote context.
#. Enter the board URI, typically `ip:<board_ip>`.

If no DHCP address is assigned, set a static address in the same subnet as the
host PC and reconnect.

AD916x bring-up checks in IIO
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use IIO controls to validate these items in order:

#. Device discovery

   - AD916x target device appears in context
   - Relevant DMA/JESD-backed channels are visible

#. Clock and JESD status

   - Link state reaches DATA
   - No persistent SYSREF alignment/link errors

#. Tone generation path

   - Enable DDS/NCO path or DMA waveform source
   - Set known frequency and amplitude
   - Confirm expected RF output on spectrum analyzer

#. Repeatability

   - Power-cycle board and verify same procedure reproduces the expected result

Practical validation flow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A typical bench validation loop:

#. Program known HDL configuration.
#. Boot software image and connect via IIO.
#. Configure a deterministic CW output.
#. Measure output frequency and level externally.
#. Log JESD and device state for each tested mode.

Shutdown and filesystem safety
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For Linux-based systems, always shut down cleanly to avoid filesystem
corruption.

.. code-block:: bash

   sudo shutdown -h now

References
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- :git-iio-oscilloscope:`IIO-Oscilloscope releases <releases>`
- :dokuwiki:`IIO-Oscilloscope overview <resources/tools-software/linux-software/iio_oscilloscope>`
- :dokuwiki:`JESD status utility <resources/tools-software/linux-software/jesd_status>`
- :dokuwiki:`AD9081 ZCU102 remote IIO workflow reference <resources/eval/user-guides/ad9081_fmca_ebz/quickstart/zynqmp>`
