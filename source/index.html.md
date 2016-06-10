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
  - establishments
  - patron_transactions
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

# API standard

for apis in Phrenzi, we follow [JSON API](http://jsonapi.org). Clients built around JSON API are able to take advantage of its features around efficiently caching responses, sometimes eliminating network requests entirely.

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
