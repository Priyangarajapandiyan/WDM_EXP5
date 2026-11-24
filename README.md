### EX5 Information Retrieval Using Boolean Model in Python
        print("\nDocument-Term Matrix:")
        print(df)

    def print_all_terms(self): # Added this function as a method within the class
        print("\nAll indexed terms:")
        print(list(self.index.keys()))

    def boolean_search(self, query):
        # Preprocessing
        query = query.lower()
        query = re.sub(r'\band\b', '&', query)
        query = re.sub(r'\bor\b', '|', query)
        query = re.sub(r'\bnot\b', '-', query)

        # Replace terms with document sets
        tokens = re.findall(r'\w+|[&|\-()]', query)
        processed_tokens = []
        for token in tokens:
            if token.isalpha():
                docs = self.index.get(token, set())
                processed_tokens.append(f"set({docs})")
            else:
                processed_tokens.append(token)

        # Evaluate the boolean expression
        final_expr = " ".join(processed_tokens)
        try:
            result_set = eval(final_expr)
            return result_set
        except:
            print("Invalid query syntax.")
            return set()

if __name__ == "__main__":
    indexer = BooleanRetrieval()

    documents = {
        1: "Python is a programming language",
        2: "Information retrieval deals with finding information",
        3: "Boolean models are used in information retrieval"
    }

    for doc_id, text in documents.items():
        indexer.index_document(doc_id, text)

    indexer.create_documents_matrix()
    indexer.print_documents_matrix_table()
    indexer.print_all_terms()

    while True:
        query = input("\nEnter your boolean query (or 'exit' to quit): ")
        if query.lower() == 'exit':
            break
        results = indexer.boolean_search(query)
        if results:
            print(f"Results for '{query}': Documents {sorted(results)}")
        else:
            print("No results found for the query.")
```

### Output:
<img width="1201" height="350" alt="Screenshot 2026-08-18 110322" src="https://github.com/user-attachments/assets/1416f442-e5ce-4639-9850-9d2371f98e62" />

### Result:
      Thus, the Implementation of Information Retrieval Using Boolean Model in Python has successfully executed.
