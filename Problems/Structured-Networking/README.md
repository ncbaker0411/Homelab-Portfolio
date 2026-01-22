# Problem Statement
When I first began building my homelab, it consisted of unorganized equipment sourced from piles of e-waste. Devices were stacked, cables were unlabeled, and changes to the network required trial-and-error troubleshooting. While functional, this setup did not reflect the level of organization, reliability, or professionalism expected in real-world IT environments.

If I intend to present myself as a professional, my homelab and network should reflect that same level of care, structure, and intentional design.

## Goals
The objective of this project was to redesign the physical and logical networking layer of the lab to:
* Eliminate cable sprawl and ambiguity
* Make the network easy to understand at a glance
* Reduce accidental outages during maintenance
* Enable safe expansion and iteration
* Mirror professional IT and data center practices on a smaller scale

## Solution Overview
I implemented a structured networking approach using a compact 10-inch rack, keystone-based cabling, and a centralized switch to act as the Layer 2 core of the lab.

Key design decisions included:
* Centralizing all Ethernet connections through keystone ports
* Using a dedicated switch instead of device-to-device cabling
* Physically separating network infrastructure from compute roles
* Documenting both logical and physical layouts

This transformed the lab from a collection of devices into a clearly defined system.

## Before and After: Physical Network Transformation
### Before
* Devices stacked or placed wherever space was available
* Ethernet cables running directly between systems with no labeling
* No clear distinction between network infrastructure and compute devices
* Troubleshooting required tracing cables by hand or disconnecting devices to test

This configuration worked, but any change introduced risk. Maintenance was slow, and the likelihood of accidental outages was high.

![Before Image]()

### After
* All devices mounted or organized within a dedicated 10-inch rack
* Ethernet connections routed through keystone ports for consistent patching
* Centralized switch serving as a clear network aggregation point
* Clean cable routing with predictable paths and minimal slack
* Physical layout documented and repeatable

With this structure in place, changes can be made confidently, new devices can be added without disruption, and troubleshooting is faster and more methodical.

![After Image]()

## 3D-Printed Rack
To support the compact form factor and improve organization, all rack components were 3D printed. This allowed for customization that would be difficult or expensive using off-the-shelf hardware.

Design Files and Resources
* [10 Inch Rack](https://makerworld.com/en/models/1294480-lab-rax-10-server-rack-5u?from=search#profileId-1325352)
* [10 Inch Rack Extension](https://makerworld.com/en/models/1294478-lab-rax-1-5u-posts-panels#profileId-1325351)
* [Switch Mount](https://makerworld.com/en/models/1476615-tp-link-tl-sg108-pe-sf1006p-10-inch-rack-mount?from=search#profileId-1541277)
* [Keystones](https://makerworld.com/en/models/825894-10-inch-keystone-patchpanel-x10-ports?from=search#profileId-769490)
* [Dell Optiplex Mount](https://www.printables.com/model/1225356-slim-dell-optiplex-mount-for-10-inch-rack-with-key)
* [Raspberry Pi Dock](https://makerworld.com/en/models/1293865-2u-7-sbc-holder-for-10-rack#profileId-1324551)
* [Hot Swap Drive Bays](https://makerworld.com/en/models/1446421-10-inch-rack-2u-6-x-3-5-inch-hdd-hot-swap#profileId-2260787)

## Lessons Learned
This project reinforced that reliability often comes from clarity rather than complexity. Even without advanced features like VLANs or managed switching, a well-organized physical network dramatically improves stability, safety, and confidence when working on live systems.

Structured networking is not just about aesthetics—it is a foundational practice that enables every other system in the lab to operate predictably.
