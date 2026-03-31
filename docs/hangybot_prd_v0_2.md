# HangyBot PRD v0.2
**Working title:** ATL Terminal Recovery + PDK FBO Catering  
**Document type:** Product Requirements Document for a fictional case study  
**Status:** Draft  
**Scope lock:** ATL and PDK are the live operating airports. BOS, TPA, and SJU remain feeder/reference airports. PiAware is used for live local visibility around ATL/PDK only.

## 1. Executive summary

HangyBot is a fictional airport food robotics company that predicts disruption-driven food demand and fulfills it through kitchen prep, smart inventory staging, digital ordering, and robot-assisted delivery.

The first product remains exactly the same:

**ATL Terminal Recovery**  
Predict disruption-driven passenger food demand in a defined ATL pilot zone and fulfill it through concession partners, pickup, human runners, and geofenced robots.

**PDK FBO Catering**  
Predict crew and private-aviation catering demand at PDK partner FBOs and fulfill it through concierge workflows, premium bundles, and optional lobby-side robot assistance.

This revision adds the platform and operating model needed to make HangyBot technically credible:

- a lakehouse + streaming data platform
- classical ML for disruption and demand prediction
- a foundation-model gateway for copilots, retrieval, and workflow automation
- dynamic model routing and provider switching
- vector search and grounded retrieval
- agentic orchestration with human approval gates
- multimodal ingestion for text, tabular, image, and audio
- MLOps and GenAIOps lifecycle management
- safety, privacy, compliance, and evaluation frameworks
- a standardized developer platform using Claude-style agent loops, MCP tooling, repo rules, and CI review workflows

To keep the MVP sane, this PRD uses three priority bands:

- **P0**: required for ATL/PDK pilot launch
- **P1**: hardening during pilot expansion
- **P2**: scale and enterprise rollout

---

## 2. Product vision

HangyBot should not be framed as “a robot that sells food.” It is a **disruption-aware airport food intelligence platform** with two delivery modes:

- **high-volume terminal recovery** for stranded commercial passengers
- **high-touch concierge catering** for private aviation

The company’s moat is the combination of:

- operational disruption intelligence
- demand forecasting by traveler cohort
- grounded AI assistance for support and operations
- robot-assisted fulfillment where it is safe and useful
- reusable architecture patterns that can scale from one terminal zone and one FBO to a broader airport network

---

## 3. Business goals

### Primary goals
- Capture more food revenue during delays, cancellations, closures, and diversions.
- Reduce stockouts and wasted prep during irregular operations.
- Give airport, concession, and FBO staff earlier visibility into demand spikes.
- Deliver better passenger and crew experiences with clear ETAs, dietary labeling, and fast service recovery.
- Prove that one shared platform can support both ATL terminal recovery and PDK FBO catering.

### Target outcomes for the pilot
- measurable uplift in disruption-window food conversion
- lower waste than manual overproduction
- lower stockout rate during surge windows
- faster support resolution times
- safe, reliable robot-assisted delivery in the ATL pilot zone
- stronger attach rate and order accuracy for PDK FBO bundles

### Design constraints
- ATL and PDK are the only live airports in v1.
- BOS, TPA, and SJU are feeder/reference airports, not live deployment sites.
- Public data may support cohort prediction but not sensitive individual inference.
- Any high-risk operational action must support human override.
- Generative AI must be grounded, audited, and resilient to service degradation.

---

## 4. Scope

### In scope
- ATL terminal pilot zone with robot-assisted and fallback fulfillment
- PDK FBO concierge workflow with optional lobby-side robot support
- feeder/reference modeling using BOS, TPA, and SJU
- local PiAware/FlightAware visibility around ATL and PDK
- disruption prediction, meal-mix forecasting, and ETA prediction
- passenger ordering surfaces and FBO desk console
- support copilot, ops copilot, and grounded internal knowledge search
- AWS-based data, ML, FM, retrieval, and observability platform
- CI/CD, evaluation, governance, and standardized internal agent tooling

### Out of scope
- live local sensing at BOS, TPA, or SJU
- airport-wide autonomous robot deployment
- autonomous airside/ramp delivery at PDK
- individual profiling from public flight or origin data alone
- unsupported fully autonomous refunds, safety overrides, or policy exceptions
- broad multi-airport expansion before ATL/PDK pilot success

---

## 5. Personas

### External personas

**Marcus — Stranded business traveler at ATL**  
Wants fast, healthy, low-friction options and trustworthy ETA updates.

**Nina — Leisure/family traveler at ATL**  
Wants familiar food, kid-friendly bundles, value pricing, and simple pickup/delivery instructions.

**Dana — ATL concessions manager**  
Needs demand alerts, prep quantities, staffing guidance, waste reduction, and visibility into what the system is recommending and why.

**Nate — PDK FBO desk agent**  
Needs rapid catering recommendations, clear order status, premium bundle templates, and easy exception handling.

**Elena — Executive assistant / charter coordinator**  
Wants reliable, premium, low-back-and-forth catering workflows for crew and passengers.

**Avery — Airport operations stakeholder**  
Needs confidence that HangyBot can operate safely, respect airport rules, and help reduce passenger frustration during irregular operations.

### Internal personas

**Alex — CTO**  
Owns architecture, integration patterns, FM strategy, deployment strategy, and standardization.

**Emma — Data Scientist**  
Owns data quality, feature engineering, forecasting, evaluation, and retraining.

**Liam — Robotics Engineer**  
Owns navigation, fleet coordination, charging, and robot safety.

**Sophia — Operations Manager**  
Owns inventory, kitchen timing, partner coordination, and service recovery.

**Ryan — Customer Support Specialist**  
Owns support flows, escalation handling, FAQ/chatbot performance, and feedback loops.

**Jordan — ML Platform Engineer**  
Owns feature store, pipelines, model registry, endpoint lifecycle, rollback, and monitoring.

**Priya — Security, Privacy, and Responsible AI Lead**  
Owns least-privilege access, PII protection, auditability, guardrails, policy checks, fairness evaluation, and regulatory readiness.

**Maya — Product and Partnerships Lead**  
Owns rollout priorities, airport/FBO partner needs, business value validation, and roadmap sequencing.

---

## 6. Use cases

### P0 launch use cases

**UC-01: ATL disruption surge prediction**  
Sophia receives a 30-minute, 2-hour, and 6-hour forecast for likely stranded demand in the ATL pilot zone, with meal-category recommendations and explainable drivers.

**UC-02: ATL smart meal staging**  
Dana receives recommended prep quantities by menu archetype such as breakfast grab-and-go, comfort meal, healthy bowl, kid bundle, and late-night shelf-stable pack.

**UC-03: ATL robot-assisted fulfillment**  
Passengers order via mobile web/app/QR, receive ETA and dietary labels, and get delivery by robot where allowed or fallback to pickup/human runner when capacity or safety requires it.

**UC-04: PDK concierge catering recommendation**  
Nate sees likely catering needs for inbound or delayed private flights and can confirm, edit, or reject a suggested premium bundle.

**UC-05: PDK diversion and late-notice recovery**  
When a private flight or crew operation changes suddenly, HangyBot proposes rapid-response bundles, staff handoff steps, and ETA.

**UC-06: Support copilot for Ryan**  
Ryan sees a grounded summary of the order, robot state, disruption context, policy guidance, and recommended recovery steps, with clear escalation paths.

**UC-07: Ops copilot for Sophia and Dana**  
An internal assistant answers questions such as “Why is ATL demand spiking?” or “What is the confidence behind this prep recommendation?” using grounded retrieval over operations data, SOPs, and recent events.

### P1 pilot hardening use cases

**UC-08: Multilingual passenger assistant**  
Passengers can ask about availability, allergens, ETA, and pickup instructions in multiple languages.

**UC-09: Voice and document ingestion**  
Support calls, ops voice notes, FBO requests, menus, SOPs, and incident docs are ingested for search, classification, and grounded assistance.

**UC-10: Cross-airport feeder analysis**  
Emma compares how BOS, TPA, and SJU inbound patterns affect ATL meal-mix forecasts and updates cohort models.

**UC-11: Dynamic model routing and failover**  
The FM gateway routes different requests to different models based on latency, cost, capability, and policy rules, with no client code changes.

**UC-12: Human-in-the-loop policy workflows**  
High-value refunds, policy exceptions, low-confidence recommendations, and safety-sensitive actions require explicit review and handoff.

### P2 scale use cases

**UC-13: Network rollout kit**  
A standardized deployment package lets HangyBot replicate the stack to new airports or FBOs with minimal custom engineering.

**UC-14: Multi-agent operational research assistant**  
A coordinator agent decomposes partner, policy, and incident-analysis tasks across specialized subagents and returns a cited synthesis.

**UC-15: Edge and jurisdiction-aware deployment**  
For airports with residency or latency constraints, parts of the stack can run in alternate regions or edge/on-prem environments.

---

## 7. Product requirements

### 7.1 User experience and workflows

**UX-01 [P0]**  
ATL passengers shall be able to order through mobile web, app, kiosk, or QR-linked surfaces.

**UX-02 [P0]**  
PDK desk agents shall be able to create, edit, approve, and monitor orders through an FBO console.

**UX-03 [P0]**  
All user-facing order views shall show ETA, dietary labels, order status, and handoff instructions.

**UX-04 [P1]**  
Passenger-facing AI assistance shall support multilingual responses, grounded answers, and escalation when confidence is low.

**UX-05 [P1]**  
The product shall expose OpenAPI-described APIs for partner systems and use API-first patterns to support future custom clients, including web, mobile, internal tools, and airport/FBO integrations.

### 7.2 Data platform requirements

**DP-01 [P0]**  
HangyBot shall ingest validated and non-validated data from public feeds, PiAware/FlightAware, POS systems, inventory systems, robot telemetry, support events, and document repositories. Supported formats shall include JSON, CSV, Apache Parquet, Apache ORC, Apache Avro, and RecordIO.

**DP-02 [P0]**  
The storage design shall separate:
- raw landing and historical replay data in Amazon S3
- low-latency transactional state in Amazon RDS and Amazon DynamoDB
- shared training and high-throughput file access in Amazon EFS or Amazon FSx for NetApp ONTAP
- high-performance training scratch space on Amazon EBS where Provisioned IOPS is justified

Curated analytical data should favor Parquet or ORC. JSON and Avro should be used for event payloads and service contracts. CSV is permitted mainly for partner exchange and manual backfills.

**DP-03 [P0]**  
Streaming ingestion shall support Amazon Kinesis, Apache Kafka, and Apache Flink-based processing, plus webhooks through Amazon API Gateway and AWS Lambda, with Amazon EventBridge for event fan-out where loose coupling is preferred.

**DP-04 [P0]**  
Data extraction and movement must support S3 Transfer Acceleration for large partner uploads where useful and efficient extraction paths from S3, EBS, EFS, RDS, and DynamoDB based on latency and cost needs.

**DP-05 [P0]**  
Data quality shall be enforced through AWS Glue Data Quality, SageMaker Data Wrangler, AWS Glue, AWS Glue DataBrew, custom Lambda validators, and CloudWatch metrics. Invalid records must be quarantined rather than silently dropped.

**DP-06 [P0]**  
Feature engineering shall support imputation, outlier treatment, deduplication, normalization, scaling, binning, log transforms, splitting, and encoding strategies such as one-hot encoding, binary encoding, label encoding, and tokenization. Features shall be versioned in SageMaker Feature Store.

**DP-07 [P1]**  
Multimodal processing shall support:
- tabular data for weather, flights, orders, and inventory
- text for SOPs, menus, support tickets, and policy docs
- audio for calls or voice notes through AWS Transcribe
- image workflows for approved operational use cases such as menu boards, packaging QA, or non-identifying visual inspection, using multimodal FMs or services such as Amazon Rekognition where appropriate

**DP-08 [P1]**  
Labeling workflows shall use SageMaker Ground Truth and, where applicable, Amazon Mechanical Turk or partner labeling teams for demand-class labels, support intent labels, incident categorization, or evaluation sets.

**DP-09 [P0]**  
Data privacy and bias controls shall include encryption at rest and in transit, PII classification, masking, anonymization, and tagging for data residency. Amazon Comprehend and Amazon Macie shall be used where helpful to detect and redact sensitive information.

**DP-10 [P1]**  
Bias assessment must consider class imbalance, difference in proportions of labels, selection bias, and measurement bias. SageMaker Clarify shall be used for pre-training and post-training checks where applicable.

### 7.3 Classical ML requirements

**ML-01 [P0]**  
HangyBot shall use classical ML first for:
- disruption probability
- stranded-demand forecasting
- dwell-time estimation
- meal-mix optimization
- robot ETA and dispatch quality
- support classification and routing

Initial baselines should prioritize interpretability where possible. More complex models should be introduced only when they materially improve business outcomes.

**ML-02 [P0]**  
Model development shall support SageMaker AI built-in algorithms, SageMaker JumpStart templates, and script mode with PyTorch, TensorFlow, XGBoost, or other supported frameworks. External models must be integrable into SageMaker AI when they outperform native options.

**ML-03 [P0]**  
Training workflows shall explicitly manage epochs, steps, batch size, early stopping, distributed training, regularization techniques such as dropout and weight decay, and hyperparameter optimization through random search, Bayesian optimization, or SageMaker Automatic Model Tuning.

**ML-04 [P1]**  
The platform shall support ensembles, stacking, boosting, feature pruning, model compression, and edge optimization using SageMaker Neo where robot-side or edge deployment becomes relevant.

**ML-05 [P0]**  
All trained models shall be versioned in SageMaker Model Registry with repeatable experiments, model cards, lineage, approval status, and rollback-ready artifacts.

**ML-06 [P0]**  
Evaluation shall include model-appropriate metrics such as RMSE, MAE, MAPE, F1, precision, recall, ROC-AUC, confusion matrices, calibration, and business lift versus baseline. Convergence and overfitting issues shall be investigated with SageMaker Model Debugger and related tooling.

**ML-07 [P1]**  
Production ML monitoring shall include drift detection, shadow variants, A/B tests, data distribution monitoring, and retraining triggers through SageMaker Model Monitor, Clarify, EventBridge, and pipeline automation.

### 7.4 Foundation model and GenAI requirements

**FM-01 [P0]**  
HangyBot shall use foundation models for grounded copilots, document analysis, multilingual assistance, query rewriting, support summarization, retrieval augmentation, and complex workflow orchestration. FMs are not the primary mechanism for core demand forecasting; they augment operational intelligence and user interaction.

**FM-02 [P0]**  
A model evaluation framework shall score candidate FMs on:
- task fit
- tool-use reliability
- retrieval grounding performance
- latency
- streaming support
- multimodal support
- token efficiency
- cost per successful task
- regional availability
- safety and guardrail compatibility
- fine-tuning or adaptation support

Selection should use benchmark tasks, business-specific eval sets, limitation analysis, and canary/shadow testing before broad rollout.

**FM-03 [P0]**  
All FM access shall go through a **HangyBot GenAI Gateway** built behind Amazon API Gateway, using Lambda or containerized services for request normalization and AppConfig for dynamic routing. This gateway shall provide:
- provider abstraction
- model selection without client code changes
- request validation
- structured output schemas
- token estimation and tracking
- semantic caching
- retry and exponential backoff
- rate limiting
- timeout handling
- streaming response support
- policy enforcement
- observability hooks

**FM-04 [P1]**  
Routing logic shall support static policies and dynamic content-based routing, including use of smaller models for routine tasks, larger models for complex tasks, and specialist models for multimodal or tool-heavy workflows. Step Functions may coordinate multi-step routing decisions when simple request transforms are insufficient.

**FM-05 [P0]**  
Prompt management shall be standardized through Amazon Bedrock Prompt Management, shared template repositories in Amazon S3 or source control, approval workflows, usage logging, and version comparison. Prompt quality must be tested continuously, not ad hoc.

**FM-06 [P1]**  
Complex prompt systems shall support reusable components, pre-processing, conditional branching, integrated tool calls, and post-processing using Amazon Bedrock Prompt Flows or equivalent orchestration.

**FM-07 [P0]**  
Input preparation for FMs shall normalize text, structure tabular context, and format requests according to model-specific requirements. This may include JSON payload shaping for Bedrock APIs, schema-constrained outputs, entity extraction with Amazon Comprehend, and normalization Lambda functions.

**FM-08 [P1]**  
HangyBot shall support FM customization and lifecycle management through domain-specific fine-tuning, low-rank adaptation, adapters, versioned deployment artifacts, approval workflows, rollback strategies, and retirement policies using SageMaker AI and Model Registry when the business case justifies it.

**FM-09 [P1]**  
For latency-sensitive or capacity-sensitive workloads, the platform shall support Lambda-based on-demand invocation, Amazon Bedrock provisioned throughput, SageMaker endpoints, and batch or asynchronous patterns as appropriate.

**FM-10 [P0]**  
The GenAI platform shall degrade gracefully during outages or rate pressure through:
- circuit breaker patterns in Step Functions
- cross-Region inference for models with limited availability
- fallback to alternate models or regions
- fallback to deterministic templates or retrieval-only mode
- human handoff where needed

### 7.5 Retrieval, vector search, and grounding requirements

**RAG-01 [P0]**  
HangyBot shall maintain grounded knowledge stores for SOPs, menus, airport rules, partner docs, runbooks, support articles, and incident history.

**RAG-02 [P0]**  
Vector architecture shall support:
- Amazon Bedrock Knowledge Bases for managed grounding where appropriate
- Amazon OpenSearch Service with vector capabilities for high-scale semantic search
- Amazon Aurora or Amazon RDS with pgvector where relational coupling is beneficial
- S3 as the document repository of record
- DynamoDB or relational metadata stores for fast document and session metadata lookups

**RAG-03 [P0]**  
All knowledge assets shall carry a metadata framework covering timestamps, document type, author/source, domain classification, airport/FBO relevance, policy status, and sensitivity tags. Metadata must survive chunking and retrieval.

**RAG-04 [P1]**  
Document segmentation shall support fixed-size, semantic, and hierarchical chunking. Chunking strategies may use Bedrock chunking support, Lambda preprocessors, or custom structure-aware chunkers. Large documents must preserve section hierarchy to reduce “lost in the middle” failures.

**RAG-05 [P1]**  
Embedding selection shall consider dimensionality, retrieval quality, latency, domain fit, and cost. The platform shall benchmark candidate embedding models and support batch generation and refresh pipelines.

**RAG-06 [P0]**  
Search shall support hybrid retrieval using keyword + vector search, reranking, metadata filtering, and topic-based segmentation to improve precision.

**RAG-07 [P1]**  
Advanced query handling shall support query expansion, decomposition, transformation, and intent-aware routing through Bedrock, Lambda, and Step Functions.

**RAG-08 [P0]**  
Vector stores must have maintenance pipelines for incremental updates, scheduled refresh, change detection, re-indexing, and staleness monitoring.

**RAG-09 [P0]**  
Grounded answers must preserve claim-source mappings, dates, and conflict annotations. Conflicting values from credible sources must be surfaced, not silently collapsed.

### 7.6 Agentic workflow requirements

**AG-01 [P0]**  
HangyBot shall support agentic workflows for support, ops research, document synthesis, and developer productivity, but not for unrestricted autonomous operations.

**AG-02 [P0]**  
Where Anthropic Claude-family models are used, the runtime shall implement the correct agentic loop lifecycle: inspect `stop_reason`, continue on `tool_use`, terminate on `end_turn`, execute requested tools, append tool results back into the conversation history, and let the model decide the next action based on updated context.

**AG-03 [P0]**  
The platform shall prefer model-driven decision-making for open-ended tasks and fixed prompt chains for predictable sequential workflows. It shall avoid anti-patterns such as parsing natural-language completion hints, using arbitrary iteration caps as the main stopping mechanism, or inferring completion from assistant prose.

**AG-04 [P1]**  
Complex investigations shall use a hub-and-spoke pattern. A coordinator agent decomposes work, routes it to subagents, aggregates results, identifies coverage gaps, and decides whether to re-run targeted subagents. Subagents operate in isolated context and do not inherit parent history automatically.

**AG-05 [P1]**  
Any coordinator that needs subagents shall have `Task` in its allowed tools. Subagent prompts must include the required context explicitly, including structured facts, source attributions, and quality criteria.

**AG-06 [P1]**  
The coordinator shall dynamically select which subagents to invoke rather than always routing through a full pipeline. Research scope should be partitioned to reduce duplication and allow iterative refinement loops.

**AG-07 [P0]**  
High-risk actions such as large refunds, policy exceptions, robot safety overrides, or partner-notification workflows shall use deterministic gates and hooks rather than prompt instructions alone.

**AG-08 [P1]**  
Post-tool and pre-tool hooks shall normalize heterogeneous data, enforce business rules, block policy-violating actions, and redirect to escalation workflows where needed.

**AG-09 [P1]**  
Tool integrations shall use standardized schemas, error handling, parameter validation, and structured error metadata including category, retryability, attempted action, partial results, and customer-friendly messages.

**AG-10 [P1]**  
Agent memory and state shall use explicit conversation history, structured “case facts” blocks, session state in DynamoDB or equivalent stores, and scratchpad artifacts for longer workflows. Summaries must preserve dates, amounts, statuses, and source mappings to avoid context degradation.

### 7.7 Robotics and fulfillment requirements

**RB-01 [P0]**  
ATL robot operations shall remain geofenced to approved terminal zones. No unrestricted terminal-wide roaming is included in v1.

**RB-02 [P0]**  
Liam’s fleet layer shall support pathfinding, obstacle avoidance, charge-state awareness, task assignment, collision prevention, and safe fallback to human intervention.

**RB-03 [P0]**  
PDK fulfillment shall default to concierge and desk-assisted handoff. Robot support, if used, shall be limited to lobby-adjacent or approved indoor zones.

**RB-04 [P0]**  
The system shall recommend human-runner mode or pickup conversion when robot availability, battery, route congestion, or safety conditions degrade.

**RB-05 [P1]**  
The dispatch service shall integrate predicted demand, order priority, congestion, charge levels, and kitchen readiness to optimize assignment quality and ETA.

### 7.8 Security, privacy, compliance, and responsible AI

**SEC-01 [P0]**  
All workloads shall use least-privilege IAM roles, resource policies, network isolation with VPCs, subnets, security groups, and private connectivity such as VPC endpoints where supported.

**SEC-02 [P0]**  
Sensitive data access shall be protected through encryption, KMS-backed key management, bucket policies, Lake Formation data permissions where relevant, SageMaker security controls, and role-based access to models and data.

**SEC-03 [P0]**  
Content safety shall use a defense-in-depth model with input sanitization, prompt injection detection, guardrails, post-generation validation, and policy filters. Harmful input and harmful output protections shall be handled separately.

**SEC-04 [P0]**  
PII and sensitive data must be minimized, masked, or redacted before FM consumption when not strictly required. Amazon Comprehend PII detection, Macie, retention policies, and S3 lifecycle controls shall support this.

**SEC-05 [P1]**  
Programmatic model cards, Glue-based lineage, decision logs, CloudTrail, and source tagging shall support auditability and compliance readiness.

**SEC-06 [P1]**  
Responsible AI shall include fairness evaluation, policy compliance checks, output attribution, user-facing explanation of grounded evidence, and escalation for ambiguous or unsupported cases.

**SEC-07 [P2]**  
Where jurisdictional or edge constraints emerge, HangyBot shall support cross-environment patterns using AWS Outposts, AWS Wavelength, or secure hybrid routing.

### 7.9 Observability, evaluation, and FinOps

**OBS-01 [P0]**  
HangyBot shall collect operational, business, and model metrics end to end using CloudWatch, logs, traces, and business dashboards.

**OBS-02 [P0]**  
FM observability shall include prompt/version identifiers, token usage, latency, response quality metrics, retrieval traces, tool-call traces, and failure categories. Model invocation logs should be retained according to policy.

**OBS-03 [P0]**  
Evaluation shall cover:
- classical ML accuracy and calibration
- retrieval relevance and latency
- FM groundedness, factuality, consistency, fluency, and safety
- task completion and tool effectiveness for agents
- robot mission success and ETA quality
- support outcomes and escalation quality
- business KPIs such as conversion, waste, and stockouts

**OBS-04 [P1]**  
Quality systems shall use golden datasets, automated regression tests, human review sets, LLM-as-a-judge style evaluation where useful, stratified random sampling, and field-level confidence thresholds.

**OBS-05 [P1]**  
Cost controls shall include tagging, budgets, cost allocation, anomaly detection, capacity planning, inference recommender analysis, compute rightsizing, purchase-option selection, semantic caching, token controls, and prompt compression.

**OBS-06 [P1]**  
Vector stores, tools, and agent workflows shall have their own operational metrics, usage baselines, performance dashboards, and anomaly detection.

### 7.10 Developer experience, CI/CD, and internal tooling

**DX-01 [P0]**  
Infrastructure shall be defined with CloudFormation or AWS CDK. CI/CD shall use CodePipeline, CodeBuild, CodeDeploy, SageMaker Pipelines, and EventBridge-driven retraining or deployment triggers as appropriate.

**DX-02 [P0]**  
Deployment strategies shall support blue/green, canary, linear rollout, rollback, shadow variants, and synthetic workflow validation before promotion.

**DX-03 [P0]**  
ML and FM workloads shall support the appropriate serving mode: real-time, asynchronous, serverless, or batch. Compute selection shall consider CPU/GPU profile, network bandwidth, latency targets, and cost. Multi-model, multi-container, ECS, EKS, Lambda, and SageMaker endpoint targets shall all be allowed where justified.

**DX-04 [P1]**  
Claude Code and internal AI-assisted development standards shall be formalized through project-level `CLAUDE.md`, path-scoped `.claude/rules/`, project commands, project skills, and MCP server definitions.

**DX-05 [P1]**  
Repository tooling shall use:
- Grep for code/content search
- Glob for file pattern discovery
- Read/Write for whole-file operations
- Edit for unique-anchor changes, with Read+Write fallback when anchors are not unique

**DX-06 [P1]**  
Complex refactors shall default to plan mode, while simple, well-understood changes may use direct execution. Verbose discovery work should be isolated through forked subagents or Explore-style patterns.

**DX-07 [P1]**  
CI-based agent review shall use non-interactive execution, structured JSON output, explicit review criteria, independent review sessions, and regression-aware re-runs. The same generation session should not be relied on as the primary reviewer of its own code.

**DX-08 [P1]**  
Project and user scoped MCP servers shall be supported, with environment-variable expansion for credentials, strong tool descriptions, scoped tool access, and resource catalogs to reduce exploratory calls.

**DX-09 [P1]**  
Internal agent workflows shall support session resumption, forked branches for divergent analysis, scratchpad files, context compaction, and explicit notices when previously analyzed files changed.

---

## 8. Reference architecture

```text
[Operational Sources]
  Weather | Airport Status | FAA/Flight Feeds | PiAware (ATL/PDK)
  POS | Inventory | Orders | Support Tickets | SOPs/Menus/Policies
  Audio Notes | Robot Telemetry | Partner Docs

            |
            v

[Ingestion + Integration Layer]
  API Gateway | Lambda | EventBridge
  Kinesis / Kafka / Flink
  Batch loads to S3 | partner webhooks | scheduled jobs

            |
            v

[Data + Storage Layer]
  S3 raw / curated / document repos
  Glue Catalog + Glue Data Quality + DataBrew
  EMR/Spark / SageMaker Data Wrangler
  RDS + DynamoDB for ops state
  EFS / FSx / EBS for training and shared workloads
  SageMaker Feature Store

            |
            v

[Intelligence Layer]
  Classical ML on SageMaker AI
  GenAI Gateway (API Gateway + Lambda/ECS + AppConfig)
  Amazon Bedrock + Prompt Management + Guardrails + Prompt Flows
  OpenSearch / Aurora pgvector / Bedrock Knowledge Bases
  Step Functions orchestration
  Agent coordinator + subagents
  Semantic cache + policy engine + human approval gates

            |
            v

[Experience Layer]
  Passenger ordering app
  PDK FBO console
  ATL ops dashboard
  Support copilot
  Partner analytics
  Robot dispatch + runner fallback service

            |
            v

[Cross-Cutting Controls]
  IAM | VPC | KMS | Lake Formation | Macie | Comprehend PII
  CloudWatch | X-Ray | CloudTrail | QuickSight | Cost controls
  Model Registry | Model Monitor | Clarify | audit logs
```

### Core architecture patterns
- event-driven ingestion for operational feeds
- lakehouse storage for historical analytics and replay
- feature-store backed classical ML for forecasts and ETA
- FM gateway abstraction for provider/model switching
- RAG for grounded assistance
- coordinator/subagent orchestration for complex internal tasks
- human-in-the-loop gates for policy and safety
- progressive degradation when models or tools are unavailable

---

## 9. Standardized technical components

To make the system repeatable across ATL, PDK, and future deployments, HangyBot shall define a reusable platform kit:

**1. Source Adapter Template**  
Normalizes feed ingestion, schema, retries, and replay.

**2. Data Quality Pack**  
Shared validation rules, quarantine patterns, CloudWatch alerts, and lineage tags.

**3. Feature Pipeline Template**  
Reusable transformations, feature naming, and Feature Store registration.

**4. Forecast Service Template**  
Standard training, registry, deployment, and rollback pattern for classical ML models.

**5. GenAI Gateway**  
Stable FM API, routing policies, caching, rate limiting, safety enforcement, and model abstraction.

**6. Retrieval Service**  
Standard document chunking, metadata tagging, embeddings, indexing, hybrid search, and claim-source mapping.

**7. Agent Orchestration Pack**  
Coordinator/subagent definitions, task routing, hook patterns, and structured handoff protocols.

**8. Guardrail and Policy Pack**  
Input/output moderation, policy checks, human approval thresholds, and escalation standards.

**9. Observability Pack**  
Dashboards, traces, model metrics, retrieval metrics, tool metrics, business KPIs, and cost views.

**10. Deployment Template**  
CDK/CloudFormation stacks, environment bootstrapping, security defaults, CI/CD stages, and rollback playbooks.

Every major workload should also pass a Well-Architected style review and a GenAI-specific readiness review before promotion.

---

## 10. Proof-of-concept plan

### POC-1: Data fusion and freshness
**Hypothesis:** Combining public disruption feeds, PiAware local telemetry, and order data produces useful short-horizon features for ATL and PDK.  
**Build:** Ingest weather, airport events, PiAware data, order history, and inventory into the lakehouse and Feature Store.  
**Exit criteria:** Reliable freshness, schema stability, replay capability, and data quality scores sufficient for modeling.

### POC-2: ATL demand forecast
**Hypothesis:** BOS, TPA, and SJU feeder context improves ATL meal-mix and surge prediction beyond daypart-only baselines.  
**Build:** Train baseline and enhanced models using historical operational and order data.  
**Exit criteria:** Clear lift over baseline in forecast quality and actionability for prep decisions.

### POC-3: PDK concierge recommendation
**Hypothesis:** AI-generated bundle recommendations reduce response time and increase attach rate for FBO orders.  
**Build:** Desk-facing workflow with bundle templates, approval/editing, and ETA estimates.  
**Exit criteria:** Faster order handling and acceptable partner satisfaction.

### POC-4: Grounded support/ops copilot
**Hypothesis:** RAG-backed copilots reduce handle time and improve operational clarity.  
**Build:** Knowledge base over SOPs, menus, policies, incident docs, and recent operational signals.  
**Exit criteria:** High citation rate, low hallucination rate, acceptable latency, and better resolution outcomes.

### POC-5: FM gateway and failover
**Hypothesis:** A routing layer can switch models/providers/regions without client changes and keep service running during partial outages.  
**Build:** AppConfig-driven gateway with fallback models and circuit breaker flow.  
**Exit criteria:** Successful failover, stable latency, policy compliance, and meaningful cost controls.

### POC-6: ATL robot dispatch
**Hypothesis:** Geofenced robot delivery plus fallback logic outperforms human-only fulfillment in specific pilot-zone scenarios.  
**Build:** Dispatch integration with orders, kitchen readiness, congestion, and battery state.  
**Exit criteria:** High completion rate, acceptable ETA error, safe intervention behavior.

---

## 11. Success metrics

### Business
- disruption-window revenue capture uplift
- stockout reduction
- waste reduction
- FBO attach rate and repeat usage
- support cost per order or per issue

### Operational
- forecast freshness
- kitchen prep lead time
- order-to-handoff time
- late-night or overnight recovery coverage
- robot mission completion and fallback rate

### ML
- surge detection precision/recall
- demand forecast error
- ETA error
- support-routing F1
- drift and retrain intervals

### FM / RAG / Agentic
- grounded answer citation rate
- hallucination rate
- retrieval relevance
- task completion rate
- tool success rate
- escalation quality
- harmful input/output catch rate
- token cost per successful task

### Governance
- data-quality pass rate
- audit coverage
- PII leakage rate
- policy violation rate
- fairness monitoring status by major cohort

---

## 12. Rollout plan

### Phase 0: Foundation
Data platform, source adapters, raw/curated storage, Feature Store, dashboards, basic SOP knowledge base, FM gateway skeleton, security baseline.

### Phase 1: Shadow mode
Run prediction and copilot workloads without controlling live operations. Measure data quality, drift, and recommendation quality.

### Phase 2: Assisted operations
Sophia and Dana use recommendations for prep and staffing. Support copilot assists Ryan. Human delivery remains primary.

### Phase 3: ATL robot-assisted pilot
Enable geofenced robot delivery in the ATL pilot zone with manual fallback.

### Phase 4: PDK FBO operationalization
Enable desk workflow, premium bundle templates, and optional lobby-side robot assistance.

### Phase 5: Scale decision
Promote proven standardized components to a network rollout kit. Consider whether BOS, TPA, SJU, or another airport becomes the next live site.

---

## 13. Risks and mitigations

**Risk: Overpromising personalization**  
Mitigation: Keep v1 centered on cohort-level demand and explicit user preferences.

**Risk: Weak grounding or hallucinations**  
Mitigation: RAG, source attribution, JSON schemas, validation, confidence thresholds, and human escalation.

**Risk: Data quality instability**  
Mitigation: Glue Data Quality, quarantine, replayable pipelines, shadow-mode validation.

**Risk: Agentic workflow brittleness**  
Mitigation: deterministic hooks for risky actions, structured error handling, small tool sets, and clear escalation.

**Risk: Robot failures or congestion**  
Mitigation: geofencing, central coordination, charge-aware dispatch, human fallback.

**Risk: Model/provider lock-in**  
Mitigation: gateway abstraction, AppConfig routing, standardized adapters, model evaluation harness.

**Risk: Cost sprawl**  
Mitigation: tagging, budgets, semantic caching, token controls, right-sized endpoints, and provisioned capacity only where justified.

**Risk: Compliance exposure**  
Mitigation: PII masking, least privilege, audit logs, model cards, source lineage, and policy gates.

---

## Appendix A — AWS implementation mapping

This appendix translates the PRD into an AWS-heavy reference stack.

### A1. Data ingestion, formats, and storage
- Use **Amazon S3** for raw, curated, replay, and document storage.
- Use **Amazon EFS** or **Amazon FSx for NetApp ONTAP** for shared training or file-based workloads that need POSIX semantics.
- Use **Amazon EBS** with appropriate IOPS profiles for high-throughput temporary training or inference workloads when local block performance matters.
- Use **Amazon RDS** for relational operational state and **Amazon DynamoDB** for low-latency state, session memory, and metadata.
- Use **Parquet** or **ORC** for curated analytics, **JSON** or **Avro** for operational contracts, **CSV** for exchange/manual loads, and **RecordIO** for certain optimized ML training paths.
- Use **Amazon Kinesis**, **Apache Kafka**, or **Apache Flink** for streaming ingestion. Use **Lambda**, **Glue**, **EMR/Spark**, **DataBrew**, and **SageMaker Data Wrangler** for transformation and enrichment.

### A2. Data prep, labeling, privacy, and bias
- Use **AWS Glue Data Quality** and custom checks for validation.
- Use **SageMaker Data Wrangler** and **DataBrew** for profiling, cleaning, dedupe, outlier handling, and transformation.
- Use **SageMaker Feature Store** for reusable online/offline features.
- Use **SageMaker Ground Truth** and **Amazon Mechanical Turk** where labeling is needed.
- Use **SageMaker Clarify** for bias and explainability analysis.
- Use **Amazon Comprehend**, **Amazon Macie**, encryption, masking, and retention policies for privacy protection.

### A3. Classical ML lifecycle
- Start with **SageMaker AI built-in algorithms** or script-mode training using **PyTorch**, **TensorFlow**, and tree-based methods.
- Use **SageMaker JumpStart** where templates accelerate prototyping.
- Use **SageMaker Automatic Model Tuning**, **Model Registry**, **Model Monitor**, **Clarify**, **Model Debugger**, and **Inference Recommender**.
- Deploy through **real-time**, **async**, **batch**, **serverless**, or **multi-model** endpoints based on workload shape.
- Use **SageMaker Neo** when edge optimization becomes useful for robot-adjacent models.

### A4. GenAI, grounding, and orchestration
- Use **Amazon Bedrock** for FM access, evaluation, knowledge bases, guardrails, prompt management, streaming, and prompt flows.
- Use **Amazon API Gateway** + **Lambda** + **AppConfig** for a model-routing gateway.
- Use **Step Functions** for complex orchestration, circuit breakers, human approval, and safe failover.
- Use **OpenSearch Service**, **Aurora pgvector**, or **Bedrock Knowledge Bases** for retrieval.
- Use **AWS Strands Agents**, **AWS Agent Squad**, or custom Step Functions/Lambda orchestration where multi-agent workflows are justified.
- Use **Amazon Transcribe**, **Translate**, **Comprehend**, **Rekognition**, and multimodal models for specialized AI tasks.
- Use **Amazon Q Developer** for internal developer productivity and **Amazon Q Business** data sources for internal knowledge tooling where helpful.

### A5. Deployment, resilience, and security
- Use **CloudFormation** or **AWS CDK** for IaC.
- Use **CodePipeline**, **CodeBuild**, **CodeDeploy**, **SageMaker Pipelines**, and **EventBridge** for CI/CD, retraining, and deployment triggers.
- Use **blue/green**, **canary**, and **shadow** rollout patterns.
- Use **VPC endpoints**, private subnets, IAM least privilege, KMS, Lake Formation, and CloudTrail for secure operation.
- Use **Bedrock Cross-Region Inference**, cross-region deployment patterns, retries, and fallback models for resilience.
- Use **Outposts** or **Wavelength** only when data residency or ultra-low-latency edge deployment becomes a real constraint.

### A6. Observability and cost
- Use **CloudWatch**, **Logs Insights**, **X-Ray**, **CloudTrail**, and **QuickSight** for operational and business visibility.
- Track token use, latency, retrieval metrics, tool-call performance, cost anomalies, and business impact.
- Use **AWS Cost Explorer**, **Trusted Advisor**, **Compute Optimizer**, **Budgets**, and purchase-option planning for FinOps.

---

## Appendix B — Internal agent and Claude-style development standards

These are internal platform standards for HangyBot Engineering and Operations. They are not end-user features, but they materially affect delivery quality, auditability, and speed.

### B1. Agent loop control
- Coordinator agents using Claude-style tool use must inspect `stop_reason` and continue only when it equals `tool_use`; they terminate only on `end_turn`.
- Tool results must be appended to conversation history so the model can reason about what happened next.
- Do not infer completion from free-form assistant text.
- Do not rely on arbitrary iteration caps as the main stop condition.
- Use fixed prompt chains only for predictable workflows; use adaptive decomposition for open-ended work.

### B2. Coordinator / subagent pattern
- Use a hub-and-spoke architecture.
- The coordinator owns task decomposition, routing, error handling, aggregation, and gap detection.
- Subagents do not inherit the parent context automatically. Required context must be passed explicitly.
- Any coordinator that needs subagents must have `Task` in its allowed tools.
- When possible, spawn parallel subagents in a single turn.
- Partition work by subtopic or source type to reduce duplication.
- Require subagents to return structured findings with claims, sources, dates, and coverage notes.

### B3. Deterministic gates and hooks
- Use programmatic prerequisite gates for actions that must not happen out of order.
- Use tool interception hooks to block policy-violating actions and redirect to human escalation.
- Use post-tool hooks to normalize timestamps, status codes, amounts, and other heterogeneous outputs before the model reasons over them.
- Prefer hooks over prompts when compliance must be guaranteed.

### B4. Tool design and error handling
- Keep tool sets small; too many tools degrade selection quality.
- Give each subagent only the tools it needs.
- Tool descriptions must clearly state purpose, input format, output format, example usage, and boundary conditions.
- Avoid overlapping tool names and vague descriptions.
- Use `tool_choice: "any"` when a tool must be called but the model can choose which one.
- Force a named tool when the workflow requires a specific first step.
- Return structured tool errors with category, retryability, attempted action, partial results, and human-readable remediation.

### B5. MCP standards
- Use project-scoped `.mcp.json` for shared team servers and user-scoped config for personal/experimental servers.
- Use environment-variable expansion for secrets.
- Provide rich MCP tool descriptions so agents do not default to weaker built-in tools.
- Expose MCP resources as content catalogs when possible so agents can see available datasets, docs, or schemas before searching.
- Route complex MCP tool interactions through the coordinator for observability.

### B6. Repo standards for Claude-assisted development
- Use project-level `CLAUDE.md` plus path-scoped `.claude/rules/` files instead of burying important instructions in user-only config.
- Use `@import` to keep repo guidance modular.
- Store team commands in `.claude/commands/` and task-specific skills in `.claude/skills/`.
- Use skill frontmatter such as `context: fork`, `allowed-tools`, and `argument-hint` to keep verbose or risky workflows isolated.

### B7. File and code exploration patterns
- Use **Grep** for content search.
- Use **Glob** for path discovery.
- Use **Read** to inspect full files.
- Use **Edit** only when the target anchor is unique.
- Fall back to **Read + Write** when Edit is ambiguous.
- Trace code incrementally rather than reading entire repositories up front.

### B8. Planning and execution
- Use plan mode for architecture changes, multi-file refactors, migrations, and ambiguous work.
- Use direct execution for small, obvious fixes.
- Use forked subagents or Explore-style patterns for discovery to keep the main session clean.
- Use named session resumption only when prior findings are still valid; otherwise start fresh and inject a structured summary.

### B9. Prompt, review, and extraction standards
- Use concrete input/output examples and few-shot examples for ambiguous tasks.
- Prefer tool-use with JSON schema for structured extraction.
- Keep fields optional when source documents may not contain the value.
- Include `other` and `unclear` enum patterns where appropriate.
- Use retry-with-error-feedback only when the source contains the missing information and the failure is structural, not absent-data related.
- Separate syntax validation from semantic validation.

### B10. Review workflow standards
- Use independent review sessions rather than having a generation session review its own output.
- Split large reviews into per-file passes plus cross-file integration passes.
- Use explicit review criteria rather than vague instructions like “be conservative.”
- Feed prior review findings into reruns so only new or unresolved issues are reported.
- Use non-interactive CI runs with structured JSON output for automated review pipelines.

### B11. Context and summarization standards
- Persist key facts separately from summarized conversation history.
- Preserve dates, amounts, order IDs, statuses, and citations.
- Trim verbose tool outputs before they accumulate.
- Use scratchpad files and structured manifests for long investigations and crash recovery.
- Summaries must preserve claim-source mappings and temporal context.

### B12. Batch vs synchronous usage
- Use synchronous APIs for blocking or interactive workflows.
- Use batch APIs only for latency-tolerant work such as nightly audits, report generation, or large-scale offline analysis.
- Do not assume batch workflows can perform interactive multi-turn tool loops.
- Use `custom_id` or equivalent correlation IDs so failed items can be retried selectively.
