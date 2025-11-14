# 🚌 Smart Public Transport Analytics Project

## 1. Overview and Goal

This project leverages integrated data analytics—combining geospatial, ticketing, and text data—to identify systemic inefficiencies in public bus transport.  
The primary goal is to provide **actionable, evidence-based recommendations** to transport authorities for:

- Optimizing routes  
- Improving schedule reliability  
- Enhancing passenger experience  

The tone of the analysis is **pragmatic, challenging, and focused on operational ROI**.

---

## 2. Core Problem Statement

Public transport services today suffer from four systemic failures, leading to **low ridership, high operating costs, and declining public trust**:

1. **Unpredictable Timings**  
   Schedules are unreliable, pushing commuters to private vehicles.

2. **Inefficient Routes**  
   Simultaneous overcrowding and empty buses cause safety risks and resource wastage.

3. **Low Awareness**  
   Lack of accurate real-time information frustrates passengers.

4. **Unnoticed Complaints**  
   Unstructured feedback (social media, forms) rarely drives operational change.

5. **Use Case: Checking Financial Feasibility**

   This use case quantifies **the monetary impact of delays and underutilized buses**, helping transport authorities understand where fuel, labor, and operational resources are being wasted.  
   It focuses on two core metrics:

---

   **5.1 Lost Time Cost Metric (Severe Delay Minutes)**

   Severe delays directly increase fuel consumption and driver labor costs.  
   This analysis identifies the **Route–Hour combinations** that contribute the most to *operational losses*.

#### **Key Logic**

---

## 3. Data Sources and Structure

The project uses **three synthetic datasets**, linked using shared identifiers.  
**Data linkage is the backbone of the entire analysis.**

| Dataset | Acronym | Purpose | Primary Link Key |
|--------|---------|----------|------------------|
| **Vehicle Location Data** | VLD | Analyze delays, speed, and movement patterns | Trip_ID, Bus_ID, Hour |
| **Electronic Ticketing Machine Data** | ETM | Analyze passenger load, crowding, and revenue | Trip_ID, Route_ID, Hour |
| **Passenger Feedback Data** | Feedback | Analyze sentiment, complaints, and awareness issues | Derived Bus_ID via NER |

---

## 4. Analytical Methodology

The project is organized into five tasks, with **Text Analytics** providing key actionable insights.

### ### Task 1: Data Preprocessing (The Foundation)
- Convert all time/date fields to proper formats  
- Extract `Route_ID` from `Trip_ID`  
- Extract `Hour` from timestamp  
- Assess missingness for critical fields (e.g., `Current_Load`, `Latitude/Longitude`)

### Task 2: Text Analytics Pipeline (Feature Engineering)
The pipeline transforms raw text feedback into structured analytical features.

| Feature Derived | Technique Used | Purpose |
|-----------------|----------------|---------|
| **Issue_Category_Topic** | Keyword Matching (Simulated Topic Modeling) | Classify complaint type |
| **Sentiment_Score** | TextBlob | Determine complaint polarity (-1.0 to 1.0) |
| **Urgency_Flag** | Threshold Logic | Assign High/Med/Low urgency based on topic & sentiment |
| **NER_Extracted_ID** | spaCy Rule-Based | Extract Bus_ID or Route_ID for linking |

---

## 5. Use Case Summary & Outputs

| Use Case | Problem Statement | Key Output Metric | Strategic Insight |
|----------|-------------------|-------------------|-------------------|
| **1. Unpredictable Timings** | Rigid schedules fail | Delay-Load Correlation | Distinguish traffic delays vs. loading inefficiencies |
| **2. Inefficient Routes** | Overcrowding vs emptiness | Overcrowding Instances & Underutilization Rate | Basis for optimizing fleet capacity & cost cuts |
| **3. Low Awareness** | No real-time ETA | Top Keywords from 'Info Lack' | Identify exact info gaps (e.g., "arrival", "tracker broken") |
| **4. Passenger Complaints** | Issues ignored | Triage Summary & Complaint-Delay Linkage | Enable automated incident response & service validation |
| **5. Financial Sustainability** | Inefficiencies cost money | Severe Delay Minutes & Wasted Capacity | Quantify monetary impact; justify new investments |

---

## 6. Next Steps for Implementation

1. **Refine NER/NEL**  
   Improve entity linking using a Gazetteer to map location names (e.g., “Mallya Road”) to Route IDs.

2. **Integrate Cost Data**  
   Add fuel cost, crew cost, and operational cost metrics to convert delays into monetary values.

3. **Visualization**  
   Build dynamic dashboards (Power BI/Tableau) including:  
   - Overcrowding heatmaps  
   - Delay-performance charts  
   - Real-time sentiment overlays  

---

