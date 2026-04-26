AIGov — AI Governance & Data Flow Builder
AIGov is a fully self-contained, browser-based tool for mapping and documenting AI system data flows with inline governance guidance. Designed for AI governance leads, risk managers, privacy engineers, and compliance teams who need to visualise how data moves through AI pipelines, identify regulatory obligations at each touchpoint, and produce audit-ready documentation.
No installation. No server. No dependencies. Open the HTML file in any modern browser and start diagramming.
***Why This Exists
Regulators and standards bodies now require organisations deploying AI systems to maintain accurate documentation of how data enters, transforms, and exits their AI pipelines. The EU AI Act mandates technical documentation, data governance records, and logging plans for high-risk systems (Arts. 10–12). NIST AI RMF asks teams to map, measure, and govern AI risk across the full system lifecycle. GDPR requires data protection impact assessments when AI processes personal data at scale (Art. 35). ISO 42001 requires an AI Management System with documented controls.
Most diagramming tools are general-purpose — they don't know what a vector store is, they won't flag that an inference response flowing into an automated decision triggers GDPR Art. 22 rights, and they can't surface the specific EU AI Act article that applies when you place a Foundation Model on the canvas.
AIGov is built specifically for AI governance documentation, with governance-aware components, colour-coded data flow types, and inline compliance guidance tied to the EU AI Act, NIST AI RMF, GDPR, and ISO 42001.
***Features
Interactive Canvas
Components are placed by clicking a type in the sidebar, then clicking the canvas. Hover any placed component to reveal four connection ports (N/S/E/W); drag from a port to another component to draw a data flow, or use Connect mode for a click-click workflow. Connections route automatically using orthogonal paths — L-bends when ports are perpendicular, Z-bends when parallel — and re-route in real time as components are repositioned.
Pan by dragging the canvas background. Scroll to zoom between 15% and 400%, zooming toward the cursor. The ± toolbar buttons zoom to the canvas center. Use ⊡ Fit to frame all components and zones.
Undo / Redo
Every action — placing a component, drawing a flow, moving items, deleting, changing a flow type — is recorded in a 50-step history. Ctrl+Z undoes and Ctrl+Y (or Ctrl+Shift+Z) redoes. Toolbar buttons grey out when the stack is empty. An amber dot indicates unsaved changes.
Multi-Select
Drag across empty canvas to rubber-band select all components within the marquee. Hold Shift and click to add or remove individual components. Selected components move together and delete together. The Properties panel shows a count summary when multiple items are active.
Copy, Paste, and Duplicate
Ctrl+C copies the current selection. Ctrl+V pastes with a grid offset so copies don't land directly on originals. Ctrl+D or right-click → Duplicate duplicates a single component. Pasted components land in a new multi-selection for immediate repositioning.
Grid Snap
All placement and drag-end positions snap to a 22-pixel grid. Arrow keys nudge the selected component by one grid unit. The ⊞ Snap button toggles snapping on and off.
Inline Label Editing
Double-click any component or zone to open a floating text input positioned and scaled to the current zoom level. Enter commits, Escape cancels, clicking away commits via blur.
Risk Classification per Component
Every component has a Risk Classification field in the Properties panel with options aligned to EU AI Act categories: Minimal Risk, Limited Risk, High Risk (EU AI Act), Unacceptable Risk, and GPAI / Foundation Model. This field is persisted in the saved JSON file for use in downstream documentation.
Governance Boundary Zones
The Boundary Zones section in the sidebar lets you draw labelled scope rectangles directly on the canvas by dragging. Zones sit below all components, do not block interaction, and are independently moveable by dragging their header bar.
Zone	Colour	Governance Context
High-Risk AI System	Red	EU AI Act Arts. 6, 9–15 conformity obligations; conformity assessment required before market placement. ISO 42001 Clause 6.1 risk assessment; A.5.2 AI impact assessment
PII Processing Zone	Orange	GDPR Art. 35 DPIA likely required; data minimisation and purpose limitation controls apply. ISO 42001 A.6.2.7 privacy by design controls
Trust Boundary	Indigo	Authentication, authorisation, and input validation controls required at all crossing points. ISO 42001 A.6.2.8 security controls; A.4.4 context documentation
Third-Party / External	Purple	NIST AI RMF GOVERN 5 vendor risk assessment; contractual controls and ongoing monitoring. ISO 42001 A.10.2–A.10.4 third-party obligations, supply chain, and procurement
Human Oversight Zone	Green	EU AI Act Art. 14 meaningful oversight design; log all interventions. ISO 42001 A.9.3 oversight controls; A.3.2 roles and responsibilities
Zones are renameable (double-click), moveable (drag the header), and deletable (right-click). Zone-specific guidance appears in the Properties panel when a zone is selected.
Governance-Aware Components (35 types)
Components are organised into seven categories that reflect a typical AI system architecture.
Category	Components
Data Sources	End User / Consumer, Enterprise Data Store, Public Dataset, Third-Party Data, Real-time Stream, Synthetic Data
AI Pipeline	Data Ingestion, Data Preprocessor, Feature Store, Training Pipeline, Fine-tuning Pipeline, Vector DB / RAG Store, Model Registry
Models	Foundation Model / LLM, Custom Trained Model, 3rd-Party Model API, Embedding Model, AI Agent / Orchestrator
Applications	Application / UI, API Consumer, Automated Decision, Human-in-the-Loop, Output Filter / Guardrail
Governance	Content Moderation, Bias / Fairness Monitor, PII Detector / Redactor, Explainability Module, Audit Log, Model Monitor, Access Control / IAM
Infrastructure	API Gateway, GPU / TPU Cluster, Model Serving
External	Model Provider (ext.), Data Provider (ext.), Regulatory / Audit Body, Cloud Infrastructure
The Automated Decision component renders in red to signal that it is the highest-risk element in most deployments and to prompt appropriate scrutiny during diagram review.
Data Flow Types
Each connection carries a type that determines its colour, line style, and the guidance shown in the Properties panel.
Type	Colour	Style	Governance notes
🔴 PII / Personal Data	Red	Dashed	GDPR Arts. 5, 25 — minimise, document lawful basis, encrypt in transit
🟠 Sensitive Data	Orange	Dashed	Access controls, classification labelling, audit logging required
🟢 Anonymized / Pseudonymized	Green	Solid	Confirm re-identification risk assessed; pseudo-anonymized data remains personal under GDPR
📚 Training Data	Blue	Solid	EU AI Act Art. 10 — provenance, consent, bias assessment, dataset versioning
➡️ Inference Request	Purple	Solid	Validate and sanitise inputs; log request metadata; PII check before forwarding
⬅️ Inference Response	Violet	Solid	Apply output guardrails; check for GDPR Art. 22 implications if flowing to Automated Decision
🔧 Model Weights / Artifacts	Indigo	Solid	Encrypt at rest and in transit; restrict access; maintain model registry entry
📋 Audit Log	Slate	Dashed	EU AI Act Art. 12 — tamper-evident, complete, retained proportionate to risk
🔄 Feedback / RLHF	Teal	Solid	Feedback becomes training data — document consent and data lineage
👁 Human Review	Amber	Dashed	EU AI Act Art. 14 — design for genuinely informed oversight, not rubber-stamping
🔌 API Call (External)	Dark blue	Solid	Data processing agreement required; assess data residency; GDPR international transfer check
→ Generic Flow	Grey	Solid	For infrastructure and non-data flows
Inference Response flows targeting an Automated Decision component trigger an enhanced warning in the Properties panel flagging GDPR Art. 22 rights and EU AI Act Art. 14 human oversight requirements.
Inline Governance Guidance
Selecting any component or flow type surfaces relevant obligations in the Properties panel.
Component or Flow	Frameworks and specific obligations surfaced
Foundation Model / LLM	EU AI Act Art. 53 (GPAI documentation, copyright summary, transparency report); Art. 12 (logging); Art. 55 (systemic risk at 10²⁵ FLOPs). ISO 42001 A.6.1 (intended purpose spec); A.7.2 (technical documentation); A.8.2 (communication to users)
Custom Trained Model	Model Card requirements; bias/fairness assessments; NIST AI RMF MEASURE 2.5; EU AI Act Art. 10. ISO 42001 A.6.4.2 (model development); A.6.4.4 (evaluation and testing); A.5.3 (impact assessment)
3rd-Party Model API	Vendor risk assessment; data processing agreement; GDPR data residency; EU AI Act Art. 28. ISO 42001 A.10.2 (third-party obligations); A.10.3 (supply chain); A.10.4 (responsible procurement)
AI Agent / Orchestrator	Action boundary definition; kill switches; escalation paths; action logging; Art. 9 conformity if high-risk. ISO 42001 A.9.3 (human oversight); A.6.2.9 (safety by design); A.9.4 (incident management)
Automated Decision	GDPR Art. 22 (right to explanation, review, contest); EU AI Act Art. 14 (meaningful oversight); DPIA under Art. 35. ISO 42001 A.9.2 (intended use); A.9.3 (oversight controls); A.5.3 (impact assessment)
Human-in-the-Loop	EU AI Act Art. 14 meaningful oversight design; intervention authority; automation bias; intervention logging. ISO 42001 A.9.3 (oversight controls); A.3.2 (roles and responsibilities)
Training Pipeline	EU AI Act Art. 10 data governance; dataset versioning; bias detection; lineage retention. ISO 42001 A.6.3 (data management); A.6.3.3 (data preparation); A.6.3.5 (data quality); A.6.4.3 (training records)
Fine-tuning Pipeline	Data use rights; risk reclassification assessment; separate dataset documentation. ISO 42001 A.6.4.3 (training records); A.6.3.2 (data acquisition)
PII Detector / Redactor	GDPR Art. 25 (privacy by design); false negative rate documentation; redaction log retention. ISO 42001 A.6.2.7 (privacy by design controls)
Vector DB / RAG Store	Embedding re-identification risk; GDPR Art. 17 right to erasure; access controls. ISO 42001 A.6.3 (data management); A.6.3.5 (data quality)
Content Moderation	Filter category documentation; bypass testing; disparate impact assessment; activation logging. ISO 42001 A.6.2.9 (safety controls); A.6.7.4 (output review)
Bias / Fairness Monitor	EU AI Act Art. 9 + NIST AI RMF MEASURE 2.5; protected characteristic coverage; threshold documentation. ISO 42001 A.6.2.5 (fairness objectives); A.6.5.2 (testing)
Audit Log	EU AI Act Art. 12 tamper-evident logging; GDPR Art. 5(2) accountability; PII exclusion verification. ISO 42001 A.7.3 (record keeping); A.6.7.3 (performance monitoring)
Model Monitor	EU AI Act Art. 9 + NIST AI RMF MANAGE 3.1; drift detection; alerting thresholds; post-market surveillance. ISO 42001 A.6.7.3 (monitoring controls); A.9.4.2 (incident detection)
Explainability Module	EU AI Act Art. 13 (high-risk AI transparency); explanation fidelity documentation; audience-appropriate outputs. ISO 42001 A.6.2.6 (transparency and explainability objectives)
Access Control / IAM	NIST AI RMF GOVERN 6.1; least-privilege; access logs; quarterly review. ISO 42001 A.6.2.8 (security controls); A.3.2 (roles and responsibilities)
Synthetic Data	EU AI Act Art. 10 representativeness requirements; re-identification risk assessment. ISO 42001 A.6.3.2 (data acquisition); A.6.3.5 (data quality evaluation)
Model Provider (ext.)	TPSP risk assessment; data processing agreement; input retention policy; model update notifications; EU AI Act Art. 28. ISO 42001 A.10.3 (supply chain risks); A.10.4 (responsible procurement)
Regulatory / Audit Body	EU AI Office; national supervisory authorities; DPAs; sector regulators; EU AI Act Art. 99 penalty scale
End User / Consumer	EU AI Act Art. 50 (AI disclosure obligation); GDPR Art. 22 rights for automated decisions; feedback collection. ISO 42001 A.8.2 (communication); A.9.2 (intended use documentation)
Data Provider (ext.)	EU AI Act Art. 11; data licensing; GDPR compliance; contractual data quality standards. ISO 42001 A.10.3 (supply chain); A.10.4 (procurement controls)
PII flow	GDPR Arts. 5, 25 — minimise, document lawful basis; consider anonymization alternative. ISO 42001 A.6.2.7 (privacy by design documentation)
Inference Response → Automated Decision	Enhanced GDPR Art. 22 + EU AI Act Art. 14 warning; human review mechanism required
Training Data flow	EU AI Act Art. 10 provenance, consent, bias assessment. ISO 42001 A.6.3 (data management); A.6.3.3 (preparation); A.6.3.5 (quality validation)
Model Weights flow	Encrypt at rest and in transit; model registry entry. ISO 42001 A.7.2 (documentation); A.6.4.2 (model lifecycle events)
Audit Log flow	EU AI Act Art. 12 completeness; PII exclusion verification. ISO 42001 A.7.3 (compliance records)
Feedback / RLHF flow	GDPR consent for use in training; data lineage documentation. ISO 42001 A.6.3.2 (data acquisition governance)
Human Review flow	EU AI Act Art. 14 meaningful oversight design; log decisions. ISO 42001 A.9.3 (oversight controls documentation)
API Call (External)	GDPR international transfer assessment; data processing agreement; fallback procedures
Narrative and Version Control
The 📝 Narrative button opens a modal for writing a free-text system narrative — intended use, risk classification, data sources, trust boundaries, human oversight mechanisms, applicable regulations, assumptions, and exclusions — alongside a version history table. Content is persisted in the saved JSON and included in PDF exports.
Save and Load
Diagrams save to a .json file preserving all components, zones, flows, labels, risk classifications, positions, canvas state, narrative, and version history. The file is human-readable and version-controllable. On load, the file is validated — unknown component types, missing coordinates, and dangling edge references are caught before any state is mutated, with a descriptive error message on failure.
Export
SVG — Scalable vector output for reports, wikis, and Confluence pages. Interactive elements are stripped from the export.
PNG — 2× resolution raster image for presentations and Word documents.
PDF — Opens a print-ready browser window containing the diagram, generation date, version badge, and the full system narrative if one has been written. Use browser Print → Save as PDF.
***Usage
Quickstart
Download AIGov.html
Open it in Chrome, Firefox, Edge, or Safari
A sample LLM application diagram loads automatically, including Trust Boundary, PII Processing, and High-Risk AI zones
Click ⬜ New to clear the canvas and start your own diagram
Building a Diagram
Start by defining your system boundaries. Under Boundary Zones in the sidebar, drag a Trust Boundary zone to represent your internal system perimeter. Add a PII Processing Zone where personal data is ingested or processed, a High-Risk AI Zone around any automated decision systems, and a Third-Party / External zone for vendor components.
Place components within the appropriate zones. Click a type in the sidebar to arm the cursor, then click the canvas to place. Press Esc when finished placing that type. Use the Properties panel to set each component's Risk Classification — this is important for high-risk AI systems, GPAI models, and automated decision components.
Connect components by hovering to reveal port circles, then dragging port to port. Select each resulting flow and set its type in the Properties panel (PII, Inference Request, Audit Log, etc.). The Properties panel surfaces the relevant governance obligation immediately — review and use the labels field to document what data specifically flows on each edge.
Document your diagram using the 📝 Narrative button. Describe the system purpose, regulatory classification, key controls, third-party dependencies, and any scoping assumptions. Add a version entry each time the diagram is updated.
Documenting High-Risk AI Systems
For systems classified as high-risk under EU AI Act Annex III (biometric categorisation, credit scoring, employment screening, critical infrastructure, law enforcement, etc.):
Draw a High-Risk AI System zone around the in-scope components
Set Risk Classification to "High Risk (EU AI Act)" on each model component
Add a Bias / Fairness Monitor connected to the model, and an Audit Log receiving flows from every decision-making component
Ensure every Automated Decision component has a Human-in-the-Loop component connected with a Human Review flow
Document the conformity assessment approach and technical documentation plan in the Narrative
Keyboard Shortcuts
Shortcut	Action
`Ctrl+Z`	Undo
`Ctrl+Y` / `Ctrl+Shift+Z`	Redo
`Ctrl+C`	Copy selection
`Ctrl+V`	Paste
`Ctrl+D`	Duplicate selected component
`Delete` / `Backspace`	Delete selected item(s)
`Arrow keys`	Nudge selected component(s) by one grid unit
`Escape`	Cancel active mode; deselect all
`Shift+click`	Add/remove component from multi-selection
***Technical Notes
The tool is implemented as a single HTML file (~1,900 lines) with no external dependencies.
Rendering — SVG-based canvas with a pan/zoom viewport transform. Zones, edges, and nodes render in separate sublayers so zones always sit beneath connections and components.
Edge routing — Orthogonal (rectilinear) paths computed from source and target port directions. L-bend when ports are perpendicular; Z-bend through the axis midpoint when both ports face the same direction. Edge label backgrounds are sized using SVGTextElement.getComputedTextLength() for accurate fit across variable-width characters and emoji.
History — Structural state (nodes, edges, zones) is JSON-serialised into a 50-entry ring buffer on every mutation. Drags snapshot state at start and commit the entry only if movement exceeds a 2px threshold, avoiding spurious history entries from clicks.
Export — The SVG clone strips all interactive elements before serialisation. PNG export renders at 2× via Canvas. All Blob URLs are revoked after download.
Save/Load — Full diagram state as JSON. On load, a validation pass checks component types, coordinates, and edge reference integrity before mutating state. Node/edge/zone ID counters are recovered using reduce() rather than spread-into-Math.max to avoid call-stack overflow on large diagrams.
Tested in Chrome 120+, Firefox 121+, Edge 120+, and Safari 17+.
***Governance Framework Context
AIGov supports documentation relevant to the following frameworks. Diagrams produced should be reviewed by qualified practitioners as part of a formal governance programme.
EU AI Act (Regulation 2024/1689)
Article	Obligation
Art. 5	Prohibited AI practices — social scoring, manipulation, real-time biometric surveillance (subject to exceptions), emotion recognition in workplace/education
Art. 6 + Annex III	Classification of high-risk AI systems
Art. 9	Risk management system for high-risk AI — continuous, iterative process throughout the lifecycle
Art. 10	Data and data governance for training, validation, and testing data — relevance, representativeness, error-freedom
Art. 11	Technical documentation — maintained before market placement and updated throughout lifecycle
Art. 12	Logging — automatic, tamper-evident, sufficient to reconstruct the operation of high-risk AI
Art. 13	Transparency and information provision to deployers — instructions for use, limitations, intended purpose
Art. 14	Human oversight — deployers must designate natural persons with authority to understand, monitor, and override
Art. 15	Accuracy, robustness, and cybersecurity — appropriate to purpose, including against adversarial inputs
Art. 26	Obligations for deployers — monitor operation, log with retention of at least 6 months, report serious incidents
Art. 28	Obligations applying to importers and distributors of GPAI models
Art. 50	Transparency obligations — disclose AI interaction to users; label AI-generated content; mark deepfakes
Art. 53	GPAI model obligations — technical documentation, training data summary, copyright compliance summary, published transparency report
Art. 55	Systemic risk obligations for GPAI models trained with more than 10²⁵ FLOPs
Art. 99	Penalties — up to €35M or 7% of global annual turnover for prohibited practice violations
NIST AI Risk Management Framework 1.0
Function	Relevance
GOVERN	Organisational accountability structures, policies, roles, and culture for AI risk management
MAP	Context establishment, AI risk identification, and categorisation across the system lifecycle
MEASURE	Analysis, assessment, benchmarking, and monitoring of AI risk using qualitative and quantitative methods
MANAGE	Risk response, treatment, recovery, and residual risk decisions
GDPR (where personal data is processed)
Art. 5 — Principles: lawfulness, purpose limitation, data minimisation, accuracy, storage limitation, integrity and accountability
Art. 6 / 9 — Lawful basis for processing personal / special category data
Art. 17 — Right to erasure — affects vector stores and training datasets containing personal data
Art. 22 — Automated individual decision-making — right to human review, explanation, and to contest
Art. 25 — Data protection by design and by default
Art. 35 — Data Protection Impact Assessment — required for large-scale profiling or systematic processing using new technologies
ISO/IEC 42001:2023
ISO/IEC 42001 specifies requirements for an AI Management System (AIMS) and a set of controls in Annex A that organisations can select based on their AI risk profile. AIGov surfaces specific Annex A controls in-context throughout the Properties panel.
Core Clauses
Clause 3.2 — Roles and responsibilities — assign and document accountability for AI system governance
Clause 4.4 — Context of the organisation — document computing resources and environmental constraints affecting AI systems
Clause 5.3 — AI impact assessment process — assess and treat impacts on individuals and society before deployment
Clause 6.1 — AI risk assessment process — identify, analyse, and evaluate risks associated with AI systems
Clause 8.2 — AI system impact assessment — structured assessment of AI system impacts proportionate to risk
Annex A Controls (as referenced in AIGov guidance)
Control	Topic
A.3.2	Roles and responsibilities for AI system governance
A.5.2	AI system impact assessment process
A.5.3	AI system impact treatment
A.6.1	Policies for AI systems — documented intended purpose and use constraints
A.6.2.5	Fairness objectives and measures
A.6.2.6	Transparency and explainability of AI systems
A.6.2.7	Privacy by design for AI systems
A.6.2.8	Security controls for AI systems
A.6.2.9	Safety controls and fail-safe mechanisms
A.6.3	Data management — governance across the full data lifecycle
A.6.3.2	Data acquisition — documentation of sources, consent, and quality
A.6.3.3	Data preparation — cleaning, labelling, transformation records
A.6.3.5	Data quality — criteria, validation, and verification
A.6.4.2	AI model development — design decisions, rationale, and lifecycle records
A.6.4.3	AI model training — records of training runs, datasets, and parameters
A.6.4.4	AI model evaluation and testing — test methodology, results, and remediation
A.6.5.2	AI system verification and validation testing
A.6.7.3	AI system performance monitoring in production
A.6.7.4	Review of AI system outputs
A.7.2	Technical documentation — maintained throughout the AI system lifecycle
A.7.3	Record keeping — evidence of compliance with AIMS controls
A.8.2	Communication about AI systems — disclosure to users and stakeholders
A.9.2	Intended use specification and use constraint documentation
A.9.3	Human oversight mechanisms — intervention thresholds, authority, and logging
A.9.4	AI system incident management — detection, response, and lessons learned
A.9.4.2	AI incident detection and reporting
A.10.2	Third-party AI provider obligations — contractual controls
A.10.3	AI supply chain risk assessment
A.10.4	Responsible procurement of AI systems and components
***> Disclaimer: AIGov assists with the documentation and visualisation of AI system data flows. It does not validate, audit, or certify compliance with any regulation or standard. All diagrams and governance assessments should be reviewed by qualified legal, privacy, and AI risk practitioners as part of a formal governance programme.
