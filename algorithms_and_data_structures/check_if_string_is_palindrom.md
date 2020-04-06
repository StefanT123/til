# Check if the string is palindrom

Pseudocode:
1. If the string is made of no letters or just one letter, then it is a palindrome.
2. Otherwise, compare the first and last letters of the string.
3. If the first and last letters differ, then the string is not a palindrome.
4. Otherwise, the first and last letters are the same. Strip them from the string, and determine whether the string that remains is a palindrome. Take the answer for this smaller string and use it as the answer for the original string.
```js
// Returns the first character of the string
var firstCharacter = function(str) {
    return str.slice(0, 1);
};

// Returns the last character of a string
var lastCharacter = function(str) {
    return str.slice(-1);
};

// Returns the string that results from removing the first
//  and last characters
var middleCharacters = function(str) {
    return str.slice(1, -1);
};

var isPalindrome = function(str) {
    if (str.length <= 1) {
        return true;
    }

    if (firstCharacter(str) !== lastCharacter(str)) {
        return false;
    }

    return isPalindrome(middleCharacters(str));
};
```
