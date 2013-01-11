resolvepair
===========

A short python script for resolving pair membership for groups of reads with the same name.

When reconstructing a FASTQ file from an aligned BAM, it is sometimes the case that query names will be non-unique not only between mates but across pairs of mates.  This script will append a unique id to the names of reads belonging to the same mate pair.

    samtools sort -b -n input.bam | resolvepair | sam2fastq

