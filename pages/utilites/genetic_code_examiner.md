---
layout: default
title: genetic_code_examiner.py
parent: Utilities
nav_order: 9
permalink: /utilities/genetic-code-examiner
---

# `genetic_code_examiner.py`

Explore potential alternative nuclear genetic codes for input taxa.

`genetic_code_examiner.py [OPTIONS] -i <input_file> -q <query_file>`

Required arguments:
- `-i`, `--input <infile.fas>` Fasta file with nucleotide sequences
- `-q`, `--queries <Unique ID1,Unique ID2,...>` Comma separated Unique IDs of related organisms in the database which should be used as queries.

Optional arguments:
- `-t`, `--threads <N>` Number of threads
  - Default: `1`
- `--prepare_alignments` Prepare alignments for genetic code analysis. MUST BE USED ON THE FIRST RUN!
- `-c`, `--conserved <N>` Proportion (0-1) of taxa from the database that have the same amino acid at a position.
  - Default: `0.7` (70%)
- `-e`, `--blast_evalue <1e-X>` E-value threshold for blast searches.
  - Default: `1e-30`
- `-a`, `--all_codons` Plot conserved positions for all codons
- `-o`, `--output <out_dir>` Path to user-defined output directory
  - Default: `./genetic_code_out_<M.D.Y>`
- `-h`, `--help` Show this help message and exit

**NOTE:** Users should have their config.ini file in the directory in which they wish to run `genetic_code_examiner.py`.
Users may need to provide updated paths in this file to account for a different directory location.

Default `genetic_code_examiner.py` output:
- a file `inputname_genecode.pdf` - Each bar chart in the file corresponds to a separate plot for codons with a suspicious genetic code signal (signal for coding schemes different from the standard nuclear genetic code) if any exist (Figure 8).

<br><br>
<figure>
    <img
        src="https://thebrownlab.github.io/phylofisher-pages/assets/images/tetrahymena.fasta_genecode.png"
        alt="fisher.py Scheme"
        height="75%"
        width="100%" 
        class="center"/>
    <figcaption>
        Figure 8: Plot produced by genetic_code_examiner.py. The y-axis shows the number of taxa from the database with the amino acid labeled on the x-axis conserved for a given site and the input taxon has the codon in the title at the same site. This plot provides evidence that the codon UAA that acts as a stop codon (*) in the standard nuclear genetic code has been reassigned to code for the amino acid glutamine (Q) in the nuclear genome of <i>Tetrahymena thermophila</i>.
    </figcaption>
</figure>