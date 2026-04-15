# 🧠 DermaVision AI  
### Skin Health Assessment & Progress Simulation Platform  

<p align="center">
  <img src="https://img.shields.io/badge/Status-MVP-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Backend-FastAPI-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Frontend-React%20%2B%20Vite-blueviolet?style=for-the-badge" />
  <img src="https://img.shields.io/badge/CV-YOLOv8%20%7C%20MediaPipe-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge" />
</p>

---

## 🚀 Overview

**DermaVision AI** is a computer vision-powered web application that analyzes facial skin from a single image and generates:

- 🧬 Lesion detection (acne, spots)
- 🎯 Zone-based facial analysis
- 🌡️ Hyperpigmentation heatmaps
- 📊 Clinical severity grading (IGA scale)
- ✨ Simulated progress preview (2-week & 4-week)

> ⚡ Built for hackathon MVP → scalable to production SaaS

---

## 🧠 Problem Statement

Skin health analysis today:
- ❌ Requires dermatologist visits (₹500–₹2000)
- ❌ Not accessible in Tier-2/3 cities
- ❌ No continuous tracking between visits

### 💡 Our Solution

A **smartphone-based AI tool** that provides:
- Instant skin report  
- Visual progress simulation  
- Objective tracking  

---

## 🏗️ Tech Stack

### 🖥️ Frontend
- ⚛️ React 18
- ⚡ Vite
- 🎨 TailwindCSS
- 🔗 Axios
- 🧭 React Router

### ⚙️ Backend
- 🚀 FastAPI (Python 3.11)
- 📦 Pydantic
- 🔒 Rate limiting (SlowAPI)

### 🧪 Computer Vision
- 🧠 MediaPipe → Face Mesh (468 landmarks)
- 🎯 YOLOv8 → Lesion Detection
- 🖼️ OpenCV → Image Processing & Simulation

---

## 🏗️ System Architecture

```mermaid
flowchart TD

    A[User uploads facial image] --> B[Frontend React + Vite]
    B --> C[POST /api/analyze]
    C --> D[FastAPI Backend]

    D --> E[Image Validation Gate]
    E --> E1[File type check]
    E --> E2[File size check]
    E --> E3[Image dimension check]
    E --> E4[Face confidence check]

    E --> F[FaceZoneService - MediaPipe]
    E --> G[LesionDetectionService - YOLOv8]
    E --> H[HyperpigmentationService - OpenCV]

    F --> I[Zone masks + landmarks]
    G --> J[Lesion detections + counts]
    H --> K[Heatmap + pigmentation metrics]

    I --> L[ResultAggregatorService]
    J --> L
    K --> L

    L --> M[Annotated image + severity grade]

    I --> N[SimulationService]
    K --> N
    N --> O1[2-week preview]
    N --> O2[4-week preview]

    M --> P[Structured JSON Response]
    O1 --> P
    O2 --> P

    P --> Q[Frontend Results Page]
    Q --> R[Annotated image]
    Q --> S[Severity badge]
    Q --> T[Zone breakdown]
    Q --> U[Simulation comparison]
```

---

## 🔥 Key Features

### 📸 Image Upload & Validation
- JPEG/PNG only
- Face detection confidence check
- Rejects invalid images

### 🧠 Face Zone Segmentation
- Forehead
- Left Cheek
- Right Cheek
- Nose
- Chin

### 🎯 Lesion Detection
- YOLOv8-based bounding boxes
- Per-zone lesion count
- Total lesion score

### 🌡️ Hyperpigmentation Analysis
- LAB color space
- Adaptive thresholding
- Heatmap overlay

### 📊 Severity Grading (IGA Scale)
| Lesions | Grade |
|--------|------|
| 0 | Clear |
| 1–5 | Mild |
| 6–20 | Moderate |
| 21+ | Severe |

### ✨ Simulation Engine
- 2-week improvement preview
- 4-week improvement preview
- Bilateral filtering + tone correction

---

## ⚙️ Component Architecture
```mermaid
flowchart TB
    subgraph Frontend
        A[React + Vite + TypeScript]
        B[Pages]
        C[Components]
        D[API Layer]
    end

    subgraph Backend
        E[FastAPI]
        F[Validation]
        G[FaceZoneService]
        H[LesionDetectionService]
        I[HyperpigmentationService]
        J[ResultAggregatorService]
        K[SimulationService]
    end

    subgraph CV_Models
        L[MediaPipe]
        M[YOLOv8]
        N[OpenCV]
    end

    A --> D
    D --> E
    E --> F
    F --> G
    F --> H
    F --> I

    G --> L
    H --> M
    I --> N

    G --> J
    H --> J
    I --> J
    G --> K
    I --> K

    J --> E
    K --> E
    E --> A
```

## 📂 Project Structure

```text
dermavision-ai/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── services/
│   │   ├── models/
│   │   └── utils/
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── api/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── pages/
│   │   └── types/
│   └── package.json
└── README.md
```

### 1. Setup / Installation
Very important. People should know how to run it.

```md
## ⚙️ Setup Instructions
```

### Backend
```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```
### Frontend
```bash
cd frontend
npm install
npm run dev
```
