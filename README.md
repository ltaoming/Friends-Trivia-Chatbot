# Friends-Trivia-Chatbot

## Overview

This is an AI Chatbot designed specifically for fans of the popular sitcom [Friends](https://en.wikipedia.org/wiki/Friends). It utilizes Retrieval-Augmented Generation (RAG) and Large Language Model (LLM), specifically LLaMA 2, which has been fine-tuned using Replicate. This setup enables the application to deliver precise, context-sensitive responses to intricate questions about the show’s content, plot, and characters. The app is built with Streamlit and includes features such as session chat history and the ability to choose from multiple LLaMA2 API endpoints on Replicate.

Ask anything about the **Friends** series on our app [here](https://friends-rag.streamlit.app/)!

## How to Start

### Prerequisites

- Relative API key(s) (optional; e.g. for embedding model)
- Python 3.11 or higher
- Git Large File Storage (LFS) for handling large datasets and model files

### Installation

1. Install dependencies.

   - [Optional but recommended] 
      - Create a virtual python environment with 
         ```
            python -m venv .venv
         ```
      - Activate it with 
         ```
            source .venv/bin/activate
         ```
   - Install dependencies with 
      ```
         pip install -r requirements.txt
      ```

2. Create the Chroma DB:
```
python populate_database.py
```

3. Setup before being able to do inference:

   - Case 1: If you choose to run the base Llama 2 model locally, you'll need to have [Ollama](https://ollama.com/) installed and run `ollama serve` in a seperate terminal.

   - Case 2: If you choose to do inference with replicate with our models locally, you'll need to have `REPLICATE_API_TOKEN` setup as an environment variable.

   - Case 3: You can simply test run our deployed project on streamlit: **friends-rag.streamlit.app**.

4. Test run to query the Chroma DB, the below command will return an output based on RAG and the selected model:
```
python query_data.py "Which role does Adam Goldberg plays?"
```

5. Start the App locally:
```
streamlit run app.py
```

### Setup & Configurations
1. For finetuning, we opted to create our own dataset of Question-Answer pairs relevant to the domain, enhancing the effectiveness of RAG.
2. Domain-specific files, including trivia.txt and s1_s2.jsonl, are organized in the data folder. Using Langchain, this data is indexed in a vector database located in the chroma folder, which can be expanded with additional content as needed.
3. The user interface and deployment of the application are handled through Streamlit.
4. Users have the flexibility to choose from several LLaMA2 chat API endpoints, including the base LLaMA2, finetuned LLaMA2, base with RAG, and finetuned with RAG.
5. Each version of the model (base, finetuned, with and without RAG) is hosted on Replicate.
