# Leveraging Structural and Biophysical Information for Machine Learning-Assisted Protein Engineering

Code for comprehensive feature extraction from multimodal, physically informed representations, including structural and biophysical information from molecular dynamics simulations and machine learning baseline tests based on one-hot encoded sequence data. Research conducted under Professor Frances Arnold at Caltech.


Below is an explanation of each of the files presented in this repository <br />

**create_json_mutant.py** - Creates a custom .json configuration file for feature extraction based on .pdb TRIAD file one wishes to extract MD-related features on and the base path one wishes to place the custom .json configuration file in. <br />

To generate a custom .json configuration file, run the following
```bash
python3 create_json_mutant.py [triad_struct_filename] [base_path]
```
All TRIAD files that can be inputted into this program must be named in a similar manner to what is presented below
```bash
2GI9_prepared_designed_9_A_40L.pdb
```
An example of a generated custom .json configuration file generated by this program can be viewed in **official_config_20ns_IGTY.json**.

**create_test_train_csv.py** - Creates the train and test datasets for GB1 sequential data with approaches based on the work of [Dallago et. al](https://www.biorxiv.org/content/10.1101/2021.11.09.467890v2.full). The datasets for baseline machine learning tests were created using the one vs. rest approach highlighted in the paper.

**mlde_test.py** - Runs the machine learning baseline tests. See documentation in **train_eval.py** for how to customize calling the MLDESim class for other baseline tests.

**official_extraction.py** - Extracts data from molecular-dynamics simulations based on a .json configuration file (that can be created via **create_json_mutant.py**) and places relevant residue-specific features in a .csv file for the specified mutant.

To generate a dataset for a customized mutant, run the following
```bash
python3 official_extraction.py [json_configuration_file]
```
**pytorch_models.py** - Contains custom neural network models for machine learning baseline tests. Currently has two implementations of a convolutional neural network and a feed forward neural network. The convolutional neural networks created are both one-dimensional. One of the convolutional neural networks has an architecture that contains max pooling, while the other contains an architecture that includes flattening and dropout probabilities.

**run-md.py** - Runs a 20 nanosecond (production step time) molecular dynamics simulation for a custom protein, and generates relevant files for the feature extraction pipeline.
To generate a dataset for a customized mutant, run the following
```bash
python3 run-md.py [triad_struct_filename]
```
**train_eval.py** - Contains the architecture for encoding sequence data via one-hot encodings, training, and testing machine learning models needed for baseline tests.

---

<h3 align="center">Abstract</h3>
<h3 align="center">Leveraging Structural and Biophysical Information for Machine Learning-Assisted Protein Engineering</h3>

Directed evolution, a powerful technique in protein engineering, enhances the transformation of challenging enzymes. However, its efficiency requires predominantly additive protein variants. Machine learning-assisted directed evolution (MLDE) overcomes this by training sequence-fitness models with experimental data from combinatorial protein variant libraries, enhancing sequence space exploration efficiency. Unlike previous MLDE methods that relied solely on protein sequence encodings, our research leverages multimodal, physically informed representations encompassing structural and biophysical information. This shift is motivated by the demand for more accurate, interpretable protein engineering models. Focusing on the immunoglobulin-binding protein GB1, we successfully engineer comprehensive features from molecular dynamics (MD) simulations, including residue-related distances, and develop a novel algorithm to calculate per-residue Shannon entropy, enriching our insights into protein dynamics. To ensure data accuracy, we rigorously verify MD equilibrium through Entropy and RMSD analyses, complemented by innovative algorithms for precision and noise reduction. Baseline tests with one-hot encoded sequences confirm our machine learning model's reliability, mirroring Dallago et al.'s findings. Our feature extraction pipeline, designed for GB1, demonstrates adaptability for other enzymes through customizable data parameters. Future work includes replicating MD simulations with varied initial conditions, building diverse machine learning models, and comprehensive evaluations for protein fitness prediction to assess our approach's effectiveness.

---
