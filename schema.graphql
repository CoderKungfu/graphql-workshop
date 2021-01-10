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
