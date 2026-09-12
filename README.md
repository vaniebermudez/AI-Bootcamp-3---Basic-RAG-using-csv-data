# InvyTrack: Basic RAG with CSV Data

This project is an AI Bootcamp activity that builds a basic retrieval-augmented generation (RAG) assistant for inventory management. The assistant retrieves relevant inventory records from a CSV file and gives them to an OpenAI chat model as context before answering a user question.

## What Was Completed

The notebook, `AI_First_Day_4_Activity_1_Van.ipynb`, demonstrates the following workflow:

1. Install the OpenAI, LangChain, ChromaDB, FAISS, and tokenization dependencies.
2. Load the inventory dataset with pandas.
3. Combine the values from each inventory row into a searchable text document.
4. Create vector embeddings with OpenAI's `text-embedding-3-small` model.
5. Store the embeddings in a FAISS `IndexFlatL2` vector index.
6. Embed a natural-language inventory question and retrieve the 10 most similar records.
7. Build a prompt containing the retrieved context and the user's question.
8. Send the prompt to `gpt-4o-mini` with an inventory-management system prompt.
9. Maintain the conversation messages and print the generated response.

The sample question asks which products are below their reorder level, how much to reorder, and the total value of the required restock.

## Streamlit App

`app.py` turns the notebook experiment into an interactive application called **InvyTrack**. It provides:

- A Home page describing the inventory assistant.
- An About Me page for the project author.
- A Model page with a chat interface.
- OpenAI API-key input through the sidebar.
- Inventory row embeddings and FAISS retrieval at runtime.
- Context-aware responses from `gpt-4o-mini`.

## Project Files

| File | Description |
| --- | --- |
| `AI_First_Day_4_Activity_1_Van.ipynb` | Step-by-step notebook implementation of the basic RAG workflow |
| `app.py` | Streamlit interface for the inventory assistant |
| `inventory_products_dataset.csv` | Inventory records used by the RAG example |
| `insurance_generated_dataset.csv` | Additional generated CSV dataset included for data exploration |
| `config.toml` | Streamlit theme configuration |
| `images/` | Application images and profile assets |
| `requirements.txt` | Python dependencies for the application |

## Inventory Data

The inventory dataset includes fields such as:

- Product ID, name, category, and SKU
- Product description and supplier
- Quantity in stock, reorder level, and reorder quantity
- Unit price and total inventory value
- Warehouse location, restock date, and lead time
- Expiration date, batch number, condition, and barcode

The sample data contains products across hardware, fasteners, supplies, safety gear, welding, tools, and electrical categories.

## Setup

Create and activate a virtual environment, then install the application dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

The notebook also installs the versions used during the activity:

```powershell
pip install openai==0.28.1 tiktoken==0.6.0 langchain==0.1.20 chromadb==0.5.0 faiss-cpu
```

Set an OpenAI API key before running the notebook. In the Streamlit app, enter the key in the sidebar when prompted.

## Run the App

From the project directory:

```powershell
streamlit run app.py
```

Then open the local URL displayed by Streamlit in a browser. Select **Model**, enter an inventory question, and submit it through the chat input.

Example questions:

- Which products need restocking?
- What is the total inventory value for the drill bit set?
- Which products have the shortest lead time?
- How much would it cost to reorder the items below their reorder level?

## RAG Design

```text
CSV inventory data
        |
        v
Row text documents
        |
        v
OpenAI embeddings
        |
        v
FAISS vector index <--- embedded user question
        |
        v
Top matching inventory records
        |
        v
Prompt with context + question
        |
        v
GPT-4o-mini response
```

## Notes and Limitations

- The app uses the legacy `openai==0.28` chat-completions API, matching the activity code.
- The app currently loads the inventory dataset from the original GitHub URL rather than the local CSV file.
- The image paths in `app.py` refer to the original `Day4/images/` layout; adjust them to `images/` when running this repository directly if the assets are not found.
- The retrieved records are supplied to the language model as context. The model does not automatically perform a database update or persist changes to the CSV.
- Do not commit API keys or other credentials to the repository.

## Author

Vanessa Althea Bermudez  
AI Enthusiast / Data Scientist
