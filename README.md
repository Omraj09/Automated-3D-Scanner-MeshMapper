# Development of an Automated 3D Scanning System

An open-source, cost-effective, and fully automated 3D scanning platform built through the integration of mechanical design, embedded electronics, and full-stack software development. By synchronizing a single high-resolution 16MP optical sensor with dual-axis stepper motor motion, this system completely eliminates the need for complex multi-sensor configurations (such as infrared or LiDAR arrays) to produce accurate, consistent 3D models suitable for reverse engineering, automation, and digital archiving.

---

## 🚀 Key Features

* **Complete Automation:** Eliminates manual scanning entirely by automating object rotation, camera positioning, and image capture into a single seamless workflow.
* **Single-Sensor Photogrammetry:** Leverages a 16-megapixel Arducam IMX519 camera module with programmable autofocus, bypassing expensive or bulky multi-sensor hardware arrays.
* **Custom Pi Shield PCB:** Centralizes power distribution, voltage regulation, and motor control onto a single board, removing fragile breadboard connections and maximizing electrical signal integrity.
* **Remote Web Interface:** A custom dashboard facilitating remote operation, real-time system status monitoring, manual hardware overrides, and full parameter tuning (shutter speed, motor angles, focus stacks, and cropping metrics).
* **Cloud Infrastructure Integration:** Dedicated cloud-based file management allows secure storage, remote accessibility, project organization, and streamlined handling of large image datasets.
* **True-to-Life Scaling Calibration:** A corrective global scaling workflow is permanently integrated into post-processing to fix depth discrepancies and maintain absolute physical fidelity.
* **Dual Operational Modes:** The scanner can be easily switched from fully automated mode to manual override mode whenever specific edge cases require manual manipulation.

---

## 🛠️ System Hardware & Specifications

The hardware architecture uses a Raspberry Pi 4B as a central processing unit to bridge user dashboard inputs directly to low-level mechanical actuation registers via a custom interface board.

### Hardware Component Configurations

| Component | Specification / Model | Role in System |
| :--- | :--- | :--- |
| **Central Controller** | Raspberry Pi 4 Model B | Main processing unit; coordinates peripheral devices, executes control logic, handles data flow, and hosts the web interface backend. |
| **Optical Sensor** | Arducam IMX519 (16MP Sony CMOS) | Connects natively via the MIPI CSI protocol; captures high-resolution surface details with automated focus tracking. |
| **Turntable Actuator** | NEMA 17 Stepper Motor (13 Ncm torque) | Rotates the object platform smoothly in predefined, precise angular step increments across a full 360° space. |
| **Rotor/Arm Actuator** | NEMA 17 Stepper Motor (40 Ncm torque) | High-torque motor managing the height, framing, and tilt orientation of the camera subsystem along the structural arm. |
| **Motor Drivers** | Dual A4988 Modules | Mounted to the Pi Shield; translates low-power GPIO signals from the Pi into clean current/voltage steps for the motors. |
| **Power Solution** | Custom Pi Shield PCB & Buck Converter | Regulates a single external 12V DC input down to stable operational voltage levels for the Pi, protection circuitry, and drivers. |
| **Illumination Hub** | Synchronized PWM LED Ring/Strip Light | Regulated via switching components on the shield to deliver uniform, shadowless lighting to optimize texture clarity. |

---

## 💻 Software Architecture & Workflow

The system software workflow relies on an unmanaged backend runtime script communicating directly with hardware peripherals, paired alongside a responsive full-stack web frontend.

### Step-by-Step Functional Lifecycle:
1. **System Initialization:** Powering up triggers the Raspberry Pi to initialize core software libraries, load camera subsystem modules, and spin up communication layers.
2. **Calibration:** Both NEMA 17 stepper motors self-calibrate back to internal home references while the camera exposure parameters settle matching the internal ambient context.
3. **Object Placement & Configuration:** The scanning target is placed on the turntable platform. The operator utilizes the web application interface to define parameters like image resolution, rotation step angles, and focus capture options.
4. **Synchronized Ingestion Loop:** The execution automated scripts sequentially iterate:
   * The turntable increments to the current index step angle.
   * The system fires the lighting control hub to achieve uniform texture exposures.
   * The Arducam IMX519 executes a uncompressed frame transfer down the low-latency CSI pipeline.
   * The rotor adjustments shift vertical heights dynamically to completely resolve compound dimensional curves.
5. **Reconstruction & Scaling Calibration:** Categorized datasets save securely locally onto the microSD card before uploading to integrated cloud endpoints. The model compiles via photogrammetry steps into an optimized `.obj` file. A permanent global scalar calculation applies an inverse factor to reverse depth anomalies, guaranteeing true-to-life dimensional accuracy.

---

## 📂 Repository Structure

```text
├── hardware/               # Mechanical designs and 3D-printable CAD component structural files
│   ├── turntable/          # Rotational platform design models
│   ├── rotor/              # Precision camera arm elevation assemblies
│   └── assembly/           # Comprehensive 3D structural model files
├── electronics/            # Fritzing circuit schematics and production-ready Gerber PCB layouts
├── backend/                # Python scripts executing low-level GPIO register adjustments and sensor pipelines
├── frontend/               # Full-stack dashboard web application codebase assets
└── README.md               # Project system documentation

👥 Contributors & Credits
Developed in partial fulfillment of the requirements for the award of the degree of Bachelor of Engineering in Mechatronics Engineering under Visvesvaraya Technological University (Jnanasangama, Belagavi) at Acharya Institute of Technology.
Project Development Team: Omraj Sawant, Kedar Topajiche, Anurag Kumar
