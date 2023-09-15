# Step 1: Species confirmation
## 1. DNA extraction, PCR amplification and gel electrophoresis, microclean, send to Sanger sequencing
Work done in the lab

## 2. Open the Sanger sequencing files
**Download the latest version of BioEdit at https://bioedit.software.informer.com/download/**

Version: 7.7.1 

## 3. Search COI sequence on databases
Blast version: 2.14.1+ <br>
Work done on info2020

**Download the latest version of blast at https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html**
```
# Install blast
wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.14.1+-x64-linux.tar.gz
wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.14.1+-x64-linux.tar.gz.md5
md5sum -c ncbi-blast-2.14.1+-x64-linux.tar.gz.md5
tar zxvpf ncbi-blast-2.14.1+-x64-linux.tar.gz
```

**Download databases**
```
# Download the ref_euk_rep_genomes (Eukaryotic representative genomes from NCBI RefSeq project) at https://www.ncbi.nlm.nih.gov/books/NBK62345/#blast_ftp_site.The_blastdb_subdirectory
perl ncbi-blast-2.14.1+/bin/update_blastdb.pl --passive --decompress ref_euk_rep_genomes

# Move downloaded database files to a new directory
mkdir blastdb
mv ref_euk_rep_genomes* blastdb/
mv taxdb.* blastdb/
```

**Search at Eukaryotic representative genomes database at https://www.ncbi.nlm.nih.gov/books/NBK62345/#blast_ftp_site.The_blastdb_subdirectory**

Try this first:
```
blastn -query ~brian/exampleForBlast.fasta -out results113.out -db /scratch/blastdb/nt_v5
```

