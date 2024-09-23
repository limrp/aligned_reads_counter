## **Read alignment to Gene sequences and count of uniquely mapped reads**

### **General Goal**
This script aligns paired-end reads from samples to DNA sequences and computes the number of uniquely mapped reads for each sequence. It produces a CSV report with read counts for each sequence in each sample. The script is designed to work with any set of sequences provided in FASTA format and is flexible enough to be adapted to various downstream analyses, depending on the user’s specific needs.

### **Personal Use**
In my particular case, this script is used for **functional and metabolic profiling of metagenomic samples**. The genes provided in the FASTA files have annotations such as **COGs (Clusters of Orthologous Groups)**, **KOs (KEGG Orthology)**, and **OGs (Orthologous Groups)**, which allow for mapping the genes to specific biological functions and metabolic pathways. The read counts generated by this script are used to compute the abundance of these functions and pathways, which helps in profiling the metabolic capabilities of the metagenomic samples.

### **Key Features**
- Aligns paired-end reads to gene sequences using **Bowtie2** and counts the number of **uniquely mapped reads**.
- Outputs a CSV report containing the number of reads aligned to each sequence in each sample, which can be used for further functional or pathway analysis.
- Flexible for use in various applications, depending on the gene annotations and input data provided by the user.

### **Inputs**
1. **Paired-end Reads**: FASTQ files containing the sequencing data, where the sample name appears before the first underscore (`_`). For example:
   - `Sample1_R1.fastq`
   - `Sample1_R2.fastq`

2. **FASTA Files for Gene Sequences**: Each sample should have a corresponding FASTA file containing its gene sequences. The sample name should match the prefix of the FASTA file, and the file can end with either `.fasta` or `.fa`. For example:
   - `Sample1_genes.fasta`

3. **Other Input Options**:
   - You can specify the number of threads to use for Bowtie2 and the output directory for storing the results.

### **Outputs**
The script generates a CSV file with the following columns:
- **Sample**: The name of the sample.
- **Gene ID**: The ID of the gene (extracted from the FASTA file).
- **Number of Aligned Reads**: The number of uniquely mapped reads aligned to each gene.

Example CSV:
```csv
Sample,ID,Number of Aligned Reads
Sample1,Sample1_gene_0001,15
Sample1,Sample1_gene_0002,30
Sample2,Sample2_gene_0001,25
```

### **How to Use the Script**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/limrp/aligned_reads_counter.git
   cd aligned_reads_counter
   ```

2. **Install Dependencies**:
   You need the following software installed:
   - **Bowtie2**: For aligning reads to gene sequences.
   - **Samtools**: For processing SAM/BAM files.
   - **Python 3**: For running the script.

   You can install these tools as follows:
   - Install Bowtie2:
     ```bash
     conda install -c bioconda bowtie2
     ```
   - Install Samtools:
     ```bash
     conda install -c bioconda samtools
     ```
   - Install Python packages (if necessary):
     ```bash
     pip install argparse pathlib logging csv
     ```

3. **Run the Script**:
   To run the script, specify the following command-line arguments:
   - **`-i`**: Path to the input reads (can include wildcards, e.g., `*_R1.fastq` for paired-end reads).
   - **`-f`**: Path to the directory containing the gene FASTA files.
   - **`-o`**: Output directory for the CSV report.
   - **`-t`**: (Optional) Number of threads for Bowtie2.
   - **`-l`**: (Optional) Path to the log file (default is `align_reads.log` in the output directory).

   Example command:
   ```bash
   python3 align_reads_bowtie2.py \
     -i "/path/to/reads/*_R1.fastq" \
     -f "/path/to/fasta_files/" \
     -o "/path/to/output_dir/" \
     -t 8
   ```

4. **View the Results**:
   After running the script, a CSV report will be generated in the specified output directory, showing how many reads were aligned to each sequence for each sample.

### **Requirements**
The following tools must be installed on your system:
- **Bowtie2**: [https://bowtie-bio.sourceforge.net/bowtie2/index.shtml](https://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
- **Samtools**: [http://www.htslib.org/](http://www.htslib.org/)
- **Python 3**: [https://www.python.org/](https://www.python.org/)


### Example Workflow for Functional and Metabolic Profiling
Once you have the read counts for each gene, you can map the genes to functional annotations (COGs, KOs, OGs) and perform metabolic pathway analysis using tools like **KEGG Mapper** or **EggNOG-mapper**. These read counts can be used to compute the abundance of functions and pathways across samples, enabling comparative analysis of the metabolic capabilities of your metagenomic data.

### **Contributing**
Contributions are welcome! If you'd like to contribute, please fork the repository and create a pull request with your changes.

### **License**
This project is licensed under the MIT License. See the LICENSE file for details.

