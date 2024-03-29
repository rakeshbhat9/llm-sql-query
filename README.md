# llm-sql-query

## Reference
The code in this project refers to langchain sql-ollama template.
[sql-ollama](https://github.com/langchain-ai/langchain/tree/master/templates/sql-ollama)
   

## Environment Setup

To run the notebooks in this repo, you will need to set up Ollama and a database.

1. Follow instructions [here](https://ollama.com/download) to download Ollama.

2. Download your LLM of interest:

    * This package uses `gemma:7b`: `ollama pull gemma:7b`
    * You can choose from many LLMs [here](https://ollama.ai/library)

3. This package is using a  Postgres instance running on LAN. The data in bitcoin is sourced from Kaggle dataset. But you should be able to use any database/table, as the code is agnostic to the dataset used.

4. As the notebook is running opensource LLM locally, the system should have atleast 8 GB RAM [LINK](https://ollama.com/library/orca-mini#:~:text=the%20sky%20blue%3F%22%0A%20%20%20%7D%27-,Memory%20requirements,-7b%20models%20generally). 

5. To-Do
    - Test on table join queries 
    - Test with llama2, mistral and zephyr to understand best model for this use-case.