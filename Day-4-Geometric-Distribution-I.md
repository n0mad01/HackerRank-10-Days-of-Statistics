# Day 4: Geometric Distribution I

https://www.hackerrank.com/challenges/s10-geometric-distribution-1/problem

The probability that a machine produces a defective product is 1/3. What is the probability that the 1st defect occurs the 5th item produced?

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  1 3
 *  5
 */

$data = fgets ($_fp);
$data = explode (' ', $data);

$p = (floatval (trim ($data[0])) / floatval (trim ($data[1])));
$n = trim (fgets ($_fp));
$q = (1 - $p);


$probability = (pow ($q, ($n - 1)) * $p);

print_r (number_format ($probability, 3, '.', ' '));
```