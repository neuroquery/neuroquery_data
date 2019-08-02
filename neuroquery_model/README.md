# NeuroQuery trained model

## Notations

- V : vocabulary size = 6308
- d : number of selected features = 188
- p : number of voxels in the brain = 28542
- n : number of studies in the training corpus = 13459
- m : word embedding dimension = 300

## Contents

### top level

- `mask_img.nii.gz` is a brain mask of the voxels that are taken into account by
  the machine-learning model. p voxels are non-zero.

- `vocabulary.csv` contains the terms recognized by the model (1st column) and
  their document frequencies (2nd column). shape: (V, 2)

- `vocabulary.csv_voc_mapping_identity.json` is a json file containing a
  dictionary of synonyms, that allow to replace some extra terms with entries of
  `vocabulary.csv`, such as "brain stem" -> "brainstem".

- `corpus_metadata.csv` contains information about each document in the training
  corpus (plus a few more documents): `pmid` (PubMed id), `title`, and
  `pubmed_url` (URL of the corresponding page on the PubMed website). shape:
  (13881, 3)

- `corpus_tfidf.npz` contains the TFIDF features of the training corpus. It can
  be loaded with `scipy.sparse.load_npz`. It is a matrix; columns correspond to
  the terms in `vocabulary.csv` and lines correspond to the lines of
  `corpus_metadata.csv`. shape: (13881, V)

### `regression`

Coefficients of the linear model that regresses the activity of each voxel in
`mask_img.nii.gz` on TFIDF features. They can be read with `numpy.load`.

- `M.npy`: the matrix that maps dependent variables to model coefficients in
  ridge regression: (X^TX + \lambda I)^{-1}X^T . shape: (d, n)

- `coef.npy`: the model coefficients. shape: (p, d)

- `intercept.npy`: the intercept. shape: (p,)

- `original_n_features.npy`: the number of features (vocabulary size) in the
  high-dimensional input space, i.e. V. int

- `residual_var.npy`: the averaged squared residual after fitting the model, for
  each voxel. shape: (p,)

- `selected_features.npy`: the indices of features (terms) kept by the feature
  selection procedure. shape: (d,)

### `smoothing`

Word embeddings used for semantic smoothing of TFIDF features, derived from
co-occurrence statistics. The smoothing matrix is V V^T with normalized rows.
They can be read with `numpy.load`.

- `V.npy`: word embeddings, one for each term in the vocabulary. shape: (V, m)

- `smoothing_weight.npy`: the weight given to the smoothed features when
  combined with the raw TFIDF features.
