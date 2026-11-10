.. zephyr:code-sample:: ble_peripheral_hr
   :name: Heart-rate Monitor (Peripheral)
   :relevant-api: bt_hrs bt_bas bluetooth

   Expose a Heart Rate (HR) GATT Service generating dummy heart-rate values.

Overview
********

Similar to the :zephyr:code-sample:`ble_peripheral` sample, except that this
application specifically exposes the HR (Heart Rate) GATT Service. Once a device
connects it will generate dummy heart-rate values.


Requirements
************

* BlueZ running on the host, or
* A board with Bluetooth LE support

Building and Running
********************

Building a minimal variant
--------------------------

.. zephyr-app-commands::
   :zephyr-app: samples/bluetooth/peripheral_hr
   :board: qemu_cortex_m3
   :goals: build
   :gen-args: -DCONF_FILE=prj_minimal.conf

Building a minimal variant for bbc_microbit
-------------------------------------------

.. zephyr-app-commands::
   :zephyr-app: samples/bluetooth/peripheral_hr
   :board: bbc_microbit
   :goals: build
   :gen-args: -DCONF_FILE=prj_minimal.conf -DEXTRA_CONF_FILE=overlay-bt_ll_sw_split-minimal.conf

Using USB CDC ACM for the console
---------------------------------

For boards with a USB device controller, the console can be routed to a USB CDC
ACM serial port by applying the CDC ACM configuration and devicetree overlay:

.. zephyr-app-commands::
   :zephyr-app: samples/bluetooth/peripheral_hr
   :board: reel_board
   :goals: build flash
   :gen-args: -DEXTRA_CONF_FILE=overlay-cdc-acm.conf -DDTC_OVERLAY_FILE=cdc-acm.overlay

Connect the board to a host over USB and open the enumerated CDC ACM serial
port to view the sample output. The selected board must provide the
``zephyr_udc0`` devicetree node. The sample waits up to 10 seconds for the host
to open the port (DTR) before starting Bluetooth, so that early output is not lost.

Boards that already use CDC ACM as their default console, such as
``nrf52840dongle``, need no overlay; build them without the extra arguments.
