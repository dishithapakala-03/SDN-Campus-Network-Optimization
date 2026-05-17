# 🌐 Enhanced SDN Controller Placement & Dynamic Load Balancing
### KSU Academic Project | Computer Networks Architecture — Spring 2026 | Business Analyst Portfolio

---

## 🎯 Business Problem

Large university campus networks suffer from **high control-plane latency, poor load distribution, and misplaced SDN controllers** under default configurations — causing slow application response times, research transfer bottlenecks, and degraded experience for thousands of concurrent users.

**The challenge:** How do you optimize a campus network's performance using only software — with zero hardware upgrades?

---

## 👥 Stakeholders

| Stakeholder | Business Need |
|---|---|
| Campus IT Operations | Reduce network complaints and support tickets |
| Researchers & Faculty | Fast, reliable data transfer for research workloads |
| Students | Low-latency access to cloud apps and streaming |
| University Administration | Network performance ROI without infrastructure spend |

---

## 📋 BA Perspective — What This Project Demonstrates

- **Requirements Definition:** Identified 6 performance KPIs to measure optimization success (RTT, throughput, packet rate, byte count, flow duration, packet loss)
- **As-Is vs To-Be Analysis:** Baseline (default) vs. Optimized (K-Median + DWRR) configuration comparison
- **Stakeholder Impact Mapping:** Translated network metrics into business outcomes (cost savings, uptime, user experience)
- **Solution Validation:** Controlled experiments under identical conditions — rigorous, reproducible, business-reportable

---

## 📊 Results — Business Impact Summary

| Metric | Before (Baseline) | After (Optimized) | Improvement |
|---|---|---|---|
| **Average Latency** | 4.071 ms | 0.215 ms | ↓ **94.7%** |
| **Network Throughput** | 38.3 Mbps | 93.6 Mbps | ↑ **144%** |
| **Packet Processing Rate** | 0.059 pkt/s | 0.590 pkt/s | ↑ **900%** |
| **Switch Packet Count** | 26 packets | 443 packets | ↑ **1,600%** |
| **Flow Duration** | 440.97 s | 751.24 s | ↑ **71%** |
| **Packet Loss** | 0% | 0% | ✓ Maintained |

> **Business Translation:** A 94.7% latency reduction and 144% throughput improvement with **zero hardware investment** — purely through intelligent software-level optimization. This validates the SDN value proposition for campus network operators.

---

## 🏗️ System Architecture

```
APPLICATION PLANE
  └── K-Median Engine (Python / scikit-learn / NetworkX)
        └── Identifies optimal controller placement nodes

CONTROL PLANE
  └── Ryu SDN Controllers × 2 (c1: port 6633, c2: port 6634)
        └── Dynamic Weighted Round Robin (DWRR) Load Balancer

DATA PLANE — Mininet Emulation
  └── 3-Tier Campus Topology
        ├── Core Layer: core1, core2
        ├── Distribution Layer: dist1*, dist2, dist3*, dist4
        └── Access Layer: acc1–acc4 → Hosts h1–h8
        (* = K-Median selected controller nodes)
```

---

## 🔬 Two-Algorithm Framework

### Algorithm 1 — K-Median Clustering for Controller Placement
- Constructs campus network graph using **NetworkX**
- Computes 10×10 pairwise latency matrix across all switches
- Identifies **dist1 and dist3** as optimal controller locations
- Advantage over K-Means: constrains controllers to **real network nodes** (not abstract centroids)

### Algorithm 2 — Dynamic Weighted Round Robin (DWRR)
- Computes per-link weights inversely proportional to current utilization: `w(l) = 1/(utilization + ε)`
- Steers new flows toward under-utilized paths in real time
- Uses live **OpenFlow 1.3** statistics from Ryu controllers
- Proactive flow rules installed at switch connection (reduces PACKET_IN overhead)

---

## 🛠️ Technology Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Mininet](https://img.shields.io/badge/Mininet-Network_Emulator-orange?style=flat-square)
![Ryu](https://img.shields.io/badge/Ryu-SDN_Framework-blue?style=flat-square)
![OpenFlow](https://img.shields.io/badge/OpenFlow-1.3-green?style=flat-square)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![NetworkX](https://img.shields.io/badge/NetworkX-Graph_Analysis-red?style=flat-square)

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `Project_Report.pdf` | Full academic paper with methodology, results, and analysis |
| `Code_Implementation.ipynb` | K-Median placement algorithm + DWRR implementation |
| `Project_Code.txt` | Complete source code reference |
| `Project_PresentationSlides.pptx` | Executive presentation of findings |
| `Initial_Report_SDN_Dishitha_Pakala.docx` | Initial project proposal and scoping |
| `CN_Dishitha_SDN.pptx` | Technical deep-dive slides |

---

## 🎓 Academic Context

**Course:** Computer Networks Architecture — Spring 2026
**Institution:** Kennesaw State University, Department of Computer Science
**Author:** Dishitha Pakala

---

## 💡 Key Takeaway for BA Roles

This project demonstrates the ability to:
✅ Define measurable KPIs before beginning a technical initiative
✅ Conduct controlled baseline vs. optimized comparisons (as-is / to-be)
✅ Translate deeply technical results (RTT, throughput, OpenFlow) into business language
✅ Deliver quantified ROI without requiring stakeholders to understand the underlying technology
