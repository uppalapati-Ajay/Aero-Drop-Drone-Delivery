# System Architecture

## Delivery subsystem

Mission Planner is used to prepare GPS waypoint missions. The Pixhawk flight controller executes the mission and manages stabilization and motor outputs. A GPS module supplies position information. A servo-operated mechanism is intended to release a lightweight payload from its box when commanded. The supplied presentation contains Mission Planner waypoint and telemetry examples and a `DO_SET_SERVO` command example.

## Reactive obstacle-avoidance subsystem

Three VL53L0X ToF sensors face forward, left, and right. The ESP32 reads their distances and exchanges telemetry/control messages with Pixhawk over MAVLink. When the front distance crosses the configured threshold, the described logic moves backward, compares the left and right distances, commands movement toward the side selected as safer, clears the temporary control command, and allows the autonomous mission to continue.

## Monitoring

The ESP32 web server exposes flight mode, arm state, sensor readings, and obstacle status. The project process document describes automatic refresh every 500 ms.

## Important implementation details still needed

- ESP32 board variant and firmware framework/version
- Exact sensor-to-ESP32 pin map and I²C addresses
- ESP32-to-Pixhawk serial port, baud rate, MAVLink version/dialect
- Obstacle threshold and filtering/debounce logic
- Exact RC override channels/values, velocity frame and units, and release conditions
- Pixhawk firmware version, parameters, and failsafe settings
- Servo output channel and calibrated PWM values
- Actual source files and repeatable test logs
