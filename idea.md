# Crop Guardian AI 3.0: Agentic Edition

## Tagline
**7 AI agents. Voice-first. Offline-first. Farmer-owned intelligence.**

## One-Line Pitch
Crop Guardian AI 3.0 is a software-first, multilingual crop-intelligence platform for Farmer Producer Organizations (FPOs). It combines leaf-image analysis, farmer voice input, local weather, crop-stage context, satellite-derived crop-health signals, verified agricultural knowledge, and market information to help farmers identify crop-health risks and choose safer, higher-value next actions.

---

## 1. The Problem

Smallholder farmers often make high-stakes decisions with incomplete information:

- A disease or nutrient problem may be noticed late, after it spreads.
- Image-only disease apps can confuse visually similar symptoms.
- Advice is often not available in the farmer's language or is inaccessible without stable internet.
- Farmers may receive treatment suggestions without cost, harvest interval, local weather, crop stage, or market context.
- FPO managers lack an aggregated early-warning view of possible outbreaks, input demand, and crop risk across villages.
- Farmers need trusted, practical answers—not a long generic list of remedies.

### Core Opportunity
Create a **decision-support system**, not just a disease classifier. The system should clearly state what it knows, what it is uncertain about, what evidence supports its recommendation, and when expert review is needed.

---

## 2. Solution Overview

Crop Guardian AI 3.0 works as a virtual agricultural support team. A farmer can submit a leaf photo, voice note, text description, or crop record. The platform evaluates the information through specialized software agents and returns a prioritized, explainable advisory.

### Core Outputs

1. Probable issue and confidence level
2. Image explanation showing the region that influenced the prediction
3. Missing-information prompts when confidence is low
4. Weather and crop-stage risk factors
5. Treatment options ranked by safety, cost, availability, waiting period, and expected benefit
6. Escalation route to an FPO/KVK/agronomist for high-risk or uncertain cases
7. Optional harvest, storage, and market timing recommendation
8. FPO-level early-warning dashboard based on anonymized, aggregated reports

---

## 3. What Makes It Unique

| Common crop app | Crop Guardian AI 3.0 |
|---|---|
| Leaf photo only | Image + farmer voice + weather + crop stage + location context |
| One black-box answer | Confidence score, Grad-CAM explanation, and uncertainty prompts |
| Static advice list | Evidence-grounded treatment ranker with cost and harvest-interval checks |
| Cloud-only workflow | Offline-first on-device screening, then sync when connected |
| Individual user focus | Farmer app plus FPO outbreak, demand, and advisory dashboard |
| Generic language interface | Tamil-first voice interface, extendable to other Indian languages |
| Model remains static | Opt-in feedback loop to improve local recommendations |

---

## 4. The Seven AI Agents

The term **agent** means a focused software module with a clear responsibility. For a hackathon, these can be simple Python services/functions rather than complex autonomous systems.

### 4.1 Intake and Quality Agent

**Purpose:** Validate the incoming report before diagnosis.

**Tasks:**
- Detect whether the image contains a usable plant leaf
- Check blur, darkness, distance, and occlusion
- Ask the farmer for crop type, approximate crop age, village, and symptom duration
- Route the report to the correct crop-specific model

**Example response:**
> “Photo is too dark for a reliable result. Please take another image in daylight, showing both the front and back of one affected leaf.”

### 4.2 Vision Agent

**Purpose:** Perform on-device image screening.

**Technology:** TensorFlow Lite / MobileNetV3 / EfficientNet-Lite.

**Tasks:**
- Identify likely crop-health class: disease, pest damage, nutrient deficiency, or healthy
- Produce confidence score
- Generate Grad-CAM/XAI heatmap to show image regions used by the model

**Safety rule:** A prediction is an advisory, not a final diagnosis. Low-confidence results must be routed to review.

### 4.3 Context Agent

**Purpose:** Add farm context that cannot be seen in a photo.

**Inputs:**
- Current and forecast weather
- Humidity, temperature, rainfall probability
- Farmer-entered soil condition
- Crop stage
- Village-level prior reports

**Tasks:**
- Assess whether conditions are favorable for the suspected problem
- Generate risk factors such as high humidity, heat stress, or probable rainfall
- Recommend re-checking or postponing spray when rain risk is high

### 4.4 Knowledge Agent

**Purpose:** Produce factual and explainable advice from a verified knowledge base.

**Technology:** Agricultural knowledge graph + Retrieval-Augmented Generation (RAG).

**Knowledge graph entities:**
- Crop
- Symptom
- Disease/pest/nutrient issue
- Pathogen type
- Crop stage
- Weather condition
- Treatment
- Dose and application method
- Pre-harvest interval
- Organic/biological status
- Safety and restricted-use note
- Local advisory source

**Rule:** The language model may summarize retrieved evidence, but it cannot invent doses, chemical names, or safety instructions.

### 4.5 Scenario Simulator Agent

**Purpose:** Compare possible farmer actions before the farmer spends money.

**Version 1 for hackathon:** Transparent rule-based scenarios.

**Example scenarios:**
- No action for 7 days
- Low-cost preventive treatment
- Recommended treatment within 48 hours
- Expert assessment first

**Outputs:**
- Estimated risk category: low / medium / high
- Approximate yield-risk band
- Estimated treatment cost
- Assumptions used by the estimate

**Future version:** Integrate validated crop-growth or digital-twin models after local calibration and agronomist partnership.

### 4.6 Market and Post-Harvest Agent

**Purpose:** Connect crop health to selling decisions.

**Tasks:**
- Display recorded mandi prices and simple trend projections
- Estimate whether expected price difference exceeds storage and spoilage cost
- Recommend: sell now, harvest selectively, use cold storage, or seek buyer quote
- Generate a lot record and QR-linked history for FPO aggregation

**Important:** Price forecasts must always display uncertainty; they are not a guarantee of future income.

### 4.7 FPO Early-Warning Agent

**Purpose:** Convert individual reports into community-level prevention.

**Tasks:**
- Aggregate anonymized reports by crop, village, date, and confidence band
- Flag unusual increases in similar symptoms
- Send a manager alert only after threshold and expert-rule checks
- Predict bulk demand for approved inputs
- Provide an operator panel for sending verified local advisories

**Example alert:**
> “Possible early-blight cluster: 14 medium/high-confidence tomato reports from three nearby villages in the last 48 hours. Review before issuing FPO advisory.”

---

## 5. Farmer Workflow

1. Farmer opens the app, WhatsApp bot, or assisted FPO kiosk.
2. Farmer sends a leaf photo and optional Tamil voice note.
3. Intake Agent checks photo quality and asks for missing details.
4. Vision Agent performs offline preliminary classification.
5. When internet is available, Context Agent adds weather and local-risk data.
6. Knowledge Agent retrieves verified crop-specific guidance.
7. Scenario Agent compares safe action choices and likely cost/risk.
8. Farmer receives a short Tamil voice response plus readable visual report.
9. Farmer can request expert review or rate the usefulness of the advice after a few days.
10. Anonymized patterns update the FPO early-warning dashboard.

---

## 6. Sample Tamil Advisory

**Farmer input:**
> “என் தக்காளி இலைகளில் பழுப்பு புள்ளிகள் இருக்கின்றன. என்ன செய்யலாம்?”

**Safe system output:**
> “படத்தில் ஆரம்பகால பூஞ்சை நோயின் அறிகுறிகள் இருக்கலாம். நம்பகத்தன்மை: நடுத்தரம். கடந்த இரண்டு நாட்களில் அதிக ஈரப்பதம் இருப்பதால் நோய் பரவல் அபாயம் அதிகமாக உள்ளது. மேலும் ஒரு தெளிவான படம் மற்றும் இலைக்குப் பின்புறப் படம் அனுப்பவும். அருகிலுள்ள வேளாண் அலுவலர் அல்லது FPO நிபுணரிடம் உறுதிப்படுத்திய பின் மட்டுமே மருந்தைப் பயன்படுத்தவும்.”

The system then shows verified options with source, cost range, safety note, waiting period before harvest, and an expert-review button.

---

## 7. Software Architecture

```text
Farmer Interfaces
  ├── Flutter/PWA mobile application (offline-first)
  ├── WhatsApp/Telegram bot (optional)
  ├── Tamil voice interface
  └── FPO operator web dashboard

API and Application Layer
  ├── FastAPI backend
  ├── JWT/OTP authentication
  ├── REST or GraphQL APIs
  ├── Background tasks (Celery/RQ)
  └── Notification service (SMS/WhatsApp/FCM)

AI and Decision Layer
  ├── TFLite vision model (offline)
  ├── Image quality checker
  ├── XAI/Grad-CAM service
  ├── Rule-based context and triage engine
  ├── RAG service with verified documents
  ├── Knowledge graph queries
  ├── Scenario calculator
  └── Early-warning cluster detector

Data Layer
  ├── PostgreSQL + PostGIS: users, farms, reports, lots, analytics
  ├── Neo4j: crop-disease-treatment knowledge graph
  ├── Redis: queues and caching
  ├── Object storage: submitted images and documents
  └── IndexedDB/SQLite: offline mobile cache

External Data (optional)
  ├── IMD/public weather sources
  ├── Market-price sources
  ├── Open satellite imagery such as Sentinel-2
  └── FPO-maintained local price, buyer, and advisory records
```

---

## 8. Offline-First Design

### On the phone, without internet
- Image-quality assessment
- Crop/leaf screening model
- Tamil text templates and preloaded treatment cards
- Saved reports and pending uploads
- QR/lot ID generation

### When connected
- Weather lookup
- Knowledge-base updates
- Expert escalation
- FPO dashboard synchronization
- Market-price updates
- Optional model update download

This design is more practical than making critical diagnosis depend entirely on a cloud connection.

---

## 9. Explainability and Trust

A winning agriculture AI platform must be trustworthy, not merely accurate.

### Trust Features

- **Grad-CAM heatmap:** Shows the leaf region the model examined.
- **Confidence bands:** High, medium, and low—not misleading absolute certainty.
- **Evidence card:** Source, treatment category, waiting period, and safety disclaimer.
- **Alternative possibilities:** e.g., “Could be nutrient deficiency; upload soil/plant details.”
- **Expert escalation:** One-tap route to FPO agronomist/KVK contact.
- **Feedback:** Farmers can report whether the issue improved, remained unchanged, or worsened.
- **Audit log:** Records model version, inputs, retrieved advisory source, and final recommendation.

### Safety Boundary
The system should never independently prescribe hazardous pesticide dosage. It should provide educational decision support and direct users to locally approved labels, qualified experts, and regulatory guidance.

---

## 10. Satellite and Remote-Sensing Layer

This is optional for the hackathon prototype but powerful in the full product.

### Data Sources
- Sentinel-2 imagery for vegetation indices
- Field boundary drawn by farmer/FPO on map
- Weather and rainfall data
- Village-level anonymized disease reports

### Uses
- Identify unusual decline in vegetation index over time
- Highlight zones for farmer photo verification
- Track drought/stress patterns
- Prioritize FPO extension visits
- Support crop-growth and harvest planning

### Correct Positioning
Satellite signals do **not** diagnose a disease by themselves. They are an early-warning and prioritization layer; farmer photos and expert validation remain essential.

---

## 11. Privacy and Farmer Data Rights

### Principles

- Farmer owns their identifiable data.
- Store only data needed for the service.
- Obtain explicit consent before sharing a photo or farm location.
- Use anonymized aggregation for FPO outbreak dashboards.
- Let users delete their account and personal reports.
- Do not sell identifiable farmer data.
- If using federated learning later, send model updates—not raw images—only with informed opt-in consent.

### Why This Matters
Trust is essential. Farmers should benefit from the data they generate and understand how it is used.

---

## 12. MVP for a 48-Hour Hackathon

Build the smallest product that demonstrates the unique intelligence.

### Must Build (P0)

1. Tamil/English web or Flutter interface
2. Upload crop-leaf image
3. Pretrained disease classifier for 2–3 crops
4. Image-quality warning
5. Confidence score and Grad-CAM heatmap
6. Weather input/mock weather API
7. Rule-based treatment comparison card
8. Cost-benefit scenario calculator
9. FPO dashboard showing anonymized reports on a map/table
10. Tamil voice output using TTS

### Nice to Have (P1)

- WhatsApp bot
- QR crop-lot record
- Market-price chart
- Knowledge graph visualization
- Offline PWA cache
- Satellite NDVI screenshot/layer for a demo field

### Do Not Build in 48 Hours

- Real smart contracts, cryptocurrency, or tokens
- Full federated learning system
- Production-grade digital twin
- Drone integrations
- Claims of real medical/agronomic regulatory approval

Use these as a **credible roadmap**, not a fake demo.

---

## 13. Suggested Tech Stack

| Layer | Recommended stack |
|---|---|
| Mobile/PWA | Flutter or React + Vite PWA |
| Frontend dashboard | React + Tailwind + Recharts |
| Backend | Python FastAPI |
| ML | TensorFlow / TensorFlow Lite, scikit-learn |
| Image explanation | Grad-CAM using TensorFlow/PyTorch |
| Database | PostgreSQL + PostGIS |
| Knowledge graph | Neo4j Community Edition or NetworkX for MVP |
| Caching/queues | Redis + Celery/RQ |
| Voice | Indic-language TTS/STT provider or browser speech APIs for demo |
| Maps | Leaflet + OpenStreetMap |
| Deployment | Vercel (frontend), Render/Railway (backend), Supabase/Neon (database) |

---

## 14. Data Model

```text
users
- id, name, phone, language, role, consent_flags

farms
- id, user_id, fpo_id, village, geometry, area, soil_type

crop_cycles
- id, farm_id, crop_name, variety, planting_date, growth_stage

health_reports
- id, crop_cycle_id, image_url, symptom_text, report_time,
  model_version, predicted_class, confidence, review_status

context_snapshots
- id, health_report_id, weather_source, temperature, humidity,
  rainfall_probability, soil_condition

advisories
- id, health_report_id, retrieved_sources, options_json,
  safety_note, expert_escalation_required

feedback
- id, health_report_id, outcome, farmer_rating, notes

fpo_alerts
- id, fpo_id, crop_name, location_cluster, alert_level,
  evidence_count, reviewed_by, status

crop_lots
- id, crop_cycle_id, harvest_date, quantity, qr_code,
  storage_history, buyer_status
```

---

## 15. Scoring Logic Example

A transparent risk score can be calculated without claiming a fully trained AI model.

```python
risk_score = (
    0.45 * visual_confidence +
    0.20 * weather_risk +
    0.15 * crop_stage_risk +
    0.10 * local_cluster_risk +
    0.10 * farmer_reported_severity
)

if risk_score >= 0.75:
    action = "High priority: seek expert confirmation within 24 hours"
elif risk_score >= 0.45:
    action = "Moderate priority: take clearer images and follow verified preventive guidance"
else:
    action = "Monitor and rescan if symptoms spread"
```

The screen must display the factors contributing to the score.

---

## 16. Evaluation Metrics

### Model Quality
- Classification accuracy and F1 score by crop/disease
- False-negative rate for high-risk cases
- Image-quality rejection accuracy
- Calibration: whether 80% confidence is correct roughly 80% of the time

### Farmer Value
- Time from report to advisory
- Percentage of reports in Tamil voice mode
- Expert escalation completion rate
- Farmer satisfaction after follow-up
- Treatment-cost savings or avoided loss, measured through pilot surveys

### FPO Value
- Number of verified early-warning alerts
- Time from cluster detection to FPO advisory
- Input-demand forecast accuracy
- Number of farmers reached with preventive advice

### Responsible AI
- Consent rate and deletion requests fulfilled
- Recommendation auditability
- Bias/error rates across crops, districts, and phone-camera quality

---

## 17. Business Model

| Customer | Offer | Possible pricing approach |
|---|---|---|
| Individual farmer | Limited free scans and basic advisory | Freemium |
| FPO | Dashboard, multilingual advisory workflow, member analytics | Monthly SaaS license |
| Agri-extension partner | Custom local knowledge base and verified alert workflow | Institutional subscription |
| Buyer/processor | Lot traceability and quality-handling records | Per lot or enterprise license |
| Input retailer | Verified product catalog, never influence diagnosis rank | Listing/service fee with clear separation |

### Ethical Revenue Rule
The platform must never recommend a treatment merely because a seller pays more. Treatment ranking must remain evidence-based and auditable.

---

## 18. Rollout Roadmap

### Phase 1: Hackathon MVP (0–2 months)
- Tomato, rice, and chilli support
- Tamil/English interface
- Image diagnosis, explainability, basic weather-aware advisory
- FPO dashboard with synthetic/demo data

### Phase 2: Field Pilot (3–6 months)
- Partner with one FPO and one KVK/agronomist
- Collect consented, expert-reviewed local images
- Validate recommendations and create a Tamil knowledge base
- Add assisted kiosk and WhatsApp workflow

### Phase 3: District Product (6–12 months)
- More crops and language support
- Market and storage decision module
- Satellite early-warning layer
- Expert network and auditable advisory process

### Phase 4: Scale (12+ months)
- Multiple FPOs and states
- Opt-in privacy-preserving learning
- Integration with storage, input, and buyer workflows
- Independent evaluation of agronomic and income impact

---

## 19. Three-Minute Demo Script

### 0:00–0:25 — Problem
“Farmers often identify crop problems too late, receive generic advice, and cannot easily access support in their own language.”

### 0:25–1:05 — Farmer Experience
“Here, a farmer uploads a tomato leaf image and speaks Tamil. The app checks image quality, performs offline screening, shows a heatmap, and reports a moderate-confidence early-blight risk.”

### 1:05–1:40 — Explainable Decision
“The app combines weather, crop stage, and verified knowledge. It explains why humidity increases risk, compares safe options by cost and harvest interval, and requests expert confirmation before action.”

### 1:40–2:15 — FPO Intelligence
“Individual reports become anonymized signals. The FPO dashboard detects a possible cluster, reviews evidence, and sends a verified prevention alert to nearby members.”

### 2:15–3:00 — Impact and Roadmap
“Crop Guardian AI is offline-first, Tamil-first, explainable, and farmer-respecting. It starts as software today and can later integrate satellite, market, storage, and expert systems without requiring expensive hardware.”

---

## 20. Final Pitch

> Crop Guardian AI 3.0 is not another leaf-scanner app. It is an explainable, Tamil-first crop intelligence network that transforms a farmer’s photo and voice note into context-aware, verified action—while helping FPOs see crop risk early, coordinate prevention, and protect farmer income.

---

## Evidence-Informed Design Notes

- Multimodal crop-health systems can combine visual symptoms with environmental and contextual information; this is more robust than relying solely on a leaf photo.
- Few-shot and transfer-learning approaches are useful where local crop-disease image datasets are small.
- Edge inference can reduce latency, bandwidth consumption, and dependence on connectivity.
- Knowledge graphs and retrieval-grounded generation are useful for making advisory systems traceable and reducing unsupported language-model output.
- Satellite imagery and vegetation indices can serve as early-warning signals but require ground verification.
- Multi-agent and simulation-grounded agricultural systems are promising research directions; they should be introduced progressively and tested with agricultural experts.

## Research Sources to Cite in Presentation

1. Reviews of AI-driven, multimodal plant disease detection and precision plant protection.
2. Research on few-shot learning for disease classification under limited image data.
3. Studies on edge AI for crop/plant disease identification.
4. Research on agricultural knowledge graphs and RAG-grounded advisory systems.
5. NITI Aayog and public-sector resources on satellite/GIS-supported agricultural intelligence.
6. IMD/public weather data documentation and agricultural extension guidance.

---

## File Purpose

This document is designed as an idea brief for a hackathon, academic project, or early product proposal. It intentionally separates:

- **Build now:** software MVP and demonstrable features
- **Pilot next:** expert-reviewed agronomic validation
- **Scale later:** satellite integration, advanced simulations, privacy-preserving learning, and operational partnerships

This keeps the project ambitious, unique, safe, and realistic.
