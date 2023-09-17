# Step 1: Species confirmation
## 1. DNA extraction, PCR amplification and gel electrophoresis, microclean, send to Sanger sequencing
Work done in the lab

## 2. View Chromatogram
**Download the latest version of UGENE at http://ugene.net/download-all.html**

Version: 48.1 <br>
Work done on macOS

**Manually select the regions with good quality.** 

Citation: *Unipro UGENE: a unified bioinformatics toolkit. Konstantin Okonechnikov, Olga Golosova, Mikhail Fursov, the UGENE team. Bioinformatics 2012 28: 1166-1167. doi: 10.1093/bioinformatics/bts091*

## 3. Prepare COI sequences for BLAST search
Work done on info2020

### Reverse complement the reverse sequence
```bash
/home/xingyuan/tools/seqkit seq -t DNA -pr "$sample"-COI-R.fasta > "$sample"-COI-R.rc.fasta
```

### Combine forward and the reverse complement of the reverse sequences
```bash
cat "$sample"-COI-F.fasta "$sample"-COI-R.rc.fasta > "$sample"-COI.aln.fasta
```

### Align the forward and reverse complement of the reverse sequences 
```bash
/1/local/bin/clustalo -i "$sample"-COI.aln.fasta --outfmt=clustal > "$sample"-COI.aln
```

### Manually join the forward and reverse sequences into one longer sequence based on the alignment

## 4. BLAST
Blast version: 2.14.1+ <br>
Work done on info2020

**Download the latest version of blast at https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html**
```bash
wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.14.1+-x64-linux.tar.gz
wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.14.1+-x64-linux.tar.gz.md5
md5sum -c ncbi-blast-2.14.1+-x64-linux.tar.gz.md5
tar zxvpf ncbi-blast-2.14.1+-x64-linux.tar.gz
```

**Download BLAST nucleotide sequence database (https://www.ncbi.nlm.nih.gov/books/NBK62345/#blast_ftp_site.The_blastdb_subdirectory)**
```bash
perl /home/xingyuan/tools/ncbi-blast-2.14.1+/bin/update_blastdb.pl --passive --decompress nt
```

**Download BOLD Data Package: Historical Data (BOLD DNA Barcode Reference Library 31-MAR-2023, DOI: doi.org/10.5883/DP-BOLD_Public.31-Mar-2023) at http://www.boldsystems.org/index.php/datapackages**	

```bash
# You should have BOLD_Public.31-Mar-2023.fasta after downloading. Make it into a blast database.
/home/xingyuan/tools/ncbi-blast-2.14.1+/bin/makeblastdb -dbtype nucl -in BOLD_Public.31-Mar-2023.fasta -title BOLD_DNA_Barcode_Reference_Library_31-MAR-2023
```

**Search at BLAST nucleotide sequence database**
```bash
/home/xingyuan/tools/ncbi-blast-2.14.1+/bin/blastn -query bv233.assembly.fasta -out bv233.blast -db ~/tools/blastdb/nt -num_threads 5
```

Citation: *Ratnasingham, Sujeevan, and Paul D N Hebert. “bold: The Barcode of Life Data System (http://www.barcodinglife.org).” Molecular ecology notes vol. 7,3 (2007): 355-364. doi:10.1111/j.1471-8286.2007.01678.x*
