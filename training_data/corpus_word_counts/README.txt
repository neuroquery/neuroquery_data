term counts for documents in the training corpus

can be read with scipy.sparse.load_npz
each row corresponds to a pubmed ID (pmid) in pmids.txt, and each column
correspond to a term in vocabulary.txt.

when a colocation from the vocabulary occurs, such as "cingulate cortex", only
the colocation is counted, and not the individual terms (even if they are also
in the vocabulary).
For example "cingulate cortex and later cortex on its own" results in

"cingulate"        : 0
"cingulate cortex" : 1
"cortex"           : 1

note that around 20% of articles do not have keywords (or none of their keywords
are in the vocabulary), and around 0.7% of abstracts are empty or missing as well.
