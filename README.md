# Shopedia
## Live Demo (Best optimized for desktop/laptop)
Project Demo is **live** at [shopedia.ca](http://shopedia.ca/)
Project GraphiQL can be accessed at [/graphiql](http://shopedia.ca/graphiql)

Hosted on an **AWS EC2 Instance** (Nginx)

## Features

- All CRUD functionalities for Articles with search capability, following core MVC principles
- Authentication: OAuth2 (secure) using Google Provider with session handling
- User database and associations with created Articles (including user dashboard view)
- [GraphQL](http://shopedia.ca/graphiql) integration for database queries and mutations
- Caching (Action and Fragment) for optimized performance
- Refined and added test cases. **All tests pass** in `article_test.rb.` Tests can be observed using `rails test` command.

## Changes

- A comprehensive list of changes to application can be viewed in the commit logs. I have utilized [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.4/)
- `feat:` denotes a new feature to the application. `fix:` denotes a commit to address bugs/revisions.


## Usage
A few important points to note:
- Only users who are signed-in can create, edit, or delete their articles.
- Once signed-in, users will be able to see a `Create` button in the navbar.
- A user may only mutate their own Articles. This is to maintain content integrity and leverage User Authentication.


## GraphQL Queries and Mutations

All queries and mutations below can be tested in [/graphiql](http://shopedia.ca/graphiql)

### Query to fetch all users
```
query GetUsers {
  users {
    email
    name
    uid
  }
}
```

### Query to fetch all articles
```
query GetArticles{
articles {
    id
    title
    content
    userId
    date
  }
}
```

### Query to search for articles (Based on content or title)
Note: you can change the query string below to test various searches
```
query SearchArticles {
  searchArticles(query: "Testing") {
    id
    title
    content
  }
}
```

### Mutation for creating an article
Note: A user is required to create articles. Use the userId provided below. Date format should be exactly the same
```
mutation CreateArticle {
  createArticle(
    input:{
      title: "GraphQL",
      content: "Some content",
      author:"Shopify",
      date: "2024-01-16",
      userId:"105777079670793482961"
    }) {
    article {
      id
      title
      content
      author
    }
    errors
  }
}
```

### Mutation for deleting an article
Note: Only articles that exist in the database can be deleted. Select an appropriate article id from GetArticles query.
```
mutation DeleteArticle {
  deleteArticle(input:{
    id: ""
  }) {
    message
  }
}
```

### Mutation for updating an article
Note: Only articles that exist in the database can be updated. Select an appropriate article id from GetArticles query.
```
mutation UpdateArticle {
  updateArticle(input:{
    id:"24"
    title: "GraphQL: Mutations"
  }) {
    article {
      id
      title
      author
      content
    }
    errors
  }
}
```

## Future Improvements

- Using auth-tokens to allow for scoped queries and mutations in GraphQL (preferably with [JWT](https://jwt.io/))
- [Elasticsearch ](https://www.elastic.co/) to enhance search functionality (real-time search, 'fuzzy' search, autocomplete etc.)
- Additional OAuth2 providers (GitHub, Microsoft etc.) 

## Dependencies
- Project was built using `Ruby 3.3.0` and `Rails 7.1.2`


## Additional Resources
- [Tailwind CSS](https://tailwindcss.com/) and [DaisyUI ](https://daisyui.com/) for Frontend design
