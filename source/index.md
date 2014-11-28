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

Parameter | Description
--------- | -----------
first_name* | First name of the user
last_name* | Last name of the user
phone_number* | Phone number of the user
cellphone | Secondary number of the user
email* | Email of the user
avatar | Profile picture of the user(url)
password* | Password set by the user
password_confirmation* | Password set by the user
address_attributes* | A key in the hash to create the address on the same request
address_attributes[:street_name]* | A key in the hash to create the address on the same request
address_attributes[:outer_number]\* | Attribute inside the address_attributes
address_attributes[:inner_number]| Attribute inside the address_attributes


<aside class="notice">
* Required.
</aside>


> The json request would be structured like this:

```json
{:first_name=>"Loma", :last_name=>"Mohr", :phone_number=>"(553)757-4987 x54512", :email=>"colby@friesen.com", :password=>"12345678", :password_confirmation=>"12345678", :neighborhood_id=>25, :address_attributes=>{:street_name=>"Raquel Ranch", :outer_number=>"7216", :inner_number=>"Apt. 739"}}
```


## Get a Specific User

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization: H7QyAxevRRVHrkbLN9S-' \
http://api.holavecinoapi.dev/users/25
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
       "avatar_url": null,
       "phone_number": "123456789",
       "cellphone": null,
       "neighborhood_id": 32,
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

<aside class="warning">A user can only see its own profile, no matter what id is sent.</aside>

### HTTP Request

`GET http://example.com/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve


## Get Current user's neighbors

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://api.holavecinoapi.dev/neighbors
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
        "avatar_url": null,
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
        "avatar_url": null,
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
        "avatar_url": null,
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
        "avatar_url": null,
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
        "avatar_url": null,
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

<aside class="warning">A user can only see profiles of people on the same neighborhood.</aside>

### HTTP Request

`GET http://example.com/neighbors`

# Neighborhood

## Get a neighborhood profile

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://api.holavecinoapi.dev/neighborhoods/1
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

<aside class="warning">A user can only see the profile of his/her own neighborhood.</aside>

### HTTP Request

`GET http://example.com/neighborhood/<ID>`


# Post

## Get all posts in the current neighborhood


```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://api.holavecinoapi.dev/posts
```

> The above command returns JSON structured like this:

```json
{
   "posts":
   [
       {
           "id": 1,
           "content": "Omnis ea eius quod eos.",
           "user":
           {
               "id": 34,
               "email": "esmeralda.emard@schmitt.co.uk",
               "first_name": "Marshall",
               "last_name": "Johnston",
               "avatar_url": "/uploads/user/avatar/34/avatar.png"
           }
       },
       {
           "id": 2,
           "content": "Id nihil saepe eum laboriosam.",
           "user":
           {
               "id": 35,
               "email": "stuart_rolfson@ritchie.com",
               "first_name": "Issac",
               "last_name": "Murray",
               "avatar_url": "/uploads/user/avatar/35/avatar.png"
           }
       },
       {
           "id": 3,
           "content": "Excepturi voluptatem inventore nam aperiam sunt et autem vitae.",
           "user":
           {
               "id": 36,
               "email": "jayde_oconner@lakinkertzmann.us",
               "first_name": "Jennie",
               "last_name": "Rohan",
               "avatar_url": "/uploads/user/avatar/36/avatar.png"
           }
       },
       {
           "id": 4,
           "content": "Velit omnis dignissimos molestias illo.",
           "user":
           {
               "id": 37,
               "email": "erna.durgan@zulauf.name",
               "first_name": "Harry",
               "last_name": "Bahringer",
               "avatar_url": "/uploads/user/avatar/37/avatar.png"
           }
       },
       {
           "id": 5,
           "content": "Inventore commodi corrupti iure earum quo.",
           "user":
           {
               "id": 38,
               "email": "leda@powlowskigraham.name",
               "first_name": "Marquise",
               "last_name": "Leffler",
               "avatar_url": "/uploads/user/avatar/38/avatar.png"
           }
       },
       {
           "id": 6,
           "content": "Quo inventore cupiditate non velit velit ut ut.",
           "user":
           {
               "id": 39,
               "email": "edward@schuppe.info",
               "first_name": "Reynold",
               "last_name": "Cartwright",
               "avatar_url": "/uploads/user/avatar/39/avatar.png"
           }
       }
   ]
}
```

This endpoint retrieves all posts of his/her neighborhood.

### HTTP Request

`GET http://example.com/posts`


## Create a Post

```shell
curl -H 'Accept: application/vnd.holavecino.v1' -H 'Authorization:  H7QyAxevRRVHrkbLN9S-' \
http://api.holavecinoapi.dev/posts
```

> The above command returns JSON structured like this:

```json
{"comment"=>{"comment"=>"Repellendus sed consequuntur velit quaerat libero tenetur.", "title"=>"rerum"}, "post_id"=>"1", "controller"=>"api/v1/comments", "action"=>"create"}
```

This endpoint retrieves a specific user.

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
Comment* | Text inside the comment
Title | Title of comment
Post_id | Id of the post being commented on



