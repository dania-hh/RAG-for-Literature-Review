## RAG System for Literature Review

The code below implements a Retrieval-Augmented Generation (RAG) system, designed to support literature review tasks by allowing access to documents published after the model’s training data cutoff, as well as documents that require special access online (e.g., documents behind paywalls or requiring credentials). This system enhances the access to contextual information from diverse documents, significantly boosting the accuracy and quality of responses from language models.

In my application, I utilize this system to process over 30 research papers on jamming source localization.

### Purpose of the RAG System

The main function of this RAG system is to aid in the review and analysis of research papers, particularly those concerning jamming source localization, though it can be adapted to other fields as well. Its objective is to efficiently gather and synthesize relevant information, thereby supporting researchers and practitioners in staying 'in-the-know' of the newest developments and techniques in this specialized area of study.

Sure, here's the updated description with the components listed in the order that they appear in the code:

### Core Components of the RAG System

- **OpenAI Embeddings (LLM)**: Utilizes OpenAI's embeddings, which serve as the foundation for generating context-aware text and creating semantic embeddings. These embeddings are crucial for retrieving the most relevant information related to user queries.

- **FAISS Vector Store**: The Facebook AI Similarity Search (FAISS) Vector Store is critical for storing and swiftly retrieving document embeddings, thus allowing the system to find and pull the most pertinent documents based on content similarity to user queries.

- **Retriever**: Functions like the system's search engine, querying the FAISS Vector Store to fetch documents that match the user's input, ensuring the responses are supported by the most relevant data.

- **Cache-Backed Embedder**: Converts text data into vector format before embedding it into the vector store, making it comprehensible and retrievable by the system for future queries.

- **Document Processing Pipeline**: Handles the processing of documents with several key subcomponents:
  - **Document Loader**: Loads and preprocesses the research papers, making them ready for embedding and retrieval.
  - **Text Splitter (Document Chunker)**: Splits extensive research papers into smaller, more manageable chunks, which are easier to process for embedding and retrieval.
  - **SimpleDocument Class**: Organizes text chunks along with their metadata, assigning a unique key to each for efficient management and retrieval.

- **LLM Setup (ChatOpenAI)**: Utilizes the ChatOpenAI model, specifically gpt-3.5-turbo, set to a temperature of 0.2 and capable of handling up to 4096 tokens. This model enhances the generation of contextual responses based on the retrieved documents.

- **Conversational Retrieval Chain**: Integrates the LLM, memory, and retriever with callback functions, enhancing the dynamic interaction between the user and the retrieval system. This chain also returns source documents for transparency and deeper analysis.
  - **Memory Management**: Features a Conversation Buffer Memory that tracks the history of user queries and responses, thereby optimizing the contextual relevance of each interaction.
  - **Output Handler**: Employs a StdOutCallbackHandler to directly print responses, facilitating immediate feedback from the system.

### Text Splitters Experimentation
The project experiments with two types of text splitters—RecursiveCharacterTextSplitter and CharacterTextSplitter—to identify the best approach for dividing large text documents into manageable chunks. Through a series of tests chunk_overlap, each splitter's performance is evaluated based on metrics like average chunk size (set to average page content length), number of chunks, and evaluation time. This process aims to find the optimal balance between efficiency (minimizing computational overhead) and granularity (ensuring detailed segmentation), enhancing both the system's performance and retrieval accuracy.

A higher number of chunks means the text is split into finer, more detailed parts. This can be beneficial for analyzing specific sections in depth but might increase processing time and complexity. Larger chunks reduce the processing load as there are fewer pieces to manage and index, which can speed up retrieval tasks. However, too large chunks might miss finer details.

We want to achieve:   
- Adequate granularity without producing an excessive number of small chunks that could slow down the system.
- Manageable chunk sizes that are not too large, maintaining necessary detail for effective analysis and retrieval.

### System Interaction and Workflow

The workflow of the RAG system is tailored to enhance research on jamming source localization by following these steps:

1. **Query Processing**: The system begins by taking a user query related to jamming source localization and converting it into an embedding.
2. **Document Retrieval**: It then retrieves documents that closely match the query's embedding from the vector store, focusing on those most relevant to jamming source localization.
3. **Response Generation**: Leveraging the retrieved documents, the system generates detailed responses that are informed by the latest research findings, helping users synthesize current trends and results in the field.


This RAG system streamlines the accessibility to state-of-the-art research in in jamming source localization or any other relevant field being researched. By simply replacing the research papers in the relevant directory with the specific research topic papers, the literature review stage can be accelerated and the concise information required can be accesses in a much more flexible way.
