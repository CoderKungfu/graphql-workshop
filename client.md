# Build a SWAPI Client

1. Start a new [CodeSandbox](https://codesandbox.io/)
2. Select a new ReactJS project
3. Add these new dependencies:

    - `graphql`
    - `@apollo/client`

4. Let's try and connect to the SWAPI API

    ```javascript
    import { ApolloClient, InMemoryCache } from "@apollo/client";
    import { gql } from '@apollo/client';
    
    const client = new ApolloClient({
      uri: "https://swapi-graphql.netlify.app/.netlify/functions/index",
      cache: new InMemoryCache()
    });
    
    client
      .query({
        query: gql`
          query {
            allFilms {
              edges {
                node {
                  title
                  episodeID
                  releaseDate
                }
              }
            }
          }
        `
      })
      .then(result => console.log(result));
    ```
    
5. Let's add the GraphQL client as a data provider to the app:

    ```jsx
    import { ApolloProvider } from '@apollo/client';
    
    const rootElement = document.getElementById("root");
    ReactDOM.render(
      <React.StrictMode>
        <ApolloProvider client={client}>
          <App />
        </ApolloProvider>
      </React.StrictMode>,
      rootElement
    );
    ```

6. Create a new file `StarWars.js` and add this React Functional component code:

    ```jsx
    import React from "react";
    import { useQuery, gql } from "@apollo/client";
    
    const ALL_FILMS = gql`
      query {
        allFilms {
          edges {
            node {
              title
              episodeID
              releaseDate
            }
          }
        }
      }
    `;
    
    export default function StarWars() {
      const { loading, error, data } = useQuery(ALL_FILMS);
    
      if (loading) return <p>Loading...</p>;
      if (error) return <p>Error :(</p>;
    
      return data.allFilms.edges.map(({ node }) => {
        const { title, episodeID, releaseDate } = node;
    
        return (
          <div key={episodeID}>
            <p>
              Episode {episodeID}: {title} (Released on: {releaseDate})
            </p>
          </div>
        );
      });
    }
    ```

7. Add new component to `App.js`:

    ```jsx
    import React from "react";
    import "./styles.css";
    import StarWars from "./StarWars";
    
    export default function App() {
      return (
        <div className="App">
          <h1>Hello CodeSandbox</h1>
          <StarWars />
        </div>
      );
    }

    ```