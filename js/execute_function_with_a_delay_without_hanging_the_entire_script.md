# Execute function with a delay without hanging the entire script

The timedProcessArray function blocks UI Threed for 25 ms, performing a chain of actions, then releases UI Threed for 25 ms and so on.
```js
function timedProcessArray(items, process, callback) {
    var todo = items.concat();   //create a clone of the original
    setTimeout(function () {
        var start = +new Date();
        do {
            process(todo.shift());
        } while (todo.length > 0 && (+new Date() - start < 50));
        if (todo.length > 0){
            setTimeout(arguments.callee, 25);
        } else {
            callback(items);
        }
    }, 25);
}

// example
function saveDocument(id) {
    var tasks = [openDocument, writeText, closeDocument, updateUI];
    timedProcessArray(tasks, [id], function() {
        alert("Save completed!");
    });
}
```
