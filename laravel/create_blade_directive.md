# Create blade directive

It’s very easy - just add your own method in ​app/Providers/AppServiceProvider.php​
For example, if you want to have this for replace `<br>` tags with new lines
`<textarea>@br2nl($post->post_text)</textarea>`

Add this directive to `AppServiceProvider`’s ​`boot()​` method
```php
public function boot()
{
    Blade::directive('br2nl', function ($string) {
        return "<?php echo preg_replace('/\<br(\s*)?\/?\>/i', \"\n\", $string); ?>";
    });
}
```
