```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-70xyxg@email.com",
    "username": "author-70xyxg",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-70xyxg@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci03MHh5eGciLCJpYXQiOjE1NzcxMzk0ODIsImV4cCI6MTU3NzMxMjI4Mn0._35WdHQLFlovsctkqaaaWlDWXWMeCFFacQb1SGqRfaE",
    "username": "author-70xyxg",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-nj84q2@email.com",
    "username": "authoress-nj84q2",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-nj84q2@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1uajg0cTIiLCJpYXQiOjE1NzcxMzk0ODIsImV4cCI6MTU3NzMxMjI4Mn0.BQ8tMkNmzT6StNwKjImaFCvjSoTZYPrw3MTN6g7rahg",
    "username": "authoress-nj84q2",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-ue0aej@email.com",
    "username": "non-author-ue0aej",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-ue0aej@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItdWUwYWVqIiwiaWF0IjoxNTc3MTM5NDgyLCJleHAiOjE1NzczMTIyODJ9.wcipoiT5T3CQMhqoaZQ7F5cAdBaXWOjEjXAH6jQXGjI",
    "username": "non-author-ue0aej",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lof1f",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139482439,
    "updatedAt": 1577139482439,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gxkxxd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139482500,
    "updatedAt": 1577139482500,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-lof1f
```
```
200 OK

{
  "article": {
    "createdAt": 1577139482439,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-lof1f",
    "updatedAt": 1577139482439,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-gxkxxd
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1577139482500,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-gxkxxd",
    "updatedAt": 1577139482500,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/77sp4
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [77sp4]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-gxkxxd

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1577139482500,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-gxkxxd",
    "updatedAt": 1577139482500,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-gxkxxd

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1577139482500,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-gxkxxd",
    "updatedAt": 1577139482500,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-gxkxxd

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1577139482500,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-gxkxxd",
    "updatedAt": 1577139482500,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-gxkxxd

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-gxkxxd

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-gxkxxd

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-gxkxxd

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-gxkxxd]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-gxkxxd

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-70xyxg]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-lof1f/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1577139482439,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-lof1f",
    "updatedAt": 1577139482439,
    "favoritedBy": [
      "non-author-ue0aej"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-lof1f
```
```
200 OK

{
  "article": {
    "createdAt": 1577139482439,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-lof1f",
    "updatedAt": 1577139482439,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-lof1f/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-lof1f_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-lof1f_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-lof1f/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1577139482439,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-lof1f",
    "updatedAt": 1577139482439,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-lof1f
```
```
200 OK

{}
```
```
GET /articles/title-lof1f
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-lof1f]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-gxkxxd
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-70xyxg]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "eomoep",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wk9n9w",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483336,
    "updatedAt": 1577139483336,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "eomoep",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lo4gdi",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-1u32h2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483382,
    "updatedAt": 1577139483382,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lo4gdi",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "q6ky96",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-el60mh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483409,
    "updatedAt": 1577139483409,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "q6ky96",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "no4vao",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qur5yl",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483431,
    "updatedAt": 1577139483431,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "no4vao",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "aowip4",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-s9wmns",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483453,
    "updatedAt": 1577139483453,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "aowip4",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "eiy13t",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3t9a42",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483474,
    "updatedAt": 1577139483474,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "eiy13t",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "clw8rf",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jev98t",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483498,
    "updatedAt": 1577139483498,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "clw8rf",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "g1e4nf",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3yk1k",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483520,
    "updatedAt": 1577139483520,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "g1e4nf",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nfvjtt",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-msvo94",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483546,
    "updatedAt": 1577139483546,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nfvjtt",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4gdh7",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-udp9zu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483569,
    "updatedAt": 1577139483569,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4gdh7",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4dkmh1",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-zb4fep",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483590,
    "updatedAt": 1577139483590,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4dkmh1",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "eqe8sc",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fxftlq",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483614,
    "updatedAt": 1577139483614,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "eqe8sc",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "o6eko0",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-q7vs6w",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483635,
    "updatedAt": 1577139483635,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "o6eko0",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8rgtq4",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-l94oyw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483668,
    "updatedAt": 1577139483668,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8rgtq4",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ncx48j",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-roqpot",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483689,
    "updatedAt": 1577139483689,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ncx48j",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "gny2qu",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gmnbx9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483709,
    "updatedAt": 1577139483709,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "gny2qu",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "l25rh7",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-btr206",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483737,
    "updatedAt": 1577139483737,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "l25rh7",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "bbcps2",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5i6nb9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483763,
    "updatedAt": 1577139483763,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "bbcps2",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ka3tvt",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-s6ouva",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483785,
    "updatedAt": 1577139483785,
    "author": {
      "username": "authoress-nj84q2",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ka3tvt",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "60irvm",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-sv7dxm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139483820,
    "updatedAt": 1577139483820,
    "author": {
      "username": "author-70xyxg",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "60irvm",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "60irvm",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483820,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sv7dxm",
      "updatedAt": 1577139483820,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ka3tvt",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483785,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s6ouva",
      "updatedAt": 1577139483785,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bbcps2",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483763,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5i6nb9",
      "updatedAt": 1577139483763,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l25rh7",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483737,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-btr206",
      "updatedAt": 1577139483737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gny2qu",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483709,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gmnbx9",
      "updatedAt": 1577139483709,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ncx48j",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483689,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-roqpot",
      "updatedAt": 1577139483689,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rgtq4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483668,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l94oyw",
      "updatedAt": 1577139483668,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "o6eko0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483635,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q7vs6w",
      "updatedAt": 1577139483635,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eqe8sc",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483614,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fxftlq",
      "updatedAt": 1577139483614,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dkmh1",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483590,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-zb4fep",
      "updatedAt": 1577139483590,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4gdh7",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483569,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-udp9zu",
      "updatedAt": 1577139483569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nfvjtt",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483546,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-msvo94",
      "updatedAt": 1577139483546,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g1e4nf",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483520,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3yk1k",
      "updatedAt": 1577139483520,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "clw8rf",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483498,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jev98t",
      "updatedAt": 1577139483498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eiy13t",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483474,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3t9a42",
      "updatedAt": 1577139483474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "aowip4",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483453,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s9wmns",
      "updatedAt": 1577139483453,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "no4vao",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483431,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qur5yl",
      "updatedAt": 1577139483431,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q6ky96",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483409,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-el60mh",
      "updatedAt": 1577139483409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lo4gdi",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483382,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1u32h2",
      "updatedAt": 1577139483382,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eomoep",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483336,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wk9n9w",
      "updatedAt": 1577139483336,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "g1e4nf",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483520,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3yk1k",
      "updatedAt": 1577139483520,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "bbcps2",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483763,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5i6nb9",
      "updatedAt": 1577139483763,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ncx48j",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483689,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-roqpot",
      "updatedAt": 1577139483689,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eqe8sc",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483614,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fxftlq",
      "updatedAt": 1577139483614,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nfvjtt",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483546,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-msvo94",
      "updatedAt": 1577139483546,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eiy13t",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483474,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3t9a42",
      "updatedAt": 1577139483474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q6ky96",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483409,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-el60mh",
      "updatedAt": 1577139483409,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-nj84q2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "ka3tvt",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483785,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s6ouva",
      "updatedAt": 1577139483785,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l25rh7",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483737,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-btr206",
      "updatedAt": 1577139483737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ncx48j",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483689,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-roqpot",
      "updatedAt": 1577139483689,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "o6eko0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483635,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q7vs6w",
      "updatedAt": 1577139483635,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dkmh1",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483590,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-zb4fep",
      "updatedAt": 1577139483590,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nfvjtt",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483546,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-msvo94",
      "updatedAt": 1577139483546,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "clw8rf",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483498,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jev98t",
      "updatedAt": 1577139483498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "aowip4",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483453,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s9wmns",
      "updatedAt": 1577139483453,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q6ky96",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483409,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-el60mh",
      "updatedAt": 1577139483409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eomoep",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483336,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wk9n9w",
      "updatedAt": 1577139483336,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-ue0aej
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-70xyxg&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "60irvm",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483820,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sv7dxm",
      "updatedAt": 1577139483820,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bbcps2",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483763,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5i6nb9",
      "updatedAt": 1577139483763,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-70xyxg&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "gny2qu",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483709,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gmnbx9",
      "updatedAt": 1577139483709,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rgtq4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483668,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l94oyw",
      "updatedAt": 1577139483668,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "60irvm",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483820,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sv7dxm",
      "updatedAt": 1577139483820,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ka3tvt",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483785,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s6ouva",
      "updatedAt": 1577139483785,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bbcps2",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483763,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5i6nb9",
      "updatedAt": 1577139483763,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l25rh7",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483737,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-btr206",
      "updatedAt": 1577139483737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gny2qu",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483709,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gmnbx9",
      "updatedAt": 1577139483709,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ncx48j",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483689,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-roqpot",
      "updatedAt": 1577139483689,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rgtq4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483668,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l94oyw",
      "updatedAt": 1577139483668,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "o6eko0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483635,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q7vs6w",
      "updatedAt": 1577139483635,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eqe8sc",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483614,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fxftlq",
      "updatedAt": 1577139483614,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dkmh1",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483590,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-zb4fep",
      "updatedAt": 1577139483590,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4gdh7",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483569,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-udp9zu",
      "updatedAt": 1577139483569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nfvjtt",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483546,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-msvo94",
      "updatedAt": 1577139483546,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g1e4nf",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483520,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3yk1k",
      "updatedAt": 1577139483520,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "clw8rf",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483498,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jev98t",
      "updatedAt": 1577139483498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eiy13t",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483474,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3t9a42",
      "updatedAt": 1577139483474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "aowip4",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483453,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s9wmns",
      "updatedAt": 1577139483453,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "no4vao",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483431,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qur5yl",
      "updatedAt": 1577139483431,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q6ky96",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483409,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-el60mh",
      "updatedAt": 1577139483409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lo4gdi",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483382,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1u32h2",
      "updatedAt": 1577139483382,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eomoep",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483336,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wk9n9w",
      "updatedAt": 1577139483336,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-nj84q2/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-nj84q2",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "ka3tvt",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483785,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s6ouva",
      "updatedAt": 1577139483785,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l25rh7",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483737,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-btr206",
      "updatedAt": 1577139483737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ncx48j",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483689,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-roqpot",
      "updatedAt": 1577139483689,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "o6eko0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483635,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q7vs6w",
      "updatedAt": 1577139483635,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dkmh1",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483590,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-zb4fep",
      "updatedAt": 1577139483590,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nfvjtt",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483546,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-msvo94",
      "updatedAt": 1577139483546,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "clw8rf",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483498,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jev98t",
      "updatedAt": 1577139483498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "aowip4",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483453,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s9wmns",
      "updatedAt": 1577139483453,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q6ky96",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483409,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-el60mh",
      "updatedAt": 1577139483409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eomoep",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483336,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wk9n9w",
      "updatedAt": 1577139483336,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-70xyxg/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-70xyxg",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "60irvm",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483820,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-sv7dxm",
      "updatedAt": 1577139483820,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ka3tvt",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483785,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s6ouva",
      "updatedAt": 1577139483785,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bbcps2",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483763,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5i6nb9",
      "updatedAt": 1577139483763,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l25rh7",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483737,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-btr206",
      "updatedAt": 1577139483737,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gny2qu",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483709,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gmnbx9",
      "updatedAt": 1577139483709,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ncx48j",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483689,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-roqpot",
      "updatedAt": 1577139483689,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rgtq4",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483668,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-l94oyw",
      "updatedAt": 1577139483668,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "o6eko0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483635,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-q7vs6w",
      "updatedAt": 1577139483635,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eqe8sc",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483614,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fxftlq",
      "updatedAt": 1577139483614,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4dkmh1",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483590,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-zb4fep",
      "updatedAt": 1577139483590,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4gdh7",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483569,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-udp9zu",
      "updatedAt": 1577139483569,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nfvjtt",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483546,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-msvo94",
      "updatedAt": 1577139483546,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g1e4nf",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483520,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3yk1k",
      "updatedAt": 1577139483520,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "clw8rf",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483498,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jev98t",
      "updatedAt": 1577139483498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eiy13t",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483474,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3t9a42",
      "updatedAt": 1577139483474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "aowip4",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483453,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s9wmns",
      "updatedAt": 1577139483453,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "no4vao",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483431,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qur5yl",
      "updatedAt": 1577139483431,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "q6ky96",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1577139483409,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-el60mh",
      "updatedAt": 1577139483409,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lo4gdi",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1577139483382,
      "author": {
        "username": "author-70xyxg",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1u32h2",
      "updatedAt": 1577139483382,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "eomoep",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1577139483336,
      "author": {
        "username": "authoress-nj84q2",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wk9n9w",
      "updatedAt": 1577139483336,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "gny2qu",
    "tag_15",
    "tag_mod_2_1",
    "tag_mod_3_0",
    "bbcps2",
    "tag_17",
    "tag_mod_3_2",
    "4dkmh1",
    "tag_10",
    "tag_mod_2_0",
    "tag_mod_3_1",
    "clw8rf",
    "tag_6",
    "aowip4",
    "tag_4",
    "lo4gdi",
    "tag_1",
    "ka3tvt",
    "tag_18",
    "g1e4nf",
    "tag_7",
    "eqe8sc",
    "tag_11",
    "no4vao",
    "tag_3",
    "q6ky96",
    "tag_2",
    "eiy13t",
    "tag_5",
    "8rgtq4",
    "tag_13",
    "ncx48j",
    "tag_14",
    "4gdh7",
    "tag_9",
    "eomoep",
    "tag_0",
    "tag_a",
    "tag_b",
    "l25rh7",
    "tag_16",
    "nfvjtt",
    "tag_8",
    "o6eko0",
    "tag_12",
    "60irvm",
    "tag_19"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-c5pezp@email.com",
    "username": "author-c5pezp",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-c5pezp@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1jNXBlenAiLCJpYXQiOjE1NzcxMzk0ODQsImV4cCI6MTU3NzMxMjI4NH0.XgI6UXgmaFHGW1q0yqQbqDanL8T_qXboQCvHABIiuWg",
    "username": "author-c5pezp",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-gwadr7@email.com",
    "username": "commenter-gwadr7",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-gwadr7@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1nd2FkcjciLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.j2dHn4buoSxRQy4Ey-9QNHlrllSKhkHzrI8AkIQG7zs",
    "username": "commenter-gwadr7",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-l2konw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1577139485018,
    "updatedAt": 1577139485018,
    "author": {
      "username": "author-c5pezp",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment l8ihut"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f650d2ba-d482-4a83-98d6-d4dbffbf0e69",
    "slug": "title-l2konw",
    "body": "test comment l8ihut",
    "createdAt": 1577139485043,
    "updatedAt": 1577139485043,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment d8d4gc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "66a21072-db8a-40b3-870c-ba8be499e545",
    "slug": "title-l2konw",
    "body": "test comment d8d4gc",
    "createdAt": 1577139485076,
    "updatedAt": 1577139485076,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment uxn2gd"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "5dbd256e-e306-4bfb-9500-34ff746d226b",
    "slug": "title-l2konw",
    "body": "test comment uxn2gd",
    "createdAt": 1577139485102,
    "updatedAt": 1577139485102,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment dicwpc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2209fcc3-c8ac-42ac-bc93-d793c8d20e19",
    "slug": "title-l2konw",
    "body": "test comment dicwpc",
    "createdAt": 1577139485133,
    "updatedAt": 1577139485133,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment kcrpcd"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "4cfda312-96b7-4537-b541-e61f766b4720",
    "slug": "title-l2konw",
    "body": "test comment kcrpcd",
    "createdAt": 1577139485167,
    "updatedAt": 1577139485167,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment 1yng2j"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f46db026-12d0-44ac-89ab-ec0876de9bc7",
    "slug": "title-l2konw",
    "body": "test comment 1yng2j",
    "createdAt": 1577139485186,
    "updatedAt": 1577139485186,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment jsgju4"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "cfda990a-a37b-4dd2-a05e-25e9d501d5a9",
    "slug": "title-l2konw",
    "body": "test comment jsgju4",
    "createdAt": 1577139485212,
    "updatedAt": 1577139485212,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment jlka5e"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f93491f4-c776-47cd-b67d-c435bd14b90f",
    "slug": "title-l2konw",
    "body": "test comment jlka5e",
    "createdAt": 1577139485234,
    "updatedAt": 1577139485234,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment ya6un3"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "90c72d36-22a3-49a2-b308-cab67d7a054b",
    "slug": "title-l2konw",
    "body": "test comment ya6un3",
    "createdAt": 1577139485261,
    "updatedAt": 1577139485261,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-l2konw/comments

{
  "comment": {
    "body": "test comment uj2i2f"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "4c87e63b-be0e-4d1e-8dc0-dc1c0e0075d6",
    "slug": "title-l2konw",
    "body": "test comment uj2i2f",
    "createdAt": 1577139485296,
    "updatedAt": 1577139485296,
    "author": {
      "username": "commenter-gwadr7",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-l2konw/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-l2konw/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment 3orube"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-l2konw/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1577139485102,
      "id": "5dbd256e-e306-4bfb-9500-34ff746d226b",
      "body": "test comment uxn2gd",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485102
    },
    {
      "createdAt": 1577139485212,
      "id": "cfda990a-a37b-4dd2-a05e-25e9d501d5a9",
      "body": "test comment jsgju4",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485212
    },
    {
      "createdAt": 1577139485076,
      "id": "66a21072-db8a-40b3-870c-ba8be499e545",
      "body": "test comment d8d4gc",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485076
    },
    {
      "createdAt": 1577139485186,
      "id": "f46db026-12d0-44ac-89ab-ec0876de9bc7",
      "body": "test comment 1yng2j",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485186
    },
    {
      "createdAt": 1577139485133,
      "id": "2209fcc3-c8ac-42ac-bc93-d793c8d20e19",
      "body": "test comment dicwpc",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485133
    },
    {
      "createdAt": 1577139485043,
      "id": "f650d2ba-d482-4a83-98d6-d4dbffbf0e69",
      "body": "test comment l8ihut",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485043
    },
    {
      "createdAt": 1577139485167,
      "id": "4cfda312-96b7-4537-b541-e61f766b4720",
      "body": "test comment kcrpcd",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485167
    },
    {
      "createdAt": 1577139485234,
      "id": "f93491f4-c776-47cd-b67d-c435bd14b90f",
      "body": "test comment jlka5e",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485234
    },
    {
      "createdAt": 1577139485296,
      "id": "4c87e63b-be0e-4d1e-8dc0-dc1c0e0075d6",
      "body": "test comment uj2i2f",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485296
    },
    {
      "createdAt": 1577139485261,
      "id": "90c72d36-22a3-49a2-b308-cab67d7a054b",
      "body": "test comment ya6un3",
      "slug": "title-l2konw",
      "author": {
        "username": "commenter-gwadr7",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1577139485261
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-l2konw/comments/f650d2ba-d482-4a83-98d6-d4dbffbf0e69
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-l2konw/comments/66a21072-db8a-40b3-870c-ba8be499e545
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-gwadr7]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-l2konw/comments/66a21072-db8a-40b3-870c-ba8be499e545
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-l2konw/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "username": "user1-0.3oelhs6jhv9",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc",
    "username": "user1-0.3oelhs6jhv9",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "username": "user1-0.3oelhs6jhv9",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.3oelhs6jhv9]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.3oelhs6jhv9@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.3oelhs6jhv9@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc",
    "username": "user1-0.3oelhs6jhv9",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.n4pvotqnq3b",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.n4pvotqnq3b]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "password": "0.orupghos77"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.3oelhs6jhv9@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc",
    "username": "user1-0.3oelhs6jhv9",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.3oelhs6jhv9
```
```
200 OK

{
  "profile": {
    "username": "user1-0.3oelhs6jhv9",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.1sxapzfj4rz
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.1sxapzfj4rz]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.7m61jHJyTI-UHhNE_p3pPkql2SpXbhNIAZJd4-iRMOA",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.ied28r4ijd",
    "email": "user2-0.ied28r4ijd@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.ied28r4ijd@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuaWVkMjhyNGlqZCIsImlhdCI6MTU3NzEzOTQ4NSwiZXhwIjoxNTc3MzEyMjg1fQ.Mm_Gc5mJUENBQY5CfCLTxQKBVEKwwigZIG4hC63G3do",
    "username": "user2-0.ied28r4ijd",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.3oelhs6jhv9@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.3oelhs6jhv9",
    "email": "updated-user1-0.3oelhs6jhv9@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.3oelhs6jhv9",
    "email": "updated-user1-0.3oelhs6jhv9@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.3oelhs6jhv9",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.3oelhs6jhv9",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuM29lbGhzNmpodjkiLCJpYXQiOjE1NzcxMzk0ODUsImV4cCI6MTU3NzMxMjI4NX0.t5HTf1nAXoiQULWQM92fpIoP8d3WCtsE_MYN0Pm4YFc"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.gm8hnh9j2h@email.com",
    "username": "user2-0.gm8hnh9j2h",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.gm8hnh9j2h@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuZ204aG5oOWoyaCIsImlhdCI6MTU3NzEzOTQ4NiwiZXhwIjoxNTc3MzEyMjg2fQ.aHEg163HykiaV7BoEx0YEL_HMdnmRLDGGXD-hnXcUmE",
    "username": "user2-0.gm8hnh9j2h",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.gm8hnh9j2h@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.gm8hnh9j2h@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2019-12-23T22:18:06.132Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
