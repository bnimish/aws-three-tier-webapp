# Build a Three-Tier Web App

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-threetier)

**Author:** nimish bali

---

## Build a Three-Tier Web App

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_2b3c4d5e)

---

## Introducing Today's Project!

In this hands-on project, I will demonstrate AWS services and capabities by creating a three tier webapp solution. It has Presentation,Logic and Data layers which will be independently built but tied together. 

### Tools and concepts

- Store website files with **S3.**
- 🌎 Deliver content globally with **CloudFront**.
- 🧠 Write serverless code with **Lambda**.
- 🚪 Create and manage APIs with API **Gateway**.
- 💾 Store and retrieve data with **DynamoDB**.

### Project reflection

This project took me approximately 2.5 hours. The most challenging part was troubleshooting console errors at testing the coudfront site. It was most rewarding to figure out the cause and apply resolution to the lambda and take an overall view of all the layers.

I chose to do this project today because I want to gets hand on AWS services.

---

## Presentation tier

For the presentation tier, I will set up s3 and cloudfront to host website and make it available to the IAM user via cloudfront only, blocking all public access.

I accessed my delivered website by cloudfront distribution on the browser

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_3a4b5c6d)

---

## Logic tier

For the logic tier, I will set up Lambda function to handle the requests (lookup into data) and also API in API gateway will receive request from user and route it to lambda for processing.

The Lambda function retrieves data by looking up by user id in DynamoDB.
Connects to DB
Looks up data - if found returns the data else returns error.

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_6a7b8c9d)

---

## Data tier

For the data tier, I will set up DynamoDB database to store user data. Lambda will lookup for user data from this database for user id provided.

The partition key for my DynamoDB table is userId which means, it will be used to lookup data for the item in the table based on that key.

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_u1v2w3x4)

---

## Logic and Data tier

Once all three layers of my three-tier architecture are set up, the next step is to test the data fetch through the api invoke.

To test my API, I... The results were:

{
  "email": "test@example.com",
  "name": "Test User",
  "userId": "1"
}

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_a112c3d5)

---

## Console Errors

Placeholder was not replaced by actual invoke link

To resolve the error, I updated script.js by replacing the file and  I then re-uploaded it into S3 because it had proper values for link

I ran into a second error after updating script.js. This was an error with... because...
/favicon.ico:1  GET https://d37ki7gfri9e8w.cloudfront.net/favicon.ico 403 (Forbidden)
(index):1 Access to fetch at 'https://6fjnm36mzd.execute-api.us-east-1.amazonaws.com/prod/users?userId=1' from origin 'https://d37ki7gfri9e8w.cloudfront.net' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
script.js:9  GET https://6fjnm36mzd.execute-api.us-east-1.amazonaws.com/prod/users?userId=1 net::ERR_FAILED 200 (OK)
fetchUserData @ script.js:9
onclick @ (index):13
script.js:19 Failed to fetch user data: TypeError: Failed to fetch
    at fetchUserData (script.js:9:32)
    at HTMLButtonElement.onclick ((index):13:43)
fetchUserData @ script.js:19
await in fetchUserData
onclick @ (index):13


![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_a1b2c3d5)

---

## Resolving CORS Errors

To resolve the CORS error, I first enabled CORS

I also updated my Lambda function because it was missing the CORS header and it needed the actual ivoke link to be in allowed paths which is more secure way to implement.

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_1qthryj2)

---

## Fixed Solution

I verified the fixed connection between API Gateway and CloudFront by using the UI app and passing userId which returned the data that was stored in DynamoDB.

![Image](http://learn.nextwork.org/fulfilled_orange_serene_sea_otter/uploads/aws-compute-threetier_2b3c4d5e)

---

---
