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

## Day 3: Clean the data + k-mers 🧬

### What I did
- Learned to clean data (drop_duplicates, length filter) and wrote my own get_kmers() function to split DNA into overlapping k-letter "words".
- Cleaning removed 774 sequences (4380 → 3606); data is still imbalanced (TF 1100 vs Ion channel 214).
- So test accuracy will be more honest now, and k = 6 is a middle ground: small k is too common to tell families apart, large k is too rare to learn from.

### Check questions
1. Why clean before k-mers?
  - Duplicates can leak into both train and test (inflating accuracy), and tiny fragments add noise.
    
3. 6-mers from a 1000-base sequence?
  -1000 − 6 + 1 = 995.
   
5. Why k=3 too small, k=12 too large?
  -k=3 gives only 64 common words that appear in every family; k=12 gives ~16.7M rare words the model can't learn from.

## Day 4: Vectorizing (Turning DNA “words” into numbers)

### What I did 
- Joined each sequence's k-mers into a "sentence" and used CountVectorizer to build a count table (X), plus labels (y).
- X has 3606 rows (sequences) and ~4100 columns (6-mers); most cells are zero (sparse matrix).
- So every sequence is now the same size and ready for a model; longer sequences have bigger counts, which could bias the model.

### Check questions
1. Row = one DNA sequence; column = one 6-mer; each cell = how many times that 6-mer appears in that sequence.
2. Most cells are zero because each sequence contains only a few hundred of the ~4096 possible 6-mers.
3. X and y need the same number of rows because each sequence needs exactly one matching family label to learn from.

## Day 5 
