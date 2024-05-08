# README: Multi-Hop RAG Pipeline using DSPy

This code demonstrates a Multi-Hop Retrieval-Augmented Generation (RAG) pipeline using the DSPy library. The pipeline retrieves relevant passages from a knowledge base and generates answers to questions based on the retrieved contexts.

## Prerequisites

Before running the code, make sure you have the following dependencies installed:

```pip install -r requirements.txt```

## Code Overview

1. Importing Required Libraries:
   - The code imports necessary libraries such as `RecursiveCharacterTextSplitter`, `WikipediaLoader`, `QdrantClient`, `QdrantRM`, and various modules from the DSPy library.

2. Data Preparation:
   - The code uses the `WikipediaLoader` to load Wikipedia data about "Leonardo Di Caprio".
   - The loaded data is split into chunks using the `RecursiveCharacterTextSplitter`.
   - The document contents and IDs are extracted and stored in separate lists.

3. Qdrant Vector Store:
   - The code initializes a Qdrant client using the ":memory:" option, which creates an in-memory database.
   - The document contents and IDs are added to a Qdrant collection named "leo_collection".

4. Retrieval Model:
   - The code creates a `QdrantRM` retrieval model using the "leo_collection" and the Qdrant client.
   - The retrieval model is configured to retrieve the top 10 relevant passages.

5. Language Model:
   - The code initializes an `OllamaLocal` language model from DSPy with specific parameters.
   - The language model is configured using `dspy.settings.configure()`.

6. Retrieval Function:
   - The code defines a `get_top_passages()` function that retrieves the top passages for a given question using the `dspy.Retrieve` module.
   - The function prints the retrieved passages along with their ranks.

7. Signature Classes:
   - The code defines two signature classes: `GenerateAnswer` and `GenerateSearchQuery`.
   - These classes specify the input and output fields for generating answers and search queries.

8. Simplified Baleen Module:
   - The code defines a `SimplifiedBaleen` module that inherits from `dspy.Module`.
   - This module implements a simplified version of the Baleen algorithm for RAG.
   - It uses the `GenerateSearchQuery` and `GenerateAnswer` signature classes to generate search queries and answers. Each search query is used to gather the relevant context.
   - The module performs multiple hops of retrieval and generation to answer a given question.

9. Usage Example:
   - The code demonstrates how to use the `SimplifiedBaleen` module to answer a specific question.
   - It creates an uncompiled instance of `SimplifiedBaleen` and calls it with the question.
   - The predicted answer and retrieved contexts are printed.

10. Inspecting Language Model History:
    - The code uses `ollama_model.inspect_history()` to inspect the last 3 interactions with the language model.

## Usage

To use this RAG pipeline:

1. Install the required dependencies mentioned in the prerequisites section.
2. Run the code in a Python environment.
3. Modify the `my_question` variable to ask your desired question.
4. Run the code and observe the predicted answer and retrieved contexts.

Note: Make sure you have a stable internet connection to load the Wikipedia data and access the Qdrant client.

## Customization

You can customize the RAG pipeline by modifying the following parameters:

- `chunk_size` and `chunk_overlap` in the `RecursiveCharacterTextSplitter` to adjust the size and overlap of document chunks.
- `k` parameter in `QdrantRM` and `dspy.Retrieve` to change the number of top passages retrieved.
- Language model parameters in `OllamaLocal` to fine-tune the generation process.
- `passages_per_hop` and `max_hops` in `SimplifiedBaleen` to control the number of passages retrieved per hop and the maximum number of hops.

Feel free to experiment with different configurations and adapt the code to your specific use case.

