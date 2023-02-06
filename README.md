## Problem formulation
We consider the scheduling problem, where operations (jobs) can be parallelized and energy consumption is taken into account. 
Execution of a job at a slower speed is more energy efficient, but leads to a longer processing time and increases 
scheduling metrics.

A set of jobs J={1,...,n} is to be scheduled on two speed scalable processors.
Each job j is characterized by processing volume (work) V_j and the number size_j of required processors.

The standard homogeneous model in speed-scaling is considered. When a processor
runs at a speed s, then the rate with which the energy is consumed is s^a,
where a > 1 is a constant. Each processor may operate at variable speed.
We assume that the total work V_j of a single mode job j should be uniformly divided between the utilized processors.
If job j uses size_j processors, then the processing volumes are the same for all these processors 
(denoted by W_j=V_j / size_j), and they run simultaneously at the same speed. 

The aim is to find a feasible schedule with the minimum sum of completion times so that the energy consumption
is not greater than a given energy budget E.

## Algorithms
We suggest two greedy methods for the problem. The first method (Algorithm 1) based on the following 
two-stages approach. At the first stage we compute a lower bound on the objective and execution times of jobs. 
Then, at the second stage, we sequence of jobs and schedule them. 
Algorithm 1 has some disadvantages. So we provide the local improvement algorithm, based on the block 
restricted insert neighborhood and additional local moves inside blocks (Algorithm 2).

## Instances generation 

We have series with block structure and also 4 series: 11, 12, 21, 22, where series ij means set SMALL_i is used for generating small jobs 
and set LARGE_j is applied for generating large jobs, i,j = 1, 2.

- SMALL_1 = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100}    
- SMALL_2 = {10, 11, 12, 13, 14, 15, 16, 17, 18, 19} 
- LARGE_1 = {200, 275, 350, 425, 500, 575, 650, 725, 800, 875}
- LARGE_2 = {520, 540, 560, 580, 600, 620, 640, 660, 680, 700}

For generating instances the following parameters were used:
        - constant a (used values: 1.5, 2.0, 2.5, 3.0),
        - the number of jobs n (used values: 50, 100),
        - small jobs probability (used values: 0.0, 0.3, 0.5, 0.7, 1.0),
        - single-processor jobs probability (used values: 0.3, 0.5, 0.7), %or blocks (used values: 2, 4, 6, 8, 10) - fixed order of single-processor and two-processor jobs,
        - series type (11, 12, 21, 22 or block).

 For each fixed set of parameters 30 instances were generated.

## Results

The test results for series 11, 12, 21 and 22 are presented in files seriesij_result.txt. 
The columns single and small contain information about probability of choosing single-processor jobs and jobs of small volumes accordingly. 
Columns Ea1 and Ea2 present average relative deviation from the lower bound (in percentage) for algorithms A1 and A2 accordingly. 
Columns Da1 and Da2 present average standard relative deviation for algorithms A1 and A2 accordingly. 

The test results for series with block structure are presented in file series_blocks_result.txt, where column "block size" present number of jobs
in one block (block with size b contains one two-processor job and b-1 single-processor jobs).

The results of the comparison with single-processor case for series 11, 12, 21 and 22 are presented in files seriesij_single_processor_case_result.txt. 
Column E1 contains the average relative deviation from the lower bound for the single-processor jobs. 
Columns MAX_w and AVG_w contain the maximum relative deviation and the average relative deviation, 
when solutions of Algorithm 2 are worse than solutions with single-processor jobs. Columns MAX_b and AVG_b contain 
maximum and average relative deviation, when solutions of the Algorithm 2 are better than solutions with single-processor jobs. 
Column COUNT_b represents the number of instances, where Algorithm 2 shows better result than the signle-processor case. 