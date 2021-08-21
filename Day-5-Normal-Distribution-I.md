# Day 5: Normal Distribution I

https://www.hackerrank.com/challenges/s10-normal-distribution-1/problem

In a certain plant, the time taken to assemble a car is a random variable, X, having a normal distribution with a mean of 20 hours and a standard deviation of 2 hours. What is the probability that a car can be assembled at this plant in:

* Less than 19.5 hours?
* Between 20 and 22 hours?

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

/**
 *  given the input is:
 *  20 2
 *  19.5
 *  20 22
 */

$l1 = fgets ($_fp);
$l1 = explode (' ', $l1);
$l2 = fgets ($_fp);
$l3 = fgets ($_fp);
$l3 = explode (' ', $l3);

$mean = floatval (trim ($l1[0]));
$standard_deviation = floatval (trim ($l1[1]));

// task 1
$less_then_x_hours = floatval (trim ($l2));

// task 2
$between_a = floatval (trim ($l3[0]));
$between_b = floatval (trim ($l3[1]));

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

// task 1
$calc_1 = normalDistribution ($less_then_x_hours, $mean, $standard_deviation);
print_r (round ($calc_1, 3) . PHP_EOL);

// task 2
$calc_2 = (normalDistribution (22, $mean, $standard_deviation) - normalDistribution (20, $mean, $standard_deviation));
print_r (round ($calc_2, 3));
```
