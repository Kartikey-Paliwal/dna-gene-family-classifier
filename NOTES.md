# Learning Log

## Day 1 — Biology + Setup

### What I did
- Created repo and Colab notebook
- Loaded human.txt (4380 sequences, 2 columns: sequence, class)

### Check questions
1. Why would genes in the same family have similar DNA?
   -  Because Genes in a family came from one ancestral gene that was duplicated.

2. What is a conserved region, and why does it stay conserved?
   - its an identical or highly similar sequence of DNA, RNA, or amino acids found across different genes or completely different species. it is conserved because Mutations in important regions usually break the protein and harm the organism, so natural selection removes them. Mutations in less important regions survive, so those parts change more.

3. What does each row in human.txt contain?
   - DNA sequence (A , T , C , G)

4. How long are the sequences? Are they all the same length?
   - NO they are not of same length

5. Why is ML useful if BLAST already exists?
   - BLAST compares a sequence to a database to find similar ones. ML learns the patterns that define each family, so it can classify new sequences even without a close match, and it scales well to large datasets. 

### Observations
- Every sequence starts with ATG (start codon) → these are coding sequences
- Rows 2 and 3 look identical → possible duplicates (check on Day 12 for data leakage)
- First sequence is 207 bases (69 codons), class 4 (synthase), looks like MT-ATP8

### Questions / confusions
-
