### EX5 Information Retrieval Using Boolean Model in Python
                    term_id = terms.index(term)
                    self.documents_matrix[i, term_id] = 1

    def print_all_terms(self):
        print("\nAll terms in Documents:")
        terms_list = sorted(self.index.keys())
        print(terms_list)

    def print_documents_matrix_table(self):
        print("\nTerm Documents Matrix :")
        df = pd.DataFrame(self.documents_matrix, columns=self.index.keys())
        print(df)

    def boolean_search(self, query):
        query = query.lower()
        query_terms = query.split()
        results = None

        for i, term in enumerate(query_terms):
            if term in self.index:
                if results is None:
                    results = self.index[term]
                else:
                    if query_terms[i-1] == 'and':
                        results = results.intersection(self.index[term])
                    elif query_terms[i-1] == 'or':
                        results = results.union(self.index[term])
                    elif query_terms[i-1] == 'not':
                        results = results.difference(self.index[term])

        return results if results else set()

indexer = BooleanRetrieval()
documents = {
        1: "Python is a programming language",
        2: "Information retrieval deals with finding information",
        3: "Boolean models are used in information retrieval"
    }
for doc_id, text in documents.items():
        indexer.index_document(doc_id, text)
indexer.create_documents_matrix(documents)
indexer.print_documents_matrix_table()
indexer.print_all_terms()
query1 = input("\nEnter your boolean query: ")
results = indexer.boolean_search(query1)
if results:
  print(f"\nResults for '{query1}': Document(s) {results}")
else:
  print("No results found for the query.")

```

### Output:
![Screenshot 2025-04-15 161543](https://github.com/user-attachments/assets/a6373d8d-32be-44d2-8cc8-b172711f135f)

### Result:
Thus, the implementation of Information Retrieval using Boolean model had been successfully done using python.
