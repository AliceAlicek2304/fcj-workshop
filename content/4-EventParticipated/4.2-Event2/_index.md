---
title: "Event 2"
date: "2025-09-10"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# AWS CLOUD MASTERY SERIES #1 EVENT SUMMARY (15/11/2025)

## PART I: GENERATIVE AI WITH AMAZON BEDROCK

### 1. Foundation Model and Prompt Engineering

The event posed a key question: **What knowledge should be learned to fit the external cloud environment?**

*   **Foundation Model:** Definition of foundation models.
*   **Prompt Engineering Techniques:** Techniques to optimize input for AI models.
    *   **Few-shot Prompting:** Providing a few specific examples to guide the model.
    *   **Chain of Thought (CoT):** Asking the model to show reasoning steps to arrive at the final answer, helping to increase accuracy.

### 2. Retrieval Augmented Generation (RAG)

The event delved into RAG and the concept of Embedding.

*   **What is Embedding?** (Concept introduced).
*   **Tools supporting RAG:**
    *   **Amazon Titan Embedding** (tool introduced).
*   **RAG in Action:** Illustration of the RAG workflow, including steps:
    1.  **User Query**
    2.  **Embedding Model** (converts question into vector)
    3.  **Vector Store / Knowledge Source** (searches for relevant information)
    4.  **Prompt Template / Prompt Alignment Model** (inserts found information into prompt)
    5.  **Large Language Model (LLM)**
    6.  **Response** (answer supplemented with external knowledge).
*   **RetrieveAndGenerate API:** An API introduced to implement RAG.

### 3. Amazon Bedrock AgentCore

Amazon Bedrock AgentCore is a platform that helps realize your AI applications by taking AI agents from the experimental stage to production.

*   **Function:** Strong support for runtime, memory, tools, security, and monitoring for agents.

## PART II: OTHER PRETRAINED AI SERVICES

The event also introduced a range of specialized, pre-trained AI services from Amazon, along with their corresponding costs:

| AI Service | Main Function | Reference Price |
| :--- | :--- | :--- |
| **Amazon Rekognition** | Image and video analysis, labeling, automatic sensitive content censoring. | $0.0013/image (<1M images) |
| **Amazon Translate** | Real-time text recognition and translation. | $15/1M characters |
| **Amazon Textract** | Extract texts and layouts from documents. | $0.05/page (<1M pages) ⟹ needs consideration. |
| **Amazon Transcribe** | Speech to text. Supports sensitive word censoring, voice recognition, and automatic translation. | $0.024/minute (<250k minutes) |
| **Amazon Polly** | Text-to-speech. | $4 per 1M characters (first 1M free). |
| **Amazon Comprehend** | Natural Language Processing (NLP). Understands text, video, keyword filtering. | $0.0001/100 characters + $0.35/1h |
| **Amazon Kendra** | SEARCH function (or question answering). | $30/index/month + $0.35/1h (extremely expensive) |
| **Amazon Personalize** | Personalize user experience (like TikTok, Shopee, Facebook). | $0.24/training hour + $0.05/GB/recommendation |
| **Amazon Lookout Family** | Includes Lookout for Equipment and Lookout for Vision (for monitoring and anomaly detection). | (No specific price in notes) |
| **Pipecat** | (Introduced, no functional details). | (No specific price in notes) |
