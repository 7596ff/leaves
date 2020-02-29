[![rust badge]][rust link] [![license badge]][license link]

# leaves 🍂

A place to leave your files.

**leaves 🍂** is a self-hostable file hosting service. Before uploading you need
a user account.

## Important routes

If open registration is enabled, then you can create an account by POSTing:

```
POST /v1/users

{
  "email": "hi@vivian.is",
}
```

You'll get back an API token and user ID:

```json
{
  "id": 4761,
  "token": "foo bar baz"
}
```

You can upload files by POSTing a body, with your API token and email:

```http request
POST /v1/files
Authorization: Basic hi@vivian.is/token:foo bar baz

post file contents as the body
```

You'll get back a URL to use:

```json
"https://example.com/61xc90l"
```

Delete your file by DELETEing it:

```http request
DELETE /v1/files/61xc90l
Authorization: Basic hi@vivian.is/token:foo bar baz
```

List your 100 most recent files:

```http request
GET /v1/users/@me/files?limit=100
Authorization: Basic hi@vivian.is/token:foo bar baz
```

## Run it

Assuming you already have a postgres container running, create a volume for the
uploaded files and bind to port 10000 on the host:

```shell script
$ docker run -itd --env-file leaves.env -v leaves_data:/data -p 10000:80 vivianis/leaves
```

[license badge]: https://img.shields.io/github/license/vivianhellyer/leaves?style=for-the-badge
[license link]: https://opensource.org/licenses/ISC
[rust badge]: https://img.shields.io/badge/Rust-1.41-93450a?style=for-the-badge
[rust link]: https://blog.rust-lang.org/2020/01/30/Rust-1.41.0.html