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
  - patron_app_patrons
  - patron_app_friendship
  - patron_app_establishments
  - patron_app_sales_transactions
  - patron_app_point_transactions
  - patron_app_summary
  - patron_app_boosters
  - patron_app_check_in
  - patron_app_invitation
  - patron_app_notification
  - management_challenges
  - management_patrons
  - management_tasks
  - management_sales_transactions
  - management_point_transactions
  - management_staffs
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

We take security as a first priority, so following security mechanism is under consider during design API:

* we use securely compared ( to protect against timing attacks )
* token is invalidate in 1 hour
* refresh token mechanism provided to refresh token

There's 3 kind of token in Phrenzi for now: App token, Patron Token, Manager Token

## APP TOKEN

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

## Patron Token

For api under `patron_app` namespace, it is protected by Patron Token:

* Patron Token consist of a pair of tokens: `token` and `refresh_token`
* `token` have 1 hour lifespan, and `refresh_token` have 1 month lifespan
* client use `token` to consume api
* if `token` is expired, then client need to use `refresh_token` to refresh token and exchange new pair of Patron Token

For the correct Patron Token, you can retrieve it by authenticate email & password using Patron login api.

## Manager Token

For api under `management` namespace, it is protected by Manager Token:

* Manager Token consist of a pair of tokens: `token` and `refresh_token`
* `token` have 1 hour lifespan, and `refresh_token` have 1 month lifespan
* client use `token` to consume api
* if `token` is expired, then client need to use `refresh_token` to refresh token and exchange new pair of Manager Token

For the correct Manager Token, you can retrieve it by authenticate email & password using Manager login api.

# Link Response Header

For some api, there might to too much data to return in one single response, so we paginate result,
and provide link for `next` ( next page ), `prev` ( previous page ), or `first` ( first page ), and `last` ( last page ) in the response header. Consumer of Phrenzi api don't need to construct the api string, everything is under response header, example on the right:

``` bash
$ curl --include 'https://phrenzi.com/managements/patrons?page=5'
HTTP/1.1 200 OK
Link: <http://localhost:3000/movies?page=1>; rel="first",
  <http://localhost:3000/movies?page=173>; rel="last",
  <http://localhost:3000/movies?page=6>; rel="next",
  <http://localhost:3000/movies?page=4>; rel="prev"
Total: 4321
Per-Page: 10
Page: 5
```

## Header Properties

there's a few properties in response headers:

Parameter | Description
--------- | ----------
Link | the navigation links
Per-Page | number of result per page
Page | current page
Total | Total result

## Library support

for iOS: [WebLinking.swift](https://github.com/kylef/WebLinking.swift)

# Staff-Id Request Header

Mostly of the APIs for iPad Companion are not only protected by manager token, but also are staff protected as well, one can only access those api after sign-in as Manager, and then select one of staff to do operations, such as create transaction, confirm task booster. Those APIs using `X-Staff-Id` as a header in the request to represent the currently loged-in staff, this is so-call Staff-Id header. Example on the right:

```shell
curl "https://phrenzi.com/api/management/patrons" \
  -H "Content-Type: application/json" \
  -H "Authorization: token" \
  -H "X-Staff-Id: 828055eb-a94d-4f71-aa90-110d5b747468"
```

Noted that example on the right, this api need Manager token, and Staff-Id Header at the same time.
