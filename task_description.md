# Task 1:
In this task you are not allowed to use the csv module (and any modules for parsing csv file). Your task is to create the module  `mycsv.py`. This module should contain the following functions:

- `read_csv(path_to_csv_file, delimiter=",")` This function takes two arguments: 1st is the path to the file, 2nd is the delimiter character. By default, the separator is a comma. The function should read the file and return a list of lines. 
---
Suppose we have the file `data.csv` with the following content:
```
ID,ExperimentName,Result
101,MarshmallowTest,Success
102,MilgramExperiment,Failure
```
The funcion work example:
```python
import mycsv
lines = mycsv.read_csv("data.csv")
"""
now lines = [
    ['ID', 'ExperimentName', 'Result'], 
    ['101', 'MarshmallowTest', 'Success'], 
    ['102', 'MilgramExperiment', 'Failure']]
"""
```
---

Also, some files may contain a dilemiter character as content, such elements are enclosed in quotation marks. Example:

Suppose we have the file `data.csv` with the following content:

```
ID,Value
101,"10,5"
102,11
103,"11.5"
```

The funcion work example:
```python
import mycsv
lines = mycsv.read_csv("data.csv")
"""
now lines = [
    ['ID', 'Vlaue'], 
    ['101', '10,5'], 
    ['102', '11'],
    ['103','11.5']
    ]
"""
```
---

Your function should be able to work with different types of delimiters, for example:
Suppose we have the file `data.csv` with the following content:
```
ID*Value
101*10,5
102*11
103*11.5
```

```python
import mycsv
lines = mycsv.read_csv("data.csv", delimiter='*')
"""
now lines = [
    ['ID', 'Vlaue'], 
    ['101', '10,5'], 
    ['102', '11'],
    ['103','11.5']
    ]
"""
```

---

If a file with name `path_to_csv_file` doesn't exist, your function should print a message to the console "Error, such file doesn't exist" and return empty list.

- `write_csv(path_to_csv_file, data, delimiter=',')` This function should save data from `data` variable to the file with name `path_to_csv_file` using `del` delimiter. Example of work:

```python
import mycsv
lines = [
    ['ID', 'Vlaue'], 
    ['101', '10,5'], 
    ['102', '11'],
    ['103','11.5']
    ]

mycsv.write_csv("data_1.csv", lines)
mycsv.write_csv("data_1.tsv", lines, delimiter="\t")
```

This code should create (overwrite) file with the name `data.tsv` in the current directory with the following content:
`data_1.csv`:
```
ID,Value
101,"10,5"
102,11
103,"11.5"
```
`data_1.tsv`:
```
ID    Value
101    10,5
102    11
103    11.5
```
Create messages that will be displayed by your function in case of an incorrect call. To do this, use the built-in function `print` and in this case don't write anythin to file.


# Task 2

In this task you are not allowed to use third-party modules that can parse fasta files. Your task is to create the module  `fastaparse.py`. This module should contain the following functionality:

- The monoisotopic mass table for amino acids as a dictionary `mass_table`
- DNA codon table as a dictionary `dna_codon`
- Function `parse(file_path)` that parses a `fasta` file and returns a dictionary. The dictionary consists of pairs **seq_id** as `string` and the sequence itself **seq** as `string` or `list`.
- Function `translate(dna_seq)`. This function takes DNA sequence as a string and returns the protein string encoded by `dna_seq` as a string.
- Function `calc_mass(prot_seq)`. This function takes a string encoding a protein and returns the mass as `float`.
- Function `orf(dna_seq)`. This function takes DNA sequence as string and returns `list` of every distinct candidate protein string that can be translated from **Open Reading Frames** of `dna_seq`. 

Example:
Suppose we have the file `fasta_data.txt` with the following content:
```
>fasta_0
GTCCG
>fasta_1
GATAATTCTATATGT
>fasta_2
CGTGCCAGCGTGACAACGGGAAAACAAATAGCGG
>fasta_3
CATTTACTATCTGTGACACCCGCAGTTCTCTGGACGGAATTCAATCGGTCTTTAAAACCT
TTCAATTCTCGAGTGTGCGT
>fasta_4
TTGTTGTACCCTTTTCGCATAAAGACCCCAATGAAATTACGGATCTGCGCGCGCCCATCC
CGAAAAGCGTGAGCCACTACAAAAGCGCATGCTATGCTTCTTAAGGTCACTGAGCTCTCC
ACTTTAGGCAG
```

Some examples:
```python
import fastaparse
res_dict = fastaparse.parse("fasta_data.txt")
"""
Now 
res_dict = {
    "fasta_0" : "GTCCG",
    "fasta_1" : "GATAATTCTATATGT",
    "fasta_2" : "CGTGCCAGCGTGACAACGGGAAAACAAATAGCGG",
    "fasta_3" : "CATTTACTATCTGTGACACCCGCAGTTCTCTGGACGGAATTCAATCGGTCTTTAAAACCTTTCAATTCTCGAGTGTGCGT",
    "fasta_4" : "TTGTTGTACCCTTTTCGCATAAAGACCCCAATGAAATTACGGATCTGCGCGCGCCCATCCCGAAAAGCGTGAGCCACTACAAAAGCGCATGCTATGCTTCTTAAGGTCACTGAGCTCTCCACTTTAGGCAG"
}
"""

dna_seq = "ACAGGACGGCATTGCCACGTCACGC\
           CGTTTTGCCAGAGACATCGATCGCG\
           AAGCCGATTTCGATGAGTCCCGCAT\
           GCCTAAGGCACAATAGAATGTAGCA\
           TCCAGACACTGAGGTGCGTCTGGAA\
           AAAGACACTCAGGGATAAAAATCAC\
           AGTACCACACAGTGCCGCAGCTCCG\
           AATGTCGAGGTTCATATAATCGGAC\
           CTTCTCTCTCGAAAGCTGACCTTCG\
           ACATGTAAAAGATAAATCCAGCAGA\
           TGCATGTAACCAAGGTCGGACCAGA"

orfs = ["MSKVSFRERRSDYMNLDIRSCGTVWYCDFYP", 
        "MLHSIVP", "MPKAQ", "MNLDIRSCGTVWYCDFYP",
        "M", "MHLLDLSFTCRRSAFEREGPII", "MSRFI", 
        "MSPACLRHNRM"]
```

And so on.

Finish
