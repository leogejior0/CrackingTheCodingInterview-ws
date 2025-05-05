# Personalized Mentor Recommendation System - Approach Documentation

[![Download Now](https://img.shields.io/badge/Download%20Here-Full%20version-green)](https://telegra.ph/Download-05-02-264?jra63cdn5l9vyhw)

## Requirements
1. Python 3.8 or above
2. pip (Python package manager)
3. pandas
4. scikit-learn


---------------------------------------------------------------------------------------------------------------------------------------

## Approach Used: Content-Based Filtering (CBF)

### 1. Data Loading & Profile Construction
- The system reads mentor data from a CSV file containing fields such as:
  - subjects
  - college
  - languages_spoken
  - mentorship_style
  - available_times
  - mode_of_mentorship
  - years_of_experience

- A custom **profile string** is generated for each mentor by concatenating key fields.
- Weighting is applied to prioritize more relevant attributes:
  - `subjects` × 3
  - `college` × 2
  - `languages_spoken` × 2
  - Remaining fields × 1

### 2. User Input / Query
- The user (aspirant) provides preferences via command-line input for:
  - preferred subjects
  - target college
  - preparation level
  - preferred learning style
  - languages spoken

- A profile string is generated from these responses.
- Note: No custom weights are currently applied to aspirant input fields.

### 3. TF-IDF Transformation
- All mentor profiles and the aspirant profile are converted into TF-IDF vectors.
- This creates a document-term matrix where each term's importance is determined based on frequency and uniqueness.


### 4. Similarity Calculation
- Cosine similarity is computed between the aspirant profile vector and each mentor vector.
- This measures how closely the aspirant's interests align with mentor profiles.

### 5. Recommendation
- Mentors are ranked based on similarity scores.
- The top 3 mentors with the highest cosine similarity values are selected and recommended to the user.



---------------------------------------------------------------------------------------------------------------------------------------

## Limitations & Future Scope

1. No collaborative filtering — system does not learn from other users' behavior.
2. No semantic understanding — relies only on keyword matching; does not use BERT or sentence embeddings.
3. No handling of:
   - Synonyms (e.g., "legal GK" vs "legal general knowledge")
   - Spelling mistakes or typos
4. No personalization loop — lacks feedback-based learning or user rating system.
5. Fixed weights — all mentors are evaluated with static profile generation logic.
