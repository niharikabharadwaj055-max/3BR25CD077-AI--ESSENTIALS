# 🚦 Smart Traffic Lights Using Local AI

### A Decentralized Edge-AI Approach for Adaptive Traffic Management and Emergency Vehicle Priority

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![AI](https://img.shields.io/badge/AI-Computer%20Vision-orange)
![Edge Computing](https://img.shields.io/badge/Edge-Computing-green)
![Traffic Management](https://img.shields.io/badge/Smart%20Traffic-Management-red)
![LaTeX](https://img.shields.io/badge/LaTeX-IEEE-blue)

---

## 📌 Overview

Traditional traffic lights generally operate using fixed timers. While this approach is simple and inexpensive, it cannot respond effectively when traffic conditions change suddenly.

This project proposes a **Smart Traffic Light System using Local Artificial Intelligence (AI) and Edge Computing**.

Instead of sending all camera footage to a remote cloud server, cameras installed near an intersection send traffic information to a **local smart-pole computer**. The local AI system analyzes the traffic and provides signal-control decisions with reduced dependence on cloud communication.

The system can also detect **emergency vehicles such as ambulances** and initiate an appropriate traffic-signal priority sequence.

### Core Concept

```text
Street Cameras
      │
      ▼
Smart-Pole Computer
(Local Edge AI)
      │
      ├──────────────► City Cloud Server
      │                  Metadata
      ▼
Traffic-Light Controller
      │
      ▼
Adaptive Traffic Signals
```

---

## 🎯 Objectives

The major objectives of this project are:

* 🚗 Detect vehicles using computer vision.
* 📊 Estimate traffic density and queue length.
* 🚦 Dynamically adjust traffic-signal timing.
* ⚡ Perform AI processing locally using edge computing.
* 🌐 Reduce dependence on continuous cloud connectivity.
* 📡 Reduce unnecessary transmission of raw video.
* 🚑 Detect emergency vehicles.
* 🟢 Provide safe emergency signal priority.
* ☁️ Send selected traffic metadata to a cloud server.
* 📈 Support long-term traffic analysis.

---

## ❗ Problem Statement

Fixed-time traffic signals cannot efficiently respond to rapidly changing traffic conditions.

For example, one road may have very few vehicles while another road has a long queue. However, both may continue to receive predetermined signal durations.

Cloud-based AI systems can provide intelligent traffic analysis, but sending continuous camera streams to remote servers can increase network requirements and introduce communication latency.

An additional challenge is **emergency vehicle movement**. Ambulances may encounter unnecessary delays when traffic signals are unaware of their presence.

Therefore, this project proposes a decentralized system that performs traffic analysis close to the road and provides adaptive signal control.

---

## 💡 Proposed Solution

The proposed system uses:

1. **Street Cameras**

   * Capture traffic video.
   * Monitor vehicles approaching the intersection.

2. **Smart-Pole Computer**

   * Performs local AI inference.
   * Detects vehicles.
   * Estimates traffic density.
   * Detects emergency vehicles.

3. **Traffic-Light Controller**

   * Receives control instructions from the edge computer.
   * Adjusts signal phases within predefined safety constraints.

4. **City Cloud Server**

   * Stores selected metadata.
   * Performs historical traffic analysis.
   * Supports city-level traffic planning.

---

## 🏗️ System Architecture

```text
                    ┌─────────────────────┐
                    │    Street Cameras  │
                    └──────────┬──────────┘
                               │
                               │ Video
                               ▼
                    ┌─────────────────────┐
                    │ Smart-Pole Computer │
                    │                     │
                    │   Local Edge AI     │
                    │                     │
                    │ • Vehicle Detection │
                    │ • Traffic Density   │
                    │ • Queue Estimation  │
                    │ • Emergency Detect. │
                    └─────────┬───────────┘
                              │
                ┌─────────────┴──────────────┐
                │                            │
                │ Control                    │ Metadata
                ▼                            ▼
      ┌──────────────────┐         ┌──────────────────┐
      │ Traffic-Light    │         │ City Cloud       │
      │ Controller       │         │ Server           │
      └────────┬─────────┘         └──────────────────┘
               │
               ▼
      ┌──────────────────┐
      │ Adaptive Traffic │
      │ Signals          │
      └──────────────────┘
```

---

## 🤖 AI Components

### Vehicle Detection

A YOLO-based object-detection model can be used to identify vehicles from camera frames.

Possible classes include:

* Car
* Bus
* Truck
* Motorcycle
* Ambulance
* Fire engine
* Police vehicle

The detected vehicles can be counted to estimate traffic conditions.

---

### 📊 Traffic Density Estimation

For lane `i`:

```text
Nᵢ = Number of detected vehicles
Cᵢ = Estimated lane capacity
```

Normalized occupancy:

```text
Oᵢ = Nᵢ / Cᵢ
```

A traffic-demand score can be calculated as:

```text
Sᵢ = w₁Nᵢ + w₂Oᵢ + w₃Qᵢ
```

where:

* `Nᵢ` = vehicle count
* `Oᵢ` = lane occupancy
* `Qᵢ` = queue length
* `w₁, w₂, w₃` = configurable weights

The controller can use this score to determine which approach should receive additional green time.

---

## 🚑 Emergency Vehicle Priority

Emergency vehicles are treated as a special traffic condition.

The sy
