# Building HTTP query

```php
$workspace_name = $workspace->name;
$api_key        = config('custom.map_api_key');

$url = 'https://maps.googleapis.com/maps/api/place/textsearch/json?';
$params = [
    'query'     => $workspace_name,
    'sensor'    => 'true',
    'key'       => $api_key
];
$url .= http_build_query($params, '', '&');
```
