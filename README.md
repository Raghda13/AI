 Multi-Agent Project Management AI

A Multi-Agent AI system that analyzes project management data and company policies using Retrieval-Augmented Generation (RAG).

The system combines information from a PDF company policy document and an Excel project management dataset, retrieves the most relevant information using semantic search, and uses multiple specialized AI agents to generate professional project analysis reports.

 Project Overview

Project managers often need to analyze large amounts of project data and company policies to identify risks, understand project performance, and make informed decisions.

This project provides an AI-powered assistant that can answer project management questions by combining:

 Company policy documents
 Project management data
 Semantic search with RAG
 Large Language Models
 Multi-Agent architecture
 Automated report generation

Instead of relying on the LLM's internal knowledge, the system retrieves relevant information from the provided project management sources before generating the final response.

 System Architecture


 Features
 Multi-Source Knowledge Base

The system loads information from:

Project_Management_Policy.pdf
Project_Management_Data.xlsx

The PDF is processed using pypdf, while the Excel data is loaded and converted into text for retrieval.

The two sources are combined into a unified knowledge base.

 Retrieval-Augmented Generation (RAG)

The knowledge base is divided into overlapping text chunks.

Each chunk is converted into an embedding using:

sentence-transformers/all-MiniLM-L6-v2

The embeddings are normalized and stored in a FAISS IndexFlatIP vector index.

For every user question, the system retrieves the top relevant chunks before generating an answer.

 Multi-Agent Architecture

The project contains four specialized agents:

1. Planner Agent

Creates a structured plan for answering the user's question.

It identifies:

Required information
What should be analyzed
What the final report should contain
2. Research Agent

Retrieves relevant information from the project knowledge base and extracts:

Policy information
Project data
Important observations

The agent is explicitly instructed not to invent information.

3. Writer Agent

Transforms the research into a professional project management report containing:

Introduction
Key Findings
Project Analysis
Relevant Policy Information
Recommendations
4. Summary Agent

Creates a concise summary containing:

Executive Summary
3–5 Key Findings
Main Recommendations
 Language Model

The project uses:

Qwen/Qwen2-1.5B-Instruct

The model is loaded using Hugging Face Transformers with 4-bit quantization through BitsAndBytesConfig.

This reduces memory requirements and makes the model more practical to run in a Google Colab GPU environment.

 Technologies Used
Technology	Purpose
Python	Core programming language
PyTorch	Deep learning and model inference
Hugging Face Transformers	LLM loading and generation
Qwen2-1.5B-Instruct	Language model
Sentence Transformers	Text embeddings
FAISS	Vector similarity search
pypdf	PDF processing
Pandas	Excel/data processing
OpenPyXL	Excel file support
Gradio	User interface
BitsAndBytes	4-bit model quantization
Google Colab	Development environment
 Installation

Install the required dependencies:

pip install -q transformers accelerate bitsandbytes sentence-transformers faiss-cpu pypdf pandas openpyxl gradio
 Project Structure
AI/

Final_Project.ipynb
 Project_Management_Data.xlsx
 Project_Management_Policy.pdf
 README.md
.gitattributes
Main Files

Final_Project.ipynb

Contains the complete implementation including:

Data loading
Knowledge-base construction
Text chunking
Embedding generation
FAISS indexing
Retrieval
LLM generation
Multi-agent workflow
Testing
Gradio interface

Project_Management_Data.xlsx

Contains the project management data used by the system.

Project_Management_Policy.pdf

Contains the company project management policy used as a knowledge source.
 How It Works
1. Load the Data

The system extracts text from the PDF and reads the Excel dataset.

pdf_text = load_pdf(PDF_PATH)
excel_text = load_excel(EXCEL_PATH)

The sources are then combined into a single knowledge base.

2. Create Text Chunks

The knowledge base is divided into chunks of 150 words with an overlap of 30 words.

chunks = chunk_text(
    knowledge_base,
    chunk_size=150,
    overlap=30
)
3. Generate Embeddings

Each chunk is converted into a vector using:

all-MiniLM-L6-v2

The project generated 229 chunks and 229 FAISS vectors during execution.

4. Retrieve Relevant Information

When a user asks a question, the question is embedded and compared against the FAISS index.

The system retrieves the top 5 relevant chunks.

retrieve(query, k=5)
5. Run the Multi-Agent Workflow

The question then passes through:

Planner
   ↓
Research
   ↓
Writer
   ↓
Summary

The orchestrator controls the complete workflow.

6. Generate the Final Report

The system produces a structured report containing an executive summary and detailed analysis.

The final report can also be saved as:

final_project_report.md
 Example Questions

The system can answer questions such as:

What are the most important project management risks?
Which projects require the most attention?
What does the company policy say about project management?
What recommendations can be made based on the project data?
🖥️ Gradio Interface

The project includes a Gradio interface where users can enter project management questions and generate reports interactively.

The interface contains:

Question input
Generate Report button

The Gradio interface connects directly to the multi-agent workflow and returns the generated report.

🧪 Testing

The system includes a testing section with multiple project-management questions.

The tests check whether the complete system successfully generates a non-empty final report.

Example test questions include:

What are the most important project management risks?
Which projects require the most attention?
What does the company policy say about project management?
What recommendations can be made based on the project data?

The testing logic marks each test as PASS or FAIL depending on whether a valid result is generated.

 Grounded Responses

One of the main goals of the system is to reduce hallucinations.

The Research Agent is instructed to use only the retrieved project management information, distinguish between policy information and project data, and avoid inventing facts.

The Writer Agent is also instructed to base the report only on the research and explicitly state when information is unavailable in the provided sources.

 Example Workflow

For a question such as:

"Analyze the project management data and explain the most important project risks, relevant company policies, and recommended actions."

The system performs:

User Question
      ↓
Planner Agent
      ↓
Retrieve relevant documents
      ↓
Research Agent
      ↓
Analyze project risks + policies
      ↓
Writer Agent
      ↓
Generate detailed report
      ↓
Summary Agent
      ↓
Generate executive summary
      ↓
Final Project Management Report
 Project Goals

This project demonstrates practical experience with:

Retrieval-Augmented Generation (RAG)
Vector databases and semantic search
Large Language Models
Prompt engineering
Multi-Agent AI systems
Document processing
Structured report generation
LLM orchestration
AI application development
Gradio-based interfaces
 Future Improvements

Possible improvements include:

Add more project management data sources
Support additional document formats
Add conversation memory
Add citations to retrieved documents
Add project risk scoring
Add visualization dashboards
Improve retrieval using hybrid search
Add reranking for retrieved documents
Add agent evaluation metrics
Add LangGraph-based agent orchestration
Deploy the application as a web service
Add authentication and user management
 Author

Raghda Elsakka

Computer Science Graduate | AI/ML Engineer

Interested in:

Machine Learning
Deep Learning
Generative AI
LLMs
RAG
AI Agents
Project Highlights

A multi-agent RAG system that transforms project management data and company policies into actionable AI-generated reports.

Built with Python, Hugging Face Transformers, Qwen2, Sentence Transformers, FAISS, PyTorch, and Gradio.

