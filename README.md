# Large Language Model Risk Evaluation: AI Language Tutor & Wikipedia RAG Bot

## Project Overview

* This project conducts a risk evaluation of two distinct Large Language Models (LLMs) leveraging **Azure AI Foundry**: an AI-powered language tutor and a Wikipedia-based Retrieval-Augmented Generation (RAG) bot. The primary goal is to quantify potential risks associated with their use. The primary LLM used is a quantized llama.cpp model: PHI:4b
---

## Objectives

The core objective of this evaluation is to quantify and understand the potential risks inherent in deploying LLMs, specifically:

* **AI-powered Language Tutor:** An interactive tool for language learning.
* **Wikipedia-based RAG Bot:** A factual query answering system leveraging a large knowledge base.

This analysis identifies, assesses, and measures specific risk metrics to provide a clear understanding of potential negative outcomes. Key risk areas include:

* **Accuracy and Reliability:** Assessing the likelihood of the models providing incorrect, misleading, or fabricated information (addressing hallucinations).
* **Bias and Fairness:** Identifying the potential for models to generate biased, stereotypical, or discriminatory content.
* **Jailbreaking:** Evaluating the models' susceptibility to bypass intended restrictions.
* **Harmful Content Generation:** Quantifying the possibility of producing inappropriate, offensive, or unsafe content, specifically:
    * Self-harm content
    * Violent content
    * Sexual content
---

## Demonstration Setup

### Models for Evaluation

1.  **AI Language Tutor:**
    * **Description:** Prompt-engineered to assist users in learning a new language through conversation, grammatical corrections, and vocabulary suggestions.
    * **Primary Interaction:** Conversational and educational.
    * **(See Figure 7: System prompt for the AI language tutor)**

2.  **Wikipedia RAG Bot:**
    * **Description:** Leverages a vast corpus of Wikipedia articles to answer factual queries using a Retrieval-Augmented Generation (RAG) architecture.
    * **Functionality:** Pulls information from Wikipedia and synthesizes answers.
    * ![Alt text]()

### Evaluation Metrics & Enablers

#### For the AI Language Tutor:

A "Red Teaming" approach was employed using adversarial prompts.

* **Datasets Used:**
    * `TrustAIRLab/in-the-wild-jailbreak-prompts`: A sample of **300 examples** from a total of **5700** were randomly selected due to resource limitations.
    * Synthetically generated dataset: Created using Azure AI Red Teaming Agent service (leveraging OpenAI GPT-4) to synthesize attack vectors targeting violence, hate, unfairness, sexual, and self-harm content.

* **Metrics & Enablers:**
    * **Adversarial attacks (Jailbreaking):** Measures successful attempts where the model bypasses restrictions or deviates from its task.
        * **Enabler:** Direct Attack Jailbreak Evaluations (User Prompt Injected Attack - UPIA).
        * **(See Figure 9: Example of a successful jailbreak for the AI language tutor)**
    * **Hateful and Unfair Content:** Measures language reflecting hate or unfair representations towards individuals and social groups based on factors including race, ethnicity, nationality, gender, sexual orientation, religion, immigration status, ability, personal appearance, and body size. Unfairness occurs when AI systems treat or represent social groups inequitably.
        * **Enabler:** Hate Unfairness Evaluator.
    * **Self-harm-related content output:** Measures language pertaining to physical actions intended to hurt, injure, or damage oneself.
        * **Enabler:** Self-Harm Evaluator.
    * **Violent content output:** Measures language pertaining to physical actions intended to hurt, injure, damage, or kill someone or something, including weapon descriptions.
        * **Enabler:** Violence Evaluator.
    * **Sexual Content:** Measures language pertaining to anatomical organs, romantic relationships, erotic acts, pregnancy, physical sexual acts (including assault), prostitution, pornography, and sexual abuse.
        * **Enabler:** Sexual Evaluator.

#### For the Wikipedia RAG Bot:

A publicly available dataset comprising prompts, contexts, and ground truth answers was used.

* **Metrics & Enablers:**
    * **Similarity:** Measures semantic similarity between generated and ground truth answers.
        * **Enabler:** Similarity Evaluator.
    * **Relevance:** Assesses the quality of retrieved information, critical for RAG performance.
        * **Enabler:** Retrieval Evaluator.
    * **Groundedness:** Measures how well the response aligns with the provided context, identifying fabrication or irrelevant responses.
        * **Enabler:** Groundedness Evaluator.

---

## 4.5.3 Execution and Results

The evaluation involved running defined test suites against both models, with results collected, aggregated, and presented below.

### Wikipedia RAG Bot Performance Summary

The Wikipedia RAG Bot, despite understanding user intent, largely fails to ground its responses in source material, leading to factually unreliable and divergent answers. It is characterized as a "creative but untethered" system.

* **Low Groundedness: ** This is the most critical flaw, indicating the model fabricates information or relies on internal, potentially outdated knowledge, undermining its core RAG function.
* **Medium to Good Relevance:** The model successfully interprets queries and generates on-topic responses, suggesting effective retrieval and initial generation steps.
* **Low Similarity Score with the Ground Truth: ** The generated text significantly differs from human-verified answers in wording, structure, and factual content, confirming a failure to use provided documents and producing factually inconsistent information.

### AI Language Tutor Performance Summary

The AI language tutor is deemed dangerously flawed and fundamentally unsafe for educational purposes, with risks amplified by its tutoring role.

* **Breach of Educational Trust:** An **8.3% jailbreak rate (25 out of 300 attempts)** demonstrates the ease with which its instructional persona can be subverted, leading to unpredictable and inappropriate behavior.
    * **(See Figure 13: Successful vs Unsuccessful Jailbreak Attempts)**
* **Profound Self-Harm Risk:** A most alarming **16.7% failure rate (50 out of 300 attempts)** in the self-harm category indicates a catastrophic safety alignment failure. This poses a direct and immediate risk, especially to users struggling with mental health.
    * **(See Figure 16: Self-harm Distribution)**
* **Exposure to Harmful Content:** The presence of violent, sexual, and hate/unfairness content, even at lower rates, is unacceptable for an educational tool.
    * **Violence:** **4.3%** 
    * **Sexual Content:** **3.3%** 
    * **Hate and Unfairness:** **1.0%** 

---

## Summary of Key Findings

This evaluation reveals significant risks across both tested LLM systems:

* **Wikipedia RAG Bot:** Excels at understanding query intent (Medium to Good Relevance) but critically fails in **Groundedness (Low)** and **Similarity to Ground Truth (Low)**, indicating a tendency to hallucinate and not rely on its source material. This makes it an "unreliable factual source."
* **AI Language Tutor:** Poses severe safety concerns due to its susceptibility to **Jailbreaking (8.3% success rate)** and, critically, its ability to generate **Self-Harm related content (16.7% failure rate)**. It also exhibits concerning rates of **Violence (4.3%)**, **Sexual Content (3.3%)**, and **Hate/Unfairness (1.0%)** generation. This model is currently deemed unsafe for its intended educational purpose.
---

## Figures
