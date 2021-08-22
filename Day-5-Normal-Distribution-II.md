# Day 5: Normal Distribution II

https://www.hackerrank.com/challenges/s10-normal-distribution-2/problem

The final grades for a Physics exam taken by a large group of students have a mean of μ = 70 and a standard deviation of σ = 10. If we can approximate the distribution of these grades by a normal distribution, what percentage of the students:

* Scored higher than 80 (i.e., have a grade > 80)?
* Passed the test (i.e., have a grade >= 60)?
* Failed the test (i.e., have a grade < 60)?

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  70 10
 *  80
 *  60
 */

$l1 = fgets ($_fp);
$l1 = explode (' ', $l1);
$l2 = fgets ($_fp);
$l3 = fgets ($_fp);

$mean = floatval (trim ($l1[0]));
$standard_deviation = floatval (trim ($l1[1]));

// task 1
$t1_greater_than = floatval (trim ($l2));

// task 2
$t2_greater_or_equal = floatval (trim ($l3));

// task 3
$t3_lesser_than = floatval (trim ($l3));

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

$calc_1 = normalDistribution ($t1_greater_than, $mean, $standard_deviation);
$calc_1 = ((1 - $calc_1) * 100);
print_r (number_format ($calc_1, 2, '.', ' ') . PHP_EOL);

$calc_2 = normalDistribution ($t2_greater_or_equal, $mean, $standard_deviation);
$calc_2 = ((1 - $calc_2) * 100);
print_r (number_format ($calc_2, 2, '.', ' ') . PHP_EOL);

$calc_3 = normalDistribution ($t3_lesser_than, $mean, $standard_deviation);
$calc_3 = ($calc_3 * 100);
print_r (number_format ($calc_3, 2, '.', ' ') . PHP_EOL);
```
