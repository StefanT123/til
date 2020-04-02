# Timestamps with timezone

In migrations there's not only `timestamps()` but also `timestampsTz()`, for the timezone

Also, there are columns dateTimeTz(), timeTz(), timestampTz(), softDeletesTz().
```php
Schema::create('employees', function (Blueprint $table) {
    $table->increments('id');
    $table->string('name');
    $table->string('email');
    $table->timestampsTz();
});
```
