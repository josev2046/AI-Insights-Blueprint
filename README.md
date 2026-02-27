## Abstract
This document outlines my architectural design and conceptual framework for a rapid **Semantic Video Search Prototype**. The system is engineered to transcend the inherent limitations of metadata-dependent archives by leveraging **neural video understanding**, facilitating natural language discovery within large-scale visual repositories.

## Demo

https://github.com/user-attachments/assets/8f50285d-91c9-48cb-aaf2-afec57ab6c77

---

## Conceptual framework
Traditional archival retrieval relies on manual indexing and keyword matching, processes frequently hampered by human error and linguistic constraints. This prototype shifts the search paradigm toward **neural feature extraction**:

* **Neural vector mapping**: Visual content is ingested and transformed into high-dimensional vectors, enabling the system to parse conceptual meaning rather than mere strings.
* **Semantic correlation**: Queries are processed to identify the nearest visual matches within the vector space, facilitating discovery based on content, action, or nuanced atmosphere.
* **Temporal deep-linking**: The system retrieves specific start and end timecodes, allowing for instantaneous playback of the relevant segment within a longer sequence.

---

## Architecture

### 1. UI (React)
The frontend serves as the primary orchestration point for user intent, managing state for:
* **Asynchronous retrieval**: Handling live updates during high-compute neural searches.
* **Temporal navigation**: Utilising URL fragments (e.g., `#t=seconds`) to command the media player to precise coordinates.

### 2. Logic layer (FastAPI)
This intermediary backend serves as a secure gateway and data sanitiser:
* **API Orchestration**: Managing the `multipart/form-data` requirements for the Twelve Labs v1.3 engine.
* **Stream Normalisation**: Converting cloud-hosted storage links (e.g., GitHub Blobs) into raw content streams compatible with HTML5 video standards.

### 3. Neural layer (TwelveLabs Marengo-2.6)
The core processing engine performs the following critical tasks:
* **Visual feature extraction**: Identifying objects, movements, and environmental contexts within the footage.
* **Probability scoring**: Assigning confidence levels to matches, ensuring the researcher can gauge the empirical accuracy of the result.

---

## Key learnings &  observations
* **Metadata independence**: The prototype demonstrated that neural search can successfully identify visual concepts (e.g., "robotic automation") even when such terms are entirely absent from the original file metadata.
* **Threshold sensitivity**: The calibration of search thresholds is critical; a "low" threshold is often necessary to capture abstract or stylistic archival footage that might be filtered out by more rigid settings.
* **Architectural decoupling**: Maintaining a strict separation between the neural processing engine and the logic layer ensures the system is future-proofed against updates in AI models without requiring a full frontend redesign.
