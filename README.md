# MAB MLST Scheme for Mycobacterium absecssus

This repository contains a 15 gene MLST scheme for *Mycobacterium absecssus* developed by Meenu Sharma, Michelle Wuzinski, Aneta Bak and others.

# Usage

Please see the [Installation][installation] instructions below for how to get this scheme setup before continuing with the below steps.

## Command-line MLST

To use this scheme with the [mlst][] software, please do the following.

```bash
mlst --scheme mab_mabscessus input/*.fasta > output.txt
```

You will likely have to set the scheme explicitly `--scheme mab_mabscessus` as other schemes in PubMLST may match your input files. The final output file will look something like:

```
input/SRR6388757.fasta  mab_mabscessus  49  hsp(1)  erm(1)   rrl(1)  rrs(1)  arr(8)  argH(4)  cya(5)  gnd(1)  murC(2)  pta(10)  purH(2)  rpoB(1)  gyrA(8)   gyrB(7)   recA(9)
input/SRR6388758.fasta  mab_mabscessus  43  hsp(1)  erm(14)  rrl(1)  rrs(1)  arr(6)  argH(1)  cya(4)  gnd(3)  murC(2)  pta(2)   purH(4)  rpoB(1)  gyrA(15)  gyrB(14)  recA(1)
```

See the [Installation][installation] documentation below for how to get this scheme installed.

## Galaxy

To use this scheme with [Galaxy][galaxy] and the [Galaxy MLST Tool][galaxy-mlst]  please set the scheme to `mab_mabscessus` and run the tool on your genomes.

1. Running the Tool

    ![galaxy-mlst-tool.png][]

2. Output

    ![galaxy-output.png][]

# Installation

## Command-line MLST

To use with Torsten's [mlst][] software please copy the contents of this repository to to `db/pubmlst/` and run `mlst/scripts/mlst-make_blast_db` (see instructions at <https://github.com/tseemann/mlst#adding-a-new-scheme>). The scheme will be named **mab_mabsecssus** in the `mlst` software.

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

## Galaxy

To make use of this scheme using the [Galaxy][galaxy] version of the MLST tool you can do the following.

### 1. Install MLST in Galaxy

Please install the [Galaxy MLST Tool][galaxy-mlst] in Galaxy.

### 2. Install this MLST scheme

To install a new MLST scheme you will have to find the location that the MLST tool is installed using [conda][] by Galaxy. By default, the Galaxy version of conda is in `galaxy/database/dependencies/_conda` (if this does not exist, please check the `galaxy/config/galaxy.yml` file for the location of conda).

Once you've found this directory, please first add the `conda` binary to your `PATH` and activate the `conda` environment containing MLST.

```bash
cd /path/to/galaxy/_conda/bin

# add bin/ directory to PATH containing conda
export PATH=`pwd`:$PATH

# Activate __mlst@2.15.1 environment (or whichever version got installed by Galaxy)
source activate __mlst@2.15.1
```

Now, change to the `db/pubmlst` directory that got installed by conda for the `mlst` program.

```bash
# cd to __mlst@2.15.1 or whichever version is installed in Galaxy
cd /path/to/galaxy/_conda/envs/__mlst@2.15.1/db/pubmlst
```

Now, you can install the MLST scheme:

```bash
git clone https://github.com/phac-nml/mab_mabscessus.git

# Make the new BLAST databases
../../scripts/mlst-make_blast_db
```

### 3. Verify scheme is installed

To verify the scheme is installed you can run the Galaxy **MLST List** tool:

![galaxy-mlst-list.png][]

You should see **mab_mabscessus** in the output if it is properly installed.

[installation]: #installation
[mlst]: https://github.com/tseemann/mlst
[conda]: https://bioconda.github.io/
[galaxy]: https://galaxyproject.org/
[galaxy-mlst]: https://toolshed.g2.bx.psu.edu/view/iuc/mlst/1f5641a52664
[galaxy-mlst-list.png]: doc/images/galaxy-mlst-list.png
[galaxy-mlst-tool.png]: doc/images/galaxy-mlst-tools.png
[galaxy-output.png]: doc/images/galaxy-output.png
