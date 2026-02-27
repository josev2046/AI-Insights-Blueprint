## Abstract
This document outlines my architectural design and conceptual framework for a semantic video search prototype. The system is designed to address the inherent limitations of metadata-dependent archives by utilising neural video understanding to enable natural language discovery within large-scale visual repositories.

## Demo



https://github.com/user-attachments/assets/8f50285d-91c9-48cb-aaf2-afec57ab6c77



## Conceptual framework
Traditional archival retrieval relies on manual indexing and keyword matching, which are prone to human error and linguistic limitations. This prototype shifts the search paradigm toward neural feature extraction:

* **Neural vector mapping**: Visual content is ingested and converted into high-dimensional vectors, allowing the system to understand concepts rather than just strings.
* **Semantic correlation**: Queries are processed to find the closest visual match within the vector space, enabling discovery based on content, action, or mood.
* **Temporal deep-linking**: The system retrieves specific start and end timecodes, allowing for instantaneous playback of the relevant segment within a longer sequence.

## High-Level System Architecture



### 1. UI (React)
The frontend serves as the orchestration point for user intent. It manages state for:
* **Asynchronous retrieval**: Handling live updates during high-compute neural searches.
* **Temporal navigation**: Utilising URL fragments (e.g., `#t=seconds`) to command the media player to precise coordinates.

### 2. The logic layer (FastAPI)
The intermediary backend serves as a secure gateway and data sanitiser:
* **API orchestration**: Managing the multipart/form-data requirements for the Twelve Labs v1.3 engine.
* **Stream normalisation**: Converting cloud-hosted storage links (e.g., GitHub Blobs) into raw content streams compatible with HTML5 video standards.

### 3. The neural layer (Twelve Labs Marengo-2.6)
The core processing engine performs the following tasks:
* **Visual feature extraction**: Identifying objects, movements, and environments within the footage.
* **Probability scoring**: Assigning confidence levels to matches to ensure the researcher can gauge the accuracy of the result.

## Key learnings & technical Observations
* **Metadata independence**: The prototype demonstrated that neural search can successfully identify visual concepts (e.g., "robotic automation") even when such terms are entirely absent from the original file metadata.
* **Threshold sensitivity**: The calibration of search thresholds is critical; a "low" threshold is often necessary to capture abstract or stylistic archival footage that might be filtered out by more rigid settings.
* **Architecture decoupling**: Maintaining a strict separation between the neural processing engine and the logic layer allows for future-proofing against updates in AI models without requiring a full frontend redesign.

