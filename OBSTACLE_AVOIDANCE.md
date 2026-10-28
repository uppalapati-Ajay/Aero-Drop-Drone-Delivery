# Obstacle Avoidance Logic

## Inputs

- Front VL53L0X distance
- Left VL53L0X distance
- Right VL53L0X distance
- Pixhawk telemetry such as flight mode and armed state

## High-level algorithm

```text
repeat while system is running:
    read front, left, and right distance sensors
    update dashboard status

    if front distance is below configured threshold:
        verify flight state permits the maneuver
        command a temporary backward movement
        compare left and right clearance
        command lateral velocity toward the selected side
        stop sending the temporary override / clear override as implemented
        verify the mission can continue
    else:
        continue normal monitoring
```

This is pseudocode based on the project report, not a replacement for the actual firmware. The report does not specify exact thresholds, command frames, velocity values, timeout behavior, or recovery verification. Those must be copied from the final source and validated against the configured flight controller.

## Safety cases to validate

- One sensor returns an invalid or stale measurement.
- Both sides appear blocked or give equal readings.
- MAVLink communication drops during a maneuver.
- The aircraft is not in an expected flight mode or is not armed.
- A pilot takes over while avoidance is active.
- The obstacle remains after the first maneuver.
- The override is not cleared as intended.

Do not claim these cases are handled unless code review and testing confirm it.
