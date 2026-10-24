# NMOSBCP004Forge Pro (v1.0.0)

### AMWA NMOS BCP-004-01 Receiver Capabilities & Constraint Schema Studio

---

## Overview

**NMOSBCP004Forge Pro** is an operational broadcast engineering workbench, constraint schema synthesizer, and stream compatibility validation CLI utility designed for broadcast control systems (BCS), IP routing matrix developers, systems integrators, and broadcast equipment manufacturers. It implements receiver capability modeling, machine-readable parameter constraint validation, and pre-flight routing verification conforming to:

- **AMWA BCP-004-01**: Receiver Capabilities (Specification & Best Current Practice)  
- **AMWA NMOS IS-04 v1.3**: Discovery & Registration (Receiver `caps` Schema)  
- **AMWA NMOS IS-05 v1.1**: Connection Management (Pre-Flight `staged` Validation)  
- **AMWA Parameter Registers**: Machine-Readable Parameter URN Namespaces  
- **SMPTE ST 2110-20**: Uncompressed Video Constraints (`video/raw`)  
- **SMPTE ST 2110-30 / ST 2110-31**: Linear and Non-PCM Audio Constraints  
- **IETF RFC 4175**: RTP Payload Format for Uncompressed Video

---

## Key Capabilities

1. **Interactive Receiver Capability Builder**:  
   - Visual configuration of receiver constraint sets across frame dimensions (min/max/step width and height), grain rates (rational fractions: 50/1, 60000/1001, 24000/1001, etc.), color sampling schemes (YCbCr-4:2:2, RGB), component bit depths (8, 10, 12-bit), channel counts (1..64), and packet times (0.125ms, 1.0ms).  
2. **IS-04 Receiver Resource JSON Synthesizer**:  
   - Generates compliant AMWA IS-04 v1.3 `receiver.json` descriptors with embedded `caps.media_types` and standardized parameter URNs (`urn:x-nmos:cap:format:...` and `urn:x-nmos:cap:transport:...`).  
   - 1-click clipboard copy and file downloads.  
3. **Pre-Flight Stream Compatibility Matcher**:  
   - Evaluates candidate sender streams (resolution, framerate, colorimetry, sampling, depth) against receiver capability schemas before routing.  
   - Outputs machine-readable status verdicts (`200 OK • COMPATIBLE` vs `400 BAD REQUEST • INCOMPATIBLE` with detailed parameter violation reports).  
   - Pre-filters routing matrix crosspoints in broadcast control systems (BCS) to prevent on-air decoder crashes.  
4. **10-Point Normative Compliance Auditor**:  
   - Automated test harness validating receiver schema root structures, MIME types, constraint sets, parameter URN namespaces, rational grain rates, and dimension boundaries.  
5. **Production Python CLI (`bcp004-cli.py`)**:  
   - Standalone CLI utility for automated broadcast CI/CD pipelines, supporting `build`, `match`, and `audit` operations.

---

## Getting Started

### Web Studio

Open `source-code/index.html` in any web browser. Runs 100% locally with zero external network or cloud dependencies.

### Command-Line Interface

\# Output standard IS-04 receiver resource JSON

python3 build/bcp004-cli.py build \--label "UHD Multiviewer Input Receiver 01"

\# Evaluate compatible stream (1080p50 10-bit YCbCr-4:2:2)

python3 build/bcp004-cli.py match \--width 1920 \--height 1080 \--fps 50.0 \--sampling YCbCr-4:2:2 \--depth 10

\# Evaluate incompatible stream (4K 60fps RGB 12-bit)

python3 build/bcp004-cli.py match \--width 3840 \--height 2160 \--fps 60.0 \--sampling RGB \--depth 12

\# Execute 10-point normative compliance audit

python3 build/bcp004-cli.py audit

### Automated Testing

python3 test\_bcp004.py