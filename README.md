# ROTA - Remote Open Trackpad Access

<p align="center">
  <img src="https://img.shields.io/badge/platform-macOS%20%7C%20iPadOS-blue" />
  <img src="https://img.shields.io/badge/Swift-5.9-orange" />
  <img src="https://img.shields.io/badge/license-MIT-green" />
</p>

ROTA is a high-performance remote desktop solution that allows you to control your Mac from your iPad with **native trackpad gestures**, **low-latency H.264 video streaming**, and **seamless input control**.

## ✨ Features

### 🎯 Native Input Experience
- **Direct Touch Positioning**: Tap anywhere to instantly move the cursor
- **Trackpad Gestures**: Two-finger scrolling, pinch to zoom
- **Double-Tap Drag**: Native macOS-style drag and drop
- **Keyboard Support**: Full keyboard input with text injection
- **Right-Click**: Long-press context menu support

### 🚀 High-Performance Streaming
- **H.264 Hardware Encoding**: ~60 FPS at 20 Mbps
- **Adaptive Bitrate**: Automatic quality adjustment based on network conditions
- **Low Latency**: < 100ms end-to-end delay on local network
- **Retina Display Support**: Automatic resolution scaling for high-DPI displays

### 🌐 Flexible Connectivity
- **iCloud Discovery**: Automatic host discovery via CloudKit
- **Remote Access**: Port forwarding support for internet access
- **Local Network**: Zero-configuration LAN connectivity
- **Fallback Support**: Automatic fallback to local IP if public IP fails

### 🔒 Security & Privacy
- **LAN-First**: Prefers local network connections
- **No Third-Party Servers**: Direct peer-to-peer connection
- **Open Source**: Full transparency of code and protocols

## 📥 Installation

### Mac Host

1. Download the latest release from [Releases](https://github.com/liyifenggit/ROTA/releases)
2. Open `ROTAHost.dmg` and drag the app to Applications
3. Launch `ROTAHost` and grant necessary permissions:
   - **Screen Recording**: Required for video streaming
   - **Accessibility**: Required for input control
4. The host will automatically publish itself to iCloud

### iPad Client

1. Build from source (App Store version coming soon):
   ```bash
   git clone https://github.com/liyifenggit/ROTA.git
   cd ROTA
   open ROTA.xcodeproj
   ```
2. Select the `ROTAClient` scheme and run on your iPad
3. Sign in with the same Apple ID used on your Mac

## 🎮 Usage

### Quick Start (Local Network)

1. **On Mac**: Launch ROTAHost
2. **On iPad**: Open ROTAClient and select your Mac from the discovered hosts
3. Tap "Connect" and choose "Open Live Stream (With Input)"

### Remote Access Setup

1. **Router Configuration**:
   - Forward ports `8090`, `8091`, `8092` to your Mac's local IP
   - Ports:
     - `8090`: Web server (health check)
     - `8091`: Video stream
     - `8092`: Input control

2. **Connect from anywhere**:
   - The iPad client will automatically try the public IP
   - Falls back to local IP if on the same network

### Controls

- **Single Tap**: Left click
- **Long Press**: Right click (context menu)
- **Double-Tap + Drag**: Click and drag
- **Two-Finger Scroll**: Scroll  (vertical/horizontal)
- **Pinch**: Zoom (simulates Cmd+Scroll)
- **Tap to Type**: Show keyboard and type

## 🛠️ Building from Source

### Requirements

- **macOS 13.0+** (Ventura or later)
- **iPadOS 16.0+**
- **Xcode 15.0+**
- **Swift 5.9+**
- **Apple Developer Account** (for signing)

### Build Instructions

```bash
# Clone the repository
git clone https://github.com/liyifenggit/ROTA.git
cd ROTA

# Open in Xcode
open ROTA.xcodeproj

# Select target:
# - ROTAHost: Mac application
# - ROTAClient: iPad application

# Build and run (Cmd+R)
```

### CloudKit Setup

ROTA uses CloudKit for device discovery. To use CloudKit:

1. Enable iCloud in your project's Signing & Capabilities
2. Create a CloudKit container or use the default container
3. Ensure both Mac and iPad targets use the same container

## 📡 Network Protocols

### Video Stream (Port 8091)
- **Protocol**: Custom binary over TCP
- **Video Codec**: H.264 (High Profile, Level 4.2)
- **Packet Format**:
  - Type 0: Configuration (SPS/PPS)
  - Type 1: Frame (Keyframe flag + PTS + Data)
  - Type 2: Cursor Position

### Input Control (Port 8092)
- **Protocol**: Custom binary over TCP
- **Commands**:
  - `0x01`: Mouse Move
  - `0x02`: Mouse Click
  - `0x03`: Scroll
  - `0x04`: Zoom
  - `0x05`: Gesture
  - `0x06`: Key
  - `0x07`: Text

## 🐛 Troubleshooting

### Video not showing
- Ensure Screen Recording permission is granted
- Check that H.264 codec is supported (it is on all modern Macs)
- Verify network connectivity

### Input not working
- Grant Accessibility permission in System Settings
- Some system dialogs (window management) block programmatic input for security

### Connection timeout
- Check firewall settings
- Verify port forwarding if using remote access
- Ensure both devices are signed in with the same Apple ID for iCloud discovery

### High latency
- Use local network instead of remote access
- Reduce video quality in adaptive bitrate settings
- Check network bandwidth

## 🗺️ Roadmap

- [ ] App Store release
- [ ] Custom resolution/quality settings
- [ ] Audio streaming support
- [ ] File transfer
- [ ] Multi-monitor support
- [ ] Clipboard synchronization
- [ ] Performance metrics overlay

## 📄 License

MIT License - see [LICENSE](LICENSE) for details

## 🙏 Acknowledgments

- Apple's ScreenCaptureKit for efficient screen capture
- VideoToolbox for hardware H.264 encoding/decoding
- CloudKit for seamless device discovery

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/liyifenggit/ROTA/issues)
- **Discussions**: [GitHub Discussions](https://github.com/liyifenggit/ROTA/discussions)

## 🔐 Privacy & Legal

- [Privacy Policy](https://liyifenggit.github.io/ROTA/privacy.html)
- [Terms of Service](https://liyifenggit.github.io/ROTA/terms.html)

---

Made with ❤️ for the Apple ecosystem
