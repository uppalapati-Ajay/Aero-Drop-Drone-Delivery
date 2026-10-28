# 🚁 Aero Drop — Smart Drone System for Medical and Essentials Delivery

<p align="center">
  <strong>An Embedded Systems Project for Autonomous UAV Navigation, Obstacle Avoidance and Payload Delivery</strong>
</p>

<p align="center">
  <em>GPS Waypoint Navigation • Pixhawk • ESP32 • MAVLink • Obstacle Detection • Servo-Based Payload Release</em>
</p>

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Problem Statement](#-problem-statement)
3. [Objectives](#-objectives)
4. [What Makes Aero Drop Special](#-what-makes-aero-drop-special)
5. [System Architecture](#-system-architecture)
6. [Complete Hardware Components](#-complete-hardware-components)
7. [Component-Level Technical Details](#-component-level-technical-details)
8. [Power Distribution and Hardware Integration](#-power-distribution-and-hardware-integration)
9. [Autonomous Flight and Mission Planner](#-autonomous-flight-and-mission-planner)
10. [GPS Waypoint Navigation](#-gps-waypoint-navigation)
11. [ESP32 Companion Computer](#-esp32-companion-computer)
12. [Obstacle Detection and Avoidance](#-obstacle-detection-and-avoidance)
13. [MAVLink Communication](#-mavlink-communication)
14. [FreeRTOS Task Management](#-freertos-task-management)
15. [Payload Delivery Mechanism](#-payload-delivery-mechanism)
16. [Telemetry and Web Monitoring](#-telemetry-and-web-monitoring)
17. [Complete Mission Workflow](#-complete-mission-workflow)
18. [Software and Development Tools](#-software-and-development-tools)
19. [Implementation Methodology](#-implementation-methodology)
20. [Testing and Results](#-testing-and-results)
21. [Performance Specifications](#-performance-specifications)
22. [Safety and Fail-Safe Considerations](#-safety-and-fail-safe-considerations)
23. [Applications](#-applications)
24. [Limitations](#-limitations)
25. [Future Enhancements](#-future-enhancements)
26. [Repository Structure](#-repository-structure)
27. [Setup and Operation](#-setup-and-operation)
28. [Troubleshooting](#-troubleshooting)
29. [Learning Outcomes](#-learning-outcomes)
30. [Project Team and Acknowledgements](#-project-team-and-acknowledgements)

---

## 🚀 Project Overview

**Aero Drop — Smart Drone System for Medical and Essentials Delivery** is a student-developed unmanned aerial vehicle (UAV) project designed to explore the delivery of lightweight medical supplies and essential items to locations where conventional transportation may be slow or difficult.

The project combines a multirotor drone platform, GPS-based autonomous navigation, a Pixhawk flight controller, Mission Planner ground-control software, and a servo-operated payload release mechanism.

An additional embedded obstacle-avoidance subsystem uses an ESP32 companion computer and short-range Time-of-Flight (ToF) distance sensors. The ESP32 processes distance measurements and communicates with the Pixhawk through MAVLink to initiate reactive avoidance maneuvers.

The obstacle-avoidance design also describes an ESP32-hosted web interface for monitoring flight mode, sensor distances, arm status and avoidance state.

The project brings together embedded systems, electronics, UAV control, sensor integration, communication protocols and mechanical payload handling in one practical engineering prototype.

### Core concept

The intended operating sequence is:

1. Prepare the drone and secure a lightweight payload.
2. Configure and upload GPS waypoints using Mission Planner.
3. Arm the flight controller and initiate the autonomous mission.
4. Navigate through programmed waypoints.
5. Monitor nearby obstacles using distance sensors.
6. Execute the configured avoidance procedure when an obstacle is detected.
7. Continue the mission after the avoidance maneuver, where supported by the implemented control logic.
8. Trigger the payload-release servo at the configured mission point.
9. Complete the mission and land at the designated location.

The exact operating sequence depends on the final flight configuration and the functions enabled in the prototype.

### Project focus

- Autonomous waypoint navigation
- GPS-based positioning
- Multirotor flight control
- Embedded sensor processing
- Reactive obstacle avoidance
- MAVLink communication
- Servo-controlled payload release
- Real-time system monitoring
- Medical and essential-item delivery applications

---

## 🎯 Problem Statement

Conventional delivery methods can be affected by road connectivity, traffic, geographical barriers and accessibility challenges. These issues can be particularly significant when delivering essential supplies to remote or hard-to-reach locations.

Drones offer an alternative transportation platform that can travel directly between suitable launch and delivery locations.

However, a practical delivery drone must address several engineering challenges:

- Maintaining stable flight during autonomous navigation
- Reaching the intended destination using GPS waypoints
- Detecting nearby obstacles that are not represented in the planned route
- Managing flight-control commands safely
- Carrying a payload without compromising flight stability
- Releasing the payload at the intended point
- Monitoring flight status and system health
- Handling communication loss, low battery and unexpected conditions

Aero Drop explores these challenges through the integration of flight-control hardware, embedded processing, distance sensors and a mechanical payload-release system.

## 🎯 Project Objectives

### Primary objectives

1. Develop a multirotor drone platform for lightweight medical and essential-item delivery.
2. Implement GPS-based waypoint navigation using a Pixhawk flight controller.
3. Configure and monitor autonomous missions through Mission Planner.
4. Integrate an ESP32-based obstacle-detection subsystem.
5. Measure obstacle distances using front, left and right ToF sensors.
6. Communicate between the ESP32 and Pixhawk using MAVLink.
7. Implement reactive obstacle-avoidance behavior.
8. Integrate a servo-controlled payload-release mechanism.
9. Explore real-time flight and obstacle-status monitoring through a web interface.
10. Evaluate the prototype through mission, sensor and payload-delivery tests.

### Secondary objectives

- Understand the relationship between a flight controller and a companion computer.
- Learn waypoint-based mission planning.
- Apply embedded programming and real-time task management.
- Integrate mechanical, electrical and software subsystems.
- Record telemetry and analyze prototype behavior.
- Identify limitations and opportunities for future improvement.

---

## ⭐ What Makes Aero Drop Special?

The distinguishing aspect of Aero Drop is its combination of delivery-oriented mechanical design, autonomous flight and embedded obstacle sensing.

| Feature | Engineering significance |
|---|---|
| GPS waypoint navigation | Allows the flight controller to follow a predefined route. |
| Mission Planner integration | Provides mission configuration, route visualization and flight-status monitoring. |
| ESP32 companion computer | Adds a separate embedded processing layer for sensor readings and avoidance decisions. |
| Three-direction ToF sensing | Provides short-range distance information from the front, left and right. |
| MAVLink communication | Connects the companion computer's control logic with the Pixhawk flight controller. |
| Reactive obstacle avoidance | Allows the configured logic to respond to detected nearby obstacles. |
| Servo-based payload release | Provides a controlled mechanical method for releasing a carried item. |
| Web-based monitoring | Offers a way to inspect sensor and flight-status information through a browser. |
| Modular system design | Separates flight stabilization, sensing, decision-making and payload handling. |

**Important distinction:** GPS waypoint navigation does not itself detect obstacles. Obstacle avoidance is an additional subsystem. Likewise, a servo-operated payload mechanism does not automatically guarantee precise delivery. Delivery accuracy depends on navigation error, wind, flight speed, payload dynamics, release timing and the landing or drop procedure.

---

## 🧩 System Architecture

### High-level architecture

```text
                   GROUND CONTROL STATION
                          |
                    Mission Planner
                          |
                    MAVLink Link
                          |
                          v
                 PIXHAWK FLIGHT CONTROLLER
                    /             \
                   /               \
           GPS / Navigation      Motor Outputs
                  |                    |
                  |             ESCs and Motors
                  |                    |
                  |                Drone Flight
                  |
           Flight Status and Data
                  |
                  v
             ESP32 COMPANION
                  ^
                  |
          Distance Measurements
                  |
        +---------+---------+
        |         |         |
      Front      Left     Right
       ToF        ToF       ToF

             ESP32 Decision Logic
                  |
             MAVLink Commands
                  |
                  v
            Pixhawk Controller

       ESP32 Web Monitoring Interface

       Pixhawk Servo Output
                  |
                  v
           Release Mechanism
                  |
                  v
             Payload Box
```

The diagram represents the functional architecture described in the project documentation. Exact wiring, communication links and the servo-output connection should be verified against the final assembled hardware.

### Functional subsystems

**1. Flight-control subsystem**

The Pixhawk handles flight stabilization, attitude control, navigation and motor-control outputs.

**2. Navigation subsystem**

The GPS receiver provides positioning information used by the flight controller for navigation and waypoint missions.

**3. Obstacle-sensing subsystem**

The ToF sensors measure nearby object distances and provide measurements to the ESP32.

**4. Decision-making subsystem**

The ESP32 processes distance measurements, evaluates the obstacle condition and determines whether the configured avoidance logic should run.

**5. Communication subsystem**

MAVLink carries supported status and control messages between the companion computer and the flight controller.

**6. Payload subsystem**

A servo-operated mechanism controls the release of the carried item.

**7. Monitoring subsystem**

The ground station and ESP32 web interface provide different views of the vehicle's status and operation.

---

## 🔩 Complete Hardware Components

The following inventory combines the components identified in the project materials and the prototype photographs. Exact part numbers and ratings should be confirmed against the installed components before the repository is treated as a final bill of materials.

| Component | Identified model or specification | Main purpose |
|---|---|---|
| Flight controller | Pixhawk 2.4.8, as identified in project details | Stabilization, navigation and motor control |
| GPS receiver | NEO-8M GPS, as identified in project details | Positioning for waypoint navigation |
| Power module | Pixhawk-compatible power module | Supplies regulated flight-controller power and, depending on model, measures battery voltage/current |
| Companion computer | ESP32 development board | Sensor processing and obstacle-avoidance logic |
| Distance sensors | Three VL53L0X ToF sensors, according to the process document | Front, left and right obstacle-distance measurements |
| Brushless motors | EMAX 930 KV, as identified in project details | Generate lift and maneuvering thrust |
| ESCs | ReadyToSky 30 A, as identified in project details | Regulate brushless motor speed |
| Propellers | Installed multirotor propellers; exact size and pitch to be confirmed | Convert motor rotation into thrust |
| Battery | 5200 mAh LiPo, as identified in project details | Main propulsion power source |
| Payload actuator | Servo motor | Operates the payload-release mechanism |
| Payload container | Custom-built payload box | Holds the medical or essential item |
| Frame | Multirotor frame shown in prototype photographs | Supports motors, controller, battery and payload |
| Landing gear | Installed landing legs | Provides ground clearance and supports landing |
| RC transmitter | FlySky FS-i6, visible in prototype photographs | Manual control and pilot override |
| RC receiver | Compatible receiver; exact model to be confirmed | Receives pilot commands |
| Ground-control software | Mission Planner | Mission configuration and flight monitoring |
| Communication protocol | MAVLink | Flight-controller telemetry and supported commands |
| Embedded runtime | FreeRTOS, as described in the process document | Supports concurrent ESP32 tasks |
| Monitoring interface | ESP32-hosted web interface, as described in the process document | Displays system status and sensor data |
| Wiring and connectors | Installed power and signal wiring | Connects the electrical subsystems |
| Auxiliary electronics | Development board, interface and power-regulation modules visible in photographs | Supporting functions; exact roles to be documented after wiring verification |

### Components requiring confirmation

The inventory should eventually include the following measured or label-verified details:

- Exact motor model and manufacturer
- Propeller diameter and pitch
- Battery cell count, nominal voltage and discharge rating
- Actual ESC model and continuous-current rating
- Exact GPS and receiver models
- Servo model, torque and operating voltage
- Exact ToF sensor breakout boards
- ESP32 board variant
- Flight-controller firmware and version
- Actual frame dimensions and all-up weight

These values should come from component labels, datasheets, configuration files or measurements—not estimates based on photographs alone.

---

## ⚙️ Component-Level Technical Details

### 1. Pixhawk Flight Controller

**Role:** Primary flight-control and navigation unit.

The Pixhawk receives pilot inputs, GPS and onboard sensor information, and mission commands. It runs the flight-control firmware and calculates the motor outputs required to maintain stable flight.

Its functions include:

- Attitude stabilization
- Flight-mode management
- GPS-assisted navigation
- Waypoint execution
- Motor and ESC output generation
- Telemetry communication
- Supported auxiliary servo outputs
- Handling configured failsafe actions

The ESP32 is not a replacement for the Pixhawk. The flight controller remains responsible for the core flight-control functions.

### 2. NEO-8M GPS Receiver

**Role:** Position information for autonomous navigation.

The GPS receiver supplies geographic positioning data to the flight controller.

This information can support:

- Current position display
- GPS-based waypoint navigation
- Route progress monitoring
- Position-related telemetry
- Navigation-related flight modes

GPS positioning accuracy is affected by satellite visibility, antenna placement, multipath reflections, interference and environmental conditions.

GPS alone does not provide reliable detection of nearby trees, walls or other obstacles.

### 3. ESP32 Companion Computer

**Role:** Additional embedded processing.

The ESP32 processes information from the distance sensors and implements the obstacle-detection and avoidance logic described in the project document.

Its built-in wireless connectivity also makes it suitable for the described browser-based monitoring interface.

Potential responsibilities in this project include:

- Reading ToF sensor measurements
- Evaluating obstacle thresholds
- Comparing left and right distances
- Tracking avoidance state
- Communicating with Pixhawk over MAVLink
- Reporting sensor and flight status
- Hosting a monitoring web page
- Running separate tasks for sensing, control and diagnostics

The ESP32's actual task structure, pin assignments and communication settings should be documented from the firmware source.

### 4. VL53L0X Time-of-Flight Sensors

**Role:** Short-range obstacle-distance measurement.

The project document identifies three VL53L0X sensors placed in front, left and right directions.

A ToF sensor estimates distance by measuring the time taken for emitted light to return after reflecting from a target.

The intended arrangement is:

| Sensor position | Purpose |
|---|---|
| Front | Detect an obstacle along the forward direction |
| Left | Estimate clearance on the left side |
| Right | Estimate clearance on the right side |

The ESP32 uses the measurements to determine whether the front obstacle threshold has been crossed and to compare the available left and right clearances.

The VL53L0X is a short-range sensor. Its practical range and reliability depend on the target's reflectivity, ambient lighting, sensor configuration and mounting.

Three directional sensors do not provide complete three-dimensional obstacle coverage. They may miss obstacles above, below or outside their sensing directions.

**Technical detail to document:** sensor addresses, I²C configuration, initialization sequence, sampling rate, invalid-reading handling and the actual configured avoidance threshold.

### 5. Brushless DC Motors

**Role:** Generate thrust for takeoff, hovering and maneuvering.

The project identifies EMAX 930 KV motors.

The KV rating indicates the approximate no-load rotational speed per volt, not the maximum payload capacity of the drone.

Motor performance depends on:

- Applied voltage
- Propeller diameter and pitch
- ESC capability
- Motor current
- Cooling
- Battery condition
- Total aircraft mass

The motors must be matched to the propellers, ESCs, battery and frame.

### 6. Electronic Speed Controllers

**Role:** Control the speed of the brushless motors.

The identified ESCs are ReadyToSky 30 A units.

The Pixhawk sends motor-control signals to the ESCs. Each ESC electronically commutates its motor to control rotational speed.

ESC selection must account for motor current, battery voltage, cooling and the manufacturer's specifications. A 30 A rating alone does not establish that the complete propulsion system is correctly matched.

### 7. LiPo Battery

**Role:** Supply energy for propulsion and onboard electronics through the appropriate power-distribution and regulation arrangements.

The project details identify a 5200 mAh lithium-polymer battery.

Battery capacity is only one factor in flight endurance. Other factors include battery voltage, usable discharge, total aircraft weight, motor efficiency, propeller choice, wind and flight behavior.

The battery's cell count, discharge rating, connector, voltage limits and measured flight duration still need to be recorded.

### 8. Pixhawk Power Module

**Role:** Support the flight controller's power supply and, depending on the module, battery monitoring.

The power module must be connected according to its exact wiring and voltage specifications.

The propulsion power path and regulated electronics power path must be understood separately. The ESP32, sensors and servo must not be assumed to receive appropriate power merely because the Pixhawk is powered.

### 9. Servo Motor and Payload Mechanism

**Role:** Mechanically release the carried item.

The servo converts a control signal into angular movement. A linkage, latch or other mechanical arrangement uses that movement to release the payload.

The final documentation should identify:

- Servo model
- Operating voltage and current
- Mechanical linkage design
- Release and locked positions
- PWM or servo-output configuration
- Mission command used to trigger release
- How the mechanism is reset
- How accidental activation is prevented

The Mission Planner screenshots include a `DO_SET_SERVO` mission command, which is relevant to the documented payload-release workflow.

The servo's operating voltage and signal requirements must be checked before connection to the flight controller.

### 10. Frame, Propellers and Landing Gear

**Role:** Mechanical structure and propulsion support.

The frame carries the flight controller, motors, ESCs, battery, GPS, companion computer and payload mechanism.

The propellers generate lift and must be installed in the correct positions and orientations.

The landing gear supports the vehicle on the ground and provides clearance for the payload mechanism.

The final documentation should include frame dimensions, motor-to-motor distance, propeller specifications, component mounting locations and total assembled weight.

### 11. RC Transmitter and Receiver

**Role:** Pilot control, configuration and manual intervention.

The FlySky FS-i6 transmitter is visible in the supplied photographs.

The RC link can be used for manual piloting and supported override behavior. Exact receiver model, channel assignments, mode-switch configuration and failsafe settings must be verified from the actual setup.

Manual control remains important even when an autonomous mission is configured.

---

## 🔋 Power Distribution and Hardware Integration

Power integration is a critical part of the system.

The final wiring diagram should show separate, clearly labeled paths for:

1. Battery power to the propulsion system.
2. Battery power through the power module to the flight controller.
3. Regulated power to the ESP32.
4. Power and signal connections to the ToF sensors.
5. Signal connections between the ESP32 and Pixhawk.
6. Servo power and control signal.
7. GPS and RC receiver connections.

A simplified functional diagram is:

```text
LiPo Battery
    |
    +---- Propulsion Power Distribution
    |          |
    |        ESCs
    |          |
    |       BLDC Motors
    |
    +---- Power Module
               |
             Pixhawk
               |
        Servo Signal Output
               |
          Payload Servo

Regulated Electronics Supply
    |
    +---- ESP32
    |       |
    |     I2C Bus
    |       |
    |    ToF Sensors
    |
    +---- Other compatible peripherals

ESP32 <---- MAVLink Serial Link ----> Pixhawk
GPS Receiver -----------------------> Pixhawk
RC Receiver ------------------------> Pixhawk
```

This is a functional representation, not a pin-by-pin wiring diagram.

Before publishing a definitive wiring diagram, verify connector pinouts, voltage levels, common-ground requirements, current consumption and the actual wiring on the assembled drone.

Never power a servo, ESP32 or sensor from an unsuitable output. Avoid connecting power rails together without confirming their electrical compatibility.

---

## 🛰️ Autonomous Flight and Mission Planner

Mission Planner is the ground-control application used to configure and monitor the autonomous flight mission.

The supplied screenshots show GPS waypoint routes and mission commands, including takeoff, waypoint navigation, a servo command and landing.

### Main Mission Planner functions

- Connect to the flight controller
- Select the appropriate communication port and baud rate
- Inspect GPS status and vehicle information
- Configure flight modes and parameters
- Plan a route using geographic waypoints
- Set waypoint altitudes
- Add supported mission commands
- Upload and read mission plans
- Monitor vehicle position and flight status
- Review telemetry and flight logs
- Inspect mission progress and recorded behavior

### Typical mission-planning workflow

1. Establish a reliable connection to the flight controller.
2. Check the GPS fix, compass and other required pre-arm checks.
3. Open the mission-planning interface.
4. Place the intended waypoints on the map.
5. Configure takeoff, waypoint, payload-release and landing commands as appropriate.
6. Set suitable altitude values and waypoint acceptance parameters.
7. Review the complete route and mission commands.
8. Upload the mission to the flight controller.
9. Read the mission back and verify the stored sequence.
10. Perform the mission only after appropriate ground checks and safety planning.
11. Review telemetry and logs after the test.

### Understanding the mission commands

| Command type | Function |
|---|---|
| `TAKEOFF` | Initiates the configured takeoff action when supported by the selected flight mode and mission setup. |
| `WAYPOINT` | Directs the vehicle toward a specified geographic location and altitude. |
| `DO_SET_SERVO` | Sets a configured servo output to a specified value, subject to firmware and output configuration. |
| `LAND` | Initiates the configured landing behavior. |

Mission command availability and behavior depend on the flight-controller firmware and configuration.

A mission screenshot proves that a route or command sequence was configured. It does not, by itself, prove that every command completed successfully in actual flight.

### Waypoint planning considerations

A waypoint mission defines a series of geographic target locations. The flight controller attempts to follow them according to its navigation and flight-control settings.

Important parameters include:

- Latitude and longitude
- Target altitude
- Altitude reference
- Waypoint acceptance radius
- Flight mode
- Speed and acceleration limits
- Takeoff and landing locations
- Geofence and failsafe settings

**Altitude reference must be documented correctly.** Relative altitude, absolute altitude and terrain-relative altitude are not interchangeable.

The screenshots show altitude fields and route points, but the final README should only state a fixed mission altitude after confirming the relevant mission file and altitude frame.

---

## 📍 GPS Waypoint Navigation

The GPS receiver provides position estimates to the flight controller.

During autonomous navigation, the controller compares the current estimated position with the target waypoint and uses its navigation and stabilization systems to move toward that target.

The basic process is:

1. Obtain valid positioning information.
2. Load the programmed waypoint mission.
3. Establish the correct flight mode and pre-arm status.
4. Begin the mission under the required operating conditions.
5. Navigate toward the current waypoint.
6. Determine when the waypoint's acceptance criteria have been met.
7. Continue to the next mission item.
8. Execute any configured auxiliary commands.
9. Complete the mission and land according to the plan.

GPS waypoint navigation is not the same as full autonomous path planning. A conventional waypoint mission follows predefined points unless additional navigation logic changes the vehicle's behavior.

---

## 🧠 ESP32 Companion Computer

The ESP32 adds sensing and decision-making functionality alongside the flight controller.

The companion computer is intended to operate independently of the Pixhawk's core stabilization loop.

Its principal responsibilities are:

- Collect distance measurements.
- Determine whether an obstacle is within the configured threshold.
- Compare left and right sensor readings.
- Track the avoidance procedure's current state.
- Send supported commands to the flight controller.
- Report sensor readings and system status.
- Support the web-monitoring interface.

### Why use an ESP32?

The ESP32 provides an embedded processing platform with integrated wireless connectivity and support for real-time task execution.

This makes it suitable for a student-level project that combines sensor processing, serial communication and monitoring without requiring a separate general-purpose computer.

The ESP32 is not a substitute for a safety-rated collision-avoidance system. Its usefulness depends on correct sensor handling, command logic, timing, power integrity and validation.

---

## 🚧 Obstacle Detection and Avoidance

### Problem addressed

A predefined waypoint route does not automatically account for every unexpected object encountered along the route.

The obstacle-avoidance subsystem adds short-range sensing and reactive control logic to address this limitation.

### Sensor arrangement

The process document specifies three VL53L0X ToF sensors:

- Front sensor: measures the distance to an object ahead.
- Left sensor: estimates clearance to the left.
- Right sensor: estimates clearance to the right.

The ESP32 evaluates the measurements and determines whether the configured avoidance procedure should be triggered.

### Obstacle-detection logic

The basic logic is:

```text
Read front, left and right distances
                 |
                 v
       Validate sensor readings
                 |
                 v
 Is a front obstacle within threshold?
            /          \
          No            Yes
          |              |
   Continue monitoring   v
                 Initiate avoidance
                         |
                         v
               Move backward using
                 configured control
                         |
                         v
               Compare left and
                right clearances
                         |
                         v
                Select safer side
                         |
                         v
                Execute lateral
                  movement
                         |
                         v
              Check whether obstacle
                    is cleared
                         |
                         v
                Release override
                         |
                         v
             Resume autonomous mission
```

This flowchart summarizes the intended procedure in the supplied document. Actual transition conditions, delays, velocity values and recovery behavior should be verified from the implementation.

### Hybrid control strategy

The process document describes two control techniques:

**1. RC override for backward movement**

A temporary override is used to command backward movement when a frontal obstacle is detected.

This requires correct channel mapping, valid control values and an explicit mechanism for releasing the override.

**2. Velocity commands for lateral movement**

The ESP32 compares the left and right measurements and commands movement toward the selected safer side.

The exact command frame, velocity values, duration and exit conditions must be documented from the firmware.

### Obstacle-clearance decision

A safe implementation should avoid treating one momentary sensor reading as sufficient proof that an obstacle has been cleared.

The system should account for:

- Invalid or missing sensor readings
- Sudden measurement changes
- Sensor update rate
- Minimum required clearance
- Whether the vehicle has actually moved
- Timeouts and command completion
- Releasing control overrides
- What happens when neither side has adequate clearance

These are important implementation and validation considerations. They should not be described as implemented features unless confirmed in the code.

### Current limitations

The three-sensor arrangement is a short-range reactive system. It does not provide complete environmental mapping.

It cannot automatically be assumed to detect:

- Obstacles behind the drone
- Objects above or below the sensor fields
- Thin wires outside the sensing field
- Every moving obstacle
- Objects beyond the effective sensor range

The project documentation does not describe a complete SLAM or global path-planning implementation. Those should remain future enhancements unless further evidence is available.

---

## 📡 MAVLink Communication

MAVLink is the message protocol used to exchange telemetry and supported control commands between the flight controller and companion computer.

The project document describes using MAVLink to read flight status and send the commands required for avoidance.

### Communication responsibilities

Depending on the implemented message set, the companion computer may need to:

- Read vehicle heartbeat messages.
- Determine the current flight mode.
- Read armed/disarmed status.
- Receive relevant telemetry.
- Send supported RC override messages.
- Send supported velocity or setpoint messages.
- Monitor communication health.
- Detect stale or missing data.

### Communication considerations

A robust implementation should define:

- Serial interface and baud rate
- MAVLink dialect and message definitions
- System and component IDs
- Message update rates
- Command acknowledgement behavior
- Timeout handling
- Link-loss behavior
- Correct release of overrides
- Valid flight modes for the requested commands

The exact message IDs, data fields, channel mappings and control values should be recorded from the source code.

MAVLink communication does not guarantee that a command will be accepted or executed. The flight controller's current mode, safety checks, firmware and configuration determine the result.

---

## ⏱️ FreeRTOS Task Management

The project process document describes FreeRTOS task management on the ESP32.

Real-time task separation helps organize sensor acquisition, communication, avoidance decisions and monitoring.

### Tasks described in the project

| Task | Responsibility |
|---|---|
| MAVLink task | Processes communication with the flight controller. |
| Sensor task | Reads the ToF sensors and updates distance data. |
| Avoidance task | Evaluates obstacle conditions and manages the avoidance state. |
| Web-server task | Provides the browser-based monitoring interface. |
| Serial/debug task | Supports diagnostic messages and development logging. |

These are the task responsibilities described in the documentation. Exact task names, priorities, stack sizes and scheduling intervals should be confirmed from the ESP32 firmware.

### Why task separation matters

Separating responsibilities can improve code organization and reduce coupling between subsystems.

However, concurrent tasks still require careful handling of shared data, timing, synchronization and communication errors.

Useful implementation details to record include:

- Task priorities
- Sampling intervals
- Queue or mutex usage
- Shared sensor-data structure
- Stack sizes
- Watchdog configuration
- Error-handling strategy
- Timing measurements

---

## 📦 Payload Delivery Mechanism

### Purpose

The payload mechanism is designed to carry and release a lightweight medical or essential item.

The physical prototype photographs show a container mounted below the drone, and the Mission Planner screenshots include a servo command relevant to the release mechanism.

### Main parts

- Payload container
- Servo actuator
- Mechanical latch or linkage
- Mounting brackets
- Servo power supply
- Flight-controller servo output
- Mission command configuration

### Intended release sequence

1. Place the item securely inside the payload container.
2. Confirm that the mechanism is locked and the payload is secured.
3. Verify the servo's configured output and release position.
4. Configure the release command at the intended mission point.
5. Confirm that the command is permitted under the selected flight configuration.
6. Execute the mission under controlled test conditions.
7. Trigger the configured servo action.
8. Verify that the payload is released as intended.
9. Confirm that the vehicle remains stable after release.
10. Inspect the mechanism and reset it before another test.

The release mechanism should be tested on the ground without propellers before being used in flight.

### Payload capacity

**The maximum payload capacity has not yet been established from the supplied materials.**

It should not be inferred from the size of the container or the motor KV rating.

To establish a defensible payload limit, record:

- Empty drone mass
- Battery mass
- Payload mechanism mass
- Payload mass
- Total takeoff mass
- Motor and propeller thrust data
- Battery voltage under load
- Hover stability and current consumption
- Manufacturer limits for the frame and propulsion components

A safe payload limit requires adequate thrust margin, stable control, acceptable endurance and verified mechanical strength.

### Payload-delivery accuracy

Delivery accuracy should be measured by recording the intended release or landing point and the actual payload landing point.

Useful measurements include:

- Horizontal distance from target
- Wind conditions
- Release altitude
- Forward velocity
- Payload mass and dimensions
- Number of repeated trials
- Average error and maximum error

A successful servo activation alone does not demonstrate accurate delivery.

---

## 📊 Telemetry and Web Monitoring

The project document describes an ESP32-hosted web interface that displays:

- Flight mode
- Armed/disarmed status
- Distance measurements
- Obstacle-detection status

The document specifies a page refresh interval of approximately 500 milliseconds. That is the stated interface refresh interval, not proof that every sensor, MAVLink message or control task executes at 2 Hz or 2,000 Hz.

### Ground-station telemetry

Mission Planner can provide flight-related information such as:

- Vehicle position
- GPS status
- Altitude
- Velocity
- Flight mode
- Mission progress
- Battery and system status, where available
- Flight logs and diagnostic messages

### Why telemetry matters

Telemetry allows the developer to compare intended behavior with actual behavior.

For example, during an obstacle-avoidance test, useful evidence includes the distance measurements before detection, the avoidance state, the control command, the flight-mode transition and the mission's subsequent progress.

For payload testing, useful records include the mission command sequence, servo activation, release time and the payload's final position.

---

## 🔄 Complete Mission Workflow

The following workflow combines the delivery mission and obstacle-avoidance subsystems.

### Phase 1 — Pre-flight preparation

- Inspect the frame, motors, propellers and landing gear.
- Secure the battery and payload.
- Inspect all power and signal connections.
- Check the flight controller and GPS status.
- Verify RC operation and configured failsafes.
- Confirm that sensor readings are valid.
- Check the servo and payload latch.
- Review the mission and its boundaries.

### Phase 2 — Mission configuration

- Create the waypoint route in Mission Planner.
- Configure altitude references and mission parameters.
- Add supported auxiliary commands.
- Verify the payload-release point.
- Upload and read back the mission.
- Confirm the flight mode and pre-arm status.

### Phase 3 — Autonomous navigation

- Initiate the mission under approved test conditions.
- Use GPS-assisted navigation to follow the route.
- Monitor the flight controller and telemetry.
- Continuously evaluate obstacle-sensor readings through the ESP32.

### Phase 4 — Obstacle response

- Detect a frontal obstacle within the configured threshold.
- Initiate the configured backward maneuver.
- Compare the left and right clearances.
- Select a suitable direction.
- Execute the lateral maneuver.
- Verify that the obstacle is cleared.
- Release temporary overrides.
- Confirm that the autonomous mission resumes as intended.

### Phase 5 — Payload release

- Reach the configured mission point.
- Execute the supported servo command.
- Verify that the payload is released.
- Record the actual delivery outcome.

### Phase 6 — Completion and analysis

- Complete the planned mission and landing.
- Review telemetry and logs.
- Inspect the aircraft and release mechanism.
- Record any unexpected behavior.
- Compare the observed results with the intended mission.

The actual order must match the uploaded mission and implemented firmware. Not every phase should be assumed to have been demonstrated in one uninterrupted flight.

---

## 🛠️ Software and Development Tools

| Tool or technology | Purpose |
|---|---|
| Mission Planner | Waypoint creation, mission upload and flight monitoring |
| ArduPilot-compatible Pixhawk firmware | Flight control and mission execution, subject to the installed firmware |
| MAVLink | Flight-controller communication |
| ESP32 firmware environment | Development of the companion-computer application |
| FreeRTOS | Concurrent embedded task execution, as described in the process document |
| I²C | Expected interface for typical VL53L0X sensor modules; verify the actual wiring |
| Serial/UART | Potential interface for MAVLink communication; confirm the selected port |
| Web browser | Access to the ESP32 monitoring interface |
| Serial monitor | Debugging and diagnostic output |
| Flight logs | Post-flight analysis and verification |

The exact firmware version, compiler, ESP32 development framework, libraries and build configuration should be added once confirmed from the project files.

---

## 🧪 Implementation Methodology

The project can be documented as a series of engineering stages.

### Stage 1 — Hardware assembly

Assemble the frame, motors, ESCs, flight controller, GPS, power module, battery and landing gear.

### Stage 2 — Flight-controller setup

Configure the flight controller, motor outputs, RC channels, flight modes and required calibrations.

### Stage 3 — GPS and waypoint testing

Create and validate a simple waypoint mission before adding more complex behavior.

### Stage 4 — Payload mechanism integration

Mount the payload container and servo. Verify the mechanical movement and output configuration on the ground.

### Stage 5 — ESP32 sensor integration

Connect the ToF sensors and verify that each sensor reports plausible distance measurements.

### Stage 6 — MAVLink integration

Establish communication between the ESP32 and Pixhawk. Verify the reception of status messages before enabling control commands.

### Stage 7 — Obstacle-avoidance implementation

Implement the threshold checks, avoidance state transitions, directional selection, timeouts and override release.

### Stage 8 — Monitoring integration

Integrate the web interface and verify that displayed values match the underlying sensor and flight-status data.

### Stage 9 — System validation

Perform ground tests, controlled sensor tests, mission tests and payload tests in a suitable safe environment.

### Stage 10 — Documentation and evaluation

Record component specifications, configuration, test conditions, outcomes, limitations and lessons learned.

---

## 🧾 Testing and Results

The process document describes tests involving autonomous missions, Loiter-mode hovering and obstacle detection. It reports that the obstacle-avoidance system detected obstacles, executed avoidance maneuvers and resumed missions.

The supplied Mission Planner screenshots also show configured waypoint routes and mission commands.

These results should be documented alongside the original screenshots, logs and test evidence.

### Suggested test matrix

| Test ID | Test | Evidence to record |
|---|---|---|
| T01 | Power-up and sensor initialization | Startup log and sensor readings |
| T02 | GPS positioning | GPS status and position information |
| T03 | Waypoint mission configuration | Mission Planner screenshot and mission file |
| T04 | Autonomous waypoint flight | Flight log, route and telemetry |
| T05 | Obstacle detection | Front, left and right sensor readings |
| T06 | Backward avoidance response | Command and telemetry record |
| T07 | Left/right directional selection | Sensor comparison and control-state log |
| T08 | Mission recovery | Evidence that the mission resumed |
| T09 | Servo operation | Ground-test video and command settings |
| T10 | Payload release | Payload mass, release evidence and target error |
| T11 | Web monitoring | Screenshots and refresh behavior |
| T12 | Failsafe behavior | Controlled test record and configuration |

### Results reporting

For each test, record:

- Date and location
- Hardware and firmware versions
- Test conditions
- Initial configuration
- Expected behavior
- Observed behavior
- Pass/fail status
- Supporting image, log or video
- Any limitations or corrective actions

Do not mark a test as passed solely because the mission was configured. Record whether the behavior was actually observed.

---

## 📐 Performance Specifications

The following table separates known design information from measurements that still need to be established.

| Parameter | Current status |
|---|---|
| Flight-controller model | Pixhawk 2.4.8 identified in project details |
| GPS receiver | NEO-8M identified in project details |
| Companion computer | ESP32 |
| Obstacle sensors | Three VL53L0X sensors specified in the process document |
| Motor rating | EMAX 930 KV identified in project details |
| ESC rating | ReadyToSky 30 A identified in project details |
| Battery capacity | 5200 mAh identified in project details |
| Navigation | GPS waypoint mission planning |
| Payload release | Servo-based mechanism |
| Obstacle response | Reactive sensing and control strategy |
| Maximum payload | Not yet verified |
| Flight endurance | Requires measurement |
| Maximum tested range | Requires measurement |
| Maximum tested altitude | Requires verified logs and altitude reference |
| Average flight speed | Requires measurement |
| Payload delivery error | Requires documented trials |
| Sensor threshold | Requires actual firmware/configuration |
| Obstacle-avoidance success rate | Requires repeated controlled tests |
| Battery consumption per mission | Requires measurement |
| Total takeoff mass | Requires weighing the complete aircraft |

### How to establish payload capacity

Payload capacity should be measured or derived from verified propulsion data and then validated in controlled flight tests.

The complete aircraft mass includes the frame, motors, ESCs, battery, electronics, wiring, landing gear and payload mechanism. Any carried item increases the required thrust and can reduce endurance.

A published payload figure should specify the test configuration and operating conditions.

### How to establish flight endurance

Measure the time from takeoff to landing under a documented payload and battery configuration. Record the battery voltage, environmental conditions and flight profile.

A single successful flight should not be presented as a guaranteed endurance rating.

---

## 🛡️ Safety and Fail-Safe Considerations

Aero Drop is an experimental student UAV, not a certified medical-delivery aircraft.

Before testing:

- Remove propellers during bench testing of electronics and control logic.
- Verify motor order and rotation before flight.
- Check propeller condition and mounting.
- Secure all wiring and electronic modules.
- Verify battery condition and power connections.
- Confirm RC control and failsafe behavior.
- Check GPS quality and flight-controller pre-arm checks.
- Use an appropriate test area and keep people clear of the flight path.
- Test the payload-release mechanism without propellers first.
- Verify how RC overrides and velocity commands are released.
- Ensure that a lost sensor or communication link cannot leave a stale control command active.
- Keep a qualified pilot ready to intervene.
- Follow applicable aviation regulations and local operating restrictions.

The obstacle-avoidance system must not be treated as a substitute for a pilot, geofence, appropriate failsafes or safe operating procedures.

Medical payload delivery also requires suitable packaging, payload security, and any necessary temperature, contamination and handling controls.

---

## 🌍 Applications

The concept can be relevant to:

- Lightweight medical-supply delivery
- Delivery of essential items to difficult-to-reach locations
- Emergency-response logistics research
- Campus-scale autonomous delivery demonstrations
- Embedded-systems education
- UAV navigation and control research
- Obstacle-detection experiments
- Payload-release mechanism development

Actual deployment for medical or commercial delivery would require additional safety validation, regulatory compliance, operational procedures and payload qualification.

---

## ⚠️ Limitations

The following limitations should be considered when evaluating the prototype:

1. GPS waypoint navigation follows predefined targets and does not independently provide complete obstacle detection.
2. The ToF sensors provide short-range measurements within their sensing fields.
3. Three directional sensors cannot guarantee complete obstacle coverage.
4. Reactive avoidance may not calculate an optimal route around complex obstacles.
5. Sensor measurements can be affected by the target surface and environment.
6. RC override and velocity-command behavior depends on flight mode, firmware and configuration.
7. The payload-release mechanism requires correct mechanical alignment and servo configuration.
8. Payload capacity and flight endurance have not been established as verified performance ratings in the available documentation.
9. Delivery accuracy must be measured across repeatable trials.
10. The project does not document a complete SLAM-based mapping or global path-planning system.
11. Real-world medical delivery requires additional operational and regulatory validation.

---

## 🔮 Future Enhancements

Potential future improvements include:

- Adding additional obstacle sensors for wider directional coverage
- Evaluating LiDAR-based distance sensing
- Implementing more robust sensor-failure detection
- Improving avoidance-state management and recovery logic
- Adding structured telemetry logging
- Creating a clearer web dashboard with historical measurements
- Implementing mission progress and payload-status reporting
- Evaluating dynamic path-planning algorithms
- Exploring visual obstacle recognition
- Investigating SLAM-based navigation
- Improving payload-latch design and mechanical reliability
- Measuring flight endurance and payload performance systematically
- Adding automated test reports and repeatable validation procedures

These are proposed enhancements, not claims about existing functionality.

---

## 📁 Recommended Repository Structure

```text
Aero-Drop-Smart-Drone/
│
├── README.md
│
├── images/
│   ├── drone-overview.jpg
│   ├── drone-assembled.jpg
│   ├── drone-components.jpg
│   ├── payload-mechanism.jpg
│   ├── esp32-controller.jpg
│   ├── obstacle-sensors.jpg
│   ├── mission-planner-route.png
│   ├── mission-waypoints.png
│   └── telemetry-monitoring.png
│
├── diagrams/
│   ├── system-architecture.png
│   ├── power-distribution.png
│   ├── obstacle-avoidance-flowchart.png
│   ├── payload-release-flowchart.png
│   └── mission-workflow.png
│
├── docs/
│   ├── project-report.pdf
│   ├── hardware-bom.md
│   ├── wiring-and-pinout.md
│   ├── mission-planner-setup.md
│   ├── obstacle-avoidance.md
│   ├── payload-mechanism.md
│   ├── test-results.md
│   ├── safety-and-limitations.md
│   └── references.md
│
├── mission/
│   ├── README.md
│   └── sample-mission-file
│
├── firmware/
│   ├── esp32/
│   │   └── README.md
│   └── pixhawk/
│       └── README.md
│
├── test-results/
│   ├── test-matrix.csv
│   └── README.md
│
└── LICENSE
```

Only add folders and files that you actually have or intend to maintain. Do not include empty placeholder firmware folders as though they contain implemented source code.

Do not upload passwords, Wi-Fi credentials, private keys, personal information, or unredacted telemetry that reveals sensitive locations. Include large binaries and videos only when useful, and consider Git LFS for large assets.

---

## ▶️ Setup and Operation

The exact steps depend on the installed firmware and the final wiring. A general preparation sequence is:

1. Assemble and inspect the hardware.
2. Verify the Pixhawk firmware and configuration.
3. Connect and verify the GPS receiver.
4. Calibrate and check the required flight-control sensors.
5. Verify motor order, rotation and ESC configuration.
6. Establish the RC link and check failsafes.
7. Verify the ESP32's power and sensor connections.
8. Confirm that each ToF sensor reports valid measurements.
9. Establish the ESP32–Pixhawk MAVLink connection.
10. Verify telemetry reception before enabling avoidance commands.
11. Test the servo and payload mechanism on the ground without propellers.
12. Configure the waypoint mission in Mission Planner.
13. Review the mission and safety parameters.
14. Perform controlled tests in an appropriate environment.
15. Save the mission, logs and test observations.

Specific serial ports, baud rates, firmware versions, ESP32 libraries and mission parameters should be documented after checking the actual configuration.

---

## 🧰 Troubleshooting

| Symptom | Possible causes to investigate |
|---|---|
| GPS position unavailable | Antenna placement, GPS connection, satellite visibility or receiver configuration |
| Mission cannot start | Pre-arm checks, flight mode, GPS quality, mission configuration or failsafe state |
| One motor does not respond | ESC wiring, motor connection, output mapping or power issue |
| ToF sensor returns invalid readings | Power, I²C wiring, address conflicts, initialization or sensor configuration |
| ESP32 cannot communicate with Pixhawk | UART wiring, baud rate, serial configuration or MAVLink message handling |
| Avoidance does not trigger | Sensor threshold, invalid readings, task execution or decision logic |
| Drone does not resume mission | Override release, control mode, command timeout or recovery-state logic |
| Servo does not release payload | Output mapping, servo power, PWM range, linkage friction or mission-command configuration |
| Web page does not update | Wi-Fi connectivity, server task, data-refresh logic or stale sensor data |
| Flight endurance is lower than expected | Payload mass, battery condition, propeller selection, motor current or environmental conditions |

Troubleshooting should start with safe ground inspection and logs. Never investigate a suspected motor-control fault with exposed spinning propellers.

---

## 📚 Learning Outcomes

This project provides practical exposure to:

- Embedded hardware integration
- Flight-controller architecture
- GPS-based navigation
- Mission planning
- Sensor interfacing
- I²C communication
- UART and MAVLink communication
- Real-time task management
- Reactive control algorithms
- Servo actuation
- Power distribution
- Telemetry and debugging
- Hardware testing and validation
- System-level engineering documentation

---

## 👥 Project Team and Acknowledgements

**Project title:** Aero Drop — Smart Drone System for Medical and Essentials Delivery

**Department:** Electronics and Communication Engineering

**Institution:** Sir C. R. Reddy College of Engineering (Autonomous)

**Project guide:** Mr. A. M. Vamsi Krishna, M.Tech. (Ph.D.), Assistant Professor, Department of ECE

**Team members:**
- U. S. V. Ajay
- T. Pavani
- Shaik Sadhiq
- S. Venkata Srikanth
- T. Sai Ganesh

The project was developed as an academic engineering effort involving UAV hardware, embedded systems, navigation and payload-delivery concepts.

---

## 📌 Final Note

Aero Drop is an educational prototype intended to explore autonomous navigation, obstacle sensing and lightweight payload delivery. Its capabilities and performance should be evaluated using the actual hardware configuration, source code, flight logs and repeatable tests.

The project demonstrates how flight control, embedded processing, sensing, communication and mechanical actuation can be integrated into a single UAV platform.

**The long-term goal is to develop a more reliable and better-documented autonomous delivery system through systematic testing, engineering improvements and continued learning.**
