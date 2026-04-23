# 🐾 ARWild - Animal Detection with Augmented Reality using AI
![Description](ARWILD.png)

## 📌 Project Description

ARWild is a portable **computer vision system powered by artificial intelligence** that enables **real-time animal detection and visualization through an augmented reality (AR) interface**.

The system uses an embedded device with **AI acceleration (NPU)** to run **YOLO-based object detection models**, together with a camera and a visualization system (screen or optical viewer similar to *smart glasses*).

When an animal is detected, visual information is displayed over the real-world environment, allowing **immediate species identification through graphical overlays**.

This project focuses on demonstrating a **functional proof of concept**, prioritizing system feasibility over full product-level integration.

It aims to explore how **AI + embedded systems + augmented reality** can be applied to:

- environmental monitoring  
- education  
- wildlife observation  
- biodiversity conservation  

---

# 🌍 Relation to the SDGs
![Objetives](ODS.png)

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

To develop a **portable animal detection system with augmented visualization capabilities** that:

- detects animals in near real time using **YOLO**
- runs AI inference on **embedded hardware**
- displays detection results through a visual interface (screen or AR-like system)
- operates locally without internet dependency  

---
# 💡 Motivation

Observing animals in natural environments often requires experience to quickly identify species.

This project aims to:

- democratize access to wildlife identification tools  
- support environmental education  
- explore real-world applications of **Edge AI**  

It also demonstrates how low-power devices can run **computer vision models locally without relying on cloud computing**.

---
# 🔬 AI Technologies

Uses **YOLO** for real-time detection.

Optimized for:

- low-power devices  
- edge inference  
- NPU execution  

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

![Hardware](sg2002-diagram.png)

The system uses a board based on the **SOPHGO SG2002 processor**.

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

![Board SG2002](images/lichervnano.jpg)
![Board SG2002](images/pantalla.jpg)

---

# 🖥 System Architecture

![System Architecture](images/1_system_architecture.png)

---
# ⚖️ Analysis of Solutions and Evaluation of Alternatives

For Edge AI execution, the following hardware and model options were evaluated:

### Hardware Evaluation

| Alternative | Advantages | Disadvantages | Decision |
|---|---|---|---|
| **Raspberry Pi 4** | Large community support | High power consumption and no native NPU | Discarded |
| **ESP32-S3** | Very low cost and power consumption | Insufficient performance for real-time YOLO | Discarded |
| **LicheeRV Nano (SG2002)** | **1 TOPS NPU, low cost, RISC-V architecture** | High technical learning curve | **Selected** |

### AI Model Selection

The **YOLOv8 Nano** model is selected, quantized to **INT8**. Although YOLOv5 is lighter, YOLOv8 provides a better accuracy/latency balance after compilation using the Sophgo toolchain (TPU-MLIR).

---

# ⚙️ Optimización del Modelo y Toolchain del NPU

Para obtener resultados en el hardware real (SG2002), es obligatorio implementar el flujo de compilación cruzada. Sin esto, el NPU no reconocerá el modelo y la CPU se saturará.

### 🔄 Flujo de Conversión (TPU-MLIR)
1. **Exportación:** Convertir el modelo entrenado de PyTorch (`.pt`) a formato `ONNX`.
2. **Cuantización (INT8):** Transformar los pesos del modelo de 32 bits a 8 bits. Esto es vital para que el modelo quepa en los 256MB de RAM y para activar el acelerador de 1 TOPS.
3. **Compilación:** Generar el binario final `.cvimodel` que el SDK de Sophgo puede ejecutar.

### 🛠 Stack de Software para Implementación
* **Lenguaje:** C (utilizando el SDK `CVI_TDL`) para garantizar el procesamiento en tiempo real.
* **Aceleración:** Uso de la unidad de procesamiento de tensores (TPU) para liberar la CPU de tareas de visión artificial.

# 🧭 Project Development Stages

![Project Development Stages](images/2_development_stages.png)

# 📋 System Requirements

## 🔰 Minimum Viable Requirements (MVP)

The system must:

- Capture video input in real time (low resolution allowed)
- Perform animal detection using a lightweight YOLO-based model
- Detect a limited number of species (e.g., 2–5 classes)
- Display results visually (bounding boxes and labels)
- Run fully offline (no cloud dependency)
- Execute inference locally on the embedded device

---

## 🟡 Optional Features (Non-Critical)

- Display confidence scores  
- Support more species  
- Improve AR-style visualization  
- Add audio feedback  
- Enhance UI/UX  

---

## ⚙️ Performance Expectations (Non-Functional)

The system is not expected to reach commercial-level performance:

- **Latency:** up to 1 second  
- **FPS:** 5–10 FPS  
- **Accuracy:** ~60–80%  
- **Power:** portable (power bank)  
- **Portability:** compact but not necessarily wearable  

### 🌡️ Environmental & Operational Requirements

- Operate within **0°C to 40°C**
- Maintain performance under variable lighting
- Tolerate moderate humidity
- Handle partial visibility (fog, dust, light rain)
- Degrade gracefully under adverse conditions

---

# ⚠️ System Constraints

## 🔻 Hardware Constraints

- 256MB RAM limitation  
- 1 TOPS NPU performance limit  
- Limited storage and power  
- Thermal limitations due to compact design  
- No active cooling system  

This requires:

- lightweight models (YOLO Tiny / Nano)  
- model quantization (INT8)  
- reduced input resolution  

---

## 🔻 Software Constraints

- Limited compatibility with RISC-V / ARM  
- Restricted AI framework support  
- Embedded Linux limitations  

---

## 🔻 Design Constraints

- Full smart glasses integration is **not required**  
- Device size and weight may exceed wearable limits  
- AR visualization can be simulated using a normal display  
- Passive cooling only (no fan)
- Basic environmental protection required for outdoor use  

The project prioritizes **functionality over miniaturization**.

---

# 🌡️ Environmental Operating Conditions

## Overview

The system is designed for outdoor use where environmental factors directly affect performance.
---

## Temperature

- High temperature → thermal throttling, lower FPS  
- Mitigation: heatsink, dynamic FPS scaling  

---

## Lighting

- Affects detection accuracy  
- Mitigation: adaptive exposure, robust training  

---

## Humidity

- Risk of condensation  
- Mitigation: enclosure, lens protection  

---

## Weather

- Rain/fog reduce visibility  
- Mitigation: preprocessing, dataset robustness  

---

## Power Interaction

- High load increases temperature and power usage  
- Mitigation: dynamic resource management  

---

# 🔄 System Flexibility & Adaptability

To ensure feasibility, the system supports multiple formats:

### Operation Modes

1. **Basic Prototype**
   - Camera + board + external display  

2. **Portable Device**
   - Self-contained with battery  

3. **AR Mode (Experimental)**
   - Optical viewer or smart glasses (if possible)  

4. **Alternative Output**
   - External screen (monitor, tablet, vehicle display)  

---

# 📉 Accepted Margin of Error

As a prototype, the system may:

- misclassify animals  
- run at low FPS  
- have detection delays  
- perform inconsistently in real environments  

These limitations are acceptable for validation purposes.

---

# 🎯 Key Engineering Principle

> The goal is to demonstrate a functional proof of concept for real-time animal detection using embedded AI, not to deliver a fully optimized commercial product.

---

# 🚧 Development Strategy Constraint

Development will follow progressive stages:

1. Validate detection on a standard display  
2. Optimize performance on embedded hardware  
3. Add portability (battery-powered system)  
4. Attempt AR integration (if feasible)  

AR is considered a **final-stage feature**, not a core requirement.

# 📊 Data Handling

## Data Sources

Training data will include:

- COCO dataset  
- Open Images Dataset  
- Wildlife datasets  

## Data Flow

![Data Flow](images/3_data_flow.png)

## Storage

- Training datasets stored externally  
- Optimized model stored on SD card  
- Detection processed in memory  

---

# 🧪 Controlled Testing

### Test 1 – Basic Detection
Verify detection using static images.

### Test 2 – Real-Time Detection
Measure FPS, latency, and resource usage.

### Test 3 – Real Environment
Test in parks, reserves, or zoos under:

- different lighting conditions  
- temperature variation  
- real animal movement  
- partial occlusion  

---

# 💰 Project Budget

| Item | Quantity | Unit Cost (COP) | Total (COP) |
|---|---|---|---|
| LicheeRV Nano (includes camera) | 1 | $100.000 | $100.000 |
| Mini LCD/OLED Display | 1 | $120.000 | $120.000 |
| Class 10 MicroSD Card (32GB) | 1 | $25.000 | $25.000 |
| Power Bank / Li-Po Battery | 1 | $35.000 | $35.000 |
| **TOTAL** | | | **$280.000** |

---

# 📈 Performance Analysis

- Accuracy  
- Latency  
- Energy consumption  
- FPS  
- Thermal behavior  
- Performance under environmental stress  

---

# 🛠 Tools and Applied Standards

### Design Tools
* **KiCad / EasyEDA:** For designing power distribution and peripheral connections.
* **TPU-MLIR:** Sophgo compiler used to convert PyTorch models into `.cvimodel` files.
* **Buildroot/Debian:** For generating the embedded operating system image.

### Standards and Regulations
* **ISO/IEC 29110:** Software engineering guideline for small projects (VSEs).
* **IEEE 802.11ax Standard:** To ensure compatibility with WiFi 6 networks.
* **Ethical AI Guidelines:** Minimization of bias in the local wildlife dataset.

---
# 🚀 Deployment

The system may be deployed as:

- embedded board  
- camera  
- display or viewer  
- portable battery  

### Possible formats:

**Option 1 – Screen-based system**  
Simple and reliable visualization  

**Option 2 – AR viewer (experimental)**  
Overlay using optical components  

---
# 📦 Project Structure

    project/
    │
    ├── model/
    │   ├── yolo_model.cvimodel
    │   └── labels.txt
    │
    ├── src/
    │   ├── main.c
    │   ├── inference.c
    │   ├── camera.c
    │   ├── display.c
    │
    ├── drivers/
    ├── scripts/
    ├── config/
    ├── build/
    └── README.md

---
# 📈 Results Analysis (Midterm Milestone)

At the midpoint of the course, the project shows the following progress:

* **PC Inference:** YOLOv8n model successfully trained for 5 species with a mAP of 0.75.
* **Compilation:** Model conversion to ONNX format was achieved.
* **Hardware:** The LicheeRV Nano board now runs a functional Linux operating system with active video output to the mini display.

**Pending:** Complete INT8 quantization so the model can run on the NPU without exhausting RAM.

---

# 🔮 Future Work

- detection of more animal species  
- GPS integration  
- wildlife observation logging  
- mobile app integration  
- advanced AR features  

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
Pruebas
![P](images/pa.gif)
![D](images/vi.gif)
