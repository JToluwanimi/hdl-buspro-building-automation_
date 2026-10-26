# HDL Buspro Building Automation System Analysis

> **Status:** Studied / Analyzed / Presented
> **Author:** Toluwanimi Jesusina
> **Context:** SIWES 2023 at H&O Automation Systems Ltd.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status](https://img.shields.io/badge/Status-Documented-green)]()

---

## 1. What is this?

A comprehensive technical analysis of the HDL Buspro system, a modular building automation solution. This repository documents the system architecture, communication protocols (RS485, UDP/IP), component integration, and wiring topologies required for smart home and commercial building management.

---

## 2. Why was it built?

During my SIWES at H&O Automation Systems Ltd, I conducted a deep-dive study into the HDL Buspro system. To synthesize this knowledge and demonstrate my understanding of industrial automation protocols, I developed and delivered a technical presentation to peers and supervisors. This repository serves as the permanent technical documentation of that study.

---

## 3. System Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        HDL BUSPRO ARCHITECTURE                              │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐    │
│  │                         FIELD LAYER                                 │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐             │    │
│  │  │  Relay   │  │  Dimmer  │  │  Curtain │  │  HVAC    │             │    │
│  │  │  Module  │  │  Module  │  │  Module  │  │  Module  │             │    │
│  │  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘             │    │
│  │       │             │             │             │                   │    │
│  │       └─────────────┴─────────────┴─────────────┘                   │    │
│  │                              │                                      │    │
│  │                    ┌─────────▼─────────┐                            │    │
│  │                    │  RS485 Bus        │                            │    │
│  │                    │  (Twisted Pair,   │                            │    │
│  │                    │   120 Ohm)        │                            │    │
│  │                    └─────────┬─────────┘                            │    │
│  └──────────────────────────────┼──────────────────────────────────────┘    │
│                                 │                                           │
│  ┌──────────────────────────────┼──────────────────────────────────────┐    │
│  │                         GATEWAY LAYER                               │    │
│  │                    ┌─────────▼─────────┐                            │    │
│  │                    │  Buspro Gateway   │                            │    │
│  │                    │  (RS485 ↔ UDP/IP) │                            │    │
│  │                    └─────────┬─────────┘                            │    │
│  └──────────────────────────────┼──────────────────────────────────────┘    │
│                                 │                                           │
│  ┌──────────────────────────────┼──────────────────────────────────────┐    │
│  │                         NETWORK LAYER                               │    │
│  │                    ┌─────────▼─────────┐                            │    │
│  │                    │  Ethernet Switch  │                            │    │
│  │                    │  (UDP/IP Backbone)│                            │    │ 
│  │                    └─────────┬─────────┘                            │    │
│  └──────────────────────────────┼──────────────────────────────────────┘    │ 
│                                 │                                           │
│  ┌──────────────────────────────┼──────────────────────────────────────┐    │ 
│  │                         USER LAYER                                  │    │
│  │                    ┌─────────▼─────────┐                            │    │
│  │                    │  Granite Display  │                            │    │
│  │                    │  / HDL ON App     │                            │    │
│  │                    └───────────────────┘                            │    │ 
│  └─────────────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Key Components Analyzed

| Component | Model | Function |
|-----------|-------|----------|
| Power Supply | MSP750.431 / MSP2400.232 | Provides 24V DC to bus |
| Buspro Gateway | HDL-MBUS01IP.431 | RS485 ↔ UDP/IP bridge |
| Relay Module | HDL-MR0816.432 | 8/12 channel switching |
| Dimmer Module | HDL-MD0403.432 | LED dimming |
| Curtain Controller | HDL-MC0403.432 | Motor control |
| AC Controller | MAC01.431 | HVAC control |
| Multifunctional Sensor | HDL-MSP07M.4C | PIR, LUX, Temp |
| Granite Display | HDL-MPTLC43.46 | Touch panel |
| DMX Controller | HDL-MDMX512 | Lighting scenes |

---

## 5. Communication Protocols

| Protocol | Layer | Purpose |
|----------|-------|---------|
| RS485 | Physical | Twisted-pair, bidirectional, 120 Ohm impedance |
| UDP/IP | Network | Backbone communication |
| HDL Buspro | Application | Device addressing, control |

---

## 6. Wiring Topologies

### 6.1 Single Subnet

- Up to 63 devices per subnet
- Daisy-chain (hand-in-hand) connection recommended
- Star topology not recommended for > 1000m

### 6.2 Multi-Subnet

- Up to 254 subnets
- Devices identified as "Subnet/Device" (e.g., "1/2")
- Gateways bridge subnets to Ethernet

---

## 7. Presentation & Technical Communication

This repository includes the presentation slides and photographic evidence of the technical delivery.

*[Insert presentation photos]*

---

## 8. Limitations

1. **Analysis Only** — This repository documents the study and presentation of the HDL Buspro system. It does not contain custom firmware or original hardware designs.
2. **No Hands-On Programming** — I studied the configuration software but did not program a full system independently.

---

## 9. Future Development

| Priority | Enhancement |
|----------|-------------|
| 1 | Integrate HDL Buspro with Home Assistant via RS485 |
| 2 | Develop custom IoT gateway |
| 3 | Study KNX protocol for comparison |

---

## 10. Lessons Learned

1. **System Integration** — Building automation requires seamless interoperability between hardware from different manufacturers.
2. **Protocol Hierarchy** — Understanding the difference between physical layer (RS485) and network layer (UDP/IP) is critical for troubleshooting.
3. **Technical Communication** — Explaining complex bus topologies to a non-technical audience requires clear diagrams and structured analogies.

---

## 11. Media

- Presentation slides (PDF)
- Presentation photos
- System topology diagrams

---

## 12. Repository Structure

```
hdl-buspro-building-automation/
├── README.md
├── LICENSE
├── docs/
│   ├── HDL_Buspro_Home_Automation_Presentation.pdf
│   ├── System_Architecture_Analysis.md
│   ├── Wiring_Topologies_and_Protocols.md
│   └── Component_Deep_Dive.md
├── media/
│   ├── presentation_slides/
│   └── presentation_photos/
└── configs/
    └── Single_Subnet_vs_Multi_Subnet.md
```

---

## 13. License

MIT License — see [LICENSE](LICENSE) for details.

---

## 14. Contact

**Toluwanimi Jesusina**
- Email: [jesusinatoluwanimi@gmail.com](mailto:jesusinatoluwanimi@gmail.com)
- LinkedIn: [linkedin.com/in/toluwanimi-jesusina](https://linkedin.com/in/your-profile)
```
