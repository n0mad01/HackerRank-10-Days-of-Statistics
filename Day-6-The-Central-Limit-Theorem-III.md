# Day 6: The Central Limit Theorem III

https://www.hackerrank.com/challenges/s10-the-central-limit-theorem-3/problem

You have a sample of 100 values from a population with mean μ = 500 and with standard deviation σ = 80. Compute the interval that covers the middle 95% of the distribution of the sample mean; in other words, compute A and B such that P(A < χ < B) = 0.95. Use the value of z=1.96. Note that z is the z-score.

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  100
 *  500
 *  80
 *  .95
 *  1.96
 */
 
$s = floatval (fgets ($_fp)); // samples
$mu = floatval (fgets ($_fp)); // mean
$sigma = floatval (fgets ($_fp)); // standard deviation
$interval = floatval (fgets ($_fp));
$z = floatval (fgets ($_fp));

$a = ($mu - ($sigma / sqrt($s)) * $z);
$b = ($mu + ($sigma / sqrt($s)) * $z);

print_r (round ($a, 2) . PHP_EOL);
print_r (round ($b, 2));
```