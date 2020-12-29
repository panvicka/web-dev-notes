# Getting data into Gatsby with GraphQL

- playground on `http://localhost:8000/___graphql` for trying out stuff http://localhost:8000/\_\_\_graphql
- gatsby: at build time (before deploy) grabs all the data it needs and sticks it into "memory" and we can query it with GraphQL
- how to trasfer data from sanity to Gatsby? With plugins defined in `gatsby-config.js`

## enviromental variables - place for secrets

- create file `.env`
- place your sensitive data f.e. `SANITY_TOKEN = adfsdfsdfsfsfsdfsdfsfs`
- in the file where it should be used

```javascript
// import dotev package
import dotenv from 'dotenv';
// set up configuration
dotenv.config({ path: '.env' });
// acces the variables
token: process.inv.SANITY_TOKEN
```

## deploy the GraphQL API 
- if you are trying to run it without 
``` 
Error: GraphQL API not deployed - see https://github.com/sanity-io/gatsby-source-sanity#graphql-api for more info
    at Object.getRemoteGraphQLSchema (C:\Users\panvicka\Documents\master-gatsby\starter-files\gatsby\node_modules\gatsby-source-sanity\src\util\remoteGraphQLSchema.ts:71:11)
    at processTicksAndRejections (internal/process/task_queues.js:97:5)

not finished onPreBootstrap - 0.224s
```
- the deploy command is in the link `sanity graphql deploy production` **do this on the backend** (enable GraphQL playground)

## Gatsby queries 
### Page queries 
- can be dynamic with variables 
- can only be run on a top level page 
- How to? Export a query from a page and Gatsby will recognize it when building
- You can then access the data in props of the component

### Static queries 
- can not be dynamic, no variables 
- but can be run anywhere 

## GraphQL fragment
- if you query the same thing over and over again stick it inside a fragment like this (warning: wont work in the plaground as the `GatsbySanityImageFluid`
is handled when building the program)
``` 
# more code
        image {
          # fetching gatsby image
          asset {
            fluid(maxWidth: 400) {
              ...GatsbySanityImageFluid
            }
          }
        }
# more code
```

## Rename Sanity Queries 
- to awoid taping the whole AllSanityXXXXX all the time, rename the query:
```
export const query = graphql`
  query {
    pizzas: allSanityPizza { 
      nodes {
        name
        id
        slug {
... more code follows

```

