# Persist request data when redirecting

Chain withInput() onto your redirects and the request values will get persisted to the redirect location - by flashing data to the session under the hood.

Includes querystrings and POST data
```php
// Call withInput() on any kind of redirect response
return redirect()->to('/some-page')->withInput();

// (this also works)
return back()->withInput();

// It stores the values in the session under the following key
"_old_input" => ['key' => 'value'];

// Which you can access in your controlle/views via:
old('key');
```
