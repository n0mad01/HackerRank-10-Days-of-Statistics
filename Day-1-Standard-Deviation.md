# Day 1: Standard Deviation

https://www.hackerrank.com/challenges/s10-standard-deviation/problem

Given an array, arr, of n integers, calculate and print the standard deviation. Your answer should be in decimal form, rounded to a scale of 1 decimal place (i.e., 12.3 format). An error margin of +-0.1 will be tolerated for the standard deviation.

```php
<?php

/*
 * Complete the 'stdDev' function below.
 *
 * The function accepts INTEGER_ARRAY arr as parameter.
 */

function stdDev ($arr) {
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

$n = intval (trim (fgets (STDIN)));

$vals_temp = rtrim (fgets (STDIN));

$vals = array_map ('intval', preg_split ('/ /', $vals_temp, -1, PREG_SPLIT_NO_EMPTY));

stdDev ($vals);
```