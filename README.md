# Job–Resume Screening Assistant (MVP)

This project is a **job–resume screening assistant** that automates candidate ranking based on job description matching.  
The assistant parses resumes, extracts skills, compares them to job requirements, and outputs ranked results with detailed coverage and explanations.

---

## Step Plan

## **Step 1 — Setup & Scope**
- Create repo structure and Python environment.  
- Install dependencies:  
  `streamlit`, `scikit-learn`, `sentence-transformers`, `rank_bm25`, `spacy`, `pdfminer.six`, `python-docx`.  
- Define clear outputs:  
  - **Match score** (0–100)  
  - **Coverage %**  
  - **Missing skills**  
  - **Ranked candidates**  

---

## **Step 2: Data Collection & Skills Dictionary**
- Gather **3–5 job descriptions** and **10–30 resumes (anonymized)**.  
- Create a **skills dictionary** (e.g., `Python`, `SQL`, `TensorFlow`) + synonyms (`"k8s"` → `"Kubernetes"`).  
- **Optional**: Plan for auto-expansion using embedding neighbors or external sources (Wikipedia/StackOverflow).  

---

## **Step 3: Ingestion & Normalization**
- Implement parsing for **PDF/DOCX/TXT** resumes.  
- Clean text: lowercase, remove noise, normalize synonyms.  
- Detect and split into sections: **Experience**, **Skills**, **Education**.  
- Deduplicate repeated skill variants.  

---

## **Step 4: Baseline Representation & Matching**
- Use **TF-IDF** or **BM25** for bag-of-words matching.  
- Compute **cosine similarity** between job description and resumes.  
- Add **keyword coverage** (required vs. preferred skills).  
- Combine into baseline score:  

  ```python
  baseline_score = 0.6 * cosine + 0.4 * coverage
  ```
## **Step 5: Semantic Upgrade (Embeddings)**
- Use **Sentence-BERT** (e.g., `all-MiniLM-L6-v2`) for embeddings.  
- Compute **cosine similarity** for semantic match.  
- Hybrid scoring formula:  

  ```python
  S = α * BM25 + (1 − α) * cosine(embeddings)

## **Step 6: Scoring & Explanation Layer**
- Apply **section-weighted scoring**  
  *(e.g., skills in Experience > skills in Skills list)*  
- Highlight and categorize:  
  -  **Matched skills**  
  - **Missing skills**  
  - **Weak terms**  
- Compute **coverage %** for required and preferred skills.  
- Generate structured **JSON output** per candidate.  

---

## **Step 7: Ranking & Reporting**
- Rank candidates by **final score**.  
- Export results as **CSV/JSON** for easy integration.  
- Provide **per-resume keyword suggestions** (skills to add or strengthen).  
- Validate ranking with a **manual evaluation set**.  

---

## **Step 8: Web App (Streamlit UI)**
- **Upload inputs**:  
  - Job description  
  - Multiple resumes  
- **Results table** format:  

  | **Candidate** | **Score** | **Coverage %** | **Missing Skills** |  
  |---------------|-----------|----------------|-----------------------------|  

- **Detail view**: highlights inside resume text with explanation.  
- **Export button**: download full report (**CSV/JSON**).  
- **MVP complete** when a **non-developer** can upload files and get a useful ranking.  
