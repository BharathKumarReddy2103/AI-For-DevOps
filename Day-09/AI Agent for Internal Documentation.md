# Building an AI Agent to Understand Internal Documentation

## Introduction

In modern DevOps and Cloud-native organizations, internal documentation is essential. It includes processes, tool usage, configurations, and platform-specific instructions that guide developers, SREs, and newcomers. However, navigating through hundreds of pages of internal docs can be overwhelming.

This article walks you through building an **AI-powered agent** that reads **internal organizational documentation** (e.g., for an observability platform named *Viraala*) and answers user queries in natural language. This is achieved using **CrewAI**, an open-source agentic framework, and **LLaMA 3**, a local LLM. The agent runs securely without sending data to external services like OpenAI, making it ideal for enterprises concerned with data privacy.

## Problem Statement

Organizations maintain confidential internal documentation for:

- Onboarding new employees
- Operating internal tools (e.g., monitoring platforms)
- Standardizing engineering practices

Accessing and understanding this documentation becomes difficult over time. Public LLMs (e.g., ChatGPT) can't be used directly due to data confidentiality concerns. This raises a need for a secure, local AI agent that can:

- Ingest internal documentation (PDF format)
- Understand and summarize key concepts
- Answer user queries contextually

## Solution Overview

We’ll develop an AI agent that can:

- Read internal documentation stored as PDF
- Respond to user queries contextually
- Be trained with examples for improved accuracy
- Operate securely using a local LLM (LLaMA 3)
- Be extended using CrewAI, a beginner-friendly agentic framework

## Step-by-Step Implementation

### 1. Create Fake Internal Documentation

To simulate a real-world observability tool, we use prompt engineering with ChatGPT to generate a fake document titled:

**"Viraala Observability Platform Documentation"**

Topics covered:

- What is Viraala Platform?
- Why is it better than Prometheus?
- Metrics, logs, traces support
- Comparisons with other tools

Ensure the document is:

- Saved in PDF format
- At least 1,000 lines long for rich content

> This avoids using publicly available PDFs that could already exist in LLM training datasets.

---

### 2. Set Up the Development Environment

**Install prerequisites:**

```bash
python3 --version  # Ensure version is between 3.10 and 3.13
pip install virtualenv
```

**Create a virtual environment:**

```bash
python3 -m venv .ai_sandbox
source .ai_sandbox/bin/activate
```

**Install CrewAI:**

```bash
pip install crewai
```

---

### 3. Clone the Example CrewAI Project

CrewAI has example agents in its GitHub repository. We’ll clone and modify the [MetaQuest knowledge agent](https://github.com/joaomdmoura/crewAI/tree/main/examples/metaquest_knowledge):

```bash
git clone https://github.com/joaomdmoura/crewAI.git
cd crewAI/examples/metaquest_knowledge
```

**Replace the sample PDF:**

```bash
mv ~/Downloads/Viraala_Observability_Platform_Documentation.pdf ./knowledge/
```

---

### 4. Update Agent Configuration

#### `config/agents.yaml`

```yaml
name: "ViraalaToolExpert"
role: "Provide the best possible answers about Viraala platform."
goal: "Help users understand and use the Viraala Observability Platform."
backstory: "You are an expert in Viraala, trained to answer technical questions from internal documentation."
```

#### `config/tasks.yaml`

```yaml
name: "AnswerQuestions"
description: "Answer questions about the Viraala platform."
expected_output: "Clear, concise answers based on internal documentation."
```

---

### 5. Modify the Python Code

#### `main.py`

Replace hardcoded input with dynamic user input:

```python
question = input("Please enter your question: ")
```

#### `crew.py`

Update PDF source:

```python
source = "knowledge/Viraala_Observability_Platform_Documentation.pdf"
```

Ensure the agent/task names match the updated configuration.

---

### 6. Configure Local LLaMA 3

**Create a `.env` file**:

```env
PROVIDER=openai
MODEL_NAME=llama3
MODEL_PATH=http://localhost:11434/api/generate
```

**Run LLaMA 3 locally**:

```bash
ollama pull llama3
ollama run llama3
```

---

### 7. Run the Agent

```bash
crewai install
crewai run
```

Example queries:

- "What is Viraala tool?"
- "How is Viraala better than Prometheus?"
- "What metrics are supported in Viraala?"

The agent will read the PDF and respond with contextual answers.

---

## Best Practices

- **Use prompt engineering** to generate realistic training data.
- **Fine-tune agent answers** using CrewAI’s `train` and `test` configurations.
- **Secure your models** by running everything locally with LLaMA.
- **Use modular architecture**: config files for agents and tasks keep the project clean and extensible.
- **Avoid hardcoding questions**; always take dynamic user input.
- **Use virtual environments** to isolate dependencies.

---

## Practical Use Cases

- **Onboarding bots** that help new hires understand internal tools
- **DevOps documentation assistants** for in-house platforms like CI/CD tools, custom monitoring solutions, etc.
- **Secure knowledge agents** in finance, healthcare, or any industry with strict data confidentiality requirements

---

## Conclusion

Building an internal AI documentation agent is no longer a complex task. With frameworks like **CrewAI** and local models like **LLaMA 3**, DevOps teams can quickly deploy secure, intelligent agents that enhance knowledge accessibility without compromising confidentiality.

This solution is scalable, customizable, and perfect for organizations looking to implement AI responsibly within their engineering ecosystems.
