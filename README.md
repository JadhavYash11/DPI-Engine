# 🔍 DPI Engine – High Performance Deep Packet Inspection System

A C++ based Deep Packet Inspection (DPI) engine that parses raw PCAP files, reconstructs network flows using 5-tuples, extracts SNI from TLS handshakes, classifies applications, and applies rule-based traffic filtering.

---

## 🚀 Project Overview

This project simulates how enterprise firewalls and ISPs inspect and control encrypted HTTPS traffic.

Even though HTTPS is encrypted, the destination domain name is exposed in the TLS Client Hello message (SNI – Server Name Indication).  
This engine extracts that information to identify applications like YouTube, Facebook, Google, etc.

The system supports both:

- 🧵 Single-threaded architecture (learning mode)
- ⚡ Multi-threaded architecture (high-performance mode)

---

## 🏗️ Architecture

PCAP Input
↓
Packet Parsing (Ethernet → IP → TCP/UDP)
↓
Flow Tracking (5-Tuple Hashing)
↓
SNI Extraction (TLS Client Hello)
↓
Application Classification
↓
Rule Engine (IP / App / Domain Blocking)
↓
Filtered PCAP Output + Statistics Report


## 🧠 Key Features

- Manual Ethernet, IPv4, TCP, UDP parsing
- 5-tuple based flow tracking
- TLS SNI extraction
- Application classification
- Rule-based blocking:
  - Block by IP
  - Block by Application
  - Block by Domain
- Multi-threaded packet processing
- Real-time traffic statistics
- PCAP input/output support

## ⚙️ Build Instructions

## ⚙️ Build Instructions

### Single-threaded Version

```bash
g++ -std=c++17 -O2 -I include -o dpi_simple \
src/main_working.cpp \
src/pcap_reader.cpp \
src/packet_parser.cpp \
src/sni_extractor.cpp \
src/types.cpp

 multithreaded
g++ -std=c++17 -pthread -O2 -I include -o dpi_engine \
src/dpi_mt.cpp \
src/pcap_reader.cpp \
src/packet_parser.cpp \
src/sni_extractor.cpp \
src/types.cpp


---

  Run Section

```markdown
## ▶️ Running the Engine

Basic usage:

```bash
./dpi_engine test_dpi.pcap output.pcap


With blocking rules:
./dpi_engine test_dpi.pcap output.pcap \
    --block-app YouTube \
    --block-ip 192.168.1.50 \
    --block-domain facebook
