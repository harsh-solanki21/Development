# Callback Hell / Pyramid of Doom

- Nested callbacks stacked below one another forming a pyramid structure.
- This style of programming becomes difficult to understand and manage.
- Callback hell is a situation where multiple nested callback functions create code that's difficult to read, understand, and maintain. It occurs when we chain asynchronous operations, each requiring a callback function that executes only after the previous operation finishes.

```javascript
// Exmaple 1:
fetchRandomJoke((joke) => {
  console.log(joke);

  translateJoke(joke, (translatedJoke) => {
    console.log(translatedJoke);

    postJoke(translatedJoke, () => {
      console.log("Joke posted successfully!");
    });
  });
});

// Example 2:
getUserData(function (userData) {
  getAddressFromUserData(userData, function (address) {
    getWeatherData(address, function (weatherData) {
      console.log(
        `The weather in ${address.city} is currently ${weatherData.temperature}°C.`
      );
    });
  });
});
```
