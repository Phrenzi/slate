---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - objects
  - patrons
  - managers
  - patron_app_profile
  - patron_app_establishments
  - patron_app_transactions
  - management_patrons
  - management_transactions
  - management_settings
  - errors

search: true
---

# Introduction

Welcome to the Phrenzi API! You can use our API to access Phrenzi API endpoints, which can get
information on various establishments, transactions, and challenges in our database.

We have language bindings in Shell! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# API Version

We have only 1 version of API now in Phrenzi,
but we are going to increse the API version in the future if we need to.
So it is better to claim the version of API you are going to call,
by inserting a special header item in every of your request.

<aside class="success">If client do not specify the api version, then server will assume that client want to request latest version of API. </aside>

> To specify the version of API, simply insert a header `ACCEPT`, with a value with `phrenzi.v#{version_of_api}`, example:

``` shell
curl "https://phrenzi.com/api_endpoint" \
  -H "ACCEPT: phrenzi.v1" \
```

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Content-Type: application/json" # this tell server to response with json \
  -H "access-token: token" \
  -H "token-type: Bearer" \
  -H "client: u4N6u_toFnoDR1o318uOVA" \
  -H "expiry: 1466692376" \
  -H "uid: abc@example.com"
```

> auth header here is required, and can be retrieved from header in last api response.

We take security as a first priority, so following security mechanism is under consider during design API:

* token is change after every request
* all the token we using during exchanged is hashed using BCrypt ( not plain text stored )
* we use securely compared ( to protect against timing attacks )
* token is invalidate after 2 weeks

## Auth Header

after authenticate ( for example, sign in api call), the header from api response will have
following 5 tags, we call it `Auth Header`, client need to extract out `Auth Header`,
and insert it in header of next api call. For a exmaple of Auth Header, please have a look at right hand side.

Noted: Any client can easily extract out this `Auth Header` exchange logic into a library and shared it out.

* access-token
* token-type
* client
* expiry
* uid


# APP TOKEN

For some public facing api, like patron sign in, patron sign up, request to reset password,  and manager sign in,

it's better to add basic level protection as well, by predefine App Token, and inserting a
`Authorization` header with App Token in your request header for public facing api, we can block anonymous attack.

For the correct App Token, please contact admin of Phrenzi.

> Token Authenticated by insert a `Authorization` header in your api request, following example is a call to patron sign in with App Token inserted.

``` shell
curl "https://phrenzi.com/patrons/sign_in" \
  -H "ACCEPT: phrenzi.v1" \
  -H "Authorization: app_token"
```
