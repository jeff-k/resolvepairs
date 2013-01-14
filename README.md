resolvepair
===========

A short python script for resolving pair membership for groups of reads with the same name.

When reconstructing a FASTQ file from an aligned BAM, it is sometimes the case that query names will be non-unique not only between mates but across pairs of mates.  This script will append a unique id to the names of reads belonging to the same mate pair.

Running SamToFastq from Picard tools on a input file with ambiguous pairs will cause it too fail with:

    Exception in thread "main" net.sf.picard.PicardException: Illegal mate state: [Read Name]
    
resolvepair reads a name sorted SAM file from STDIN and writes a SAM file with renamed query names to STDOUT.

Example
-------

    samtools sort -o -n input.bam | ./resolvepair | java -Xmx16g -XX:-UseGCOverheadLimit -jar $PICARD/SamToFastq.jar I=/dev/stdin F=r_1.fastq F2=r_2.fastq

Behaviour
---------

resolvepair will write a short summary to stderr.  Reads that do not belong to evenly populated groups (lonely reads) will be omitted.

resolvepair requires SAM input **sorted by read name**.

Currently, reads are renamed by appending an incremented integer to the first of colon delimited fields (if any) in the original readname.

**Note that such improperly named reads might indicate a failure in an early stage of the sequencing pipeline**
