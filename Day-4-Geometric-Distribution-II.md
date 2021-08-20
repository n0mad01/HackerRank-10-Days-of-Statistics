# Day 4: Geometric Distribution II

https://www.hackerrank.com/challenges/s10-geometric-distribution-2/problem

The probability that a machine produces a defective product is 1 : 3. What is the probability that the 1st defect is found during the first 5 inspections?

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

$probability = 0;

/**
 *  geometric series
*/
function geometric ($n, $p) {
    return (pow ((1 - $p), ($n - 1)) * $p);
}

for ($i = 1; $i <= $n; $i++) {
    $probability +=  geometric ($i, $p);
}

print_r (number_format ($probability, 3, '.', ' '));
```