# 🦈 Real-Time Beach Protector  
### Intelligent Underwater Threat Detection and Deterrence System  

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/) 
[![Powered by Raspberry Pi](https://img.shields.io/badge/Powered%20by-Raspberry%20Pi-orange.svg)](https://www.raspberrypi.org/)
[![Topic: Computer Vision](https://img.shields.io/badge/Topic-Computer%20Vision-yellowgreen)](https://en.wikipedia.org/wiki/Computer_vision) 


![System Overview](./docs/images/system_overview.png)

---

## 🌊 Overview  

**Real-Time Beach Protector** is a modular AI-powered system designed to **detect harmful or dangerous marine species** in real time and automatically **trigger deterrent mechanisms** to protect swimmers and coastal areas.  

The system combines **computer vision**, **embedded AI**, and **multi-modal deterrent activation** to monitor underwater environments and respond autonomously. It is built around a **Raspberry Pi 5 (8GB)** with **four Raspberry Pi Camera Module 3 Wide NOIR** cameras providing 360° coverage, connected via an **Arducam Quad Camera Hub**.  

Infrared ring lights with light sensors provide night vision capabilities, and the Raspberry Pi interfaces with chemical, visual, and auditory deterrent modules through GPIO-controlled relays.  

---

## Demo Video

This is a Demstration of an image of a shark (NOT in the training dataset)
- [Real-time Solar Beach Monitoring and Marine Hazard Detection System in Action](https://youtube.com/shorts/FiiL1iqBk74)

---

## 🚀 Key Features  

✅ **Multi-Camera 360° Coverage**  
- Four NOIR cameras connected via an Arducam hub  
- Automatic IR illumination in low-light conditions  

✅ **AI-Powered Detection**  
- Trained on a **12,800+ image dataset** of underwater animals  
- Detects a wide range of **harmful and dangerous species**  
- Deployed on Raspberry Pi 5 using **EfficientNet B0** (best-performing model)  

✅ **Multi-Modal Deterrent System**  
- **Chemical deterrent** (repellent sprayer)  
- **Visual deterrent** (high-intensity strobe)  
- **Auditory deterrent** (low-frequency sound)  
- Automatically activated upon confirmed detection  

✅ **Remote Logging and Reporting**  
- Generates structured JSON logs for each detection  
- Sends data to a **central API** for remote monitoring and government oversight  

✅ **Scalable and Modular Architecture**  
- Supports multiple deterrent types and camera configurations  
- Easily extendable with new AI models or hardware accelerators  

---

## 🧠 System Architecture  

![Architecture](./docs/images/architecture_diagram.png)

The system integrates:  

- **Hardware Layer:**  
  - Raspberry Pi 5 (8GB)  
  - 4× Camera Module 3 Wide NOIR  
  - Arducam Quad Camera Hub  
  - IR LED rings + light sensors  
  - Deterrent modules (chemical, strobe, sound)  
  - Optional GPS module  

- **Software Layer:**  
  - Python-based inference pipeline  
  - TensorFlow Lite / ONNX runtime for edge deployment  
  - Async data logging and deterrent control threads  
  - RESTful API interface for reporting  

---

## 🧩 Methodology  

1. **Data Collection & Preprocessing**  
   - Dataset includes 23 marine species (fish, shark, jellyfish, etc.)  
   - Augmentation for varying light and turbidity conditions  
   - Dataset split: 80% train / 20% validation  

2. **Model Training**  
   - Three CNN architectures implemented:  
     1. RegNetY800 (baseline)  
     2. EfficientNet B0 *(best performer)*  
     3. EfficientNet B3 (advanced, heavier variant)  
   - Training performed on NVIDIA A100 GPU  
   - Final model quantized for Raspberry Pi deployment  

3. **Real-Time Detection**  
   - Inference via TensorFlow Lite on Pi  
   - Species probability threshold → deterrent activation  
   - Detection logged locally and via JSON API  

4. **Deterrent Activation Process**  
   - Model prediction > confidence threshold  
   - GPIO control triggers deterrent modules  
   - Event metadata stored with timestamp, species, and confidence  

---

## 📈 Results Summary  

| Model | Accuracy (%) | Inference Time (s) | Notes |
|:------|:-------------:|:------------------:|:------|
| RegNetY800 | 82.34 | 0.89 | Initial prototype |
| EfficientNet B0 | **87.59** | **0.51** | Best model for Pi |
| EfficientNet B3 | 89.02 | 1.23 | Too heavy for real-time |

**Performance:**  
- Achieved real-time inference at ~2 FPS on Raspberry Pi 5  
- IR-enhanced visibility enables operation in low light  
- Reliable detection of marine hazards including jellyfish and sharks  

---


## 🌐 JSON Reporting Format
Each detection event generates a structured JSON entry:

json
{
  "timestamp": "2025-11-09T18:22:31Z",
  "species": "Shark",
  "confidence": 0.88,
  "gps": [21.4563, 39.2531],
}

## 🔮 Future Work
Expand dataset with rare or region-specific species

Integrate AI accelerators (Hailo-8L, Jetson) for higher throughput

Deploy multi-sensor networks for larger beach coverage

Add cloud dashboard for live visualization and analytics

Implement adaptive deterrent intensity based on species and context


## 📚 References
The project builds upon recent research in underwater computer vision and shark deterrence systems, including:

ADA-SHARK (Martin et al., 2024)

Shark-EYE (Merencilla et al., 2021)

Underwater Fish Detection using Mask R-CNN (Khai et al., 2022)

Shark Detection from Aerial Imagery (Sharma et al., 2018)

Hart & Collin, Shark Senses and Repellents (2015)



Keywords: Underwater AI • Marine Safety • EfficientNet • Raspberry Pi • Real-Time Detection • Multi-Modal Deterrent


