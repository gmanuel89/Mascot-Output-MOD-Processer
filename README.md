# MASCOT OUTPUT MOD-PROCESSER

***

## Programming language
R: The Comprehensive R Archive Network

https://www.r-project.org/

***

## Scope of the software
The software imports the output csv files yielded by Mascot, one corresponding to the whole (unmodified) proteome and the other corresponding to the proteome that underwent modification. It automatically discards all the information that Mascot adds and keeps only the matrix for the analysis.

The software at first discards the peptides which do not overpass the identity and homology threshold value (after establishing the identity or the homology according to the value). Afterwards, it splits the modified peptides from the unmodified ones and then performs duplicate removal according to protein name, peptide sequence, type of modification and modification position, keeping only the peptides with the highest score. For the modified peptides, it generates also a list of modified sequences, discarding the redundant information and keeping only the unique sequences (it discards the sequences which are listed more than one time due to different modification positions).

Finally the software identifies the true modified peptides, by matching the modified peptides in the modified proteome with the modified peptides in the unmodified proteome, in such a way that only the peptides that underwent modification due to the application of the protocol are kept.

These true modified peptides are then merged with the unmodified peptides and the column "Class" is added, so that the yielded matrix can be submitted to statistical analysis. 

***

## Type of data and its organization

#### Type of data
The software reads a folder containing the CSV files from Mascot.


#### Organization of the data
The two CSV files should be put in the same folder, which will be read by the software. One file name should start with "PROT" (the unmodified proteome) and the other one with "MOD" (the proteome that underwent modification), so that the software can recognize where the information comes from.

It is not necessary to manually remove the additional information from the Mascot CSV file, because the software automatically discards it by keeping only the information needed (in the form of a matrix).


#### Output data
The software generates a folder named "MASCOT" followed by an incremental number, in which all the output files are placed.

The results are organized as follows:
* A folder named "MODIFIED PROTEOME" in which there are the following CSV files:
    * A copy of the original file (the one with the name beginning with "MOD")
    * A file named "Non-modified peptides" with the peptides that do not carry any modification.
    * A file named "Modified peptides" with the peptides that carry at least one modification.
    * A file named "Modified peptides (unique sequences)" with the peptides that carry at least one modification, after discarding the duplicates (according to the peptide sequence) by keeping only the peptide sequence with the highest score.
    
* A folder named "NON-MODIFIED PROTEOME" in which there are the following CSV files:
    * A copy of the original file (the one with the name beginning with "PROT")
    * A file named "Non-modified peptides" with the peptides that do not carry any modification.
    * A file named "Modified peptides" with the peptides that carry at least one modification.
    * A file named "Modified peptides (unique sequences)" with the peptides that carry at least one modification, after discarding the duplicates (according to the peptide sequence) by keeping only the peptide sequence with the highest score.
    
* A file named "True modified peptides" in which there are the peptides that carry at least one modification that are unique for the modified proteome compared with the non-modified proteome: only the modified peptides in the modified proteome (file starting with "MOD") that are not in the non-modified proteome (file starting with "PROT") are preserved.

* A file named "Non-modified peptides and True modified peptides" in which there are both the true modified peptides and the non-modified peptides, with additional information (Class and Type) is added.

***

## Example

#### Organization of the data
Example of folder hierarchy:

/Input folder/PROT File 1.csv

/Input folder/MOD File 2.csv


The folder provided to the software should be the "Input folder", which will be read also as the class of the files. So it would be appropriate to name the folder according to the class (e.g. CTRL or DISEASE). 
