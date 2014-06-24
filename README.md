nL_Prime
========


How is the sort performed?

Sorting is done stepwise. The columns (1-indexed for the UNIX bash shell) are:

30 : Oracle Penalty (this penalty is based on the Oracle program; more details to follow below)

12 : Inclusivity of the all of the desired <inclusion set> allowing for 2 total mismatches

10 : Inclusitivy of the of the desired <inclusion set> allowing for 0 total mismatches

2 : Thermodynamic penalty assessed by primer3 based on self-dimerization, hetero-dimerization, GC richness, ect.


##Oracle Penalty##

###Similarity independent penalty###

In this method, each primer is delivered to the program Oracle3.py.

>Column 0: Primer ID

>1: Primer3 Penalty  
>2: Forward Sequence  
>3: Reverse Sequence  
>4: Fmelting  
>5: Rmelting  
>6: Start Position  
>7: End Position  
>8: Length  
>9: Percent of inclusion set matched with no mismatches  
>10: Accessions of inclusion set matched with no mismatches  
>11: Percent of inclusion set matched with 2 total mismatches  
>12: Accessions of inclusion set matched with 2 total mismatches  
>13: Percent of inclusion set matched with 4 total mismatches  
>14: Accessions of inclusion set matched with 4 total mismatches  
>15: Percent of inclusion set matched with 6 total mismatches  
>16: Accessions of inclusion set matched with 6 total mismatches  
>17: Percent of inclusion set matched with 8 total mismatches  
>18: Accessions of inclusion set matched with 8 total mismatches 
>19: Percent of EXCLUSION set matched with no mismatches  
>20: Accessions of EXCLUSION set matched with no mismatches  
>21: Percent of EXCLUSION set matched with 2 total mismatches  
>22: Accessions of EXCLUSION set matched with 2 total mismatches  
>23: Percent of EXCLUSION set matched with 4 total mismatches  
>24: Accessions of EXCLUSION set matched with 4 total mismatches  
>25: Percent of EXCLUSION set matched with 6 total mismatches  
>26: Accessions of EXCLUSION set matched with 6 total mismatches  
>27: Percent of EXCLUSION set matched with 8 total mismatches  
>28: Accessions of EXCLUSION set matched with 8 total mismatches









###Similarity dependent penalty###
Here, the oracle penalty relies on the blastp tabular results. 







