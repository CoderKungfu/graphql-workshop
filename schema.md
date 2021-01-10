# Build our own GraphQL Schema

You are building a database for a Library. Here are the specifications:

- A library has many books
- Book has ISBN
- Book has publish date
- Book has many authors
- Book has many categories

## Sample Schema

```graphql
type Author {
  name: String
}

type Category {
  name: String
}

type Book {
  isbn: String
  title: String
  publishDate: String
  authors: [Author]
  categories: [Category]
}

type Query {
  allBooks: [Book]
  book(isbn: String!): Book
}
```

[As a file](./schema.graphql)

> The "Query" type is special: it lists all of the available queries that clients can execute, along with the return type for each. In this case, the "books" query returns an array of zero or more Books (defined above).