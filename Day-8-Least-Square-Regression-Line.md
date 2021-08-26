# Day 8: Least Square Regression Line

https://www.hackerrank.com/challenges/s10-least-square-regression-line/problem

A group of five students enrolls in Statistics immediately after taking a Math aptitude test. Each student's Math aptitude test score, x, and Statistics course grade, y, can be expressed as the following list of (x,y) points:

95 85
85 95
80 70
70 65
60 70

If a student scored an 80 on the Math aptitude test, what grade would we expect them to achieve in Statistics? Determine the equation of the best-fit line using the least squares method, then compute and print the value of y when x = 80.

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

function mean ($dataset) {
    return (array_sum ($dataset) / count ($dataset));
}

function stdDev ($arr) {
    sort ($arr);
    $mean = mean ($arr);
    $sd_sum = 0;
    
    foreach ($arr as $i => $val) {
        $sd_sum += (pow (($val - $mean), 2));
    }
    return (sqrt ($sd_sum / count ($arr)));
}

function pearsonCorrelationCoefficient ($dataset_x, $dataset_y) {
    $calc = 0.0;
    $mu_x = mean ($dataset_x); // mean X
    $mu_y = mean ($dataset_y); // mean Y
    $sigma_x = (stdDev ($dataset_x)); // standard deviation X
    $sigma_y = (stdDev ($dataset_y)); // standard deviation Y
    $n = count ($dataset_x); // assume len X == len Y
    
    for ($i = 0; $i < $n; $i++) {
        $calc += ((($dataset_x[$i] - $mu_x) * ($dataset_y[$i] - $mu_y)) / ($n * $sigma_x * $sigma_y));
    }
    
    return $calc;
}

/**
 *  given the input is:
 *  95 85
 *  85 95
 *  80 70
 *  70 65
 *  60 70
*/

$dataset_x = [];
$dataset_y = [];

while (!feof ($_fp)) {
    $line = trim (fgets ($_fp));
    $arr = explode (' ', $line);
    $dataset_x[] = floatval ($arr[0]);
    $dataset_y[] = floatval ($arr[1]);
}

$mu_x = mean ($dataset_x); // mean X
$mu_y = mean ($dataset_y); // mean Y
$sigma_x = (stdDev ($dataset_x)); // standard deviation X
$sigma_y = (stdDev ($dataset_y)); // standard deviation Y

$b = (pearsonCorrelationCoefficient ($dataset_x, $dataset_y) * ($sigma_y / $sigma_x));
$a = ($mu_y - ($b * $mu_x));
$x = 80;
$calc = ($a + ($b * $x));
print_r (number_format ($calc, 3, '.', ''));

fclose($_fp);
```