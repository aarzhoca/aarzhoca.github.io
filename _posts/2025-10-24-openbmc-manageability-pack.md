---
layout: post
title: "OpenBMC Manageability Pack — Sensors, Redfish/IPMI, and Recovery"
date: 2025-10-24 10:00:00 -0700
tags: [OpenBMC, Redfish, IPMI, PLDM, MCTP, Platform-Architecture]
description: A clean-room, vendor-neutral toolkit showing end-to-end manageability flows on OpenBMC.
---

**TL;DR:** I open-sourced a clean-room *OpenBMC Manageability Pack* that demonstrates end-to-end manageability flows:
sensors/FRU/SEL, Redfish/IPMI paths, and recovery/rollback + remote debug. It includes host tools to validate features
the way a bring-up or EOL line would.

### Why
Platform architects need repeatable workflows from DBus service hooks through Redfish/IPMI and field recovery.
This repo shows those patterns in a portable, testable way (works with upstream OpenBMC/QEMU).

### What’s inside
- BMC-side service stubs for sensors/FRU/SEL
- Redfish **UpdateService** example with rollback checks
- IPMI chassis/power/FRU sample flows
- Host tools: `redfish_sweep.py`, `obmcctl.py`
- CI for unit tests and a simple integration harness

### Try it
```bash
git clone https://github.com/aarzhoca/openbmc-manageability-pack
cd openbmc-manageability-pack
python3 -m venv .venv && source .venv/bin/activate
pip install -r host-tools/requirements.txt
python host-tools/redfish_cli/redfish_sweep.py --bmc https://127.0.0.1:8443 --user root --password 0penBmc
