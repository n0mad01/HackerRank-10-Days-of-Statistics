# Day 4: Binomial Distribution I

https://www.hackerrank.com/challenges/s10-binomial-distribution-1/problem

The ratio of boys to girls for babies born in Russia is 1.09 : 1. If there is 1 child born per birth, what proportion of Russian families with exactly 6 children will have at least 3 boys?

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

$data = fgets ($_fp);
$data = explode (' ', $data);
$b = floatval ($data[0]); // ratio boys
$g = floatval ($data[1]); // ratio girls

$c_max = 6; // count children per family
$b_min = 3; // count at least boys

$p = ($b / ($b + $g)); // probability value
$q = 1 - $p; // proportion

$prob = 0.0;

function factorial ($n) {
    if ($n < 2) { 
        return 1;
    }
    return $n * factorial ($n-1);
}

function  binomialCoefficient ($n, $r) {
    return factorial ($n) / (factorial ($r) * factorial ($n - $r));
}
    
for ($i = $c_max; $i >= $b_min; $i--) {
    $prob += binomialCoefficient ($c_max, $i) * pow ($p, $i) * pow ($q, $c_max - $i);
}

print_r (number_format ($prob, 3, '.', ' '));
```