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

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: secret_token"
```

> Make sure to replace `secret_token` with your API key.

Phrenzi uses different type of tokens to allow access various of API.

Phrenzi expects for the `token` to be included in all API requests to the server in a header that looks like the following:

`Authorization: secret_token`

<aside class="notice">
You must replace <code>secret_token</code> with your personal API key.
</aside>

In Phrenze, we have 3 type of api token, which will use in different api endpoints.

## App Token

This is a normal token used in apis that don't need authenticate of Patron or Manager, such as
Patron login, Patron Sign Up, Manager login

## Patron Token

This is a token used apis that need patron authenticate, after successfully Patron login, server
will return a `user_token`, then client can consume the patron related apis using this token.

## Manager Token

This is a token used apis that need manager authenticate, after successfully Manager login, server will return a
`manager_token`, then client can consume the manager related apis using this token.
