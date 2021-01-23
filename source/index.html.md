---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - java
  - shell

toc_footers:
  - Documentation Powered by Slate

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

The eLB Core API is organized around REST. Our API returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Authentication

The eLB core API uses API keys to authenticate requests. You can view and manage your API keys in the Core Dashboard.

Use your API key by assigning it to Elb.apiKey. The Java library will then automatically send this key in each request.

```java 
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

Organization organization = Organization.retrieve(
  1992,
  requestOptions,
);

organization.save(); // Uses the same API Key.
```

```shell
curl https://example.com/api/internal/organizations/1992 \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc"

```

<aside class="notice">
You must replace <code>elb_4eC39HqLyjWDarjtT1zdp7dc</code> with your personal API key.
</aside>

# Organizations

The API allows you to create, delete, and update your organizations. You can retrieve individual user as well as a list of organizations

## The Organization object

>The Organization object

```json
{
  "id": 1992,
  "name": "Dev A2Z",
  "description": null,
  "object": "organization"
}
```

Attribute      | Type           | Description   | Readonly
-------------- | -------------- | --------------| --------------
id             | Long           | Unique identifier for the object. | Yes
name           | String         | The organization's name  | No
description    | String         | The organization's description | No
object         | String | String representing the object’s type. Objects of the same type share the same value. | Yes


## Get a Specific Organization

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();


Organization organization = Organization.retrieve(
  1992,
  requestOptions,
);
```

```shell
curl https://example.com/api/internal/organizations/1992 \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc"

```

> The above command returns JSON structured like this:

```json
{
  "id": 1992,
  "name": "Dev A2Z",
  "description": "org description",
  "object": "organization"
}
```

This endpoint retrieves a specific organization.


### HTTP Request

`GET /api/internal/organizations/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the organization to retrieve

## Update a Specific Organization

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

Map<String, Object> params = new HashMap();  
params.put("id", 1992);
params.put("name", "Dev A2Z");
params.put("description", "org description");

Organization organization = Organization.update(
  params,
  requestOptions,
);
```

```shell
curl https://example.com/api/internal/organizations/1992 \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" \
   --header "Content-Type: application/x-www-form-urlencoded" \
   -d id=1992 \
   -d name="Dev A2Z" \
   -d description="org description" 

```

This endpoint updates a specific organization.


### HTTP Request

`PUT /api/internal/organizations/:id`

### Request Body
<aside class="notice">
<code>
<br/>{
  <br/>&nbsp;&nbsp;"id": 1992,
  <br/>&nbsp;&nbsp;"name": "Dev A2Z",
  <br/>&nbsp;&nbsp;"description": "org description",
  <br/>&nbsp;&nbsp;"object": "organization"
<br/>}
</code>
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the organization to update

## Create a Specific Organization

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

Map<String, Object> params = new HashMap();  
params.put("name", "Dev A2Z");
params.put("description", "org description");

Organization organization = Organization.create(
  params,
  requestOptions,
);
```

```shell
curl https://example.com/api/internal/organizations/1992 \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" \
   --header "Content-Type: application/x-www-form-urlencoded" \
   -d name="Dev A2Z" \
   -d description="org description"
```

This endpoint updates a specific organization.


### HTTP Request

`POST /api/internal/organizations`

### Request Body
<aside class="notice">
<code>
<br/>{
  <br/>&nbsp;&nbsp;"name": "Dev A2Z",
  <br/>&nbsp;&nbsp;"description": "org description",
  <br/>&nbsp;&nbsp;"object": "organization"
<br/>}
</code>
</aside>

## Delete a Specific Organization

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

Organization organization =
  Organization.retrieve(1992);

Organization deletedOrg = organization.delete();
```

```shell
curl https://example.com/api/internal/organizations/1992 \
   -X DELETE \
   -header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" 

```

This endpoint deletes a specific organization.


### HTTP Request

`DELETE /api/internal/organizations/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the organization to delete


# Users
The API allows you to create, delete, and update your users. You can retrieve individual user as well as a list of users

## The User object

>The User object

```json
{
  "id": 2367,
  "firstName": "Peter",
  "lastName": "Parker",
  "email": "peter.parker@dev-a2z.com",
  "username": "peter.parker@dev-a2z.com",
  "password": null,
  "langKey": "en",
  "imgUrl": null,
  "phoneNumber": null,
  "countryCode": "us",
  "country": "United States",
  "state": "FL",
  "authorities": ["author"],
  "object": "user"
}
```

Attribute      | Type           | Description   | Readonly
-------------- | -------------- | --------------| --------------
id             | Long           | Unique identifier for the object. | Yes
firstName | String         | The user's first name  | No
lastName    | String         | The user's last name | No
email    | String         | The user's email | No
username    | String         | The user's username | No
password    | String         | The user's password | No
langKey    | String         | The user's language key | No
imgUrl    | String         | The user's avatar url | No
phoneNumber    | String         | The user's phone | No
countryCode    | String         | The user's country code | No
country    | String         | The user's country | No
state    | String         | The user's state/province | No
authorities    | Array         | The user's roles. Allowed values: 'author', 'user', 'org admin' | No
object         | String | String representing the object’s type. Objects of the same type share the same value. | Yes

## Get a Specific User

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

User user = User.retrieve(
  2367,
  requestOptions,
);
```

```shell
curl https://example.com/api/internal/users/2367 \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" \
```

> The above command returns JSON structured like this:

```json
{
  "id": 2367,
  "firstName": "Peter",
  "lastName": "Parker",
  "email": "peter.parker@dev-a2z.com",
  "username": "peter.parker@dev-a2z.com",
  "password": null,
  "langKey": "en",
  "imgUrl": null,
  "phoneNumber": null,
  "countryCode": "us",
  "country": "United States",
  "state": "FL",
  "authorities": ["author"],
  "object": "user"
}
```

This endpoint retrieves a specific user.


### HTTP Request

`GET api/internal/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the user to retrieve

## Update a Specific User

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

Map<String, Object> params = new HashMap();  
params.put("id", 2367);
params.put("firstName", "Kent");
params.put("lastName", "Clark");

User user = User.update(
  params,
  requestOptions,
);
```

```shell
curl https://example.com/api/internal/users/2367 \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" \
   --header "Content-Type: application/x-www-form-urlencoded" \
   -d id=2367 \
   -d firstName="Kent" \
   -d lastName="Clark" 
```

This endpoint updates a specific user.


### HTTP Request

`PUT /api/internal/users/:id`

### Request Body
<aside class="notice">
<code>
<br/>{
<br/>&nbsp;&nbsp;"id": 2367,
<br/>&nbsp;&nbsp;"firstName": "Kent",
<br/>&nbsp;&nbsp;"lastName": "Clark",
<br/>&nbsp;&nbsp;"object": "user"
<br/>}
</code>
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the user to update

## Create a Specific User

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

Map<String, Object> params = new HashMap();  
params.put("firstName", "Kent");
params.put("lastName", "Clark");
params.put("email", "kent.clark@gmail.com");
params.put("username", "kent.clark@gmail.com");
params.put("password", "123$notGood");

User user = User.create(
  params,
  requestOptions,
);
```

```shell
curl https://example.com/api/internal/users \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" \
   --header "Content-Type: application/x-www-form-urlencoded" \
   -d firstName="Kent" \
   -d lastName="Clark" \
   -d email="kent.clark@gmail.com" \
   -d username="kent.clark@gmail.com" \
   -d password="123$notGood" 
```

This endpoint updates a specific organization.


### HTTP Request

`POST /api/internal/users`

### Request Body
<aside class="notice">
<code>
<br/>{
<br/>&nbsp;&nbsp;"firstName": "Kent",
<br/>&nbsp;&nbsp;"lastName": "Clark",
<br/>&nbsp;&nbsp;"email": "kent.clark@gmail.com",
<br/>&nbsp;&nbsp;"username": "kent.clark@gmail.com"
<br/>&nbsp;&nbsp;"object": "user"
<br/>}
</code>
</aside>

## Delete a Specific User

```java
RequestOptions requestOptions = RequestOptions.builder()
  .setApiKey("elb_4eC39HqLyjWDarjtT1zdp7dc")
  .build();

User user =
  User.retrieve(2367);

User deletedUser = user.delete();
```

```shell
curl https://example.com/api/internal/users/2367 \
   -X DELETE \
   --header "X_ELB_KEY: elb_4eC39HqLyjWDarjtT1zdp7dc" 
```

This endpoint deletes a specific organization.


### HTTP Request

`DELETE /api/internal/users/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the user to delete
