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
