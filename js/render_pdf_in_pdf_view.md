# Render PDF in PDF view

```js
// Fetch raw binary PDF data
const response = await fetch('https://some.pdf');
// Extract response body as Blob
const blob = await response.blob();
// Create an URL pointing to the object
const url = URL.createObjectURL(blob);

// Render a PDF viewer
// <object data={url} type="application/pdf"></object>
```
