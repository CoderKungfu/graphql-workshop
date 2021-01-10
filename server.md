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

6. Try to make this GraphQL Query through the Graphiql client in the browser panel:

    ```GraphQL
    {
      books{
        title
        author
      }
    }
    ```

## Enhancement

Let's enhance the schema to display the authors as a new `Author` type and as a list of Authors.

1. Update the `typeDefs` to include the new `Author` type:

    ```javascript
    const typeDefs = gql`
      type Author {
        name: String
      }
    
      type Book {
        title: String
        author: [Author]
      }
    
      type Query {
        books: [Book]
        hello: String
      }
    `;
    ```

2. Update the `books` database.

    ```javascript
    const books = [
      {
        title: "The Awakening",
        author: [{ name: "Kate Chopin" }]
      },
      {
        title: "City of Glass",
        author: [{ name: "Paul Auster" }]
      },
      {
        title: "Harry Potter and the Philisopher's Stone",
        author: [{ name: "J.K. Rowling" }]
      }
    ];
    ```

3. Reload the Graphiql client in the browser panel and try to make this GraphQL query:

    ```GraphQL
    {
      books{
        title
        author {
          name
        }
      }
    }
    ```