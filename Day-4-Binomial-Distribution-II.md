# Day 4: Binomial Distribution II

https://www.hackerrank.com/challenges/s10-binomial-distribution-2/problem

A manufacturer of metal pistons finds that, on average, 12% of the pistons they manufacture are rejected because they are incorrectly sized. What is the probability that a batch of 10 pistons will contain:
1. No more than 2 rejects?
2. At least 2 rejects?

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

$data = fgets ($_fp);
$data = explode (' ', $data);

$percentage_rejects = $data[0];
$batch_size = $data[1];

$p = ($percentage_rejects / 100);
$n = $batch_size;

$max_rejects = 2;
$min_rejects = 2;


function factorial ($n) {
    if ($n < 2) { 
        return 1;
    }
    return $n * factorial ($n-1);
}

function  binomialCoefficient ($n, $r) {
    return factorial ($n) / (factorial ($r) * factorial ($n - $r));
}


$no_more_than_2_rejects = 0;
for ($i = 0; $i < $n; $i++) {
    if ($i <= 2) {        
        $no_more_than_2_rejects += (binomialCoefficient ($n, $i) * pow ($p, $i) * pow ((1.0 - $p), $n - $i));
    }
}
print_r (number_format ($no_more_than_2_rejects, 3, '.', ' ') . PHP_EOL);

$at_least_2_rejects = 0;
for ($i = 0; $i < $n; $i++) {
    if ($i >= 2) {        
        $at_least_2_rejects += (binomialCoefficient ($n, $i) * pow ($p, $i) * pow ((1.0 - $p), $n - $i));
    }
}

print_r (number_format ($at_least_2_rejects, 3, '.', ' ') . PHP_EOL);
```