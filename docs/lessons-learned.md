# Lessons Learned

## 1. Overview
This document summarizes key technical and architectural learnings from building a production-grade Azure data engineering solution.

---

## 2. Azure Data Factory Learnings
- Metadata-driven pipelines significantly reduce duplication
- Proper parameterization improves maintainability
- Control flow activities are essential for orchestration
- Mapping Data Flow performance depends heavily on partitioning

---

## 3. Data Modeling Insights
- Layered data lake architecture simplifies debugging
- Keeping raw data immutable enables safe reprocessing
- Analytics schemas should prioritize read performance

---

## 4. Orchestration Challenges
- Managing dependencies across pipelines requires clear ownership
- Parent-child pipelines improve observability
- Trigger dependencies must be carefully designed to avoid deadlocks

---

## 5. Monitoring & Debugging
- Built-in ADF monitoring is necessary but not sufficient
- Log Analytics enables deeper visibility
- Capturing activity-level metrics helps with SLA tracking

---

## 6. CI/CD Learnings
- ARM templates must be parameterized for environments
- Secrets should never be hard-coded
- Separate build and release pipelines improve control

---

## 7. Performance Optimization
- Avoid unnecessary data movement
- Push transformations closer to compute engines
- Tune Data Flow settings based on dataset size

---

## 8. What I Would Do Differently
- Introduce stronger data quality checks early
- Automate schema validation
- Add cost monitoring dashboards

---

## 9. Key Takeaway
Building data pipelines is not just about moving data —  
it is about **designing reliable, observable, and scalable systems**.
