# Product Requirements Document (PRD)

**Title:** Network Assets Management Agent
**Date:** 2026-10-09
**Owner:** Asset Management / IT Operations
**Solution Category:** AI Agent

---

## Product Purpose & Value Proposition

**Elevator Pitch:**
Field engineers and asset managers waste significant time navigating complex ERP screens to find network assets and coordinate maintenance. This agent provides an instant, conversational interface to SAP S/4HANA — so anyone can locate an asset or retrieve a maintenance plan in seconds, using plain language.

**Business Need:**
Network operations teams manage large portfolios of telecom, IT, and utility infrastructure assets. Today, finding a specific asset's location or checking its maintenance schedule requires navigating multiple SAP transactions, leading to delays and frustration — especially in field scenarios. There is no intelligent interface to surface this information quickly.

**Expected Value:**
A 50% reduction in time spent locating assets, freeing engineers for higher-value fieldwork and reducing operational delays caused by information lookup bottlenecks.

**Product Objectives (Prioritized):**
1. Enable instant natural language lookup of network asset inventory and location from S/4HANA
2. Provide conversational access to maintenance plans and schedules
3. Allow asset managers to raise maintenance notifications through the agent without accessing SAP directly

---

## Business Metrics

| Metric | Baseline | Target | Timeline | Process / Capability | Source |
|--------|----------|--------|----------|----------------------|--------|
| Time spent locating assets | — | 50% reduction | — | Asset inventory tracking | user |

---

## User Profiles & Personas

### Primary Persona: Alex — Network Field Engineer

Alex is a 34-year-old network technician responsible for inspecting and maintaining telecom towers, routers, switches, and cabling across a regional network. He is frequently on-site and needs to quickly identify what equipment is installed at a location, confirm its technical specs, and check whether any maintenance activity is planned. He currently has to call the office or open SAP on a laptop to find this information — a slow process when working in the field. Alex is comfortable with mobile apps and chat interfaces but has limited SAP experience. He needs answers fast, in plain language.

**Goals:**
- Find the exact location and details of any asset without navigating SAP transactions
- Confirm maintenance status before beginning fieldwork

**Key Tasks:**
- Query an asset by name, ID, or location
- Retrieve functional location and equipment details
- Check whether a maintenance notification exists for a specific asset

---

### Secondary Persona: Maya — Asset Manager & Planner

Maya is a 41-year-old asset management specialist who oversees maintenance planning across a portfolio of thousands of network assets. She coordinates with field teams, schedules maintenance windows, and tracks compliance with maintenance plans. She spends considerable time cross-referencing equipment records and maintenance plans in SAP. She wants to accelerate planning tasks and reduce the back-and-forth with field teams.

**Goals:**
- Quickly retrieve and compare maintenance plans for multiple assets
- Create and manage maintenance notifications efficiently

**Key Tasks:**
- Look up active maintenance plans for an asset or functional location
- Create a new maintenance notification
- Review planned maintenance schedules

---

## Product Principles

1. **Plain language first**: Every interaction must be usable without SAP knowledge — queries and responses use business language, not system codes.
2. **Read before write**: The agent defaults to information retrieval; write operations (creating notifications, orders) require explicit user confirmation before execution.
3. **Transparency**: The agent always cites which S/4HANA record it is referencing, so users can trust and verify the information.
4. **Field-ready**: Responses must be concise and actionable — suitable for engineers consulting the agent from a mobile device in the field.

---

## Business Context

**Current State:**
Engineers and planners use SAP S/4HANA Cloud Private Edition as the system of record for all asset and maintenance data. Accessing this data requires navigating complex transaction screens (PM/EAM module), which is inefficient — especially for field staff who need quick answers. There is no conversational or simplified interface today.

**Strategic Alignment:**
This agent directly supports the "Acquire to Decommission" E2E process by improving the efficiency of asset maintenance planning and execution. It aligns with the organisation's goal of reducing operational overhead and making SAP data more accessible to non-expert users.

---

## Goals and Non-Goals

### Goals (In Scope)

- Natural language querying of equipment records and functional locations from S/4HANA
- Retrieval and presentation of maintenance plans and maintenance items
- Creation of maintenance notifications via the agent
- Functional location hierarchy navigation
- Conversational assistance for maintenance scheduling

### Non-Goals (Out of Scope)

- Real-time IoT sensor data ingestion or live equipment health monitoring
- Automated decommissioning workflows
- Financial or procurement processes (SAP Ariba, FI/CO modules)
- Integration with non-SAP asset management systems
- UI application — the agent is the interface

---

## Requirements

### Must-Have Requirements

**R1: Asset Location Lookup**

- **Problem to Solve**: Engineers spend too long finding where a specific asset is installed when navigating SAP screens.
- **User Story**: As a field engineer, I need to ask the agent for an asset's location and receive its functional location and physical details so that I can find it quickly without opening SAP.
- **Acceptance Criteria**:
  - Given I provide an asset name, ID, or description, when I ask the agent, then it returns the correct equipment record with functional location, installation details, and technical data.
  - Given the asset does not exist, when I query, then the agent responds with a clear "not found" message and suggests alternatives.
- **Maps to Objective**: Objective 1
- **Priority Rank**: 1

---

**R2: Natural Language Asset Search**

- **Problem to Solve**: Engineers often need to search by asset type or location rather than an exact asset ID, which S/4HANA does not support conversationally.
- **User Story**: As a field engineer, I need to search for assets by type, category, or site in plain language so that I can find the right equipment even when I don't know the exact asset ID.
- **Acceptance Criteria**:
  - Given I provide a search term (e.g., "all routers at site Berlin-North"), when I query the agent, then it returns a list of matching equipment records.
- **Maps to Objective**: Objective 1
- **Priority Rank**: 2

---

**R3: Maintenance Plan Retrieval**

- **Problem to Solve**: Planners manually look up maintenance plans across multiple SAP screens, which is time-consuming when covering large asset portfolios.
- **User Story**: As an asset manager, I need to retrieve the maintenance plan and schedule for any asset so that I can plan fieldwork and ensure compliance with maintenance cycles.
- **Acceptance Criteria**:
  - Given I ask for the maintenance plan of a specific asset or location, when the agent queries S/4HANA, then it returns the relevant maintenance plan details including intervals, next due date, and responsible parties.
- **Maps to Objective**: Objective 2
- **Priority Rank**: 3

---

**R4: Maintenance Notification Creation**

- **Problem to Solve**: Creating a maintenance notification in SAP requires navigating multiple screens, which field engineers avoid — leading to underreporting of faults.
- **User Story**: As a field engineer or asset manager, I need to raise a maintenance notification through the agent so that I can report faults or schedule work without navigating SAP transactions.
- **Acceptance Criteria**:
  - Given I describe a fault or maintenance need, when I instruct the agent to create a notification, then it presents the notification details for my confirmation before submitting.
  - Given I confirm, then the agent creates the notification in S/4HANA and returns the notification number.
- **Maps to Objective**: Objective 3
- **Priority Rank**: 4

---

**R5: Confirmation & Action Summary**

- **Problem to Solve**: Users need to trust that agent-initiated actions (writes) have been executed correctly.
- **User Story**: As a user, I need the agent to confirm every completed action with a clear summary so that I can verify what was done and have a reference for follow-up.
- **Acceptance Criteria**:
  - Given any write action is completed (e.g., notification created), when the agent responds, then it includes the SAP record ID and a plain-language summary of what was created or changed.
- **Maps to Objective**: Objectives 2 and 3
- **Priority Rank**: 5

---

**R6: Functional Location Hierarchy Navigation**

- **Problem to Solve**: Understanding where an asset sits within the network structure (site → rack → device) requires multiple SAP lookups.
- **User Story**: As a field engineer, I need to browse the functional location hierarchy for a site so that I can understand the network structure and find all assets at a location.
- **Acceptance Criteria**:
  - Given I ask for the assets or structure at a specific location, when the agent queries the functional location hierarchy, then it returns a structured view of sub-locations and associated equipment.
- **Maps to Objective**: Objective 1
- **Priority Rank**: 6

---

### High-Want Requirements

**R7: Maintenance Order Retrieval**

- **Problem to Solve**: Planners need to review open or completed maintenance orders for audit and compliance.
- **User Story**: As an asset manager, I need to retrieve maintenance orders for an asset or location so that I can track work progress and compliance.
- **Priority Rank**: 1

**R8: Multi-Asset Comparison**

- **Problem to Solve**: Planners often need to compare maintenance schedules across multiple assets at once to optimise field scheduling.
- **User Story**: As an asset manager, I need to compare the maintenance schedules of multiple assets in a single query so that I can plan crew deployments efficiently.
- **Priority Rank**: 2

---

## Non-Functional Requirements

### Performance

- **Latency**: 95th percentile response time under 5 seconds for read queries; under 8 seconds for write operations including confirmation step.
- **Throughput**: Support concurrent sessions for up to 50 users.

### Reliability

- **Availability**: Agent service available 99.5% of business hours.
- **Fallback**: If S/4HANA APIs are unavailable, the agent informs the user clearly and does not return stale or fabricated data.

### Explainability

- **Traceability**: Every response cites the S/4HANA record(s) used (equipment number, functional location ID, maintenance plan number).
- **Decision Logging**: All tool calls and their outcomes are logged for auditability.
- **Uncertainty Communication**: When the agent cannot find a match or has low confidence, it states this explicitly and offers to refine the search.

---

## Solution Architecture

**Architecture Overview:**
A Python AI agent deployed on SAP BTP, communicating via the A2A protocol. The agent uses MCP tools — generated from S/4HANA OData API specifications — to query and write data in SAP S/4HANA Cloud Private Edition. Users interact with the agent through a conversational interface.

**Key Components:**

- **AI Agent (Python/A2A)**: Core reasoning engine deployed on SAP BTP. Interprets natural language requests, selects appropriate MCP tools, and orchestrates multi-step interactions.
- **MCP Translation Layer**: Seven MCP tool definitions generated from S/4HANA OData API specs, exposing equipment, location, and maintenance operations as callable tools.
- **SAP S/4HANA Cloud Private Edition**: System of record for all asset and maintenance master data.
- **SAP BTP Destination Service**: Manages authentication and connectivity between the agent and S/4HANA APIs.

**Integration Points:**

- Equipment API (`API_EQUIPMENT:v1`): Read equipment master data — read-only
- Functional Location API (`API_FUNCTIONALLOCATION:v1`): Read functional location records — read-only
- Functional Location Hierarchy API (`FUNCNLLOCSTRUCLIST_0001:v1`): Read location hierarchy — read-only
- Maintenance Plan API (`API_MAINTENANCEPLAN:v1`): Read maintenance plans — read-only
- Maintenance Item API (`API_MAINTENANCEITEM:v1`): Read maintenance items — read-only
- Maintenance Order API (`CE_API_MAINTENANCEORDER_0002:v2`): Read/write maintenance orders
- Maintenance Notification API (`API_MAINTNOTIFICATION:v1`): Create and read maintenance notifications — write with confirmation gate

---

### Agent Extensibility & Instrumentation

**Agent Extensibility:**
The agent is designed with named extension points to allow future capabilities to be added without modifying core logic:

- **Tool extension point**: New MCP tools (e.g., for spare parts lookup, GIS location data) can be registered and made available to the agent without core changes.
- **Skill extension point**: New conversational skills (e.g., asset risk scoring, decommissioning advisory) can be added as modular skill files.
- **Prompt extension point**: The system prompt supports override sections so that tenant-specific terminology or guardrails can be injected at deployment time.

**Business Step Instrumentation:**
Every key business step emits a structured log on achievement and on miss, enabling observability and monitoring in production. See the Milestones section for the full log statement specification.

---

### Automation & Agent Behaviour

**Automation Level:** Autonomous agent with human confirmation gate for write operations

**Actions the system performs without human approval:**
- Searching and retrieving equipment records
- Querying functional locations and hierarchy
- Retrieving maintenance plans, items, and orders

**Actions that require human review or approval:**
- Creating maintenance notifications
- Creating or updating maintenance orders

**Model or engine used:** Large language model via SAP Generative AI Hub (GPT-4o or equivalent)

**Knowledge & data sources accessed:**
- SAP S/4HANA Cloud Private Edition (equipment master data, functional locations, maintenance plans, notifications, orders) — governed by the asset management team

**Tools or connectors invoked:**
- Equipment tool (via MCP): Look up equipment records by ID, name, or attributes — read-only
- Functional Location tool (via MCP): Retrieve functional location records and attributes — read-only
- Functional Location Hierarchy tool (via MCP): Browse location structure — read-only
- Maintenance Plan tool (via MCP): Retrieve maintenance plan details — read-only
- Maintenance Item tool (via MCP): Retrieve maintenance items — read-only
- Maintenance Order tool (via MCP): Read/write maintenance orders
- Maintenance Notification tool (via MCP): Create and retrieve maintenance notifications — write with confirmation

**Guardrails & fail-safes:**
- Write operations (notification creation, order updates) always present a confirmation step before execution — the agent never writes to S/4HANA without explicit user approval in the same session.
- The agent must never fabricate asset data; if a record is not found, it states so clearly.
- If S/4HANA APIs return errors, the agent surfaces a user-friendly message and does not retry automatically.
- The agent does not store or cache asset master data between sessions — all data is fetched live from S/4HANA.

---

## Milestones

### M1: Asset Query

- **Description**: The agent receives a natural language question about an asset and successfully retrieves the matching equipment record from S/4HANA.
- **Achieved when**: A valid equipment record is returned from the Equipment API in response to the user's query.
- **Log on achievement**: `M1.achieved: asset query completed — equipment record retrieved for [equipment_id]`
- **Log on miss**: `M1.missed: asset query did not return a valid equipment record — [reason]`

---

### M2: Location Identification

- **Description**: The agent returns accurate functional location and physical installation details for the queried asset.
- **Achieved when**: The functional location and installation data for the equipment are successfully presented to the user.
- **Log on achievement**: `M2.achieved: location identified — functional location [fl_id] returned for equipment [equipment_id]`
- **Log on miss**: `M2.missed: functional location not resolved for equipment [equipment_id] — [reason]`

---

### M3: Maintenance Plan Retrieval

- **Description**: The agent fetches and presents the relevant maintenance plan(s) or schedule(s) for a given asset or location.
- **Achieved when**: One or more maintenance plan records are returned from the Maintenance Plan API and presented to the user.
- **Log on achievement**: `M3.achieved: maintenance plan retrieved — [plan_count] plan(s) returned for [asset_or_location_id]`
- **Log on miss**: `M3.missed: no maintenance plan found for [asset_or_location_id] — [reason]`

---

### M4: Maintenance Scheduling Assistance

- **Description**: The agent assists the user in scheduling or raising a maintenance activity by creating a maintenance notification in S/4HANA after explicit user confirmation.
- **Achieved when**: A maintenance notification is successfully created in S/4HANA and the notification number is returned to the user.
- **Log on achievement**: `M4.achieved: maintenance notification created — notification [notification_id] for equipment [equipment_id]`
- **Log on miss**: `M4.missed: maintenance notification not created — [reason]`

---

### M5: Confirmation & Summary

- **Description**: The agent confirms all completed actions and delivers a clear, plain-language summary to the user.
- **Achieved when**: A confirmation message including the SAP record reference is delivered to the user after a completed action.
- **Log on achievement**: `M5.achieved: action confirmed and summary delivered — [action_type] for [record_id]`
- **Log on miss**: `M5.missed: confirmation or summary not delivered after [action_type] — [reason]`

---

## Risks, Assumptions, and Dependencies

### Risks

- **API authorisation misconfiguration**: S/4HANA OData APIs require correct BTP destination setup and authorisation roles. Incorrect configuration will block all agent tool calls.
- **Asset data quality**: If equipment records or functional locations in S/4HANA are incomplete or outdated, the agent's responses will reflect those gaps, reducing trust among field users.
- **LLM hallucination on asset data**: The agent must be constrained to use only tool-returned data and never generate asset details from its own knowledge.

### Assumptions

- SAP S/4HANA Cloud Private Edition is the single system of record for all network asset and maintenance data in scope.
- The seven OData APIs identified are accessible from SAP BTP via the Destination Service with appropriate authorisation.
- Users interact with the agent via a supported conversational channel (e.g., SAP Build Work Zone, Joule, or similar).

### Dependencies

- SAP BTP subscription with Generative AI Hub access
- SAP S/4HANA Cloud Private Edition with the relevant Plant Maintenance (PM/EAM) configuration complete
- BTP Destination Service configured for S/4HANA connectivity
- MCP translation files generated for each of the seven OData APIs

---

## Open Questions

- Which conversational channel will users access the agent from (SAP Build Work Zone, Joule, standalone chat)?
- Are there additional asset categories (e.g., civil infrastructure) that should be in scope in future iterations?
- Should the agent support multiple languages for field teams in different regions?

---

## Appendix

### Glossary

- **Equipment**: An individual physical asset registered in SAP S/4HANA (e.g., a router, switch, or cable segment).
- **Functional Location**: A hierarchical organisational unit in SAP representing where an asset is installed (e.g., site > building > rack).
- **Maintenance Plan**: A scheduled maintenance programme in SAP defining intervals and tasks for an asset.
- **Maintenance Notification**: A record raised in SAP to report a fault, request inspection, or trigger a maintenance activity.
- **MCP Tool**: A callable function exposed to the AI agent, wrapping an S/4HANA OData API endpoint.
- **A2A Protocol**: Agent-to-Agent communication protocol used by SAP BTP AI agents for interoperability.

### References

- SAP S/4HANA Equipment OData API: `sap.s4:apiResource:API_EQUIPMENT:v1`
- SAP S/4HANA Functional Location OData API: `sap.s4:apiResource:API_FUNCTIONALLOCATION:v1`
- SAP S/4HANA Maintenance Plan OData API: `sap.s4:apiResource:API_MAINTENANCEPLAN:v1`
- SAP S/4HANA Maintenance Notification OData API: `sap.s4:apiResource:API_MAINTNOTIFICATION:v1`
- SAP S/4HANA Maintenance Order OData API: `sap.s4:apiResource:CE_API_MAINTENANCEORDER_0002:v2`
- SAP Build Knowledge Graph — Acquire to Decommission E2E Process
