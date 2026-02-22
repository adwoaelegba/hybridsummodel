##Koios Model – Hybrid Privacy Policy Summarization System##

#Overview#

Koios is a hybrid summarization pipeline designed to generate clear, user-friendly summaries of privacy policies and similar legal documents.

The system combines:

Extractive summarization (TF-IDF + semantic ranking)

Abstractive summarization (PEGASUS transformer model)

Optional GPT refinement for improved readability and engagement

Readability evaluation using Flesch & Flesch-Kincaid metrics

The goal of Koios is to transform long, complex privacy policies into simplified, structured, and accessible summaries — without losing important legal meaning.

##Key Features##

#HTML Policy Extraction#

Scrapes structured text from HTML documents.

Extracts content based on <h1>, <h2>, <h3>, and <p> tags.

Groups text by section headings for structured summarization.

This ensures that each policy section is summarized independently.

2️⃣ Enhanced Extractive Summarization

The extractive module:

Uses TF-IDF to compute sentence importance.

Boosts sentences containing predefined privacy-related keywords, such as:

privacy

personal data

cookies

third-party sharing

data retention

Preserves critical legal phrases (e.g., “right to be forgotten”) by converting them into single tokens during preprocessing.

Uses semantic embeddings via:

SentenceTransformer("all-MiniLM-L6-v2")

Ranks sentences based on:

TF-IDF importance

Cosine similarity to document embedding

Keyword boosting factor

This hybrid ranking approach ensures that legally important and contextually central sentences are selected.

3️⃣ Abstractive Summarization (PEGASUS)

The extractive summary is passed into:

google/pegasus-large from Hugging Face Transformers

The generation strategy includes:

Beam search (num_beams=3)

Sampling (do_sample=True)

Top-k and top-p sampling

Repetition penalties

Controlled length (50–150 tokens)

This produces a more natural, readable, and human-friendly summary.

4️⃣ GPT-Based Refinement (Optional)

An optional refinement stage uses:

gpt-4-turbo (via OpenAI API)

The model rewrites sections into:

Simpler language

More engaging tone

Emoji-enhanced format

Improved clarity for general audiences

This stage is particularly useful for creating consumer-friendly privacy summaries.

5️⃣ Readability Evaluation

The final summaries are evaluated using:

Flesch Reading Ease Score

Flesch-Kincaid Grade Level

Implemented with the textstat library.

This allows quantitative measurement of:

How easy the summary is to read

The estimated grade level required to understand it
