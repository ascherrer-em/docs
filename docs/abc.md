# ABC classification

ABC classification is a simple method to form 3 (or 4) groups of objects based on the distribution of some value associated with them. 

It is greatly inspired by the 80/20 Pareto rule, indicating that often 80% of a measure (for instance the revenue) comes from only 20% of entities (for instance customers).

The archetypical example is to classify customers based on the amount of revenue they bring to a company.

## Definitions and notations

 - We will consider $N$ objects 
 - $M_i$: the measure for object $i$ that corresponds to the classification criterion
 - $P_i$: the proportion of $M_i$ with respect to the total measure.
 
  $\displaystyle P_i = \frac{M_i}{\sum_{i=1}^{N} M_i }$
- $f$: the frequency, which is equal to $1/N$

## Methodology

1. Define properly your business objective (what are )
1. Gather the data needed to perform the classification
1. Identify the measure $M$ that will be the classification critrion
1. Sort your objects in descending order according to that measure
1. Compute the frequency (constant $f$), the cummulated frequency (cummulative sum of $f$), the proportion $P_i$ and the cummulative proportion (cummulative sum of $P_i$)
1. Plot a Pareto chart (cummulative proportion versus cummulative frequency)
1. Plot also the diagonal line
1. Classify your objects in 3 classes using the empirical rule defined below

## Excel implementation

Using Excel, you should use the following columns to perform the classification:

 - Object: The object your are considerring
 - $M$: The measure that drives the classification for each object. **Your table should be sorted in descending order based on that column**
 - $f$: The frequency ($f = 1/N$)
 - $C_f$: The cummulative frequency
 - $P$: The proportion of $M$
 - $C_P$: The cummulative proportion (cummulative sum of $P$)
 - $S_i$: The trapeze area for the current point: $S_i = \frac{1}{2} f (C_{P_i}+C_{P_{i-1}})$. When $i=1$, use $S_1 = \frac{1}{2} f C_{P_i}$

Then, outside your object table, you need to compute the following quantities:

 - $S1$: the area under the curve, which is the sum of $S$: $\displaystyle S1 = \sum_{i=1}^{N} S_i$
 - $S$: the area between the diagonal and the curve: $S= S1-0.5$
 - $B$: the area above the curve: $B=1-S1$
 - $G$: the Gini index: $\displaystyle G = \frac{S}{S+B}$

 ## Classification

 Then based on the value of the Gini index $G$, you can use the following empirical rules:

| G                 | Class A            | Class B            | Class C            |
| ----------------- | ------------------ | ------------------ | ------------------ |
| $0.90 < G < 1.00$ | 10%                | 10%                | 80%                |
| $0.85 < G < 0.90$ | 10%                | 20%                | 70%                |
| $0.75 < G < 0.85$ | 20%                | 20%                | 60%                |
| $0.60 < G < 0.75$ | 20%                | 30%                | 50%                |

> **$G < 0.6$ indicates that no classification can take place.
