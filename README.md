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
    - Really bad for second chain, hence using mistral.
    - Even after specific prompts always uses different case for variable in sql query which leads to no results.
    - Might need to play around with temperature as even for a simple questions end up getting diff SQL query in chain one.
    ```python

        sql_chain.invoke({"question": "How many films were released in 2006?"})
        ' SELECT COUNT(*) FROM film WHERE release_year = 2006;'

        print(sql_run_chain.invoke({"question": "Give me breakdown of films by release year"})) 
        'Errors out' 

        # Per langsmith, below is the query returned when invoked in final chain.
        ' SELECT 
            * 
        FROM (
            PIVOT film ON release_year USING COUNT(*) GROUP BY title
        ) pivot_alias;
        '
    ```
    - Fixed the above issue by adding camelcase_conditions parser. Doesn't like some actors.