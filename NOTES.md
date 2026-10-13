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
## Day 2: data exploration

### What I did
- Learned to explore data with pandas (value_counts, describe, groupby) and plot charts with matplotlib.
- Found the data is imbalanced, sequence lengths vary from 5 to 18,921 bases, and ~17% are duplicates.
- So I'll need k-mers to handle different lengths, and must remove duplicates before training to avoid inflated accuracy.

### Check questions
1. Is the dataset balanced across families? Which is largest and smallest?
  - Not balanced. Transcription factor is the largest class and ion channel the smallest.

2. What are the shortest and longest sequence lengths? Why is that a problem for ML models?
  - Shortest is 5 bases and the longest one is 18,921 bases. ML models need inputs of the same size, so raw sequences can’t be fed in directly that's why i'll convert them to k-mers on day-3.

3. Which family has the longest genes (median)?
  - G protien - coupled receptors

4. Do human, chimp, and dog have similar family distributions?
  - No

5. How many exact duplicates are there? Why could they make the model look better than it really is?
  - There are 751 duplicates. That’s about 17% of the data If one copy lands in the training set and the other in the test set, the model has already “seen the answer,” so test accuracy looks higher than real performance. I will remove duplicates before splitting
