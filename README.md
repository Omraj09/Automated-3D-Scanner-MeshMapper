Development of an Automated 3D Scanning System
An open-source, cost-effective, and fully automated 3D scanning platform built using mechanical precision, embedded electronics, and a full-stack web-driven software architecture. By synchronizing a single high-resolution 16MP optical sensor with dual-axis stepper motor motion, this system eliminates the need for complex multi-sensor configurations (like infrared or LiDAR arrays) to produce accurate, high-fidelity digital models suitable for reverse engineering, digital archiving, and rapid prototyping.

🚀 Key Features
End-to-End Automation: Complete elimination of manual camera work or object repositioning through software-synchronized mechanical hardware.
Single-Sensor Photogrammetry: Leverages a 16-megapixel Arducam IMX519 with programmable autofocus, bypassing expensive or bulky multi-sensor configurations.
Custom Pi Shield PCB: Centralized power regulation and motor driver integration, eliminating fragile breadboard connections and ensuring electrical signal integrity.
Remote Web Interface: A custom responsive full-stack dashboard allowing real-time monitoring, manual hardware overrides, crop adjustments, and full parameter control (exposure, shutter speed, focus stacks).
Cloud Infrastructure Integration: Automated secure cloud-based data management for systematic image dataset handling, storage, and cross-platform remote accessibility.
True-to-Life Scaling Calibration: Out-of-the-box post-processing scaling workflows permanently integrated to fix photogrammetry depth anomalies and maintain true physical dimensions.

🛠️ System Architecture & Hardware Specs
The system bridges low-level physical actuation with high-level software workflows via a centralized processing hub.

[ Web UI / Cloud Backend ] <---> [ Raspberry Pi 4B ] <---> [ Custom Pi Shield PCB ]
                                                                   |
                                    +------------------------------+------------------------------+
                                    |                              |                              |
                        [ NEMA 17 Turntable Motor ]      [ NEMA 17 Rotor Motor ]      [ Synchronized LED Ring ]
                        
Hardware Component Specifications
Component	Specification / Model	Role in System
Central Controller	Raspberry Pi 4 Model B (Quad-core Cortex-A72 @ 1.8GHz)	Main processing unit; orchestrates motor scripts, camera triggers, and hosts the web interface backend.
Optical Sensor	Arducam IMX519 (16MP Sony IMX519 CMOS)	Connects via low-latency MIPI CSI protocol; handles high-resolution image capture with dynamic autofocus tracking.
Turntable Actuator	NEMA 17 Stepper Motor (13 Ncm torque)	Rotates the object platform smoothly in predefined angular increments across a full 360° space.
Rotor/Arm Actuator	NEMA 17 Stepper Motor (40 Ncm torque)	High-torque motor controlling camera height and angular orientation along the custom curved mounting arm.
Motor Drivers	Dual A4988 Modules	Translates low-power logic GPIO signals from the Pi into precise current/voltage step steps.
Power Solution	Custom Pi Shield PCB (with Onboard Buck Converter)	Regulates a single 12V DC input down to safe voltage levels for the Pi while filtering transient electrical noise.
Illumination Hub	Synchronized PWM LED Ring Light	Positioned around the optical module to provide shadowless, uniform lighting to optimize photogrammetric texture fidelity.

💻 Software Architecture & Workflow
The software environment relies on a full-stack architecture running natively on the Raspberry Pi Unix environment to bridge user inputs directly to low-level hardware registers.
Execution Steps:
System Initialization: Embedded Python libraries, camera subsystem drivers, and GPIO configurations load up. Peripherals calibrate back to home reference positions via virtual endstops.
Scan Configuration: The user accesses the hosted web interface to define step increments, shutter speeds, focus tracking ranges, and cropping fields.
Synchronized Data Acquisition: The backend coordinates the hardware loop:
The Turntable stepper increments to a set angle.
The LED array pulses to lock uniform exposure.
The camera triggers an uncompressed frame capture over the CSI pipeline.
The camera arm adjusts height via the rotor motor when complex geometries require multiple vertical planes.
Data Ingestion & Pipeline Handling: Image folders are categorized locally on the microSD card and systematically mirrored up to cloud storage for processing.
3D Mesh Generation & Scaling Correction: Captured frames are compiled using photogrammetry algorithms to build a dense point cloud and export a standard .obj mesh file. A permanent corrective 2:3 global scaling algorithm runs automatically to match true physical caliper measurements.

👥 Contributors & Credits
Developed as part of the Major Project Phase II requirement for the award of the degree of Bachelor of Engineering in Mechatronics Engineering at Acharya Institute of Technology (Affiliated to Visvesvaraya Technological University, Belagavi).
Project Members: Anurag Kumar, Kedar Topajiche, Omraj Sawant
