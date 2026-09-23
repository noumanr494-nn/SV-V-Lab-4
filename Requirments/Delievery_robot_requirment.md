# Autonomous Delivery Robot — Requirements

| Req. ID | Requirement |
|--------|-------------|
| R1 | The robot shall remain in the IDLE state when it is switched on and no delivery request is available. |
| R2 | The robot shall start NAVIGATING only after receiving a valid delivery request. |
| R3 | The robot shall move toward the requested destination while in the NAVIGATING state. |
| R4 | When an obstacle is detected during navigation, the robot shall enter the AVOIDING_OBSTACLE state. |
| R5 | After successfully avoiding an obstacle, the robot shall return to the NAVIGATING state. |
| R6 | The robot shall enter the DELIVERING state only after reaching the destination through navigation. |
| R7 | After successful package delivery, the robot shall enter the RETURNING state and travel toward the warehouse. |
| R8 | If the battery becomes critically low during navigation, the robot shall stop the current delivery journey and enter the RETURNING state. |
| R9 | When the robot reaches the warehouse, it shall enter the IDLE state and wait for a new delivery request. |
| R10 | The robot shall not transition directly from IDLE to DELIVERING or from AVOIDING_OBSTACLE to DELIVERING. |
