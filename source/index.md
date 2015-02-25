---
title: API Reference

language_tabs:
  - shell
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to Hola Vecino's API.
Hola Vecino is an application that intends to unite the people by neighborhoods, creating an application that eases the relationship between them.

# Users

## Create a User

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
first_name | First name of the user | String | Yes
last_name | Last name of the user | String | Yes
phone_number | Phone number of the user | String | Yes
cellphone | Secondary number of the user | String | No
email | Email of the user | String (email format) | Yes
avatar | Profile picture of the user(url) | File | Yes
neighborhood_id | Id of the neighborhood previously selected | Integer | Yes
password | Password set by the user | String minimum 8 characters long | Yes
password_confirmation | Password set by the user | Same as password | Yes
address_attributes | A key in the hash to create the address on the same request | Json object | Yes
address_attributes[:street_name] | A key in the hash to create the address on the same request | String | Yes
address_attributes[:outer_number] | Attribute inside the address_attributes | String | Yes
address_attributes[:inner_number]| Attribute inside the address_attributes | String | No
address_attributes[:neighborhood_id]| Id of the neighborhood the address is created on | Integer | Yes

> The format received by the API has this format:


```json
{:first_name=>"Loma", :last_name=>"Mohr", :phone_number=>"(553)757-4987 x54512", :email=>"colby@friesen.com", :password=>"12345678", :password_confirmation=>"12345678", :neighborhood_id=>25, :address_attributes=>{:street_name=>"Raquel Ranch", :outer_number=>"7216", :inner_number=>"Apt. 739"}}
```

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/users/<ID>`

## Update a User | Approve a User

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
first_name | First name of the user | String | No
last_name | Last name of the user | String | No
phone_number | Phone number of the user | String | No
cellphone | Secondary number of the user | String | No
avatar | Profile picture of the user(url) | File | No
password | Password set by the user | String minimum 8 characters long | No
password_confirmation | Password set by the user | Same as password | No
address_attributes | A key in the hash to create the address on the same request | Json object | No
address_attributes[:street_name] | A key in the hash to create the address on the same request | String | No
address_attributes[:outer_number] | Attribute inside the address_attributes | String | No
address_attributes[:inner_number]| Attribute inside the address_attributes | String | No
approved | Boolean attribute the leader can change, if a user is

> The format received by the API has this format:


```json
{"id"=>"9", "controller"=>"api/v1/users", "action"=>"destroy", "user"=>{}}
```

### HTTP Request

`PUT/PATCH http://holavecino-dev.herokuapp.com/api/users/<ID>`

## Reject a user | Destroy a user

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization: H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/users/25
```
### HTTP Request

`DELETE http://holavecino-dev.herokuapp.com/api/users/<ID>`

## Get a Specific User


```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization: H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/users/25
```

> The above command returns JSON structured like this:

```json
{
   "user":
   {
       "id": 27,
       "email": "alicia@icalialabs.com",
       "first_name": "Alicia",
       "last_name": "Gonzalez",
       "auth_token": "H7QyAxevRRVHrkbLN9S-",
       "avatar": null,
       "phone_number": "123456789",
       "cellphone": null,
       "neighborhood_id": 32,
       "is_leader?": true,
       "pending_number": 9,
       "address":
       {
           "id": 28,
           "street_name": "Voyager",
           "outer_number": "405",
           "inner_number": ""
       }
   }
}
```

This endpoint retrieves a specific user.

<aside class="notice">A user can only see its own profile, no matter what id is sent.</aside>

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/users/<ID>`

### URL Parameters

Parameter | Description | Type        | Required
--------- | ----------- | ----------- |-----------
ID | The ID of the user to retrieve | Integer | Yes

## Get number of pending neighbors requests

```
9
```
This endpoint retrieves the number of pending requests a leader has.
### HTTP Request
`GET http://holavecino-dev.herokuapp.com/api/pending_count`

## Get Current user's neighbors

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/neighbors
```

> The above command returns JSON structured like this:

```json
{
    "users": [{
        "id": 28,
        "email": "halle@schultz.biz",
        "first_name": "Quinn",
        "last_name": "Schiller",
        "auth_token": "1zG4hS3B6etuJ8gECZhP",
        "avatar": null,
        "phone_number": "235-369-4229 x028",
        "cellphone": null,
        "neighborhood_id": 42,
        "address": {
            "id": 29,
            "street_name": "Ruthe Crest",
            "outer_number": "2605",
            "inner_number": "Apt. 760"
        }
    }, {
        "id": 29,
        "email": "shyann@aufderhar.co.uk",
        "first_name": "Pierce",
        "last_name": "Jast",
        "auth_token": "UbQAaHxD2PHGyofsuQLn",
        "avatar": null,
        "phone_number": "1-389-937-2862 x534",
        "cellphone": null,
        "neighborhood_id": 42,
        "address": {
            "id": 30,
            "street_name": "Emily Fort",
            "outer_number": "6931",
            "inner_number": "Apt. 082"
        }
    }, {
        "id": 30,
        "email": "brennan@murray.ca",
        "first_name": "Enos",
        "last_name": "Volkman",
        "auth_token": "xyDPMCMyqBzwYE3s8oS4",
        "avatar": null,
        "phone_number": "1-892-904-3903",
        "cellphone": null,
        "neighborhood_id": 42,
        "address": {
            "id": 31,
            "street_name": "Theresa Mountains",
            "outer_number": "732",
            "inner_number": "Suite 191"
        }
    }, {
        "id": 31,
        "email": "aisha@heller.com",
        "first_name": "Faye",
        "last_name": "Ruecker",
        "auth_token": "25xUpDAQkWb1ukeeRsve",
        "avatar": null,
        "phone_number": "466-975-0935 x508",
        "cellphone": null,
        "neighborhood_id": 42,
        "address": {
            "id": 32,
            "street_name": "Bogan Village",
            "outer_number": "7027",
            "inner_number": "Apt. 649"
        }
    }, {
        "id": 32,
        "email": "layla_spencer@reilly.com",
        "first_name": "Everett",
        "last_name": "Casper",
        "auth_token": "ug6kGAWBF48zhyLavn2y",
        "avatar": null,
        "phone_number": "1-384-614-1243",
        "cellphone": null,
        "neighborhood_id": 42,
        "address": {
            "id": 33,
            "street_name": "Waldo Courts",
            "outer_number": "10714",
            "inner_number": "Apt. 128"
        }
    }]
}
```

This endpoint retrieves the current user's neighbors.

<aside class="notice">A user can only see profiles of people on the same neighborhood.</aside>

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/neighbors`

## Pending Neighbors

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/pending
```

> The above command returns JSON structured like this:

```json
{
    "users": [
        {
            "id": 41,
            "email": "marlen.torp@sawaynkoepp.com",
            "short_name": "Eladio Reichel",
            "avatar": "avatar.png",
            "is_leader?": false,
            "approved": false
        },
        {
            "id": 48,
            "email": "bryon@kassulkewuckert.biz",
            "short_name": "Junior Sipes",
            "avatar": "avatar.png",
            "is_leader?": false,
            "approved": false
        },
        {
            "id": 49,
            "email": "chyna@rutherford.name",
            "short_name": "Cathrine Mante",
            "avatar": "avatar.png",
            "is_leader?": false,
            "approved": false
        },
        {
            "id": 50,
            "email": "aniya_strosin@murazik.us",
            "short_name": "Payton Hilpert",
            "avatar": "avatar.png",
            "is_leader?": false,
            "approved": false
        }
    ]
    }
```
### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/pending`

## Reset password

There will be no headers on this request

This is not a json response, it will return html.

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/users/password/new`


# Neighborhood

## Neighborhoods index

```shell
curl -H 'Accept: application/vnd.holavecino.v1' \
http://holavecino-dev.herokuapp.com/api/neighborhoods
```
> The above command returns JSON structured like this:

```json
{
    "neighborhoods": [
        {
            "id": 16,
            "name": "Alexanne Orchard",
            "city_name": "Monterrey"
        },
        {
            "id": 17,
            "name": "Alexanne Orchard",
            "city_name": "Monterrey"
        },
        {
            "id": 65,
            "name": "Armani Oval",
            "city_name": "Monterrey"
        },
        {
            "id": 64,
            "name": "Armani Oval",
            "city_name": "Monterrey"
        },
        {
            "id": 22,
            "name": "Birdie Landing",
            "city_name": "Monterrey"
        },
        {
            "id": 21,
            "name": "Bogisich Glens",
            "city_name": "Monterrey"
        },
        {
            "id": 60,
            "name": "Brekke Forge",
            "city_name": "Monterrey"
        },
        {
            "id": 61,
            "name": "Brekke Forge",
            "city_name": "Monterrey"
        },
        {
            "id": 18,
            "name": "Carlo Union",
            "city_name": "Monterrey"
        },
        {
            "id": 3,
            "name": "Chasity Islands",
            "city_name": "Monterrey"
        },
        {
            "id": 2,
            "name": "Chasity Islands",
            "city_name": "Monterrey"
        },
        {
            "id": 1,
            "name": "Col. Test",
            "city_name": "Monterrey"
        },
        {
            "id": 9,
            "name": "Elliott Heights",
            "city_name": "Monterrey"
        },
        {
            "id": 45,
            "name": "Ervin Manors",
            "city_name": "Monterrey"
        },
        {
            "id": 46,
            "name": "Ervin Manors",
            "city_name": "Monterrey"
        }
    ],
    "meta": {
        "pagination": {
            "per_page": 15,
            "total_pages": 5,
            "total_objects": 65
        }
    }
}
```
There is no need for authentication to show this endpoint.

This endpoint retrieves all neighborhoods on the server.

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- |--------- |
search | String to be search in the neighborhood's name | lowercase string | No


## Get a neighborhood profile

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/neighborhoods/1
```

> The above command returns JSON structured like this:

```json
{
   "neighborhood":
   {
       "id": 42,
       "name": "Mittie Corners",
       "about": "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
       "postal_code": 89165,
       "created_at": "2014-11-24T20:50:57.553Z",
       "updated_at": "2014-11-24T20:50:57.553Z",
       "cover_image_url": null
   }
}
```

This endpoint retrieves a specific user.

<aside class="notice">A user can only see the profile of his/her own neighborhood.</aside>

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/neighborhoods/<ID>`

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- |--------- |
id | Any number will retrieve the current user's neighborhood | integer | Yes

# Post

## Get all posts in the current neighborhood

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/posts
```

> The above command returns JSON structured like this:

```json
{
    "posts": [
        {
            "id": 2,
            "content": "Id nihil saepe eum laboriosam.",
            "created_at": "2014-11-25T17:05:17.906Z",
            "likes": 0,
            "category_name": null,
            "liked": false,
            "user": {
                "id": 35,
                "email": "stuart_rolfson@ritchie.com",
                "short_name": "Issac Murray",
                "avatar_url": "/uploads/user/avatar/35/avatar.png"
            },
            "poll": null
        },
        {
            "id": 3,
            "content": "Excepturi voluptatem inventore nam aperiam sunt et autem vitae.",
            "created_at": "2014-11-25T17:05:19.668Z",
            "likes": 0,
            "category_name": null,
            "liked": false,
            "user": {
                "id": 36,
                "email": "jayde_oconner@lakinkertzmann.us",
                "short_name": "Jennie Rohan",
                "avatar_url": "/uploads/user/avatar/36/avatar.png"
            },
            "poll": null
        },
        {
            "id": 4,
            "content": "Velit omnis dignissimos molestias illo.",
            "created_at": "2014-11-25T17:05:21.522Z",
            "likes": 0,
            "category_name": null,
            "liked": false,
            "user": {
                "id": 37,
                "email": "erna.durgan@zulauf.name",
                "short_name": "Harry Bahringer",
                "avatar_url": "/uploads/user/avatar/37/avatar.png"
            },
            "poll": null
        },
        {
            "id": 5,
            "content": "Inventore commodi corrupti iure earum quo.",
            "created_at": "2014-11-25T17:05:22.711Z",
            "likes": 0,
            "category_name": null,
            "liked": false,
            "user": {
                "id": 38,
                "email": "leda@powlowskigraham.name",
                "short_name": "Marquise Leffler",
                "avatar_url": "/uploads/user/avatar/38/avatar.png"
            },
            "poll": null
        },
        {
            "id": 6,
            "content": "Quo inventore cupiditate non velit velit ut ut.",
            "created_at": "2014-11-25T17:05:23.317Z",
            "likes": 0,
            "category_name": null,
            "liked": false,
            "user": {
                "id": 39,
                "email": "edward@schuppe.info",
                "short_name": "Reynold Cartwright",
                "avatar_url": "/uploads/user/avatar/39/avatar.png"
            },
            "poll": {
                "id": 1,
                "question": "MyText",
                "created_at": "2014-12-11T21:13:12.551Z",
                "upvotes_percent": 50,
                "downvotes_percent": 50
            }
        },
        {
            "id": 1,
            "content": "Omnis ea eius quod eos.",
            "created_at": "2014-11-24T22:12:42.393Z",
            "likes": 1,
            "category_name": "Crime and Security",
            "liked": false,
            "user": {
                "id": 34,
                "email": "esmeralda.emard@schmitt.co.uk",
                "short_name": "Marshall Johnston",
                "avatar_url": "/uploads/user/avatar/34/avatar.png"
            },
            "poll": null
        }
    ],
    "meta": {
        "pagination": {
            "per_page": 25,
            "total_pages": 1,
            "total_objects": 6
        }
    }
}
```

This endpoint retrieves all posts of his/her neighborhood.
The polls are embedded on the post, an example is Post with id 6.

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/posts`


## Create a Post

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/posts
```


> The format received by the API has this format:


```json
{"post"=>{"content"=>"Nihil eveniet quis laborum iste voluptatibus sed excepturi."}, "controller"=>"api/v1/posts", "action"=>"create"}
```

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/posts`

### URL Parameters

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
content | Text inside the post | Text | Yes
photo | Picture to be posted  | File | No
category_id | Id of the category the post belongs to | Integer | Yes

## Like a Post

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/posts/<ID>/toggle_like
```

> The above command returns JSON structured like this:

```json
{"id"=>"12", "controller"=>"api/v1/posts", "action"=>"toggle_like", "post"=>{}}
```

This endpoint adds a like or removes the like of the current user.

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/posts/<ID>/toggle_like`

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- | -----------
id | Id of the post being commented on | Integer | Yes

## Flag a Post

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/posts/<ID>/toggle_flag
```

> The format received by the API has this format:

```json
{"id"=>"12", "controller"=>"api/v1/posts", "action"=>"toggle_flag", "post"=>{}}
```

This endpoint retrieves a specific user.

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/posts/<ID>/toggle_flag`

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- | -----------
id | Id of the post being commented on | Integer | Yes

## Delete a Post

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/posts/<ID>
```

> The above command returns JSON structured like this:

```json
{"comment"=>{"comment"=>"Repellendus sed consequuntur velit quaerat libero tenetur.", "title"=>"rerum"}, "post_id"=>"1", "controller"=>"api/v1/comments", "action"=>"create"}
```

This endpoint retrieves a specific user.

### HTTP Request

`DELETE http://holavecino-dev.herokuapp.com/api/posts/<ID>`

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- | -----------
id | Id of the post being commented on | Integer | Yes

# Poll
Poll works as an extension to Post, so a post is created with a each poll

## Create a Poll

> The format received by the API has this format:

```json
{"poll"=>{"post_attributes"=>{"content"=>"Nobis quo quis culpa et ut alias.", "category_id"=>"1"}}, "controller"=>"api/v1/polls", "action"=>"create"}
```

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/poll`

### URL Parameters

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
content | Text inside the post | Text | Yes
id | Id of the post being commented on | Integer |Yes
category_id | Id of the category the post belongs to | Integer | No

## Get a specific poll

```json
{
    "post": {
        "id": 6,
        "content": "Quo inventore cupiditate non velit velit ut ut.",
        "created_at": "2014-11-25T17:05:23.317Z",
        "likes": 0,
        "category_name": null,
        "liked": false,
        "flagged": false,
        "photo": null,
        "photo_width": null,
        "photo_height": null,
        "number_of_comments": 3,
        "user": {
            "id": 39,
            "email": "edward@schuppe.info",
            "short_name": "Reynold Cartwright",
            "avatar": "avatar.png",
            "is_leader?": false,
            "approved": false,
            "phone_number": "555.756.5036",
            "address": {
                "id": 40,
                "street_name": "Durgan Loaf",
                "outer_number": "342",
                "inner_number": "Suite 862"
            }
        },
        "poll": {
            "upvotes_percent": 50,
            "downvotes_percent": 50
        }
    }
}
```
### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/post/<ID>`

## Upvote a Poll

> The format received by the API has this format:
```json
{"id"=>"6", "controller"=>"api/v1/polls", "action"=>"upvote", "poll"=>{}}
```

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
id | Id of the POST being commented on | Integer |Yes

## Downvote a Poll

> The format received by the API has this format:
```json
{"id"=>"4", "controller"=>"api/v1/polls", "action"=>"downvote", "poll"=>{}}
```

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
id | Id of the POST being commented on | Integer |Yes

# Category

## Get all categories

```json
{
    "categories": [
        {
            "id": 2,
            "name": "Crimen y Seguridad"
        },
        {
            "id": 3,
            "name": "Clasificados"
        },
        {
            "id": 4,
            "name": "General"
        },
        {
            "id": 5,
            "name": "Articulos perdidos"
        },
        {
            "id": 6,
            "name": "Recomendaciones"
        }
    ]
}
```
### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/categories`

# Comment

## Get all comments from a post


```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/comments/
```

> The above command returns JSON structured like this:

```json
{
    "comments": [
        {
            "id": 6,
            "comment": "\"comment\"",
            "created_at": "2015-02-03T17:07:16.194Z",
            "user": {
                "id": 54,
                "email": "zachery@durgan.name",
                "short_name": "Reid Gislason",
                "avatar": "avatar.png",
                "is_leader?": false,
                "approved": false,
                "phone_number": "040-894-6418",
                "address": {
                    "id": 56,
                    "street_name": "Mayert Trail",
                    "outer_number": "44899",
                    "inner_number": "Apt. 279"
                }
            }
        },
        {
            "id": 7,
            "comment": "This is a comment",
            "created_at": "2015-02-03T17:15:43.651Z",
            "user": {
                "id": 54,
                "email": "zachery@durgan.name",
                "short_name": "Reid Gislason",
                "avatar": "avatar.png",
                "is_leader?": false,
                "approved": false,
                "phone_number": "040-894-6418",
                "address": {
                    "id": 56,
                    "street_name": "Mayert Trail",
                    "outer_number": "44899",
                    "inner_number": "Apt. 279"
                }
            }
        },
        {
            "id": 8,
            "comment": "This is another comment",
            "created_at": "2015-02-03T17:15:49.952Z",
            "user": {
                "id": 54,
                "email": "zachery@durgan.name",
                "short_name": "Reid Gislason",
                "avatar": "avatar.png",
                "is_leader?": false,
                "approved": false,
                "phone_number": "040-894-6418",
                "address": {
                    "id": 56,
                    "street_name": "Mayert Trail",
                    "outer_number": "44899",
                    "inner_number": "Apt. 279"
                }
            }
        }
    ],
    "meta": {
        "pagination": {
            "per_page": 25,
            "total_pages": 1,
            "total_objects": 3
        }
    }
}
```

This endpoint retrieves all posts of his/her neighborhood.

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/comments?post_id=<POST_ID>`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- | ----------- | -----------
post_id | Id of the post's comments you want to retrieve | Integer | Yes


## Create a comment

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/comments/
```

> The above command returns JSON structured like this:

```json
{"comment"=>{"comment"=>"Repellendus sed consequuntur velit quaerat libero tenetur.", "title"=>"rerum"}, "post_id"=>"1", "controller"=>"api/v1/comments", "action"=>"create"}
```

This endpoint retrieves a specific user.

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/comments/<ID>`

### URL Parameters

Parameter | Description | Type | Required
--------- | ----------- |----------- | -----------
Comment | Text inside the comment | Text | Yes
Title | Title of comment | String | No
Post_id | Id of the post being commented on | Integer | Yes

## Flag a comment
```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/comments/<ID>/toggle_flag
```

> The format received by the API has this format:

```json
{"id"=>"12", "controller"=>"api/v1/comments", "action"=>"toggle_flag", "post"=>{}}
```

This endpoint retrieves a specific user.

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/comments/<ID>/toggle_flag`

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- | -----------
id | Id of the post being commented on | Integer | Yes

## Delete a Comment

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/comments/<ID>?post_id=<POST_ID>
```


### HTTP Request

`DELETE http://holavecino-dev.herokuapp.com/api/comments/<ID>?post_id=<POST_ID>`

### URL Parameters

Parameter | Description | Type      | Required
--------- | ----------- | --------- | -----------
id | Id of the comment | Integer | Yes
post_id | Id of the post the comment belongs to | Integer | Yes

# Tehuan Reports
## Get all reports in a neighborhood
```json
{
    "tehuan_reports": [
        {
            "id": 16,
            "content": "Accidente en Miguel Aleman frente al Carls Jr",
            "created_at": "2014-12-26T20:45:15.693Z",
            "photo": null,
            "photo_width": null,
            "photo_height": null,
            "tehuan_category": "Accidente",
            "user": {
                "id": 27,
                "email": "alicia@icalialabs.com",
                "short_name": "Alicia Gonzalez",
                "avatar": null,
                "is_leader?": true,
                "approved": false,
                "phone_number": "123456789",
                "address": {
                    "id": 28,
                    "street_name": "Voyager",
                    "outer_number": "405",
                    "inner_number": ""
                }
            }
        },
        {
            "id": 15,
            "content": "Accidente en Miguel Aleman frente al Carls Jr",
            "created_at": "2014-12-26T20:41:45.835Z",
            "photo": null,
            "photo_width": null,
            "photo_height": null,
            "tehuan_category": "",
            "user": {
                "id": 27,
                "email": "alicia@icalialabs.com",
                "short_name": "Alicia Gonzalez",
                "avatar": null,
                "is_leader?": true,
                "approved": false,
                "phone_number": "123456789",
                "address": {
                    "id": 28,
                    "street_name": "Voyager",
                    "outer_number": "405",
                    "inner_number": ""
                }
            }
        }
    ],
    "meta": {
        "pagination": {
            "per_page": 25,
            "total_pages": 1,
            "total_objects": 2
        }
    }
}
```
This endpoint retrieves all the reports created on his/her neighborhood

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/tehuan_reports`

## Create a Tehuan Report

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://holavecino-dev.herokuapp.com/api/tehuan_reports
```
> The format received by the API has this format:


```json
{"tehuan_report"=>{"content"=>"Nihil eveniet quis laborum iste voluptatibus sed excepturi.", "tehuan_category"=>"ACCIDENTE"}, "controller"=>"api/v1/posts", "action"=>"create"}
```

### HTTP Request

`POST http://holavecino-dev.herokuapp.com/api/tehuan_reports`

### URL Parameters

Parameter | Description | Type        | Required
--------- | ----------- | ----------- | -----------
content | Text inside the post | Text | Yes
photo | Picture to be posted  | File | No
photo_height | Height of the photo | No
photo_width | Width of the photo | No
tehuan_category | Name of the category the report belongs to | String | No

## Get Tehuan Categories

```json
{
    "tehuan_reports": [
        "ACCIDENTE",
        "ALCANTARILLAS",
        "ALUMBRADO PUBLICO",
        "AUTO ABANDONADO",
        "AVISOS",
        "BACHE O VIA DAÑADA",
        "DETENCION DE BANDAS",
        "EMERGENCIAS",
        "EVENTO PUBLICO",
        "EXTORSION",
        "FALTA ELECTRICIDAD",
        "FUGA",
        "HOMICIDIO",
        "INCENDIO",
        "MTYMUYBIEN",
        "OBRAS Y/O VIA CERRADA",
        "OBSERVADOR CIUDADANO",
        "OTROS",
        "PARQUES DESCUIDADOS",
        "PERCEPCION DE INSEGURIDAD",
        "PROPUESTA COMUNIDAD",
        "PROPUESTA SEGURIDAD",
        "PROPUESTA SERV PUBLICOS",
        "PROPUESTA VIALIDAD",
        "RECOLECCION DE BASURA",
        "ROBO",
        "ROBO AUTO",
        "SECUESTRO",
        "SEMAFORO DESCOMPUESTO",
        "SITUACION DE RIESGO",
        "SOSPECHOSO",
        "VIALIDAD"
    ]
}
```
This endpoint retrieves the tehuan categories a tehuan report can have.

### HTTP Request

`GET http://holavecino-dev.herokuapp.com/api/tehuan_categories`
