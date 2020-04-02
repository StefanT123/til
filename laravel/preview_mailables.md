# Preview mailables

If you use Mailables to send email, you can preview the result without sending, directly in your browser. Just return a Mailable as route result
```php
Route::get('/mailable', function () {
    $invoice = App\Invoice::find(1);
    return new App\Mail\InvoicePaid($invoice);
});
```
