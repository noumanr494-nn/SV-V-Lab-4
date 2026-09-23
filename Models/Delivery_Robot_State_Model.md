# Autonomous Delivery Robot — State Model

## States

| State ID | State Name | Description |
|----------|------------|-------------|
| S1 | IDLE | Robot is waiting for a delivery request. |
| S2 | NAVIGATING | Robot is moving toward the delivery destination. |
| S3 | AVOIDING_OBSTACLE | Robot is temporarily stopped from normal navigation and is avoiding an obstacle. |
| S4 | DELIVERING | Robot has reached the destination and is delivering the package. |
| S5 | RETURNING | Robot is travelling back to the warehouse. |

## Valid State Flow

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

Critical battery during NAVIGATING:
## Events / Conditions

| Event ID | Event / Condition |
|----------|-------------------|
| E1 | Delivery Request Received |
| E2 | Destination Reached |
| E3 | Delivery Successful |
| E4 | Warehouse Reached |
| E5 | Obstacle Detected |
| E6 | Obstacle Avoided |
| E7 | Critical Battery |

NAVIGATING
  ↓
RETURNING
  ↓
IDLE
