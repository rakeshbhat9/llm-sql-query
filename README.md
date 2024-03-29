# llm-sql-query

## Reference
The code in this project refers to langchain sql-ollama template.
[sql-ollama](https://github.com/langchain-ai/langchain/tree/master/templates/sql-ollama)
   

## Environment Setup

To run the notebooks in this repo, you will need to set up Ollama and a database.

1. Follow instructions [here](https://ollama.com/download) to download Ollama.

2. Download your LLM of interest:

    * This package uses `duckdb-nsql: ollama pull duckdb-nsql`
    * You can choose from many LLMs [here](https://ollama.ai/library)

3. This package is using a  Postgres instance running on LAN. dvdrental database is used which is widely available on the internet.

4. As the notebook is running opensource LLM locally, the system should have atleast 8 GB RAM [LINK](https://ollama.com/library/orca-mini#:~:text=the%20sky%20blue%3F%22%0A%20%20%20%7D%27-,Memory%20requirements,-7b%20models%20generally). 

5. To-Do
    - Test on table join queries 
    - Test with llama2, mistral and zephyr to understand best model for this use-case.
    
6. duckdb-nsql
    - Had to update custom parser to remove extra \\ generated in SQL Query.
    - Doesn't get the queries right - Always queries film_actor instead of actors. This leads to chain failure.
    ```python
    sql_chain.invoke({"question": "How many films has Penelope starred in?"})
    " SELECT COUNT(DISTINCT film_id) FROM film_actor WHERE first_name = 'Penelope' AND last_name = (SELECT last_name FROM actor WHERE actor.actor_id = film_actor.actor_id);"

    ```