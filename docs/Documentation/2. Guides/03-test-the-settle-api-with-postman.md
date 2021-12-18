# Install and use Postman for testing the Settle API

#### In this Postman tutorial, you will learn:

- What is Postman?
- Why Use Postman?
- How to Download and Install POSTMAN
- How to use Postman to execute APIs
- Working with GET Requests
- Working with POST Requests

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
16. **Body** – This is where one can customize details in a request commonly used in POST request.
17. **Pre-request Script** – These are scripts that will be executed before the request. Usually, pre-request scripts for the setting environment are used to ensure that tests will be run in the correct environment.
18. **Tests** – These are scripts executed during the request. It is important to have tests as it sets up checkpoints to verify if response status is ok, retrieved data is as expected and other tests.