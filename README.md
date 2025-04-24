# Getting-Fasta-File-IDs
Generate fasta files ids and invetigate wether there are any duplicated ids or not in linux



To list all gene IDs from a FASTA file, use the following command(s). The gene ID is the part immediately following the > symbol in the FASTA header line.

# Method 1: Using grep, sed, and cut (Linux/Mac)

# For a single FASTA file:
```
grep '^>' your_file.fasta | sed 's/^>//' | cut -d ' ' -f1

```
# For all FASTA files in a directory:
```
grep '^>' *.fasta | sed 's/^>//' | cut -d ' ' -f1
```
Explanation:

grep '^>': Extract lines starting with > (FASTA headers).

sed 's/^>//': Remove the > character from the beginning of each line.

cut -d ' ' -f1: Split the header at the first space and keep only the gene ID (assumes the ID ends at the first space).

# Method 2: Using awk (More Efficient)

# For a single FASTA file:
```
awk '/^>/ {print substr($0, 2)}' your_file.fasta | cut -d ' ' -f1
```

# For all FASTA files in a directory:
```
awk '/^>/ {print substr($0, 2)}' *.fasta | cut -d ' ' -f1
```
# Method 3: Save IDs to a File

# Save all gene IDs to a text file:
```
grep '^>' *.fasta | sed 's/^>//' | cut -d ' ' -f1 > all_gene_ids.txt
```
# Method 4: Check for Duplicates (Optional)
To identify duplicate gene IDs (e.g., AMN1A008800.1 vs. AMN1A008800.2):

```
grep '^>' *.fasta | sed 's/^>//' | cut -d ' ' -f1 | sort | uniq -d
```
