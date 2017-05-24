# MASCOT OUTPUT MOD-PROCESSER



## Programming language
R: The Comprehensive R Archive Network

https://www.r-project.org/



## Scope of the software
The software imports the output csv files yielded by Mascot, one corresponding to the whole (unmodified) proteome and the other corresponding to the proteome that underwent modification. It automatically discards all the information that Mascot adds and keeps only the matrix for the analysis.

The software at first discards the peptides which do not overpass the identity and homology threshold value (after establishing the identity or the homology according to the value). Afterwards, it splits the modified peptides from the unmodified ones and then performs duplicate removal according to protein name, peptide sequence, type of modification and modification position, keeping only the peptides with the highest score. For the modified peptides, it generates also a list of modified sequences, discarding the redundant information and keeping only the unique sequences (it discards the sequences which are listed more than one time due to different modification positions).

Finally the software identifies the true modified peptides, by matching the modified peptides in the modified proteome with the modified peptides in the unmodified proteome, in such a way that only the peptides that underwent modification due to the application of the protocol are kept.

These true modified peptides are then merged with the unmodified peptides and the column "Class" is added, so that the yielded matrix can be submitted to statistical analysis. 



## Type of data and its organization

#### Type of data
The software reads a folder containing the CSV files from Mascot.


#### Organization of the data
The two CSV files should be put in the same folder, which will be read by the software. One file name should start with "PROT" (the unmodified proteome) and the other one with "MOD" (the proteome that underwent modification), so that the software can recognize where the information comes from.
