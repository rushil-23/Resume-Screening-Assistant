Step Plan for Job–Resume Screening Assistant (MVP)
Step 1 — Setup & Scope
•	Create repo structure and Python environment.
•	Install dependencies: streamlit, scikit-learn, sentence-transformers, rank_bm25, spacy, pdfminer.six, python-docx.
•	Define clear outputs: match score (0–100), coverage %, missing skills, ranked candidates.
________________________________________
Step 2 — Data Collection & Skills Dictionary
•	Gather 3–5 job descriptions and 10–30 resumes (anonymized).
•	Create a skills dictionary (Python, SQL, TensorFlow, etc.) + synonyms (“k8s” → “Kubernetes”).
•	Optional: plan for auto-expansion (embedding neighbors, Wikipedia/StackOverflow terms).
________________________________________
Step 3 — Ingestion & Normalization
•	Implement parsing functions for PDF/DOCX/TXT.
•	Clean text: lowercase, remove noise, normalize synonyms.
•	Detect and split into sections: Experience, Skills, Education.
•	Deduplicate repeated skill variants.
________________________________________
Step 4 — Baseline Representation & Matching
•	Use TF-IDF or BM25 for bag-of-words matching.
•	Compute cosine similarity between job and resumes.
•	Add keyword coverage (required vs. preferred skills).
•	Combine into baseline score: e.g., 0.6 * cosine + 0.4 * coverage.
________________________________________
Step 5 — Semantic Upgrade (Embeddings)
•	Use Sentence-BERT (e.g., all-MiniLM-L6-v2) to get embeddings.
•	Compute cosine similarity for semantic match.
•	Hybrid score: S = α*BM25 + (1−α)*cosine(Embeddings) (tune α).
•	Improve robustness beyond keyword matching.
________________________________________
Step 6 — Scoring & Explanation Layer
•	Section-weighted scoring: skills in Experience > skills in Skills list.
•	Highlight matched skills, missing skills, weak terms.
•	Compute overall coverage % for required and preferred skills.
•	Generate JSON output per candidate.
________________________________________
Step 7 — Ranking & Reporting
•	Rank candidates by final score.
•	Export results as CSV/JSON.
•	Include per-resume keyword suggestions (which terms to add/strengthen).
•	Verify ranking with small manual evaluation set.
________________________________________
Step 8 — Web App (Streamlit UI)
•	File uploader: job description + multiple resumes.
•	Results table: Candidate | Score | Coverage% | Missing Skills (Top 5).
•	Detail view: highlights in text + explanation.
•	Export button for full report (CSV/JSON).
•	Done when a non-dev can upload files and get a useful ranking.

