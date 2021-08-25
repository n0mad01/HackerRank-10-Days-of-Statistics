# Day 1: Quartiles

https://www.hackerrank.com/challenges/s10-quartiles/problem

Given an array, arr, of n integers, calculate the respective first quartile (Q1), second quartile (Q2), and third quartile (Q3). It is guaranteed that Q1, Q2, and Q3 are integers.

```php
<?php
/*
 * Complete the 'quartiles' function below.
 *
 * The function is expected to return an INTEGER_ARRAY.
 * The function accepts INTEGER_ARRAY arr as parameter.
 */

/**
 *  given the input is:
 *  9
 *  3 7 8 5 12 14 21 13 18
 */

function getQuartile ($arr, $quartile) {
  $pos = (count ($arr) - 1) * $quartile;
 
  $base = floor ($pos);
  $rest = $pos - $base;
  // print_r($base . ' ::: ' . $rest . PHP_EOL);
 
  if (isset ($arr[$base+1])) {
    if (count ($arr) % 2 == 0) {
    } else {
    }
    return $arr[$base] + $rest * ($arr[$base+1] - $arr[$base]);
  } else {
    return $arr[$base];
  }
}

function quartiles ($arr) {
    sort ($arr);
    // print_r($arr);
    $c = count ($arr);
    $m = floor ($c / 2);

    $median_l = round (getQuartile($arr, 0.25));
    $median_x = round (getQuartile($arr, 0.5));
    $median_u = round (getQuartile($arr, 0.75));
    
    return [
        $median_l,
        $median_x,
        $median_u
    ];
}


$fptr = fopen(getenv("OUTPUT_PATH"), "w");

$n = intval(trim(fgets(STDIN)));

$data_temp = rtrim(fgets(STDIN));

$data = array_map('intval', preg_split('/ /', $data_temp, -1, PREG_SPLIT_NO_EMPTY));

$res = quartiles($data);

fwrite($fptr, implode("\n", $res) . "\n");

fclose($fptr);
```