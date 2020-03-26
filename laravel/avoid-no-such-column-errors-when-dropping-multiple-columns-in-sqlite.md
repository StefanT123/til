# Avoid "no such column" error when dropping multiple columns in sqlite

If we are dropping multiple tables from the database in sqlite (usually when running `migrate:refresh`), instead if this:
```php
Schema::table('products', function (Blueprint $table) {
    # This can cause "no such column" errors in SQLite
    $table->dropColumn('sku');
    $table->dropColumn('base_price');
    $table->dropColumn('description');
});
```

We should do this:
```php
Schema::table('products', function (Blueprint $table) {
    $table->dropColumn([
        'sku',
        'base_price',
        'description'
    ]);
});
```
