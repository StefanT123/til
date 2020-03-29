# Calculate the similarity between two strings

```php
similar_text(str1, str2, &percent); // Calculate the similarity between two strings


// EXAMPLE #1:

$word1 = "Connotation";
$word2 = "Annotation";
$match = similar_text($word1, $word2);
echo "$match letters are the same between '$word1' and '$word2'\n";

// EXAMPLE #2:

$word1 = "Connotation";
$word2 = "Annotation";
$match = similar_text($word1, $word2, $percent);
$percent = round($percent, 2);
echo "$match letters are the same between '$word1' and '$word2': a $percent% match.\n";

```
