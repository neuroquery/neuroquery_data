minimal set of data to conduct meta-analysis with the neuroquery corpus.

- `corpus_tfidf.npz` contains a sparse matrix of TFIDF features: (13881 documents x 6308 expressions). It can be loaded with `scipy.sparse.load_npz`.
- feature_names.txt gives the expression corresponding to each column of `corpus_tfidf.npz` (one per line).
- pmids.txt gives the PubMed id corresponding to each row of `corpus_tfidf.npz` (one per line)
- `coordinates.csv` contains sterotactic coordinates extracted from each
  article. These can be transformed into brain maps using for example
  https://gist.github.com/jeromedockes/142a0e51237a93ea61a68eb3d0c01ddc
