# Day 7: Spearman's Rank Correlation Coefficient

https://www.hackerrank.com/challenges/s10-spearman-rank-correlation-coefficient/forum

Given two n-element data sets, X and Y, calculate the value of Spearman's rank correlation coefficient.

```php
<?php
$_fp = fopen("php://stdin", "r");
/* Enter your code here. Read input from STDIN. Print output to STDOUT */

function getRanks ($arr) {
    $count = count ($arr);
    $rank = $arr;
    sort ($rank);
    $ranked = [];

    foreach ($arr as $sort) {
        $ranked[] = (array_search ($sort, $rank));
    }
    return $ranked;
}

function SpearmansRankCorrelationCoefficient ($dataset_ranked_x, $dataset_ranked_y) {
    $count = count ($dataset_ranked_x);
    $d = 0;
    for ($i = 0; $i < $count; $i++) {
        $d += (pow (($dataset_ranked_x[$i] - $dataset_ranked_y[$i]), 2));
    }
    
    return (1 - ((6 * $d) / ($count * (pow ($count, 2) - 1))));
}

$elements_count = floatval (trim( fgets ($_fp)));
$l_2 = trim (fgets ($_fp));
$l_3 = trim (fgets ($_fp));

$dataset_x = array_map ('floatval', preg_split ('/ /', $l_2, -1, PREG_SPLIT_NO_EMPTY));
$dataset_y = array_map ('floatval', preg_split ('/ /', $l_3, -1, PREG_SPLIT_NO_EMPTY));
$dataset_ranked_x = getRanks ($dataset_x);
$dataset_ranked_y = getRanks ($dataset_y);

$calc = SpearmansRankCorrelationCoefficient ($dataset_ranked_x, $dataset_ranked_y);
print_r (number_format ($calc, 3, '.', ''));
```