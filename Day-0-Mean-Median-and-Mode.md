# Day 0: Mean, Median, and Mode

https://www.hackerrank.com/challenges/s10-basic-statistics/problem

Given an array, X, of N integers, calculate and print the respective mean, median, and mode on separate lines. If your array contains more than one modal value, choose the numerically smallest one.

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

$count = fgets ($_fp);
$ints = fgets ($_fp);
$arr = explode (' ', $ints);
sort ($arr);

// Mean
$mean = (array_sum ($arr) / count ($arr));

// Median
$center = (count ($arr) / 2);
if ((count ($arr) % 2) == 0) {
    $median = (($arr[$center] + $arr[$center - 1]) / 2);
} else {
    $median = $arr[(floor ($center))];
}

// Mode
$dup = array_count_values ($arr);
$mode = $arr[0];
$mode_i = 0;
foreach ($dup as $i => $val) {
    if ($val > 1) {
        if ($val > $mode_i) {
            $mode = $i;
            $mode_i = $val;            
        }
    }
}

print_r ($mean . PHP_EOL);
print_r ($median . PHP_EOL);
print_r ($mode . PHP_EOL);

fclose ($_fp);
```