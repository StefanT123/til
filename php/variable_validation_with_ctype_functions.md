# Variable validation with ctype functions

The matches are absolute, which means that ctype_digit() will return false for the value "123456789a" because of the "a" at the end
```php
ctype_alnum(text) // matches A-Z, a-z, 0-9
ctype_alpha(text) // matches A-Z, a-z
ctype_cntrl(text) // matches ASCII control characters
ctype_digit(text) // matches 0-9
ctype_graph(text) // matches values that can be represented graphically
ctype_lower(text) // matches a-z
ctype_print(text) // matches visible characters (not whitespace)
ctype_punct(text) // matches all non-alphanumeric characters (not whitespace)
ctype_space(text) // matches whitespace (space, tab, new line, etc)
ctype_upper(text) // matches A-Z
ctype_xdigit(text) // matches digits in hexadecimal format
```
