# Details tag

The `<details>` tag provides on demand details to the user. If you have a need to show content to the user on demand, use this tag. By default, the widget is closed. When open, it expands, and displays the content within.

The `<summary>` tag is used with `<details>` to specify a visible heading for it.
```html
<details>
    <summary>Click Here to get the user details</summary>
    <table>
        <tr>
            <th>#</th>
            <th>Name</th>
            <th>Location</th>
            <th>Job</th>
        </tr>
        <tr>
            <td>1</td>
            <td>Adam</td>
            <td>Huston</td>
            <td>UI/UX</td>
        </tr>
    </table>
</details>
```
