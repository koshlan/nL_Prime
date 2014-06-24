nL_Prime
========


How is the sort performed?

Sorting is done stepwise. The columns (1-indexed for the UNIX bash shell) are:

30 : Oracle Penalty (this penalty is based on the Oracle program; more details to follow below)

12 : Inclusivity of the all of the desired <inclusion set> allowing for 2 total mismatches

10 : Inclusitivy of the of the desired <inclusion set> allowing for 0 total mismatches

2 : Thermodynamic penalty assessed by primer3 based on self-dimerization, hetero-dimerization, GC richness, ect.


Oracle Penalty
========

The oracle penalty relies on the blastp tabular results. It function is based on the following logic:







