# Day 1: Standard Deviation

https://www.hackerrank.com/challenges/s10-standard-deviation/problem

```php
<?php

/*
 * Complete the 'stdDev' function below.
 *
 * The function accepts INTEGER_ARRAY arr as parameter.
 */

function stdDev($arr) {
    // Print your answers to 1 decimal place within this function
    sort ($arr);
    $mean = (array_sum ($arr) / count ($arr));
    $sd_sum = 0;
    
    foreach ($arr as $i => $val) {
        $sd_sum += (pow (($val - $mean), 2));
    }
    
    $sd = round (sqrt ($sd_sum / count ($arr)), 1);
    print_r (number_format ($sd, 1, '.', ''));
}

$n = intval(trim(fgets(STDIN)));

$vals_temp = rtrim(fgets(STDIN));

$vals = array_map('intval', preg_split('/ /', $vals_temp, -1, PREG_SPLIT_NO_EMPTY));

stdDev($vals);
```