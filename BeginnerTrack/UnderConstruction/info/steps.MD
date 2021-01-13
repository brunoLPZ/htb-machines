# Under Construction

There's a web page under development that allows to register and login with existing users. We have
the source code and we see that authentication is based on JWT.

## How does it work?

User can register a user by filling the registration form and after that he can login with the
existing user. Taking a look at the source code we are able to identify that there's a point that
seems vulnerable to SQL injection. How could we exploit that? Well, we need to modify the JWT as
the application parses this token to get the username and then perform the DB query.

## Exploiting the SQL injection

We're going to use the (jwt_tool)[https://github.com/ticarpi/jwt_tool].
