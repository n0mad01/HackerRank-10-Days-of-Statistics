# Day 7: Pearson Correlation Coefficient I

https://www.hackerrank.com/challenges/s10-pearson-correlation-coefficient/problem

Given two n-element data sets, X and Y, calculate the value of the Pearson correlation coefficient.

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  10
 *  10 9.8 8 7.8 7.7 7 6 5 4 2 
 *  200 44 32 24 22 17 15 12 8 4
 *
 *  or
 *  10
 *  10 9.8 8 7.8 7.7 7 6 15 4 2 
 *  200 414 32 24 212 17 15 12 8 4
 */

function mean ($dataset) {
    return (array_sum ($dataset) / count ($dataset));
}

function stdDev ($arr) {
    sort ($arr);
    $mean = mean ($arr);
    $sd_sum = 0;
    
    foreach ($arr as $i => $val) {
        $sd_sum += (pow (($val - $mean), 2));
    }
    return (sqrt ($sd_sum / count ($arr)));
}

function pearsonCorrelationCoefficient ($dataset_x, $dataset_y, $elements_count) {
    
    $calc = 0.0;
    $mu_x = mean ($dataset_x); // mean X
    $mu_y = mean ($dataset_y); // mean Y
    $sigma_x = round (stdDev ($dataset_x), 5); // standard deviation X
    $sigma_y = round (stdDev ($dataset_y), 4); // standard deviation Y
    
    for ($i = 0; $i < $elements_count; $i++) {
        $calc += ((($dataset_x[$i] - $mu_x) * ($dataset_y[$i] - $mu_y)) / ($elements_count * $sigma_x * $sigma_y));
    }
    
    return $calc;
}

$elements_count = floatval (trim( fgets ($_fp)));
$l_2 = trim (fgets ($_fp));
$l_3 = trim (fgets ($_fp));
$dataset_x = array_map ('floatval', preg_split ('/ /', $l_2, -1, PREG_SPLIT_NO_EMPTY));
$dataset_y = array_map ('floatval', preg_split ('/ /', $l_3, -1, PREG_SPLIT_NO_EMPTY));

$pearson = pearsonCorrelationCoefficient ($dataset_x, $dataset_y, $elements_count);
print_r (number_format ($pearson, 3, '.', ''));
```