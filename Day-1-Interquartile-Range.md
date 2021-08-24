# Day 1: Interquartile Range

https://www.hackerrank.com/challenges/s10-interquartile-range/problem

The interquartile range of an array is the difference between its first (Q1) and third (Q3) quartiles (i.e., Q3 - Q1).

Given an array, values, of n integers and an array, freqs, representing the respective frequencies of values's elements, construct a data set, S, where each values[i] occurs at frequency freqs[i]. Then calculate and print S's interquartile range, rounded to a scale of 1 decimal place (i.e., 12.3 format).

```php
<?php
/*
 * Complete the 'interQuartile' function below.
 *
 * The function accepts following parameters:
 *  1. INTEGER_ARRAY values
 *  2. INTEGER_ARRAY freqs
 */

/**
 *  given the input is:
 *  6
 *  6 12 8 10 20 16
 *  5 4 3 2 1 5
 */

function getQuartiles($arr) {
    
    $mid = floor (count ($arr) / 2);
    if (count ($arr) % 2 === 0) {
        // even
        $median = (($arr[$mid] + $arr[$mid -1]) / 2);
    } else {
        // odd
        $median = $arr[$mid];
    }
    
    if ($mid % 2 === 0) {
        // even 
        $lower_quartile_pos = floor ($mid / 2);
        $lower_quartile = (($arr[$lower_quartile_pos] + $arr[$lower_quartile_pos - 1]) / 2);
        $upper_quartile_pos = floor ($mid + round ($mid * 0.5));
        if (count ($arr) % 2 === 0) {
            $upper_quartile = (($arr[$upper_quartile_pos] + $arr[$upper_quartile_pos - 1]) / 2);
        } else {
            $upper_quartile = (($arr[$upper_quartile_pos] + $arr[$upper_quartile_pos + 1]) / 2);
        }
    } else {
        // odd
        $lower_quartile_pos = floor ($mid / 2);
        $lower_quartile = $arr[$lower_quartile_pos];
        
        if (count ($arr) % 2 === 0) {
            $upper_quartile_pos = floor ($mid + floor ($mid * 0.5));
        } else {
            $upper_quartile_pos = floor ($mid + round ($mid * 0.5));
        }
        
        $upper_quartile = $arr[$upper_quartile_pos];
    }
    
    return [
        $lower_quartile,
        $median,
        $upper_quartile
    ];
}

function quartiles($arr) {
    sort ($arr);
    $c = count ($arr);
    $m = floor ($c / 2);

    $qs = getQuartiles ($arr);    
    $median_l = round ($qs[0]);
    $median_x = round ($qs[1]);
    $median_u = round ($qs[2]);
    
    $ret = [
        $median_l,
        $median_x,
        $median_u
    ];
    
    return $ret;
}

function interQuartile ($values, $freqs) {
    // Print your answer to 1 decimal place within this function
    $arr = [];
    foreach ($freqs as $i => $f) {
        for ($j = 0; $j < $f; $j++) {
            $arr[] = $values[$i];
        }
    }
    sort ($arr);
    
    $qs = getQuartiles ($arr);
    // print_r ($qs);
    $q_l = $qs[0];
    $q_u = $qs[2];
    $iq = round ($q_u - $q_l);
    print_r (number_format ($iq, 1));
}

$n = intval (trim (fgets (STDIN)));

$val_temp = rtrim (fgets (STDIN));

$val = array_map ('intval', preg_split ('/ /', $val_temp, -1, PREG_SPLIT_NO_EMPTY));

$freq_temp = rtrim (fgets (STDIN));

$freq = array_map ('intval', preg_split ('/ /', $freq_temp, -1, PREG_SPLIT_NO_EMPTY));

interQuartile ($val, $freq);
```