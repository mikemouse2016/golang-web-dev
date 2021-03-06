# In this step:

We will get a user from mongodb

First we will get the user id from the URL

```
id := p.ByName("id")
```

Next we will Verify that the id is an ObjectId

```
if !bson.IsObjectIdHex(id) {
	w.WriteHeader(http.StatusNotFound) // 404
	return
}
```

ObjectIdHex returns an ObjectId from the provided hex representation.

```
	oid := bson.ObjectIdHex(id)
```

Now we will create an empty user to store the results in
	
```
	u := models.User{}
```

And then we will get the user information

```
if err := uc.session.DB("go-web-dev-db").C("users").FindId(oid).One(&u); err != nil {
	w.WriteHeader(404)
	return
}
```


# Run this code

1. Start your server
You must use "go build" as you need to build a binary that includes a dependency (models package).

```
go build
./04_update-user-controllers-get
```

1. Enter this at the terminal

```
curl -X POST -H "Content-Type: application/json" -d '{"name":"James Bond","gender":"male","age":32}' http://localhost:8080/user
```

-X is short for --request
Specifies a custom request method to use when communicating with the HTTP server.

-H is short for --header

-d is short for --data