# Output tag

The `<output>` tag represents the result of a calculation. Typically this element defines a region that will be used to display text output from some calculation.
```html
<form oninput="x.value=parseInt(a.value) * parseInt(b.value)">
   <input type="number" id="a" value="0"> * <input type="number" id="b" value="0"> = <output name="x" for="a b"></output>
</form>
```

If you are performing any computation in the client side JavaScript and, want the result to reflect on the page, use `<output>` tag. You do not have to walk the extra steps of getting an element using `getElementById()`.
