# Group Monitoring in Mobile IoT

IoT devices carried by people detect each other by radio proximity, form groups when enough of them are in contact, and report to a backend that tracks group membership, lifetime and statistics.

| | |
|---|---|
| Course | Networked Software for Distributed Systems |
| University | Politecnico di Milano, M.Sc. Computer Science and Engineering |
| Semester | Academic year 2023/24 |
| Type | Team project |

## Overview

- **Devices (Contiki-NG, simulated in COOJA):** each mote broadcasts UDP packets to discover nearby devices, keeps a list of mutual contacts, and reports group formation to the backend over MQTT.
- **Network:** an RPL border router connects the wireless motes, which reach each other over multiple hops through a static IPv6 border router.
- **Backend (Node-RED):** creates groups, updates their members, removes members that time out, dismantles groups that fall below the minimum size, and computes group lifetime and cardinality statistics.

The full design and results are in the [project report](<NSDS project/Group_Monitoring_in_Mobile_IoT Report.pdf>).

## Repository structure

| Path | Contents |
|---|---|
| [`NSDS project/mqtt-mote/`](NSDS%20project/mqtt-mote/) | Contiki-NG mote that handles MQTT and UDP communication |
| [`NSDS project/udp-signaler/`](NSDS%20project/udp-signaler/) | Contiki-NG mote that sends proximity signals |
| [`NSDS project/rpl-border-router/`](NSDS%20project/rpl-border-router/) | RPL border router with a small web server |
| [`NSDS project/Node-RED/`](NSDS%20project/Node-RED/) | Node-RED flow and its function nodes |
| [`NSDS project/GroupMonitoringProject.csc`](NSDS%20project/GroupMonitoringProject.csc) | COOJA simulation |
| [`NSDS project/Contiki-how-to-run.txt`](NSDS%20project/Contiki-how-to-run.txt) | Step-by-step run instructions |

## Getting started

The project runs in the course's Contiki-NG virtual machine with Docker for Node-RED. In short:

1. Copy the project into your Contiki-NG installation and start the COOJA simulator (`ant run` in `tools/cooja`).
2. Load `GroupMonitoringProject.csc` and recompile the three motes.
3. Configure the local Mosquitto broker to bridge to the course MQTT broker, then restart it.
4. Start the RPL border router with `make TARGET=cooja connect-router-cooja`.
5. Start the Node-RED container (http://127.0.0.1:1880), import the flow, and start the simulation.

The complete steps are in [`NSDS project/Contiki-how-to-run.txt`](NSDS%20project/Contiki-how-to-run.txt).

## Tech stack

Contiki-NG, COOJA, C, MQTT, UDP, RPL, Node-RED, JavaScript.

## Team

Rishabh Tiwari and Alexandre Boving.
