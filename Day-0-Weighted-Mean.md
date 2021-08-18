# Day 0: Weighted Mean

https://www.hackerrank.com/challenges/s10-weighted-mean/problem

```php
<?php

/*
 * Complete the 'weightedMean' function below.
 *
 * The function accepts following parameters:
 *  1. INTEGER_ARRAY X
 *  2. INTEGER_ARRAY W
 */

function weightedMean ($x, $w) {
    $sum = 0;
    foreach ($x as $i => $val) {
       $sum += ($val * $w[$i]);
    }
    $wm = ($sum / array_sum ($w));
    print_r (number_format($wm, 1));
}

$n = intval (trim (fgets(STDIN)));

$vals_temp = rtrim (fgets(STDIN));

$vals = array_map ('intval', preg_split ('/ /', $vals_temp, -1, PREG_SPLIT_NO_EMPTY));

$weights_temp = rtrim (fgets(STDIN));

$weights = array_map ('intval', preg_split('/ /', $weights_temp, -1, PREG_SPLIT_NO_EMPTY));

weightedMean ($vals, $weights);
```