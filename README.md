# Rag-Based-Document-Chatbot

**1. Source Code Documentation**

Overview: 
This chatbot implements a Retrieval-Augmented Generation (RAG) framework using Google's Gemini-1.5-Pro model. It allows users to upload PDFs, extracts text, converts it into vector embeddings, and retrieves contextually relevant information to answer user queries.

Key Functionalities:
i)	PDF Processing
  o	Extracts text from uploaded PDFs.
  o	Splits text into manageable chunks for efficient retrieval.

ii) Vector Store (FAISS) Creation
  o	Converts text into embeddings using GoogleGenerativeAIEmbeddings.
  o	Stores vectors using FAISS for efficient retrieval.

iii) Query Processing & Response Generation
  o	Uses similarity search in FAISS to find relevant text.
  o	Passes retrieved content to Gemini-1.5-Pro for answer generation.

iv) Streamlit UI
  o	Provides an interactive interface for users to upload PDFs and ask questions.

**2. Instructions for Running the Chatbot**

Step 1: Install Required Libraries
    Run the following command in your terminal:
      Code:  pip install streamlit PyPDF2 langchain langchain_google_genai google-generativeai faiss-cpu

Step 2: Obtain a Google API Key
    •	Visit MakerSuite to generate your API key.

Step 3: Run the Chatbot
    Save the provided script as chatbot.py and execute:
      Code: streamlit run chatbot.py

Step 4: Interact with the Chatbot
  1.	Enter your Google API key.
  2.	Upload one or more PDF files.
  3.	Click "Submit & Process" to generate the knowledge base.
  4.	Ask questions, and the chatbot will return relevant answers.

**3. Tech Stack Choices**
🔹 Programming Language
    •	Python – Ideal for AI-based applications due to its rich ecosystem of ML and NLP libraries.
🔹 Frontend & UI
    •	Streamlit – Used for building the web-based UI for document upload and interaction.
🔹 Document Processing
    •	PyPDF2 – Extracts text from PDFs.
🔹 AI & NLP
    •	Google Gemini API (ChatGoogleGenerativeAI) – Generates intelligent responses.
    •	LangChain (load_qa_chain) – Manages the retrieval and answering process.
🔹 Vector Storage & Retrieval
    •	FAISS (langchain.vectorstores.FAISS) – Stores and retrieves document embeddings efficiently.

**4. Response Structuring Approach**
  The chatbot retrieves relevant content before passing it to Gemini-1.5-Pro for answer generation. The response structure ensures:
    1.	Context-Aware Answers: Uses a prompt to ensure responses stick to the document and avoid hallucinations.
    2.	Structured Output:
          o	If answer is found: The model provides a well-structured, concise response.
          o If no answer is found: It explicitly states: "Answer is not available in the context" instead of generating false information.

**Prompt Template Used**

Prompt_template = """
    Answer the question as detailed as possible from the provided context, make sure to provide all the details. 
    If the answer is not in the provided context, just say, "answer is not available in the context".
    Don't provide incorrect answers.
    Context:\n {context}?\n
    Question: \n{question}\n
    Answer:
"""

**5. Challenges Faced & Solutions Implemented**
   
🔸 Challenge 1: Google API Model Not Found (404 Error)
      •	Problem: "models/gemini-pro is not found for API version v1beta".
      •	Solution: Updated the API to use gemini-1.5-pro, ensuring compatibility with the latest version.
🔸 Challenge 2: FAISS Serialization Warning
      •	Problem: FAISS raised an error requiring allow_dangerous_deserialization=True.
      •	Solution: Explicitly enabled safe deserialization by verifying the source before loading FAISS:
            Code: new_db = FAISS.load_local("faiss_index", embeddings, allow_dangerous_deserialization=True)
🔸 Challenge 3: PDF Text Extraction Issues
      •	Problem: Some PDFs didn’t extract text properly due to encoding issues.
      •	Solution: Used extract_text() inside a loop to process each page separately.
🔸 Challenge 4: Slow Response Time
      •	Problem: Long texts took too much time to process.
      •	Solution: Optimized chunking strategy using:
          Code: text_splitter = RecursiveCharacterTextSplitter(chunk_size=10000, chunk_overlap=1000)

This ensured better balance between context length and retrieval accuracy.
