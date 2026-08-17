# WorkflowAutomation-bpmn-process-assignment
# BPMN Process Modeling Assignment

This repository contains three BPMN 2.0 process models built in Camunda Modeler, each covering a different business scenario.

## Repository structure

```
bpmn-assignment/
├── README.md
├── diagrams/
│   ├── employee-leave-approval.bpmn
│   ├── purchase-order.bpmn
│   └── it-service-request.bpmn
└── images/
    ├── employee-leave-approval.png
    ├── purchase-order.png
    └── it-service-request.png
```

## Tools used

- **Camunda Modeler** — used to design and export all BPMN diagrams
- BPMN elements used across the models: Start Events, Tasks, Exclusive Gateways, End Events, Sequence Flows

## Scenario 1: Employee Leave Approval

**Description:** An employee submits a leave request. The system checks the employee's leave balance. If the balance is insufficient, the employee is notified and the process ends. If sufficient, the request is sent to the manager for a decision. If approved, the leave balance is updated and an approval notification is sent; if rejected, a rejection notification is sent.

**Process flow:**
1. Start Event — Employee submits leave request
2. Task — Check leave balance
3. Exclusive Gateway — Is leave balance sufficient?
   - **No** → Task: Send insufficient balance notification → End Event
   - **Yes** → Task: Send request to manager
4. Exclusive Gateway — Manager decision
   - **Approved** → Task: Update employee leave balance → Task: Send approval notification → End Event
   - **Rejected** → Task: Send rejection notification → End Event

**File:** `diagrams/employee-leave-approval.bpmn`
**Diagram:**
![Employee Leave Approval Process](images/employee-leave-approval.png.jpeg)

## Scenario 2: Online Purchase Order Processing

**Description:** A customer places an order. The system checks product availability, processes payment if the product is available, and ships the order if payment succeeds. Failure at any check ends the process with the appropriate customer notification.

**Process flow:**
1. Start Event — Customer places order
2. Task — Check product availability
3. Exclusive Gateway — Product available?
   - **No** → Task: Notify customer of out-of-stock → End Event
   - **Yes** → Task: Process payment
4. Exclusive Gateway — Payment successful?
   - **No** → Task: Notify customer of payment failure → End Event
   - **Yes** → Task: Confirm order → Task: Prepare product for shipment → Task: Ship order → Task: Send shipping confirmation → End Event

**File:** `diagrams/purchase-order.bpmn`
**Diagram:**
![Purchase Order Process](images/purchase-order.png.jpeg)

## Scenario 3: IT Service Request

**Description:** An employee reports an IT problem, which the help desk registers and triages by severity to the appropriate technician. The technician attempts to resolve the issue internally, escalating to an external provider if necessary, before the help desk closes out the request.

**Process flow:**
1. Start Event — Employee reports IT problem
2. Task — Submit IT support request
3. Task — Help desk registers request
4. Exclusive Gateway — Security level?
   - **Low** → Task: Assign to support technician
   - **High** → Task: Assign to senior technician
5. Task — Technician investigates problem
6. Exclusive Gateway — Can be resolved internally?
   - **Yes** → Task: Fix the problem
   - **No** → Task: Escalate to external service provider
7. Task — Help desk updates request status
8. Task — Send resolution notification to employee
9. End Event

**File:** `diagrams/it-service-request.bpmn`
**Diagram:**
![IT Service Request Process](images/it-service-request.png.jpeg)


