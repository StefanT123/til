# Deep clone object

```js
var cloner = {
    _clone: function _clone(obj) {
        if (obj instanceof Array) {
            var out = [];

            for (var i = 0, len = obj.length; i < len; i++) {
                var value = obj[i];
                out[i] = (value !== null && typeof value === "object") ? _clone(value) : value;
            }
        } else {
            var out = {};

            for (var key in obj) {
                if (obj.hasOwnProperty(key)) {
                    var value = obj[key];
                    out[key] = (value !== null && typeof value === "object") ? _clone(value) : value;
                }
            }
        }

        return out;
    },
    clone: function(it) {
        return this._clone({
            it: it
        }).it;
    }
};

var newObject = cloner.clone(oldObject);
```

---

```js
function cloneObject(obj) {
    // Handle the 3 simple types, and null or undefined
    if (null == obj || "object" != typeof obj) return obj;

    // Handle Date
    if (obj instanceof Date) {
        copy = new Date();
        copy.setTime(obj.getTime());

        return copy;
    }

    // Handle Array
    if (obj instanceof Array) {
        let copy = [];
        for (var i = 0, len = obj.length; i < len; i++) {
            copy[i] = cloneObject(obj[i]);
        }

        return copy;
    }

    // Handle Object
    if (obj instanceof Object) {
        let copy = {};
        for (var attr in obj) {
            if (obj.hasOwnProperty(attr)) copy[attr] = cloneObject(obj[attr]);
        }

        return copy;
    }

    throw new Error("Unable to copy obj! Its type isn't supported.");
}
```
