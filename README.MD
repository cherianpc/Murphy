## Overview
This is an autonomous navigation framework with modular movement primitives, enhanced safety systems, and simplified motor group abstractions. Made for Murphy

## Quick Reference Guide

### Movement Functions
```python
# Drive forward/backward
drive_distance(1.0, velocity_percent=70)     # 1 turn forward
drive_distance(-0.5, velocity_percent=50)    # 0.5 turns backward

# Turning
turn_in_place(0.3, velocity_percent=50)      # ~90° pivot turn

# Precise positioning  
drive_to_absolute(2.0, 2.0)                  # Move to exact positions
```

### Intake/Shooting
```python
intake_in(1.5, speed=80)                     # Collect for 1.5 sec
fire_flywheel(2.0, speed=100)                # Shoot for 2 sec
```

### Pneumatics
```python
set_scoop(True)     # Raise scoop
set_scoop(False)    # Lower scoop
set_wing(True)      # Deploy wing
set_wing(False)     # Retract wing
```

### Emergency Stop
Press **Controller Right Button** during autonomous for immediate stop.

## Example Autonomous
```python
def my_auto():
    drive_distance(1.5)        # Drive off bar
    turn_in_place(0.25)        # Turn toward triballs
    intake_in(2.0)             # Collect
    fire_flywheel(3.0)         # Score
    drive_distance(-1.0)       # Return
```
___

### What Timeouts Do

Every movement function has a timeout_sec parameter that prevents your robot from getting stuck forever:
```python
# With timeout (recommended)
drive_distance(2.0, velocity_percent=70, timeout_sec=5.0)

# Without timeout (dangerous?)
drive_distance(2.0)  # Could get stuck forever if blocked but default is 5 seconds
```
___

### if not Statements and Early Returns
What They Do

These patterns create a safety net that stops your autonomous immediately if something goes wrong:
python

```python
if not drive_distance(2.0, velocity_percent=70):
    return  # ⛔ STOP HERE IF FAILED
```
How It Works
- if not checks if the function returned False
- return immediately exits the entire autonomous function
- Result: If Step 1 fails, Steps 2, 3, 4 never run