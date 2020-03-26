# Handle 419 session token expired error in SPA context

If you're making AJAX calls to CSRF protected endpoints in a SPA context, you'll want to handle situations where the session token expires before a full-page reload

Here's a minimal solution with axios to intercept any 419 failed calls to obtain a new CSRF token
```js
window.axios.interceptors.response.use(null, function (error) {
    if (error.response && error.response.status === 419) {
        axios.get('/csrf').then(res => {
            let token = res.data;

            // Set the CSRF token in the header for all future requests
            window.axios.defaults.headers.common['X-CSRF-TOKEN'] = token;

            // Set the CSRF token for this request before retrying it
            error.config.headers['X-CSRF-TOKEN'] = token;
            return axios.request(error.config);
        });
    }

    return Promise.reject(error);
});
```

```php
Route::get('/csrf', function () {
    return csrf_token();
});
```
