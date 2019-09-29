# Client-Server Communication Discussion Questions

## Objectives

* Explain what the `fetch` function is used for
* Use `fetch` to retrieve data from a server

## Exercise

Take a look at each of the code samples below. Each example will show you some code, as well as either the return value of what is logged to the console.

1. How does this piece of code work?
2. Why does the code do what it does?
3. Given this code sample, what can you learn or describe about JavaScript

### Example 1

```javascript
const url = "https://data.cityofnewyork.us/api/views/p94q-8hxh" // CityBike Data from data.gov
const data = fetch(url)

console.log(data) // Promise {<pending>}
```
1. This piece of code works by making a GET request to the URL provided. It returns a `Promise` which is resolved to the server's response to that request.
2. The URL is an address to a resource. `fetch()` by default will make a GET request at the URL provided. Since it takes time for the request to be made and the server to respond, JavaScript handles it asynchronously by immediate return a `Promise` that can be resolved to the response once it arrives.
3. JavaScript is the verb of a browser and website, shipping and receiving information and making a website more dynamic. It runs asynchronously [on a single thread](https://stackoverflow.com/questions/8963209/does-async-programming-mean-multi-threading) to facilitate transactions and handle events.

### Example 2

```javascript
const url = "https://data.cityofnewyork.us/api/views/p94q-8hxh" // CityBike Data from data.gov
fetch(url).then(console.log)
// Response {type: "cors", url: "https://data.cityofnewyork.us/api/views/p94q-8hxh", redirected: false, status: 200, ok: true, …}
```
1. Here we resolve the `Promise` returned by `fetch()` using then `.then` method, inside of which the results are implicitly passed to the `console.log` method (the second line could also be written `fetch(url).then(response => console.log(response));`). The `Response` object contents meta(data) from the server in response to the original GET request.
2. This code does what it does because a `Promise` must be resolved with callback functions in a `.then` method to get at the good. The `Response` object is the way in which JavaScript's Fetch API packages a server's response to a request.
3. This code highlights a few features of JavaScript: asynchronicity, callback functions, and implicit function calling. Additionally, many features that we consider integral to our usage of JavaScript are themselves relatively new or tacked on to the JavaScript body. 

### Example 3

```javascript
const url = "https://data.cityofnewyork.us/api/views/p94q-8hxh" // CityBike Data from data.gov
fetch(url)
  .then(function(response){
    return response.json()
  }).then(console.log)
// {id: "p94q-8hxh", name: "Citi Bike Live Station Feed (JSON)", attribution: "CitiBike", attributionLink: "http://citibikenyc.com/stations/json", averageRating: 0, …}```
```
1. In this code, we resolve the original GET request by JSON-ifying the contents of the server's response, after which we log it to the console.
2. [According to MDN](https://developer.mozilla.org/en-US/docs/Web/API/Body/json),
> The `json()` method of the `Body` mixin takes a `Response` stream and reads it to completion. It returns a `Promise` that resolves with the result of parsing the body text as JSON. 
3. There's a lot of layers!

### Bonus

How would you implement a function called `getJSON` so that the below code works as outlined?

```javascript
const url = "https://data.cityofnewyork.us/api/views/p94q-8hxh" // CityBike Data from data.gov

getJSON(url).then(console.log)
// {id: "p94q-8hxh", name: "Citi Bike Live Station Feed (JSON)", attribution: "CitiBike", attributionLink: "http://citibikenyc.com/stations/json", averageRating: 0, …}``
```
```javascript
function getJSON(url) {
  return fetch(url).then(response => response.json());
};
```