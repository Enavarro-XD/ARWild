# 🐾 ARWild - Animal Detection with Augmented Reality using AI

## 📌 Project Description

ARWild is a portable **computer vision system powered by artificial intelligence** that allows **real-time animal detection and visualization through an augmented reality (AR) interface**.

The system uses an embedded device with **AI acceleration (NPU)** to run **YOLO-based object detection models**, together with a camera and a visualization system (screen or optical viewer similar to *smart glasses*).

When the system detects an animal, visual information is displayed over the real-world environment, allowing **immediate species identification through graphical overlays**.

This project aims to demonstrate how **AI + embedded systems + augmented reality** can be applied to:

- environmental monitoring
- education
- wildlife observation
- biodiversity conservation

---

# 🌍 Relation to the SDGs

This project mainly contributes to the following **Sustainable Development Goals (SDGs)**.

### SDG 15 – Life on Land

The system can be used for:

- wildlife monitoring
- species identification
- environmental conservation support
- ecological education

### SDG 9 – Industry, Innovation and Infrastructure

It promotes the development of:

- intelligent embedded systems
- Edge AI devices
- new technological applications for environmental protection

---

# 🎯 Project Objective

To develop a **portable augmented reality animal detection device** capable of:

- detecting animals in real time using **YOLO**
- running AI inference on **embedded hardware**
- displaying information through **augmented reality overlays**
- operating autonomously as a portable system

---

# 💡 Motivation

Observing animals in natural environments often requires experience to quickly identify species.

This project aims to:

- democratize access to wildlife identification tools
- support environmental education
- explore applications of **Edge AI**

It also demonstrates how small devices can run **computer vision models locally without relying on cloud computing**.

---

# 🧠 Technologies Used

- Computer Vision
- Artificial Intelligence
- YOLO Object Detection
- Edge AI
- Embedded Systems
- Embedded Linux
- Augmented Reality

---

# 🧩 Project Hardware

The system will use a board based on the **SOPHGO SG2002 processor**.

### Main Specifications

| Component | Description |
|---|---|
| CPU | SOPHGO SG2002 |
| Main Core | 1GHz RISC-V C906 / ARM A53 |
| Secondary Core | 700MHz RISC-V |
| Low Power Core | 8051 (25–300 MHz) |
| NPU | 1 TOPS INT8 |
| Memory | 256MB integrated DDR3 |
| Storage | TF Card / SD NAND |
| Camera | MIPI CSI (4 lane) |
| Display | MIPI DSI |
| Audio | Integrated microphone and amplifier |
| Connectivity | WiFi 6 + BLE 5.4 |
| USB | USB 2.0 Type-C |
| Operating System | Linux (Buildroot / Debian) |

---

# 🖥 System Architecture

![System Architecture](images/1_system_architecture.png)

---

# 🧭 Project Development Stages

![Project Development Stages](images/2_development_stages.png)

---

# 📋 System Requirements

## 🔰 Minimum Viable Requirements (MVP)

The system must satisfy the following core functionalities to be considered a valid prototype:

### Functional Requirements (Mandatory)

- Capture video input from a camera in real time (low resolution allowed)
- Perform object detection using a YOLO-based model on embedded hardware
- Detect at least a small set of animal classes (e.g., 2–5 species)
- Display detection results on a screen (bounding boxes and/or labels)
- Operate fully offline (no cloud dependency)
- Execute inference locally using the embedded processor/NPU

---

## 🟡 Extended Functional Requirements (Optional)

The following features are desirable but not required for the initial prototype:

- Display confidence scores for detections
- Support a larger number of animal species
- Provide a more advanced AR-style overlay
- Include audio feedback or notifications
- Improve visualization with smoother UI

---

## ⚙️ Non-Functional Requirements

These define acceptable performance ranges rather than strict targets:

- **Latency:** 200 ms – 1 second per detection (acceptable for prototype)
- **Frame Rate (FPS):** 5–10 FPS is sufficient
- **Accuracy:** 60–80% detection accuracy is acceptable
- **Power Consumption:** Must run on a portable power source (e.g., power bank)
- **Portability:** System should be reasonably compact, but not necessarily wearable in early stages

---

# ⚠️ System Constraints

## 🔻 Hardware Constraints

- Limited memory (256MB RAM)
- Limited compute performance (1 TOPS NPU)
- Restricted storage capacity
- Power limitations for portable operation

Implications:

- Use lightweight models (e.g., YOLO Tiny / Nano)
- Apply quantization (e.g., INT8)
- Use reduced input resolution

---

## 🔻 Software Constraints

- Limited compatibility with RISC-V / ARM environments
- Restricted availability of optimized AI libraries
- Embedded Linux limitations (Buildroot / minimal Debian)

---

## 🔻 Design Constraints

- The system is **not required to be fully integrated into smart glasses**
- Device size and weight may exceed wearable limits in early versions
- AR visualization may be simulated using a standard display

---

# 🔄 System Flexibility & Adaptability

To ensure project feasibility, the system must support multiple deployment formats:

### Supported Operation Modes

1. **Basic Prototype Mode**
   - Camera + embedded board + external display

2. **Portable Mode**
   - Self-contained unit with battery and screen

3. **AR Mode (Experimental)**
   - Integration with optical viewer or smart glasses (if feasible)

4. **Alternative Display Mode**
   - Output to external screens (e.g., monitor, tablet, vehicle display)

---

# 📉 Accepted Margin of Error

Given the experimental nature of the project, the following limitations are acceptable:

- Occasional misclassification of animals
- Reduced performance in real-world environments
- Low frame rate compared to commercial systems
- Detection delays up to 1 second
- Limited number of detectable species

---

# 🎯 Key Engineering Principle

> The goal of this project is to demonstrate a functional proof of concept for real-time animal detection using embedded AI and AR visualization — not to achieve full product-level integration or performance.

---

# 🚧 Development Strategy Constraint

The system will be developed in stages:

1. Validate detection on a standard display
2. Optimize performance on embedded hardware
3. Integrate portability (battery-powered system)
4. Attempt AR visualization (if feasible)

AR integration is considered a **final-stage feature**, not a core requirement.
---

# 📊 Data Handling

## Data Sources

Training data for the model will come from animal datasets such as:

- COCO dataset
- Open Images Dataset
- Wildlife image datasets

## Data Flow

![Data Flow](images/3_data_flow.png)

## Storage

- Dataset stored for training
- Optimized model stored on the SD card
- Detection results processed in temporary memory

---

# 🧪 Controlled Testing

To validate system performance, different testing scenarios will be conducted.

### Test 1 – Basic Detection

Objective:

Verify that the model correctly detects animals.

Procedure:

- display animal images to the camera
- evaluate detection accuracy

---

### Test 2 – Real-Time Detection

Objective:

Evaluate system performance using live video.

Metrics:

- FPS
- detection latency
- CPU/NPU usage

---

### Test 3 – Real Environment Test

Objective:

Evaluate the system in real environments.

Scenario:

- parks
- nature reserves
- zoos

---

# 📈 Performance Analysis

The following indicators will be evaluated.

### Model Accuracy

Percentage of correct detections.

### Latency

Time between image capture and detection result.

### Energy Consumption

Measurement of embedded system power usage.

### FPS

Frames processed per second.

---

# 🚀 Deployment

The system will be deployed as a **portable device** composed of:

- embedded Linux board
- camera
- screen or optical viewer
- portable battery

Possible device formats.

### Option 1 – Integrated Screen

A small display shows detection results.

### Option 2 – Smart Glasses Style Viewer

Using:

- semi-transparent mirror
- mini projector or micro display

This allows overlay information to appear directly in the user's field of view.

---

# 🔬 AI Technologies

The project will use **YOLO (You Only Look Once)** for object detection.

Advantages:

- real-time detection
- high accuracy
- optimized for edge devices

The model will be optimized to run on the **1 TOPS NPU** available on the device.

---

# 📦 Project Structure

```
project/
│
├── dataset/
│
├── training/
│   ├── train_yolo.py
│
├── inference/
│   ├── detect.py
│
├── ar_interface/
│   ├── display.py
│
├── hardware/
│   ├── camera_driver
│
└── README.md
```

---

# 🔮 Future Work

Possible improvements for the system include:

- detection of more animal species
- GPS integration
- wildlife observation logging
- connection with mobile applications
- more advanced augmented reality features

---

# 👨‍💻 Development Team

Project developed by students for the **Intelligent Systems Prototyping course**.

---

# 📚 References

NI. (n.d.). *7 Steps in Creating a Functional Prototype*  
https://www.ni.com/es/solutions/design-prototype/7-steps-in-creating-a-functional-prototype.html

YOLO Object Detection  
https://pjreddie.com/darknet/yolo/

Edge AI Vision Alliance  
https://www.edge-ai-vision.com/

---

# ⭐ Project Status

🚧 In development
