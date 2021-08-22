# Day 6: The Central Limit Theorem I

https://www.hackerrank.com/challenges/s10-the-central-limit-theorem-1/problem

A large elevator can transport a maximum of 9800 pounds. Suppose a load of cargo containing 49 boxes must be transported via the elevator. The box weight of this type of cargo follows a distribution with a mean of μ = 205 pounds and a standard deviation of σ = 15 pounds. Based on this information, what is the probability that all 49 boxes can be safely loaded into the freight elevator and transported?

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  9800
 *  49
 *  205
 *  15
 */

$x = floatval (fgets ($_fp));
$n = floatval (fgets ($_fp));
$mu = floatval (fgets ($_fp)); // mean
$sigma = floatval (fgets ($_fp)); // standard deviation

$mu_sum = ($n * $mu);
$sigma_sum = (sqrt ($n) * $sigma);

/**
 * Error function (also called the Gauss error function)
 * Value is computed using 
 * "Numerical Recipes in Fortran 77: The Art of Scientific Computing"
 * (ISBN 0-521-43064-X), 1992, page 214, Cambridge University Press.
 * Maximum error is 1.2 * 10^-7
 * 
 * https://en.wikipedia.org/wiki/Error_function
 * 
 * @param float $x
 * @return float
 */
function erf ($x) {
    $t =1 / (1 + 0.5 * abs ($x));
    $tau = $t * exp (
            - $x * $x
            - 1.26551223
            + 1.00002368 * $t
            + 0.37409196 * $t * $t
            + 0.09678418 * $t * $t * $t
            - 0.18628806 * $t * $t * $t * $t
            + 0.27886807 * $t * $t * $t * $t * $t
            - 1.13520398 * $t * $t * $t * $t * $t * $t
            + 1.48851587 * $t * $t * $t * $t * $t * $t * $t
            - 0.82215223 * $t * $t * $t * $t * $t * $t * $t * $t
            + 0.17087277 * $t * $t * $t * $t * $t * $t * $t * $t * $t);
    if ($x >= 0) {
        return 1 - $tau;
    } else {
        return $tau - 1;
    }
}

function normalDistribution ($x, $mean, $sdev) {   
    return ((1/2) * (1 + erf (($x - $mean) / ($sdev * sqrt (2)))));
}

$calc2 = normalDistribution ($x, $mu_sum, $sigma_sum);
print_r (round ($calc2, 4));
```