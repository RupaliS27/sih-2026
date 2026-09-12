# Crop Health Surveillance & Disease Management System

A multi-tiered platform providing early detection, microclimate forecasting, insect trap surveillance, and actionable agricultural advisories for farmers, extension officers, and state agricultural authorities.

## Language

### Core Entities & Roles

**Farmer**:
A grower managing one or more crop blocks or orchards who requires immediate localized diagnosis and safe treatment guidance.  
_Avoid_: User, client, account holder, customer

**Extension Worker**:
A field officer or agronomist covering an agricultural taluk or cluster, responsible for ground-truthing farmer reports, inspecting orchards, and verifying borderline automated detections.  
_Avoid_: Agent, field rep, scout, inspector

**Agriculture Official**:
A state or district level authority (such as a District Agricultural Officer or MSInS director) monitoring regional outbreak trends, pesticide supply chains, and issuing preventive emergency broadcasts.  
_Avoid_: Admin, superuser, operator

**Diagnostic Laboratory**:
An accredited institutional or university pathology laboratory (such as KVK or state agricultural university lab) performing microscopic or molecular PCR validation on ambiguous samples.  
_Avoid_: Testing facility, third-party lab, backend service

---

### Diagnosis, Pathology & Computer Vision

**Domain Gate**:
A binary neural filter deployed before pathology classification to verify whether an input image belongs to the target plant leaf domain, immediately rejecting non-target foliage, documents, or out-of-distribution clutter.  
_Avoid_: Preprocessor, input sanitizer, sanity checker

**Disease Diagnosis**:
The automated identification of a specific pathological infection or insect damage on host foliage, paired with an inference confidence score.  
_Avoid_: Classification, prediction, leaf tag

**Pathological Severity**:
A quantified measurement of tissue necrosis and lesion area relative to healthy leaf area, graded as continuous metric and ordinal category (Low, Medium, High).  
_Avoid_: Sickness score, damage index, infection grade

**Explainability Map**:
A visual gradient-weighted attention heatmap (Grad-CAM) overlaid on the original leaf image highlighting the exact morphological lesions that informed the neural decision.  
_Avoid_: Saliency image, heatmap visualization, visual artifact

---

### Surveillance, Hardware & Microclimate

**Smart Trap Node**:
A low-power, solar-assisted field unit deployed inside a pheromone or yellow sticky trap that wakes periodically to record canopy microclimate and capture high-resolution imagery of trapped insect pests.  
_Avoid_: IoT device, sensor box, hardware bug, camera trap

**Trap Catch Count**:
The quantified number of target insect specimens captured on an optical trap liner during a surveillance cycle.  
_Avoid_: Bug score, insect count, photo count

**Economic Threshold Level (ETL)**:
The pest population density at which management interventions must be initiated to prevent an increasing pest population from reaching the economic injury level.  
_Avoid_: Danger limit, alert threshold, trigger point

**Canopy Microclimate**:
Local temperature, relative humidity, and calculated Vapor Pressure Deficit (VPD) recorded directly within the crop foliage micro-environment, governing fungal spore germination and insect activity.  
_Avoid_: Weather data, ambient climate, sensor telemetry

**Outbreak Hotspot**:
A geospatial cluster of neighboring crop blocks or taluks exhibiting elevated pathological severity or trap counts exceeding the Economic Threshold Level within an epidemiological risk window.  
_Avoid_: Danger zone, red area, cluster map

---

### Agronomic Decision Support & Interventions

**Integrated Pest and Disease Management (IPDM)**:
An ecosystem-based strategy focusing on long-term prevention through a combination of cultural practices, biological control agents, and judicious targeted chemical applications.  
_Avoid_: Treatment plan, spray schedule, pest control

**Safe Input Protocol**:
Scientifically validated dosage guidelines specifying chemical or biological formulations per liter of water, spray volume per hectare, and safety equipment requirements.  
_Avoid_: Dosage recommendation, medicine instruction

**Pre-Harvest Interval (PHI)**:
The minimum mandatory period in days required between the last application of an agrochemical and harvest to guarantee residue safety below statutory thresholds.  
_Avoid_: Waiting period, withholding time, cooldown

**Maximum Residue Limit (MRL)**:
The maximum legally permitted concentration of an agrochemical residue on agricultural produce, strictly monitored for domestic safety and export compliance.  
_Avoid_: Toxin limit, residue threshold

**Active Learning Confirmation**:
The formal verification or correction of an automated diagnosis by an extension agronomist, promoting validated field images into the continuous retraining corpus.  
_Avoid_: Human feedback, review tag, relabeling
