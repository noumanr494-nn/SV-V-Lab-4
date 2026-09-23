# Autonomous Delivery Robot — State Transition Table

| Current State  | Event / Condition         | Next State       | Requirement |
|--------------- |------------------         |------------      |-------------|
| IDLE           | Delivery Request Received | NAVIGATING       | R2 |
| NAVIGATING     | Obstacle Detected         |AVOIDING_OBSTACLE | R4 |
| AVOIDING_OBSTACLE | Obstacle Avoided       | NAVIGATING       | R5 |
| NAVIGATING     | Destination Reached       | DELIVERING       | R6 |
| DELIVERING     | Delivery Successful       | RETURNING        | R7 |
| NAVIGATING     | Critical Battery          | RETURNING        | R8 |
| RETURNING      | Warehouse Reached         | IDLE             | R9 |

## Invalid Transitions

| Current State     | Event                             | Invalid Next State   | Reason |
|---------------    |-------                            |-------------------    |--------|
| IDLE              | No delivery request               | DELIVERING            | Violates R2 and R10 |
| AVOIDING_OBSTACLE | Obstacle not avoided              | DELIVERING            | Violates R6 and R10 |
| IDLE              | Delivery Request Received         | DELIVERING            | Robot must navigate before delivery |


# State Transition Table Verification

## Check 1 — Invalid Transition

### Question
Can the following transition happen?

IDLE → DELIVERING

### Verification Result
NO. This transition is invalid.

The robot cannot directly move from IDLE to DELIVERING.

The robot must first receive a delivery request and enter the NAVIGATING state. It can enter DELIVERING only after reaching the destination.

### Violated Requirements
- R2 — The robot shall start NAVIGATING only after receiving a valid delivery request.
- R6 — The robot shall enter DELIVERING only after reaching the destination through navigation.
- R10 — The robot shall not transition directly from IDLE to DELIVERING.

### Correct Transition

IDLE
↓
NAVIGATING
↓
DELIVERING


---

## Check 2 — Missing Transition

### Question
What happens if there is no transition back from:

NAVIGATING
↓
AVOIDING_OBSTACLE

### Verification Result
The robot cannot continue its delivery journey.

If the robot enters AVOIDING_OBSTACLE and there is no transition back to NAVIGATING, the robot will remain stuck in obstacle-avoidance mode.

### Required Transition

AVOIDING_OBSTACLE
↓
Obstacle Avoided
↓
NAVIGATING

### Related Requirement
R5 — After successfully avoiding an obstacle, the robot shall return to the NAVIGATING state.


---

## Check 3 — Obstacle During Delivery

### Question
Can the robot move directly from:

AVOIDING_OBSTACLE → DELIVERING

### Verification Result
NO. This transition is invalid.

The robot must first return to NAVIGATING after avoiding the obstacle. It can enter DELIVERING only after reaching the destination.

### Correct Flow

AVOIDING_OBSTACLE
↓
Obstacle Avoided
↓
NAVIGATING
↓
Destination Reached
↓
DELIVERING

### Violated Requirements
- R5 — The robot shall return to NAVIGATING after avoiding an obstacle.
- R6 — The robot shall enter DELIVERING only after reaching the destination.
- R10 — The robot shall not transition directly from AVOIDING_OBSTACLE to DELIVERING.


---

# Overall Verification Result

| Check | Transition / Problem | Result |
|------|-----------------------|--------|
| Check 1 | IDLE → DELIVERING | INVALID |
| Check 2 | AVOIDING_OBSTACLE has no return transition | INVALID / MISSING TRANSITION |
| Check 3 | AVOIDING_OBSTACLE → DELIVERING | INVALID |

## Conclusion

The state transition model was verified against the defined requirements.

Invalid transitions were identified and the missing transition from AVOIDING_OBSTACLE back to NAVIGATING was identified.

The verified valid flow is:

IDLE
↓
NAVIGATING
↓
AVOIDING_OBSTACLE
↓
NAVIGATING
↓
DELIVERING
↓
RETURNING
↓
IDLE

Critical battery condition:

NAVIGATING
↓
RETURNING
↓
IDLE
