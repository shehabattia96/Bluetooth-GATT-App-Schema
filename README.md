# Bluetooth GATT App Schema

> GATT is Generic Attribute Profile, as defined in the [Bluetooth Core 5.4 Specification, Vol1, Part 1, Section 6, Bluetooth Application Architecture, Sub-Section 6.4, Generic Attribute Architecture](./Bluetooth_Core_v5.4_Vol1_Part1_6_Bluetooth_Application_Architecture.pdf) ([External Link](https://www.bluetooth.com/specifications/specs/core-specification-5-4/)).


## Problem Statement

As an application designer, I want to be able to define GATT Profile information to be shared unambiguously between my Central and Peipheral applications. There are no reliable schema to share this information between application codebases.


## GATT Profile Information

This is the GATT Profile Information that we are interested in:
- Service Names and UUID's
    - Both official and custom Services.
        - Official Services are defined in the [GATT Spec Supplement](./GATT_Specification_Supplement_v9.pdf).
- Advertized Services (i.e. available to any scanning centrals).
- Descriptor Names and UUID's.
- Characteristic Names and UUID's
- Characteristic and Descriptor payload information.
    - Somtimes payloads will follow the GATT Format Types spec defined in the [GATT Spec Supplement](./GATT_Specification_Supplement_v9.pdf).
    - However, sometimes the payload is encoded with multiple datatypes. We wish to identify these here as well. For example, `0b0001001` the first/_LSB zero_ bit could flag one sensor's state and the fourth could flag an application state. These are custom implementations that only the app designers would be aware of.


## Central and Peripheral Responsibilities

Typically, 

The Peripheral application will:
- broadcast available Services.
- handle to READ/WRITE requests.
- handle NOTIFY requests.
- handle connection status changes.
- handle special requests, such as firmware flashing (tethethered or OTA).

The Central application will:
- scan for nearby peripheals.
    - It may filter results based on known Service UUID's.
- discover available Services.
- WRITE/READ characteristics or descriptors.
- request NOTIFY characteristics.
- handle OnDataRecieved events.


## Resources

- Bluetooth's [Assigned Numbers](https://bitbucket.org/bluetooth-SIG/public/src/main/assigned_numbers/uuids/): contains yaml files with official Service and Characteristic UUID's.
- Nordic's [Bluetooth Numbers Database](https://github.com/NordicSemiconductor/bluetooth-numbers-database/tree/master/v1): contains json files with Service and Characteristic UUID's, among other things. Some of these are non-official numbers.
- [GATT Spec Supplement](./GATT_Specification_Supplement_v9.pdf)
- [Bluetooth Core Specification 5.4](https://www.bluetooth.com/specifications/specs/core-specification-5-4/)
- [Bluetooth Basics article from Silicon Labs](https://community.silabs.com/s/article/x-deprecated-kba-bt-0102-ble-basics-master-slave-gatt-client-server-data-rx-x?language=en_US)