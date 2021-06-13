# **What is an REST API and how to build one with Firebase Functions**

## **First, what is an RESTful API?**

A Representational State Transfer (or just REST) is a particular style of software architecture designed for network applications. A REST API is one of the most common APIs on the internet today. The pattern of a REST api is quite easy to build, these patterns can be used to make many different sources available from a web URL. This URL link can then be fetched/loaded onto a website or platform, making the data available within the application.

### **Why is an API useful?**

An API can be a good addition to an application. For example, if you are working on a new platform, and you want to load tweets from a specific user into it in real-time, you can use the Twitter API. This API ensures that the data from twitter becomes available within the application. Or if you are building a platform for a customer, and they want to build a platform with all kinds of images, then the unsplash API is ideal for this.

All in all, it means that you can make an enormous amount of data from the internet usable within your application. Most APIs are free to use, making them a good option for developers when they want to add an API.

## **What is Firebase**

First a short introduction to Firebase, Firebase uses a Backend as a Service (Boss) model, which means it uses a serverless environment. This allows you to build an application quite easily without having to code your own server. While that's handy, sometimes it comes in handy to use a server anyway because you don't want to use something specific on the front-end, but want to store it in a database.

### **And how about Firebase Functions**

Firebase Functions (Cloud Functions) is a serverless framework that provides to run your backend code in response to triggered events from the frontend. The functions are triggered by Firebase features & HTTPS requests. The JavaScript file on the backend will be stored inside the Google Cloud Storage, and runs on their server. This means that no server maintenance is required. The code that is written is hosted on a firebase service. The code can then connect to other Firebase services, such as Firestore, Hosing, Authentication or Storage. Firebase Cloud Functions run on the NodeJS environment, which ensures that you can write all functions in JavaScript or TypeScript.

## **How does it works?**

### **Create Firebase environment for your project**

Before you can get started building your own API, you need to create a few things. For example, you have to create a new project in the [Firebase ​console](https://console.firebase.google.com/).

![Create firebase environment](https://user-images.githubusercontent.com/48051912/121822436-60278080-cc9f-11eb-93b9-d92632633635.jpg)

You also have to convert your payment plan to a 'Pay as you go', which means that you pay per API request. The first 2 million requests are free, after that a certain amount will be debited from your account.

![Change pay options to pay as you go](https://user-images.githubusercontent.com/48051912/121822438-6289da80-cc9f-11eb-8a45-0fbb1b8c38e2.png)

### **Set up Node.js and Firebase tools**

Before you can create a local Firebase environment, you will need to install Node.js and NPM. The best way to start is installing Node on your device from [here](https://nodejs.org/en/). After the installation is complete, the next step is to download the Firebase CLI. To install the CLI via npm, use:

```bash
  npm install -g firebase-tools
```

### **Initialize your project**

After installing the tools, to work with Firebase on your development device, it's neccessary to init the firebase project. You can create a empty project, with a bit of boilerplate code, code language (TypeScript or JavaScript), and linting options.

#### **1. Initialize project**

```
  firebase login
```

```
  firebase init functions
```

#### **2. Choose project type**

```
  Use an existing project
```

#### **3. Set up code environment options**

Choose your prefered code options. JavaScript or TypeScript, linter or not, and install dependencies right away.

**The code structure should look like this:**

```markdown
myproject/
+-- .firebaserc
+-- firebase.json
+-- functions/ #
| +-- .eslintrc.json
| +-- package.json
| +-- index.js
| +-- node_modules/
```

#### **4. Import required packages, functions and create export**

```js
const functions = require('firebase-functions');
const express = require('express');
const app = express();

const admin = require('firebase-admin');
admin.initializeApp();

app.get('/api', (req, res, next) => {
  // Send get request, for example: data from DB
  res.json({ result: 'GET succeed' });
});

app.post('/api', (req, res, next) => {
  // Handle posted data, for example: save it in DB
  res.json({ result: 'POST succeed' });
});

exports.app = functions.https.onRequest(app);
```

#### **Congratulations, your first Firebase Function!**

You have now written your first function. The structure of Firebase functions works exactly the same as within a Node.js application with an Express framework. The server can be started with the script `npm run serve`, a local development API will be created.

### **How to use the API inside your front-end environment**

Now that you've written a simple API, you naturally want it to be usable in your frontend. The best way to do this is to fetch the data. Below I give an example of how this is applied in React, in combination with axios.

#### **Fetch data with axios**

By using the axios package, you can quite easily fire a HTTP request inside an JavaScript application. To use this package, the only thing you'll need to provide is importing the package. Because you only want to fetch the data inside the component once, you'll need to use the `useEffect` hook to call the function, when the component is mounted.

```js
// Import package inside component
import axios from 'axios';
import { useEffect } from 'react';

// inside asynchronos function
const data = await axios.get(`/api/order-details`).then((res) => {
  console.log(res.data);
});

useEffect(() => {
  getData();
}, []);
```

#### **Store data inside state**

After fetching the data, the data need to be used inside a state. By using `useState` within react, it is possible to store the data here. Nadat de data is ingeladen zal het element worden geupdatem met de nieuwe data..

```js
import { useState, useEffect } from 'react';

const [data, setData] = useState(null);

const data = await axios.get(`/api/order-details`).then((res) => {
  setData(res.data);
});

useEffect(() => {
  getData();
}, []);
```

#### **Component**

Now that the data has been loaded and read on the page, it is possible to retrieve data from the API. The entire component looks like this:

```js
import { useState, useEffect } from 'react';
import axios from 'axios';

const AboutComponent = async () => {
  const [data, setData] = useState(null);
  const getData = async () => {
    try {
      const data = await axios.get(`/api/order-details`).then((res) => {
        setData(res.data);
      });
    } catch (e) {
      console.log(e);
    }
  };

  useEffect(() => {
    getData();
  }, []);

  return <p>{data}</p>;
};
```

**Post data**

If data needs to be sent to the API, for example to store in the database, it looks like below. The data is then brought in in a post route within Firebase Functions, for further processing.

```js
const postData = async () => {
  const loggedInUseer = {
    name: 'John',
    lastName: 'Doe',
  };

  const res = await axios.post('/api/reservations', loggedInUser).then((res) => console.log(res));
};
```

### **Deploy Firebase Functions**

After you've got the app working through the localhost test environment, it's just a matter of deploying the application, so that it produces a definitive URL that can be used within a project. With the run script `npm run deploy` you can easily deploy the final version.
