# RAGNet-CMI

RAGNet-CMI is a relation-aware graph neural network framework for
circRNA--miRNA interaction (CMI) prediction. The model integrates
multi-view biological similarity information with heterogeneous graph
learning to identify potential circRNA--miRNA associations.

The framework contains three main components:

1.  **Multi-view graph construction**
    -   Multiple similarity views are constructed for miRNA and circRNA.
    -   RNA similarity views include sequence, expression/other
        similarity information and GIP similarity.
    -   circRNA similarity views include sequence, expression/other
        similarity information and GIP similarity.
    -   Homogeneous and heterogeneous graph edges are generated for
        graph representation learning.
2.  **Relation-aware heterogeneous graph encoding**
    -   RAGNet uses graph attention-based message passing.
    -   Multiple relation views are adaptively fused through attention
        mechanisms.
    -   Homogeneous and heterogeneous neighborhood information is
        integrated through relation-aware gating.
3.  **Dual-stream interaction prediction**
    -   Structural and semantic representations of circRNA--miRNA pairs
        are learned.
    -   A gating mechanism combines different feature streams.
    -   The final association probability is predicted by a neural
        decoder.

# Requirements

-   Python 3.7 or higher
-   PyTorch
-   torch-geometric
-   scikit-learn
-   pandas
-   numpy
-   scipy
-   matplotlib

# Data

Put all required data files in the `./data/` directory.

The input data preparation pipeline requires:

-   Known circRNA--miRNA interaction file:
    -   `9905pairs.csv`
-   circRNA similarity matrices:
    -   `circ_seq_similarity.csv`
    -   `circ_exp_similarity.csv`
    -   `circ_str_similarity.csv`
-   miRNA similarity matrices:
    -   `mi_seq_similarity.csv`
    -   `mi_exp_similarity.csv`
    -   `mi_str_similarity.csv`

The preprocessing script constructs the multi-view graph data file:

    ./data/processed/multi_view_graph_data.npz

This file contains:

-   circRNA--miRNA interaction matrix
-   multiple miRNA similarity views
-   multiple circRNA similarity views
-   homogeneous graph edges
-   heterogeneous circRNA--miRNA interaction edges

# Data Preparation

Run:

    python data_prepare.py

The script will generate the required multi-view graph structure for
model training.

# Running the Code

Run the training and evaluation pipeline:

    python main.py

The default setting performs 5-fold cross-validation.

Main parameters can be modified in `main.py`, including:

-   number of epochs
-   hidden dimension
-   number of graph layers
-   learning rate
-   weight decay
-   dropout rate
-   random seed

The model is configured to use CPU execution for stable and reproducible
experiments.

# Model Architecture

The main model file is:

    RAGNet.py

The implementation includes:

-   Multi-view feature encoders
-   Relation-aware heterogeneous graph layers
-   Graph attention convolution
-   View-level attention fusion
-   Dual-stream decoder
-   circRNA--miRNA interaction predictor

# Output

During training, the program prints:

-   Training loss
-   Training AUC
-   Training AUPR
-   Test AUC
-   Test AUPR
-   ACC
-   Precision
-   F1-score
-   MCC


