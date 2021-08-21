# Day 5: Poisson Distribution II

https://www.hackerrank.com/challenges/s10-poisson-distribution-2/problem

The manager of a industrial plant is planning to buy a machine of either type A or type B. For each day’s operation:

* The number of repairs, X, that machine A needs is a Poisson random variable with mean 0.88. The daily cost of operating 
    A is CA = 160 + 40X².
* The number of repairs, Y, that machine B needs is a Poisson random variable with mean 1.55. The daily cost of operating 
    B is CB = 128 + 40Y².

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  0.88 1.55
 */

$data = fgets ($_fp);
$data = explode (' ', $data);

$a = floatval (trim ($data[0])); // mean of machine of type A
$b = floatval (trim ($data[1])); // mean of machine of type B


$cost_a = (160 + (40 * (pow ($a, 2) + $a)));
print_r (number_format ($cost_a, 3, '.', ' ') . PHP_EOL);

$cost_b = (128 + (40 * (pow ($b, 2) + $b)));
print_r (number_format ($cost_b, 3, '.', ' ') . PHP_EOL);
```