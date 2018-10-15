# Novel MLST Schema for Mycobacterium absecssus

This repository contains a novel (14 gene) MLST schema for *Mycobacterium absecssus* developed by Meenu Sharma, Michelle Wuzinski, Aneta Bak and others.

To use with Torsten's [mlst](https://github.com/tseemann/mlst) software please copy the contents of this repository to to `db/pubmlst/` and run `mlst/scripts/mlst-make_blast_db` (see instructions at <https://github.com/tseemann/mlst#adding-a-new-scheme>).

# Cleaning up files

To clean up the original files I did the following:

1. Fix alleles

    ```bash
    dos2unix *.fasta
    
    # Manually remove newline from gyrA.fasta
    
    # Consistent formatting for fasta files
    for i in *.fasta; do echo $i; bp_seqconvert --from fasta --to fasta < $i > $i.tfa; done
    
    # Use `grep '^>' *.fasta.tfa` to check headers
    
    # Removing _WT_ parts from headers to leave only gene_allele
    sed -i -e 's/_WT.*//' *.fasta.tfa
    
    # Some additional cleanup on hsp
    sed -i -e 's/_[TCE].*//' hsp.fasta.tfa
    
    # Some additional cleanup on rpoB
    sed -i -e 's/_[ES].*//' rpoB.fasta.tfa
    
    # Some additional cleanup on erm
    sed -i -e 's/_[ES].*//' erm.fasta.tfa
    
    # Manually fix up non-printable characters in rrl
    
    # Rename files properly
    prename 's/\.fasta\.tfa/\.fasta\.new/' *.fasta.tfa
    rm *.tfa
    
    prename 's/\.fasta\.new/\.tfa/' *.fasta.new
    ```

2. Fix Profiles

    ```bash
    dos2unix ntmabscessus.txt.new

    # Convert to tab-delimited
    sed -i -e 's/,/\t/g' ntmabscessus.txt.new

    # Move ST column to first column
    cut -f 16 ntmabscessus.txt.new > /tmp/ST
    cut --complement -f 16 ntmabscessus.txt.new > /tmp/REST
    paste /tmp/ST /tmp/REST > ntmabscessus.txt
    ```
