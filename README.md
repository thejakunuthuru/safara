# safara
Safara (Safe + Aura) - Your Intelligent Road Companion.  Drive smarter, safer, and with confidence. Safara combines advanced AI with your smartphone camera to transform your device into an intelligent driving assistant that watches the road when you can't.

# 🚗 Safara - AI-Powered Driving Assistant

<p align="center">
  <img src="assets/logo.png" alt="Safara Logo" width="200"/>
</p>

<p align="center">
  <strong>Your Intelligent Road Companion</strong>
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#architecture">Architecture</a> •
  <a href="#installation">Installation</a> •
  <a href="#roadmap">Roadmap</a> •
  <a href="#contributing">Contributing</a> •
  <a href="#license">License</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-iOS%20%7C%20CarPlay-blue" alt="Platform"/>
  <img src="https://img.shields.io/badge/Swift-5.9-orange" alt="Swift"/>
  <img src="https://img.shields.io/badge/Python-3.11-green" alt="Python"/>
  <img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="License"/>
  <img src="https://img.shields.io/badge/status-alpha-yellow" alt="Status"/>
</p>

---

## 📖 Overview

Safara transforms your smartphone into an intelligent driving assistant that combines advanced computer vision, AI-powered incident detection, and conversational AI to make every journey safer. Inspired by cutting-edge automotive AI systems like those in the Skoda Kushaq with Google Gemini integration, Safara brings premium driver assistance features to any vehicle.

### The Problem

Modern vehicles come with advanced driver assistance systems (ADAS), but millions of drivers in older vehicles lack access to these life-saving technologies. Existing dashcam apps are passive recording tools without intelligent awareness. Safara bridges this gap.

### The Solution

- **Smart Dashcam**: AI-powered incident detection that knows when something important happens
- **Real-time Assistance**: Computer vision algorithms that watch the road and alert you to hazards
- **Voice AI Companion**: Local LLM-powered assistant for hands-free interaction
- **Intelligent Storage**: Only saves what matters, with AI-generated summaries
- **Privacy-First**: Local processing keeps your data secure

---

## ✨ Features

### 🎥 Intelligent Dashcam
- **AI-Powered Event Detection**
  - Automatic collision detection
  - Hard braking events
  - Near-miss incidents
  - Sudden lane changes
  - Anomaly detection
  
- **Smart Recording**
  - Continuous loop recording
  - Event-triggered save (configurable pre/post buffer)
  - Efficient H.265/HEVC compression
  - Configurable quality (720p - 4K)
  - Low-light enhancement

### 🛡️ Safety Features
- **Computer Vision Alerts**
  - Forward collision warning
  - Lane departure detection
  - Pedestrian and cyclist detection
  - Traffic sign recognition (speed limits, stop signs, yield)
  - Vehicle tracking and trajectory prediction
  
- **Driver Monitoring**
  - Distraction detection (looking at phone)
  - Drowsiness alerts
  - Hands-off-wheel detection (future)

### 🤖 AI Assistant
- **Local LLM Integration**
  - Natural language conversation
  - Context-aware responses (time, location, driving conditions)
  - Multi-turn dialogue with memory
  - Voice-to-text and text-to-voice
  
- **Smart Capabilities**
  - Trip summaries and highlights
  - Incident explanation and analysis
  - Navigation assistance
  - Weather and traffic queries
  - Calendar integration
  - Hands-free messaging and calls

### 📊 Analytics & Insights
- Trip logging with GPS tracking
- Driving behavior scoring
- Fuel efficiency estimation
- Maintenance reminders
- Incident history and patterns
- Exportable reports for insurance

### 🚗 CarPlay Integration
- Optimized in-car interface
- Voice-first interaction
- Minimal distraction design
- Quick access to alerts
- Now Playing integration

### 🔒 Privacy & Security
- **Local-First Processing**
  - On-device AI inference
  - No cloud dependency for core features
  - Your videos stay on your device
  
- **Optional Cloud Features**
  - End-to-end encrypted backups
  - Privacy filters (blur faces/plates)
  - Granular sharing controls
  - GDPR compliant

---

## 🏗️ Architecture

### Tech Stack

#### iOS/CarPlay App
```
- Language: Swift 5.9+, SwiftUI
- Minimum iOS: 16.0
- Frameworks:
  * AVFoundation (camera capture)
  * Vision (object detection)
  * Core ML (on-device inference)
  * Speech (voice recognition)
  * CarPlay (in-car interface)
  * MapKit (location services)
  * CloudKit (cloud sync)
```

#### Computer Vision Engine
```
- Language: Python 3.11+
- Libraries:
  * OpenCV 4.8+ (video processing)
  * NumPy, SciPy (numerical computing)
  * PyTorch/TensorFlow Lite (model inference)
  * YOLO v8 (object detection)
  * MediaPipe (real-time CV)
```

#### AI/ML Models
```
- Object Detection: YOLOv8n (optimized for mobile)
- Lane Detection: Custom CNN + Hough Transform
- LLM: Llama 3.2 3B (quantized) or Mistral 7B
- Speech: Apple Speech Framework + Whisper (offline)
- TTS: Apple AVSpeechSynthesizer
```

#### Backend (Optional Cloud Services)
```
- Language: Python (FastAPI) / Node.js
- Database: PostgreSQL + TimescaleDB
- Storage: AWS S3 / CloudKit
- Cache: Redis
- Queue: Celery / AWS SQS
```

### System Architecture
```
┌─────────────────────────────────────────────────────────┐
│                     iOS App Layer                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │   SwiftUI    │  │   CarPlay    │  │  Widgets     │  │
│  │  Interface   │  │  Interface   │  │   (Today)    │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                          │
┌─────────────────────────────────────────────────────────┐
│                  Core Services Layer                     │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Camera Manager    │  Video Processor             │  │
│  │  (AVFoundation)    │  (Frame buffer, encoding)    │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │  ML Inference      │  Event Detector              │  │
│  │  (Core ML/Vision)  │  (Incident classification)   │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │  LLM Engine        │  Voice Manager               │  │
│  │  (llama.cpp)       │  (Speech/TTS)                │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Storage Manager   │  Cloud Sync                  │  │
│  │  (SQLite, FileSystem) │ (CloudKit/S3)            │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                          │
┌─────────────────────────────────────────────────────────┐
│              ML Models & Processing                      │
│  ┌────────────┐ ┌────────────┐ ┌──────────────────┐   │
│  │  YOLOv8    │ │Lane Model  │ │  LLM (Llama 3.2) │   │
│  │ (Core ML)  │ │ (Core ML)  │ │   (quantized)    │   │
│  └────────────┘ └────────────┘ └──────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

### Data Flow
```
Camera Feed → Frame Capture → Preprocessing → ML Inference
                    ↓                              ↓
              Video Buffer                   Detections
                    ↓                              ↓
              Circular Buffer ← Event Detection ← Classification
                    ↓                              ↓
            [Incident?] ─Yes→ Save Video + Generate Summary
                    ↓                              ↓
                   No                      Notify User + LLM
                    ↓                              ↓
              Discard Frame              Store Metadata + Upload
```

---

## 🚀 Getting Started

### Prerequisites

- macOS 13.0+ (for development)
- Xcode 15.0+
- iOS device with iOS 16.0+ (simulator limited for camera features)
- Apple Developer Account (for CarPlay entitlements)
- Python 3.11+ (for CV engine development)
- Homebrew (recommended)

### Installation

#### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/safara.git
cd safara
```

#### 2. iOS App Setup
```bash
cd ios
pod install  # or swift package resolve
open Safara.xcworkspace
```

Configure your development team and bundle identifier in Xcode.

#### 3. Python CV Engine Setup
```bash
cd cv-engine
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

#### 4. Download ML Models
```bash
# Object detection model
python scripts/download_models.py --model yolov8n

# LLM (this will be large, ~4GB)
python scripts/download_models.py --model llama-3.2-3b-quantized
```

#### 5. Configure Environment
```bash
cp .env.example .env
# Edit .env with your API keys (optional cloud features)
```

#### 6. Run the App
- Open `Safara.xcworkspace` in Xcode
- Select your device
- Build and run (⌘R)

### Running Tests
```bash
# iOS tests
cd ios
xcodebuild test -workspace Safara.xcworkspace -scheme Safara -destination 'platform=iOS Simulator,name=iPhone 15'

# Python tests
cd cv-engine
pytest tests/
```

---

## 📱 Usage

### Basic Dashcam Mode
1. Launch Safara
2. Grant camera and location permissions
3. Tap "Start Recording"
4. Mount your phone securely on dashboard
5. Safara runs in background and detects incidents automatically

### Voice Assistant
- Say "Hey Safara" or tap microphone button
- Ask questions: "What's the speed limit here?"
- Give commands: "Navigate to nearest gas station"
- Get summaries: "Summarize my trip"

### CarPlay
1. Connect iPhone to CarPlay
2. Launch Safara from CarPlay home
3. Voice-first interface for safety
4. Alerts appear as banners

### Incident Review
1. Tap notification when incident detected
2. Review AI summary and video clip
3. Save to camera roll or cloud
4. Share with insurance if needed

---

## 🗺️ Roadmap

### Phase 1: MVP (Current - Q2 2025)
- [x] Basic camera capture and recording
- [x] Simple incident detection (hard braking)
- [ ] Local video storage
- [ ] Basic iOS UI
- [ ] Event playback

### Phase 2: AI Enhancement (Q2-Q3 2025)
- [ ] YOLOv8 object detection integration
- [ ] Lane departure detection
- [ ] Forward collision warning
- [ ] Traffic sign recognition
- [ ] Local LLM integration
- [ ] Video summarization
- [ ] CarPlay basic integration

### Phase 3: Voice & Intelligence (Q3-Q4 2025)
- [ ] Voice assistant with Llama 3.2
- [ ] Context-aware conversations
- [ ] Proactive notifications
- [ ] Trip analytics dashboard
- [ ] Driving behavior scoring

### Phase 4: Cloud & Sharing (Q4 2025)
- [ ] Cloud backup (encrypted)
- [ ] Cross-device sync
- [ ] Family sharing
- [ ] Insurance integration API
- [ ] Community hazard sharing

### Phase 5: Android & Expansion (Q1 2026)
- [ ] Android app
- [ ] Android Auto integration
- [ ] Multi-camera support
- [ ] OBD-II diagnostics
- [ ] Fleet management features

### Future Considerations
- AR navigation overlay
- Predictive maintenance
- Driver coaching
- Gamification elements
- Hardware dashcam integration

---

## 🤝 Contributing

We welcome contributions! Safara is built in the open to make advanced driver assistance accessible to everyone.

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Development Guidelines

- Follow Swift style guide for iOS code
- PEP 8 for Python code
- Write unit tests for new features
- Update documentation
- Ensure CI/CD passes

### Areas We Need Help

- 🎨 UI/UX design improvements
- 🧠 ML model optimization for mobile
- 🌍 Internationalization (i18n)
- 📝 Documentation and tutorials
- 🐛 Bug reports and fixes
- 🧪 Testing on various devices
- 🚗 Real-world driving data for model training

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### Third-Party Licenses
- OpenCV: Apache 2.0
- YOLOv8: AGPL-3.0
- Llama: Custom Meta License
- See [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) for full list

---

## 🙏 Acknowledgments

- Inspired by advanced systems in Skoda Kushaq, Tesla Autopilot, and Comma.ai
- YOLOv8 by Ultralytics
- Llama by Meta AI
- OpenCV community
- Apple's Core ML and Vision frameworks
- All our contributors and beta testers

---

## 📞 Contact & Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/safara/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/safara/discussions)
- **Email**: support@safara.app
- **Twitter**: [@SafaraApp](https://twitter.com/SafaraApp)
- **Discord**: [Join our community](https://discord.gg/safara)

---

## 💰 Support the Project

Safara is free and open-source, but development takes time and resources.

- ⭐ Star this repo
- 🐛 Report bugs and suggest features
- 💻 Contribute code
- 📢 Spread the word
- ☕ [Buy us a coffee](https://buymeacoffee.com/safara)

---

## ⚠️ Disclaimer

Safara is a driver assistance tool and does NOT replace attentive driving. Always keep your eyes on the road, hands on the wheel, and mind on driving. The driver is solely responsible for the safe operation of their vehicle.

AI detection systems may have false positives/negatives. Do not rely solely on Safara for safety. Always drive defensively and follow all traffic laws.

Check local regulations regarding dashcam usage and recording laws in your jurisdiction.

---

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/yourusername/safara?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/safara?style=social)
![GitHub issues](https://img.shields.io/github/issues/yourusername/safara)
![GitHub pull requests](https://img.shields.io/github/issues-pr/yourusername/safara)

---

<p align="center">
  Made with ❤️ by developers who care about road safety
</p>

<p align="center">
  <strong>Drive Safe. Drive Smart. Drive with Safara.</strong>
</p>
