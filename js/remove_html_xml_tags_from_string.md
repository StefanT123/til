# Remove HTML/XML tags fro string

```js
const stripHTMLTags = str => str.replace(/<[^>]*>/g, '');

stripHTMLTags('<p><em>lorem</em> <strong>ipsum</strong></p>'); // 'lorem ipsum'
```
