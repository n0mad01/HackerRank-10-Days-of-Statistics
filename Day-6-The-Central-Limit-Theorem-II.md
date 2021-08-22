# Day 6: The Central Limit Theorem II

https://www.hackerrank.com/challenges/s10-the-central-limit-theorem-2/problem

The number of tickets purchased by each student for the University X vs. University Y football game follows a distribution that has a mean of μ = 2.4 and a standard deviation of σ = 2.0.

A few hours before the game starts, 100 eager students line up to purchase last-minute tickets. If there are only 250 tickets left, what is the probability that all 100 students will be able to purchase tickets?

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