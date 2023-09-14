# Step 1: Species confirmation
## Method 1: NCBI
Blast version: 2.14.1+ <br>
Work done on info2020

**Download the latest version of blast at https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html**
```
# Install blast
wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.14.1+-x64-linux.tar.gz
wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.14.1+-x64-linux.tar.gz.md5
md5sum -c ncbi-blast-2.14.1+-x64-linux.tar.gz.md5
tar zxvpf ncbi-blast-2.14.1+-x64-linux.tar.gz

# Download the ref_euk_rep_genomes (Eukaryotic representative genomes from NCBI RefSeq project) (describe here https://www.ncbi.nlm.nih.gov/books/NBK62345/#blast_ftp_site.The_blastdb_subdirectory)
perl ncbi-blast-2.14.1+/bin/update_blastdb.pl --passive --decompress ref_euk_rep_genomes

$ Move downloaded database files to a new directory
mkdir blastdb
mv ref_euk_rep_genomes* blastdb/
mv taxdb.* blastdb/
```

Try this first:
```
blastn -query ~brian/exampleForBlast.fasta -out results113.out -db /scratch/blastdb/nt_v5
```
## Method 2: BOLD
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1890991/

**Follow the instruction to download the postgresql: https://www.endpointdev.com/blog/2013/06/installing-postgresql-without-root/**
```

```
