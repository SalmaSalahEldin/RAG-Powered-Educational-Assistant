# RAG-Powered-Educational-Assistant

## Purpose and Overview

The **RAG-Powered Educational Assistant** is designed to revolutionize the way educational content is processed and utilized. This system automates the extraction of main topics from books or documents and generates diverse, metadata-rich questions and answers. It’s built to handle complex educational materials, providing features like confidence scoring for questions, detailed clarifications for answers, and maintaining a transparent link to the original content.

This system is a blend of cutting-edge AI frameworks and tools, tailored to enhance learning experiences for both educators and learners. From managing files to interacting with structured data, this assistant is an all-in-one solution for creating meaningful and engaging educational content.


## System Features

### 1. **File Management**
The system offers robust file management capabilities, allowing users to upload books or documents for processing. It ensures that content is split into manageable chunks and stores embeddings for efficient retrieval.

### 2. **Structured Data Handling**
The system is equipped to handle complex structured data such as multi-page tables, merged cells, and intricate layouts. These are preserved during extraction and stored in a PostgreSQL database for future interaction and analysis.

### 3. **SQL Agent for Data Interaction**
The SQL agent interacts intelligently with the stored structured data, enabling queries and meaningful insights from complex datasets. It serves as the backbone for managing and utilizing structured content effectively.

### 4. **Main Agent with Tools for Topic Extraction and Question Generation**
This module serves as the core of the system:
- Extracts **main topics** from uploaded materials.
- Generates diverse **question types** (e.g., MCQs, open-ended, true/false) with metadata.
- Provides **clarifications and confidence scores** for each question and answer.
- Links each question to the relevant **source content**, ensuring traceability.
- Outputs results in a structured JSON format, organized by topic.


## Tools and Frameworks Chosen

- **LangChain**: A framework for building applications with large language models (LLMs). It provides tools for text splitting, document processing, and interacting with vector stores like Chroma.
  
- **Azure Document Intelligence**: A suite of AI-powered tools from Microsoft Azure to extract structured data (e.g., tables, text) from PDFs, including complex documents with merged cells.

- **Chroma**: A vector store used to persist document embeddings and perform fast similarity search. It stores the chunks of text generated from PDFs and the corresponding embeddings.

- **PyMuPDF (fitz)**: A Python library for reading, extracting, and processing PDF files. It's used to load PDFs, extract text, and split it into chunks.

- **SQLAlchemy / psycopg2**: A library to interact with PostgreSQL databases. It’s used to store and manage structured data, such as tables extracted from PDFs.
  
- **Pydantic Models**: Pydantic schemas (e.g., `GetTopicSchema`, `GetQuestionSchema`, `EmptyArgsSchema`) are used to validate and structure the data, ensuring that any input or output adheres to the expected format.


## Setup Instructions

### 1. Install Dependencies

Before running the script, ensure all required dependencies are installed. To do this, run the following command to install the necessary packages from the `requirements.txt` file:

pip install -r requirements.txt

### 2. Create a postgres database
Create a PostgreSQL database to store structured data, such as complex tables with merged cells, ensuring proper handling of such data from any PDF.

Note that this will be managed using the SQL_Agent file, which will interact with and process the data. Keep this in mind for later steps.

If you're working with a very simple PDF that doesn't contain complex tables or feel this step is unnecessary, you can comment out this part in File_service file.

### 3. Modify the .env File
replace data in .env file with your own credentials

### Uploading a Book to Chroma
To upload any book to Chroma, follow these steps:

Ensure the File_Service file is correctly set up and the necessary dependencies are installed.

In the File_Service file, 

Provide the file_path of the PDF file you want to upload. This path should point to the location of the PDF on your system.

uncomment the following two lines to upload a PDF file:
chatbot = AiCompanyFileService()
response = asyncio.run(chatbot.document_uploading(file_path))
print(response)

Run the script, and the book will be processed, its content split into chunks, and embeddings will be stored in Chroma.



### Deleting Files
uncomment the following two lines to delete a PDF file:
response = chatbot.delete_pdf_for_company(file_path)
print(response)

Run the script, and the specified file will be deleted from both Chroma and the PostgreSQL database



### Running the Main Agent with Tools for Extracting Topics and Generating Questions
To extract the main topics and generate questions from a PDF, follow these steps:

Ensure the necessary files are set up and dependencies are installed.

Run the Tools file to activate the main agent, which will handle the topic extraction and question generation

The main agent will process the PDF, extract key topics, and generate relevant questions based on the content of the book.


## Approaches to Interact with Structured Data in the Future

Handling structured data such as complex tables and merged cells in PDFs requires special attention to ensure that the data is properly parsed, stored, and made accessible for future tasks. By organizing and processing this data separately at the beginning, we can ensure its integrity and usability across different stages of document analysis and processing.

The **SQL_Agent** file provides a simple implementation of how we can interact with structured data. This agent currently handles the parsing of structured data from PDFs, stores it in a PostgreSQL database, and can be easily adjusted to extend its functionality for future use cases. 

By continuing to evolve this SQL_Agent, we can ensure that structured data is not only accurately captured but also maximized in its utility for multiple tasks such as topic extraction, question generation, and further analysis. This approach will play a crucial role in unlocking the full potential of document data processing in future applications.









