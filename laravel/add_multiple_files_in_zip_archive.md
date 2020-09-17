# Add multiple files in zip archive

If you want to create ZIP archive and add multiple files in it for download.
**NOTE**: you would need PHP ZipArchive class - [ZIP Archive](https://www.php.net/manual/en/class.ziparchive.php)
```php
$zip_file = 'invoices.zip';
$zip = new \ZipArchive();
$zip->open($zip_file, \ZipArchive::CREATE | \ZipArchive::OVERWRITE);

$path = storage_path('invoices');
$files = new \RecursiveIteratorIterator(new \RecursiveDirectoryIterator($path));
foreach ($files as $name => $file)
{
    // We're skipping all subfolders
    if (!$file->isDir()) {
        $filePath     = $file->getRealPath();

        // extracting filename with substr/strlen
        $relativePath = 'invoices/' . substr($filePath, strlen($path) + 1);

        $zip->addFile($filePath, $relativePath);
    }
}
$zip->close();
return response()->download($zip_file);
```
