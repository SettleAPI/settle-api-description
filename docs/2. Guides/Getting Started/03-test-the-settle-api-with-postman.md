# Install and use Postman for testing the Settle API

#### In this Postman tutorial, you will learn:

- What is Postman?
- Why Use Postman?
- How to Download and Install POSTMAN
- How to use Postman to execute APIs
- Working with GET Requests
- Working with POST Requests
- Settle Postman Collection

## What is Postman?

[Postman](https://www.postman.com/) is a scalable API testing tool that quickly integrates into CI/CD pipeline. It started in 2012 as a side project by Abhinav Asthana to simplify API workflow in testing and development. API stands for Application Programming Interface which allows software applications to communicate with each other via API calls.

## Why Use Postman?

With over 4 million users nowadays, Postman Software has become a tool of choice for the following reasons:

- Accessibility – To use Postman tool, one would just need to log-in to their own accounts making it easy to access files anytime, anywhere as long as a Postman application is installed on the computer.
- Use of Collections – Postman lets users create collections for their Postman API calls. Each collection can create subfolders and multiple requests. This helps in organizing your test suites.
- Collaboration – Collections and environments can be imported or exported making it easy to share files. A direct link can also be used to share collections.
- Creating Environments – Having multiple environments aids in less repetition of tests as one can use the same collection but for a different environment. This is where parameterization will take place which we will discuss in further lessons.
- Creation of Tests – Test checkpoints such as verifying for successful HTTP response status can be added to each Postman API calls which help ensure test coverage.
- Automation Testing – Through the use of the Collection Runner or Newman, tests can be run in multiple iterations saving time for repetitive tests.
- Debugging – Postman console helps to check what data has been retrieved making it easy to debug tests.
- [Continuous Integration](https://www.guru99.com/continuous-integration.html) – With its ability to support continuous integration, development practices are maintained.


## How to Download and Install Postman

Being an Open Source tool, Postman can be easily downloaded. Here are the steps to install:


### 1. Download Postman

  1. Go to https://www.postman.com/downloads/ and choose your desired platform among Mac, Windows or Linux.
  2. Click `Download` and then install Postman.

### 2. Signup for Postman Account

![011119_1057_PostmanTuto4.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/wm3r1wiMhUc)

> #### Note
>
> There are two ways to sign up for a Postman account. One is to create an own Postman account, and the other is to use a Google account. Though Postman allows users to use the tool without logging in, signing up ensures that your collection is saved and can be accessed for later use.

### 3. Click on Save My Preferences

Select the workspace tools you need and click Save My Preferences

![011119_1057_PostmanTuto5.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/o7vme1JGvXs)

#

### 4. Congratulation!

You will see the Startup Screen

![011119_1057_PostmanTuto6.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/TFGiL6hJJcw)

####

## How to use Postman to execute APIs

Below is the Postman Workspace. Let’s explore the step by step process on **How to use Postman** and different features of the Postman tool.

![011119_1057_PostmanTuto7.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/Qe6u7oJsYXw)


01. **New** – This is where you will create a new request, collection or environment.
02. **Import** – This is used to import a collection or environment. There are options such as import from file, folder, link or paste raw text.
03. **Runner** – Automation tests can be executed through the Collection Runner. This will be discussed further in the next lesson.
04. **Open New** – Open a new tab, Postman Window or Runner Window by clicking this button.
05. **My Workspace** – You can create a new workspace individually or as a team.
06. **Invite** – Collaborate on a workspace by inviting team members.
07. **History** – Past requests that you have sent will be displayed in History. This makes it easy to track actions that you have done.
08. **Collections** – Organize your test suite by creating collections. Each collection may have subfolders and multiple requests. A request or folder can also be duplicated as well.
09. **Request tab** – This displays the title of the request you are working on. By default, “Untitled Request” would be displayed for requests without titles.
10. **HTTP Request** – Clicking this would display a dropdown list of different requests such as `GET`, `POST`, `COPY`, `DELETE`, etc. In Postman API testing, the most commonly used requests are `GET` and `POST`.
11. **Request URL** – Also known as an endpoint, this is where you will identify the link to where the API will communicate with.
12. **Save** – If there are changes to a request, clicking save is a must so that new changes will not be lost or overwritten.
13. **Params** – This is where you will write parameters needed for a request such as key values.
14. **Authorization** – In order to access APIs, proper authorization is needed. It may be in the form of a username and password, bearer token, etc.
15. **Headers** – You can set headers such as content type JSON depending on the needs of the organization.
16. **Body** – This is where one can customize details in a request commonly used in `POST` request.
17. **Pre-request Script** – These are scripts that will be executed before the request. Usually, pre-request scripts for the setting environment are used to ensure that tests will be run in the correct environment.
18. **Tests** – These are scripts executed during the request. It is important to have tests as it sets up checkpoints to verify if response status is ok, retrieved data is as expected and other tests.

####

## Working with GET Requests

Get requests are used to retrieve information from the given URL. There will be no changes done to the endpoint.

We will use the following URL for all examples in this Postman tutorial:

`https://jsonplaceholder.typicode.com/users`

##### In the workspace:

1. Set your HTTP request to GET.
2. In the request URL field, input link
3. Click Send
4. You will see 200 OK Message
5. There should be 10 user results in the body which indicates that your test has run successfully.

![011119_1057_PostmanTuto8.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/wXeO2D5w91A)

> #### Note
>
> There may be cases that Get Postman request may be unsuccessful. It can be due to an invalid request URL or authentication is needed.

####

## Working with `POST` Requests

Post requests are different from Get request as there is data manipulation with the user adding data to the endpoint. Using the same data from the previous tutorial in Get request, let’s now add our own user.

##### 1. Click a new tab to create a new request.

![011119_1057_PostmanTuto9.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/7vTk3O7B2EY)

#

##### 2. In the new tab

  1. Set your HTTP request to POST.
  2. Input the same link in request url: https://jsonplaceholder.typicode.com/users
  3. switch to the Body tab

![011119_1057_PostmanTuto10.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/SWNfShwkHIM)

#

##### 3. In Body,

  1. Click raw
  2. Select JSON

#

##### 4. Copy and paste just one user result from the previous get request like below. 

Ensure that the code has been copied correctly with paired curly braces and brackets. Change id to 11 and name to any desired name. You can also change other details like the address.

```json
[
  {
    "id": 11,
    "name": "Krishna Rungta",
    "username": "Bret",
    "email": "Sincere@april.biz",
    "address": {
      "street": "Kulas Light",
      "suite": "Apt. 556",
      "city": "Gwenborough",
      "zipcode": "92998-3874",
      "geo": {
        "lat": "-37.3159",
        "lng": "81.1496"
      }
    },
    "phone": "1-770-736-8031 x56442",
    "website": "hildegard.org",
    "company": {
      "name": "Romaguera-Crona",
      "catchPhrase": "Multi-layered client-server neural-net",
      "bs": "harness real-time e-markets"
    }
  }
]
```

![011119_1057_PostmanTuto12.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/oyeLsiwIMnI)


> #### Note
>
> Online Post request should have the correct format to ensure that requested data will be created. It is a good practice to use Get first to check the JSON format of the request. You can use tools like https://jsonformatter.curiousconcept.com/

![011119_1057_PostmanTuto13.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/3ZfTMgayqFY)


##### 5. Next

1. Click Send.
2. Status: 201 Created should be displayed
3. Posted data are showing up in the body.

![011119_1057_PostmanTuto14.webp](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/j4ItqomDpPc)


####

## Settle Postman Collection

##### 1. Select Postman Resource

To import both the collection and environment directly into Postman, click the `Run in Postman` button for the API which you wish to integrate.


API | Postman Resource
---------|----------
 Settle Merchant API v1 | [![Run in Postman](https://run.pstmn.io/button.svg)](https://god.gw.postman.com/run-collection/10464426-1e7ad8df-e6fb-4342-8a7f-9ee526461dec?action=collection%2Ffork&collection-url=entityId%3D10464426-1e7ad8df-e6fb-4342-8a7f-9ee526461dec%26entityType%3Dcollection%26workspaceId%3De3cce287-88ec-43e1-8eb4-0ee1a1be5d1a#?env%5BSandbox%5D=W3sia2V5IjoiYmFzZV91cmwiLCJ2YWx1ZSI6Imh0dHBzOi8vYXBpLnNhbmRib3guc2V0dGxlLmV1IiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJtZXJjaGFudF9pZCIsInZhbHVlIjoiNXJnMWRrazgiLCJlbmFibGVkIjp0cnVlfSx7ImtleSI6InVzZXJfaWQiLCJ2YWx1ZSI6IjR0cWhmeHI0IiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJpbnRlZ3JhdG9yX2lkIiwidmFsdWUiOiI3ZTNjYmIxNyIsImVuYWJsZWQiOnRydWV9LHsia2V5Ijoic2V0dGxlbWVudF9hY2NvdW50X2lkIiwidmFsdWUiOiI1cmcxZGtrOCIsImVuYWJsZWQiOnRydWV9LHsia2V5IjoiU0VDUkVUIiwidmFsdWUiOiIyWjQ5X0hvcUVkUHUwVnFHbjZ2eTI2NzkrdFlPVDBGbCIsImVuYWJsZWQiOnRydWV9LHsia2V5IjoiUlNBIiwidmFsdWUiOiIiLCJlbmFibGVkIjp0cnVlfSx7ImtleSI6InJldHVybmVkX2NsaWVudF9pZCIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJkZWZhdWx0X3JlZGlyZWN0X3VyaSIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJwb3NfdGlkIiwidmFsdWUiOiIiLCJlbmFibGVkIjp0cnVlfSx7ImtleSI6InJldHVybmVkX3JpZCIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJwb3NfaWQiLCJ2YWx1ZSI6IiIsImVuYWJsZWQiOnRydWV9LHsia2V5IjoicmVxdWVzdF9kZXNjcmlwdGlvbiIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJpZGVtcG90ZW5jeV9pZCIsInZhbHVlIjoiIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJjaGF0X3RleHQiLCJ2YWx1ZSI6IiIsImVuYWJsZWQiOnRydWV9LHsia2V5IjoiY3VycmVudExvY2FsVGltZXN0YW1wIiwidmFsdWUiOiIiLCJlbmFibGVkIjp0cnVlfSx7ImtleSI6InRpZCIsInZhbHVlIjoicGFlZTZiaGVxODViIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJzaG9ydGxpbmtfaWQiLCJ2YWx1ZSI6Im1RNzlUIiwiZW5hYmxlZCI6dHJ1ZX0seyJrZXkiOiJzdGF0dXNfY29kZSIsInZhbHVlIjoiNDEzIiwiZW5hYmxlZCI6dHJ1ZX1d)

> #### Note
>
> If the above buttons do not work, you can download the collections here, respectively:
>   - [Settle Merchant API v1](https://www.getpostman.com/collections/bb5bc8d26d571f26134c)


##### 2. Import Files

After clicking Run in Postman above, follow the steps in the Postman landing page to open the Postman application.

The Postman collection will appear in the left sidebar.

  1. Select the associated environment from the drop-down menu.
  2. Click the eye to see all variables.
 

##### 3. Insert Values

The Postman environment comes prefilled with some values, but there are still some required values which you must enter manually. For a complete overview over such values and where to find them, see [Postman Variable Overview](#postman-variables-overview).

  - Click `Edit` and paste in values for each variable.


### Tabs

Some methods require a body with information that is sent with the request. Settle provides pre-populated test data, but this can be modified.

You might want to make the same request from your own application.

You can generate snippets of code in various languages that will help you do this.

  - Click the `Code` link to open the `Generate code` snippets modal.


### Postman Variables Overview

This is an overview of where to obtain Postman values for each of our APIs.

Follow the instructions in [this article](./ZG9jOjM0ODE0NTcz-the-sandbox-environment) to create and obtain your Sandbox values.


#### Common Variables

These variables are required for all Settle APIs.

Variable | Description
-|-
api_user_id | `X-Settle-User`
merchant_id | `X-Settle-Merchant`

#### Merchant API Specific Variables

Variable | Description
-|-
mobileNumber | Mobile number which the payment request is sent to. 
successPrefix | URL for redirecting users after successful payment.
failurePrefix | URL for redirecting users after failed payment.
callbackPrefix | Merchant hosted endpoint where Settle will send transaction updates. 
action | Action to perform on payment request. [What is this?](./settleapis/b3A6ODY4MjgyNA-merchant-payment-request-create#request-body)
currency | The currency used for the payment. [What is this?](./settleapis/c2NoOjQwNjM0Ng-currency)

<!-- theme: success -->
> #### Tip
>
> We're always happy to help with code or other questions you might have! Please [submit a request](https://support.settle.eu/hc/en-150/requests/new) to contact us.



