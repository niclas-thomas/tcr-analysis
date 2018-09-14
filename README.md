# Setup

* Download or clone this repository to your Documents and navigate to it using

``cd Documents/tcranalysis``

* You'll then need to download all necessary packages using

``pip install -r requirements.txt``

* Edit the file ``/notebooks/config.py`` so that ``OUTPUT_DIRECTORY`` and ``DATA_DIRECTORY`` are correct for your own
machine. ``CHAIN`` will determine which set of CDR3 sequences your code analyses.

* Put your alpha sequences in ``DATA_DIRECTORY/alpha`` and beta sequences in ``DATA_DIRECTORY/beta``.

* Once you've got all the required packages, you can start a notebook using

``jupyter notebook``

From there you'll be able to navigate into ``/notebooks`` and open the notebook
that you wish to run.

# Notebooks

There are 3 notebooks that perform different tasks.

### Summary

This notebook provides some summary metrics of each repertoire, including

**Frequency distribution of CDR3 sequences** overlaying known specificities from VDJdb.

**Shannon entropy** of each repertoire.

**Number of copies vs % of total repertoire** plots on a log-log scale.

### Networks

This notebook provides an alternative way of analysing TCR repertoires,
using graph theory to create a network where each point represents a CDR3 sequence
projected into 2D space using multi-dimensional scaling. An edge between two points
is drawn when the Levenshtein distance between a pair of CDR3 sequences is less than
``max_weight`` (this is defined in the config file). This approach gives a means of visualising
a full repertoire in one plot.

### LIME

This notebook provides a method to predict CDR3 specificity (i.e. control vs diabetes) based on sequence characteristics.
CDR3 sequences are transformed into numerical vectors using TF-IDF, which are then used to train and test a logistic
regression model. Each CDR3 sequence is then classified as belonging to a control repertoire or diabetes repertoire, and
visualised using LIME to determine which amino acid(s) are most influential in making the prediction. The user can set
``N_GRAMS`` in the config file, which tells the model how many consecutive amino acids should be used to contruct a feature
(i.e. ``N_GRAMS=1`` means that each amino acid is considered only by itself, whereas ``N_GRAMS=2`` uses all consecutive pairs
of amino acids in the CDR3 sequence).