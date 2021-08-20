# Day 5: Poisson Distribution I

https://www.hackerrank.com/challenges/s10-poisson-distribution-1/problem

A random variable, X , follows Poisson distribution with mean of 2.5. Find the probability with which the random variable X is equal to 5.

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  2.5
 *  5
 */
 
$lambda = floatval (trim (fgets ($_fp))); // mean / average number of successes
$k = intval (trim (fgets ($_fp))); // x equal to

function factorial ($n) {
    if ($n < 2) { 
        return 1;
    }
    return $n * factorial ($n-1);
}

function poissonDistribution ($k, $lambda) {
    return ((pow ($lambda, $k) * pow (M_E, -$lambda)) / factorial ($k));
}

$probability = poissonDistribution ($k, $lambda);
print_r (number_format ($probability, 3, '.', ' '));
```