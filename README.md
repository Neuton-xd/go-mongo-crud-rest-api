First, start a MongoDB instance using docker:

docker run --name mongodb -d -p 27017:27017 mongo
Next, clone the repository:

git clone git@github.com:parsaakbari1209/go-mongo-crud-rest-api.git
Next, change the current directory to the repository:

cd go-mongo-crud-rest-api
Next, install the dependencies:

go get ./...
Finally, run the app on port 9080:

go run .
Endpoints:
GET    /users/:email
POST   /users
PUT    /users/:email
DELETE /users/:email
Get User
This endpoint retrieves a user given the email.
Send a GET request to /users/:email:

curl -X GET 'http://127.0.0.1:9080/users/bob@gmail.com'
Response:

{
  "user": {
    "id": "<user_id>",
    "name": "Bob",
    "email": "bob@gmail.com",
    "password": "ilovealice"
  }
}
Create User
This endpoint inserts a document in the users collection of the users database.
Send a POST request to /users:

curl -X POST 'http://127.0.0.1:9080/users' -H "Content-Type: application/json" -d '{"name": "Bob", "email": "bob@gmail.com", "password": "ilovealice"}'
Response:

{
  "user": {
    "id": "<user_id>",
    "name": "Bob",
    "email": "bob@gmail.com",
    "password": "ilovealice"
  }
}
Update User
This endpoint updates the provided fields within the specified document filtered by email.
Send a PUT request to /users/:email:

curl -X PUT 'http://127.0.0.1:9080/users/bob@gmail.com' -H "Content-Type: application/json" -d '{"password": "loveyoualice"}'
Response:

{
  "user": {
    "id": "<user_id>",
    "name": "Bob",
    "email": "bob@gmail.com",
    "password": "loveyoualice"
  }
}
Delete User
This endpoint deletes the user from database given the email.
Send a DELETE request to /users/:email:

curl -X DELETE 'http://127.0.0.1:9080/users/bob@gmail.com'
Response:

{}
Errors
All of the endpoints return an error in json format with a proper http status code, if something goes wrong:

{
  "error": "user not found"
}
