nL_Prime
========

How is the sort performed?

Sorting is done stepwise. The columns (1-indexed for the UNIX bash shell) are:

> 30 : Oracle Penalty (this penalty is based on the Oracle program; more details to follow below)  
> 12 : Inclusivity of the all of the desired <inclusion set> allowing for 2 total mismatches  
> 10 : Inclusitivy of the of the desired <inclusion set> allowing for 0 total mismatches  
> 2 : Thermodynamic penalty assessed by primer3 based on self-dimerization, hetero-dimerization, GC richness, ect.  

## Oracle Penalty Methods ##

###Similarity dependent penalty###

In this method, each primer is delivered to the program Oracle3.py as a tab deliminated file. the Program relies on blastp output to determine how similar each exclusion sequence found is to the referene sequences and those homologues found in the inclusion set.

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

The code does the following 
<ul>
<li> 1st. Extraction of those sequences that are in the exclusion set. It does this by grabbing every other column starting at 20,22,24,26,28. </li>
<li> 2nd. A custom helper function called "list-partition" takes this list of list and makes a single non-redundant LIST of LISTS **non-redundant-hits**</li> 
</ul>

> Example: ["A|B|C","A|B|C|D","A|B|C|D|E","A|B|C|D|E|F"] =>[['A', 'C', 'B'], ['D'], ['E'], ['F']]  


> [[], ['BAF33878.1', 'CBG27804.1', 'YP_006099175.1', 'YP_787975.1'], [], [], []]  

+ 3rd.  **non-redundant-hits** is mapped to blast similarity scores to produce **non-redundant-hits-similarity**  

> [[], ['BAF33878.1', 'CBG27804.1', 'YP_006099175.1', 'YP_787975.1'], [], [], []]  

Converted to:

> [[], [96.98, 98.49, 98.49, 96.98], [], [], []]  

+ 4th the similarity is then converted to a list difference score via the power function (k = 4). This ensures that the penalty explodes scales rapidly for those sequences very disimilar to those in th inclusion set. The resultinglist is called the  **non_redundant_hits_difference**  

> [[], [16.64966415999987, 0.06765201000000272, 0.06765201000000272, 16.64966415999987], [], [], []]  

> (inclusion_set_threshold-x_i)**k 

+ 5th a penalty vector is applied that discounts the penalty based the number of mismatches, between the exclusion sequence and the primer. That is, the penalty for perfect complimentarity will remain much greater than the penalty for only partial complimentarity. 

> penalty = [1.0, 0.9, 0.8, 0.5, 0.25]

Below the penalty discount was applied.

> [[], [14.984697743999883, 0.06088680900000245, 0.06088680900000245, 14.984697743999883], [], [], []]  

+ 6th a final penalty is assessed by summing all the penalties. (not that this would greatly inflate penalties based on the number of sequences considered and so is likely only appropriate if the database is quantatively representative of what might be found in a given environment. Alterantives might be to take the maximum penalty score, repressenting the worst case scenario independent of the number of matching sequences. In this case the final_penalty is assessed:  

> 30.091169106  

### Similarity independent penalty ###

Appropriate primers can also be found simply by sorting the mismatch percentage column. 

