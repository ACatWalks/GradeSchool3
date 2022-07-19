# GradeSchool

## What This App Does
Allows substitute teachers to rate school districts and individual schools, based on factors such as salary, staff support, and levels of student misbehavior, similar to Yelp or GlassDoor. Users may navigate to the schools or districts tab on the navbar and  view comments and ratings for individual schools or districts by clicking on an individual school or district. Users may also add, edit, and delete comments. Users may also add schools and districts with easy access to the forms on the navbar. 

## Why It Matters
Substitute teachers are independent contractors. As such they have no union and word of mouth is slow and inefficient in the digital age. As demand for substitute teachers grows relative to supply, substitutes should know the best places to invest their limited time. 

## Technologies
This app requires:
### Back End:
*   cors
*   dotenv
*   express
*   mongoose
*   typescript
*   The following @types: cors, express, node
### Front End:
*   react, react-dom, react-router-dom, react-scripts, react-simple-star-rating
*   The following @testing-libraries: jest, react-dom, user-event
*   The following @types: jest, node, react-dom, react
*   method-override
*   typescript
*   web-vitals
*   autoprefixer

## Technical Information

### To Install:
1.   Download app from Heroku
2.   Install all dependencies (make sure you install both within the frontend and the backend directory)
3.   To start the backend type "nodemon" in the terminal running the backend
4.   To start the frontend type "npm start" in the terminal running the frontend

### Important:
This app uses React, SCSS, TypeScript, Express, and MongoDB. If your browser does not support these technologies, the app will not work.

## Issues

Future features could include authentication of users, which would allow users to update and delete only their own comments, not other people's. Updating and deleting schools and districts should also be restricted to administrators only. Otherwise a school or district with bad reviews could simply delete their own profile, defeating the purpose of this app. Also, viewing the index pages shows the list of schools and districts briefly, then a blank page. I was able to add a new school, so the issue is unlikely to be with our database. More likely, there was an unforeseen issue with the conversion to TypeScript, most likely with a mapping function with the cards or with state: {stateParams: true}. 

## Data Structure Key Points
- # use this url to interact with api 

```
fetch('https://back-end-for-grade-school.herokuapp.com/schools')
```

## API Documentation
This app utilizes REST APIs. The following endpoints enable our CRUD (Create, Read, Update, Destroy) capabilities:
*   The "/schools" and "/districts" endpoints send a GET request by running MongoDB's .find() command on the database. There are no parameters.
*   The "/schools/:id" and "/districts/:id" endpoints send a GET request by running MongoDB's .findById() command on the database, wherein the id number is passed to the findById() command as req.params.id. We also chain .populate(comments) to this request to ensure that the user is able to read all comments attached to that school or district.
*   Submitting a new school or district sends a POST request to "/schools" or "/districts" using MongoDB's .create() command on the database, passing in the form information as the parameter req.body. 
*   Submitting a new comment on a school or district sends a POST request to "/schools/:id" or "/districts/:id". First it calls the .create() function on the MongoDB database, passing in the comment's req.body as a parameter. Then it looks up the school or district the comment is attached to by calling MongoDB's .findById() method and passing in req.params.id as a parameter. Finally the new comment is pushed to the array of comments for that school or district.
*   Deleting a school or district sends a DELETE request to "/schools/:id" or "/districts/:id" by calling MongoDB's findByIdAndDelete() method, passing in req.params.id as the parameter so that only one school or district is deleted.
*   Deleting a comment sends a DELETE request to "/deleteComments/:id" by calling MongoDB's .findByIdAndDelete() method, passing in req.params.id as the parameter. Note that req.params.id refers to the comment's id, not the school or district's, as we maintain a separate database of comments as part of the microservices architecture of this project.
*   Updating a school or district sends a PUT request to "/schools/:id" or "/districts/:id" by calling MongoDB's .findByIdAndUpdate() method, which takes in 3 parameters: 1) req.params.id to identify which school or district is being updated 2) the req.body of the new information being passed in and 3) an object {new:true} which flags the new information to be used in place of the old data.
*   Updating a comment sends a PUT request to "/updateComments/:id" by calling MongoDB's .findByIdAndUpdate() method, which takes in 3 parameters: 1) req.params.id to identify which comment is being updated 2) the req.body of the new data being passed in and 3) an object {new:true} which flags the new data to be used in place of the old data.
