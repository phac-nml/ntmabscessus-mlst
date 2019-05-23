# MAB MLST Scheme for Mycobacterium absecssus

This repository contains a 15 gene MLST scheme for *Mycobacterium absecssus* developed by Meenu Sharma, Michelle Wuzinski, Aneta Bak and others.

# Installation

To use with Torsten's [mlst](https://github.com/tseemann/mlst) software please copy the contents of this repository to to `db/pubmlst/` and run `mlst/scripts/mlst-make_blast_db` (see instructions at <https://github.com/tseemann/mlst#adding-a-new-scheme>). The scheme will be named **mab_mabsecssus** in the `mlst` software.

For example:

```bash
cd db/pubmlst/

git clone https://github.com/phac-nml/mab_mabscessus.git

../../scripts/mlst-make_blast_db
```

You can verify it's installed by running:

```bash
mlst --longlist|grep mab_mabscessus
mab_mabscessus  hsp     erm     rrl     rrs     arr     argH    cya     gnd     murC    pta     purH    rpoB    gyrA    gyrB    recA
```

# Usage

Once the scheme is installed, you can use like:

```bash
mlst --scheme mab_mabscessus input/*.fasta > output.txt
```

You will likely have to set the scheme explicitly `--scheme mab_mabscessus` as other schemes in PubMLST may match your input files. The final output file will look something like:

```
column -s$'\t' -t output.txt 
input/SRR6388757.fasta  mab_mabscessus  49  hsp(1)  erm(1)   rrl(1)  rrs(1)  arr(8)  argH(4)  cya(5)  gnd(1)  murC(2)  pta(10)  purH(2)  rpoB(1)  gyrA(8)   gyrB(7)   recA(9)
input/SRR6388758.fasta  mab_mabscessus  43  hsp(1)  erm(14)  rrl(1)  rrs(1)  arr(6)  argH(1)  cya(4)  gnd(3)  murC(2)  pta(2)   purH(4)  rpoB(1)  gyrA(15)  gyrB(14)  recA(1)
```
