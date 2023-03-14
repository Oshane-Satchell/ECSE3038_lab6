# Lab 6

Summary

**In this lab, a platform creatd  to control electronic devices connected to an ESP32 module. Two applications were written, one to be used as an API accessible over the internet, and the other as an Arduino sketch for the ESP32. Pins 22 and 23 were used for the Fan and Light pins, respectively. The ESP32 sent a PUT request to the API containing the current temperature, and a GET request to determine the state of the fan and light pins. The API was deployed to an online cloud hosting service, and the GET request handler which returned a JSON body with the fan and light attributes. The fan attribute was set to true if the temperature is greater than or equal to 28.0, and false otherwise. The light attribute was set to true if the current time is later than today's sunset time obtained from an external API, and false otherwise. The PUT request handler returned an HTTP 204 status code on success and an HTTP 400 otherwise, and the request body was saved directly to the database.**

For this lab, students will be implementing part of an end-to-end platform to be used to control the state of electronic devices connected to the ESP32 module.

Students will be asked to write two separate applications, one to be used as an API that should be accessible over the internet and the other to used as an arduino sketch to be programmed on to ESP32 module.

## Embedded

For consistency, use pins 22 and 23 for your Fan and Light pins respectively.

Also, use the variable names WIFI_USER and WIFI_PASS as the wifi information in your arduino code.

### PUT request

Create a function that reads the current temperature from a connected digital temperature sensor. This temperature value should be used to populate the body of a PUT request that should be sent form the ESP32 to your API.

```
PUT /api/temperature HTTP/1.1
Host: {https://your.api.domain}
Content-type: application/json
Content-length: 23

{ "temperature": 29.2 }
```

If you don't have access to a digital temperature sensor, you may create a function that generates and returns a random float between 21.0 and 33.0. 

### GET request

Your ESP32 module code should also include a get request that should be sent to your API.

```
GET /api/state HTTP/1.1
Host: {https://your.api.domain}
```

The response of this request should determine how your circuit reacts, ie, the state of your fan pin and light pin.

## API

You’ll be expected to make your API available over the internet by deploying your server application to an online cloud hosting service like [https://render.com/](https://render.com/).

Make sure that your code works from your local machine first then commit to GitHub so that render has access to it.

### GET request

The API response from the GET request handler should contain a JSON body that has a fan and and light attribute. 

The fan attribute of the JSON response should be true if the current temp in the database is greater than or equal to 28.0 and it should be false otherwise. 

The light attribute should be true if the current time is later than todays sunset time according to the below API, and should be false otherwise. 

```
GET /api/sunset HTTP/1.1
Host: https://ecse-sunset-api.onrender.com
```

### PUT request

The API response from the PUT request handler should return am HTTP 204 status code on a successful PUT and return an HTTP 400 otherwise.

Your request body from the ESP32 should be saved directly to the database.

## Submission

Your GitHub repository should be organised as follows:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4289dd66-ad66-4880-ac6c-d9ee36545d0f/Untitled.png)

Due date is Sunday March 12, 2023.

The repo name must be "ECSE3038_lab6".

Include a README.md. This readme should outline what was done to complete the lab.

Also include a link to your API URL in the readme.

Your repository should **NOT** include the `.vscode` folder at all.

Remember to ignore your `env.h` file.

You're only required to provide a link to your GitHub repository. 

Any commits made to the repo after the due date will not be considered.
