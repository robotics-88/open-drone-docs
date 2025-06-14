# Task Manager: State Machine

The primary control loop is the state machine in the task manager node. This state machine is described in the diagram below:

```mermaid
stateDiagram
   direction TB

   accTitle: State machine diagram for Open Drone Core

   classDef system fill:var(--md-default-bg-color),stroke:#555,color:var(--md-default-fg-color)

   [*] --> INITIALIZING:::system
   INITIALIZING --> PREFLIGHT_CHECKS:::system
   PREFLIGHT_CHECKS--> READY:::system : if ready to arm
   READY --> PREFLIGHT_CHECKS : if not ready to arm

   READY --> MANUAL : on pilot takes off
   MANUAL --> COMPLETE:::system : on arm -> disarm
   COMPLETE --> PREFLIGHT_CHECKS

   READY --> TAKING_OFF : on accepted mission
   TAKING_OFF --> MISSION : on altitude reached
   MISSION --> MISSION : on new mission accepted
   MISSION --> RTL_88 : on mission complete

   RTL_88 --> LANDING : on reached home
   LANDING --> COMPLETE : on arm -> disarm
```

## States
describe all

## Events
describe all