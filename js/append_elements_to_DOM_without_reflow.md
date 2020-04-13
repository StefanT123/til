# Append elements to DOM without reflow

Under the hood, for every time we append the countryCard to the parentElement, we're causing a browser reflow
```js
// Select the parent element
const parentElement = document.querySelector('.countries');
// Loop over the array of countries and create each element
countries.forEach(country => {
    // Create a new div element
    const countryCard = document.createElement('div');
    // Create a new image element
    const img = document.createElement('img');
    // Set the src attribute of the image to the flag value from the data
    img.src = country.flag;
    // Attach the image to the div we initially created
    countryCard.appendChild(img);
    // Attach the card to parent element
    parentElement.appendChild(countryCard);
});
```

The right way
```js
let fragment = new DocumentFragment();
// or let fragment = document.createDocumentFragment();
const parentElement = document.querySelector('.countries');
// Loop over the array of countries and create each element
countries.forEach(country => {
    // Create a new div element
    const countryCard = document.createElement('div');
    // Create a new image element
    const img = document.createElement('img');
    // Set the src attribute of the image to the flag value from the data
    img.src = country.flag;
    // Attach the image to the div we initially created
        countryCard.appendChild(img);
    // Append card to fragment element
    fragment.appendChild(countryCard);
});
// After iterating, we then insert fragment contents into the DOM
parentElement.appendChild(fragment);
```
