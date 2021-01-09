# Build a Books Server

1. Start a new [CodeSandbox](https://codesandbox.io/)
2. Select a new Apollo Server project
3. Update the schema:

    ```javascript
    const typeDefs = gql`
      type Book {
        title: String
        author: String
      }
    
      type Query {
        books: [Book]
        hello: String
      }
    `;
    ```

4. Add a `books` constant:

    ```javascript
    const books = [
      {
        title: "The Awakening",
        author: "Kate Chopin"
      },
      {
        title: "City of Glass",
        author: "Paul Auster"
      }
    ];
    ```

5. Add a new Query resolver:

    ```javascript
    const resolvers = {
      Query: {
        hello: (root, args, context) => "Hello world!",
        books: () => books
      }
    };
    ```