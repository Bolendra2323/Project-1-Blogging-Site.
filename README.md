# Uranium
Discussion:->
Project Overview →

In this project we were required to implement the backend part of Blogging Site.

We can relate this Project with WordPress,

where authorized user can publish blogs , articles and can also update and

delete their respective articles.

Problem Statements →

It consist of total 2 Models (Blog-Model, Author-Model)

Blog-Controller→ It consist of 5 API’s (1-Post , 1-Get,1-Put,2-Delete)

Author-Controller → It consist of 2 API’s(2-Post)

Used Appropriate Status code , Used middleware for authentication ,also

implemented authorisation so that only valid author can create,edit, update or

delete their respective article.

Approach —>

● Before starting the project we download different dependencies.

● Dependencies like —>

○ Express→ (This will help us in creating different api endpoints),

○ Mongoose→ (This will help us to work with mongodb easily)

○ Nodemon→ (This will help us in restarting the node application

whenever some changes(even the minute change) in the files are noticed

in the directory)

● Then we created SRC folder where all other sub folders are stored in a

hierarchical manner.We have created Sub folders like Models, routes,

Validators. Controller, Middleware,

● Initiated the project by creating Schemas for Blog and Author then with the

further continuation we have stored end points in route files. Basically route file

is created for storing all the end points .

● Then in the question it was mentioned that only the author of the respective

blog can perform the following operation i.e, edit, delete , update. So in order to

make this possible we have created one file called middleware , where the user

was authenticated by using JWT and authorized.

● In controller folder ,we have created files for Blog and Author where it has

their respective API’s . In this folder we have wrote all the functions that were

supposed to perform.


***********************************************************************************************************************************************************
Repository for backend cohort - Uranium

## Blogging Site Mini Project Requirement

## Phase I

### Models
- Author Model   
```
{ fname: { mandatory}, lname: {mandatory}, title: {mandatory, enum[Mr, Mrs, Miss]}, email: {mandatory, valid email, unique}, password: {mandatory} }
```
- Blogs Model   //Vinit
```
{ title: {mandatory}, body: {mandatory}, authorId: {mandatory, refs to author model}, tags: {array of string}, category: {string, mandatory, examples: [technology, entertainment, life style, food, fashion]}, subcategory: {array of string, examples[technology-[web development, mobile development, AI, ML etc]] }, createdAt, updatedAt, deletedAt: {when the document is deleted}, isDeleted: {boolean, default: false}, publishedAt: {when the blog is published}, isPublished: {boolean, default: false}}
```

### Author APIs /authors  
- Create an author - atleast 5 authors
- Create a author document from request body.
  `Endpoint: BASE_URL/authors`

### POST /blogs  
- Create a blog document from request body. Get authorId in request body only.
- Make sure the authorId is a valid authorId by checking the author exist in the authors collection.
- Return HTTP status 201 on a succesful blog creation. Also return the blog document. The response should be a JSON object like [this](#successful-response-structure) 
- Create atleast 5 blogs for each author

- Return HTTP status 400 for an invalid request with a response body like [this](#error-response-structure)

### GET /blogs   
- Returns all blogs in the collection that aren't deleted and are published
- Return the HTTP status 200 if any documents are found. The response structure should be like [this](#successful-response-structure) 
- If no documents are found then return an HTTP status 404 with a response like [this](#error-response-structure) 
- Filter blogs list by applying filters. Query param can have any combination of below filters.
  - By author Id
  - By category
  - List of blogs that have a specific tag
  - List of blogs that have a specific subcategory
example of a query url: blogs?filtername=filtervalue&f2=fv2

### PUT /blogs/:blogId  
- Updates a blog by changing the its title, body, adding tags, adding a subcategory. (Assuming tag and subcategory received in body is need to be added)
- Updates a blog by changing its publish status i.e. adds publishedAt date and set published to true
- Check if the blogId exists (must have isDeleted false). If it doesn't, return an HTTP status 404 with a response body like [this](#error-response-structure)
- Return an HTTP status 200 if updated successfully with a body like [this](#successful-response-structure) 
- Also make sure in the response you return the updated blog document. 

### DELETE /blogs/:blogId 
- Check if the blogId exists( and is not deleted). If it does, mark it deleted and return an HTTP status 200 without any response body.
- If the blog document doesn't exist then return an HTTP status of 404 with a body like [this](#error-response-structure) 

### DELETE /blogs?queryParams   
- Delete blog documents by category, authorid, tag name, subcategory name, unpublished
- If the blog document doesn't exist then return an HTTP status of 404 with a body like [this](#error-response-structure)

## Phase II

- Add authentication and authroisation feature

### POST /login  
- Allow an author to login with their email and password. On a successful login attempt return a JWT token contatining the authorId
- If the credentials are incorrect return a suitable error message with a valid HTTP status code

### Authentication
- Add an authorisation implementation for the JWT token that validates the token before every protected endpoint is called. If the validation fails, return a suitable error message with a corresponding HTTP status code
- Protected routes are create a blog, edit a blog, get the list of blogs, delete a blog(s)
- Set the token, once validated, in the request - `x-api-key`
- Use a middleware for authentication purpose.

### Authorisation 
- Make sure that only the owner of the blogs is able to edit or delete the blog.
- In case of unauthorized access return an appropirate error message.

## Testing (Self-evaluation During Development) 
- To test these apis create a new collection in Postman named Project 1 Blogging 
- Each api should have a new request in this collection
- Each request in the collection should be rightly named. Eg Create author, Create blog, Get blogs etc
- Each member of each team should have their tests in running state


Refer below sample

 ![A Postman collection and request sample](assets/Postman-collection-sample.png)

## Response

### Successful Response structure
```yaml
{
  status: true,
  data: {

  }
}
```
### Error Response structure
```yaml
{
  status: false,
  msg: ""
}
```

## Collections
### Blogs
```yaml
{
  "title": "How to win friends",
  "body": "Blog body",
  "tags": ["Book", "Friends", "Self help"],
  "category": "Book",
  "subcategory": ["Non fiction", "Self Help"],
  "published": false,
  "publishedAt": "", // if published is true publishedAt will have a date 2021-09-17T04:25:07.803Z
  "deleted": false,
  "deletedAt": "", // if deleted is true deletedAt will have a date 2021-09-17T04:25:07.803Z,
  "createdAt": "2021-09-17T04:25:07.803Z",
  "updatedAt": "2021-09-17T04:25:07.803Z",
}
```

#### Refer https://jsonplaceholder.typicode.com/guide/ for some fake blogs data.

#### Note: Create a group database and use the same database in connection string by replacing `groupXDatabase
