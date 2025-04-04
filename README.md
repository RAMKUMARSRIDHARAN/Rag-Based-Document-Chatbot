# Rag-Based-Document-Chatbot

Overview: 
This chatbot implements a Retrieval-Augmented Generation (RAG) framework using Google's Gemini-1.5-Pro model. It allows users to upload PDFs, extracts text, converts it into vector embeddings, and retrieves contextually relevant information to answer user queries.

**How to interact with Chatbot**

1. Start the Application: Launch the Streamlit application by running the command:

                _Code : streamlit run <path_to_script.py>_

2. Replace <path_to_script.py> with the path to the script file.

3. Enter Your Google API Key: Securely enter your Google API key when prompted. This key enables the application to access Google's Generative AI models.

4. Upload PDF Documents: You can upload one or multiple PDF documents. The application will analyze the content of these documents to respond to queries.

5. Ask Questions: Once your documents are processed, you can ask any question related to the content of your uploaded documents.

**Technical Stack**
 
    •	Python – Ideal for AI-based applications due to its rich ecosystem of ML and NLP libraries.
    •	Streamlit – Used for building the web-based UI for document upload and interaction.
    •	PyPDF2 – Extracts text from PDFs.
    •	Google Gemini API (ChatGoogleGenerativeAI) – Generates intelligent responses.
    •	LangChain (load_qa_chain) – Manages the retrieval and answering process.
    •	FAISS (langchain.vectorstores.FAISS) – Stores and retrieves document embeddings efficiently

**Prompt Template Used**

Prompt_template = """
    Answer the question as detailed as possible from the provided context, make sure to provide all the details. 
    If the answer is not in the provided context, just say, "answer is not available in the context".
    Don't provide incorrect answers.
    Context:\n {context}?\n
    Question: \n{question}\n
    Answer:
"""

**Response Structuring Approach**
  The chatbot retrieves relevant content before passing it to Gemini-1.5-Pro for answer generation. The response structure ensures:
    1.	Context-Aware Answers: Uses a prompt to ensure responses stick to the document and avoid hallucinations.
    2.	Structured Output:
          o	If answer is found: The model provides a well-structured, concise response.
          o If no answer is found: It explicitly states: "Answer is not available in the context" instead of generating false information.
