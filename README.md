# Protein Conformation Datasets

This github provides description for Protein Conformation Datasets.

## Dataset creation
Data acquisition:
1. Choose protein X with single polypeptide chain
2. Find all occurences of X in Protein Data Bank (PDB). Occurence means the exact match sequence-wise. They can be found in proteins, that contain multiple polypeptide chains.
3. Collect all of them to create a cluster.
4. Go to point 1. until all proteins were captured.
5. Split clusters into data blocks.
Data preprocessing:
1. Remove all proteins, that are missing more than 30% of captured positions.
2. Remove all clusters, that are smaller than 5.
3. Align protein structures and center them around point (0,0,0).

## Dataset versions
There are few options:
1. Data
   - Plain - Any missing 3D position of amino acid in protein is missing from this version
   - Padded - Any missing 3D position of amino acid in protein is filled using simple interpolation algorithm. If missing position is at the beginning or end (no real position to the left or right), then closest real position is assigned. If it is in the middle, then interpolation is done using nearest real left and right neighbour.
2. Maximum Protein Length
   - 200 - maximum length of the protein is 200. Any cluster containing longer proteins is discarded.
   - 300 - maximum length of the protein is 200. Any cluster containing longer proteins is discarded.
3. Cluster split into data blocks
   - Random - Each cluster was assigned to data block at random. 
   - Similarity - Each cluster was assigned to data block based on Jaccard similarity. Jaccard Similarity between amino acid sequences between 2 clusters. If the similarity score is above 0.4, then they are placed in different data blocks, otherwise they are placed in the same one.

## Available dataset versions
There are 10 versions available:
- Raw Protein Conformation
- Padded Protein Conformation 
- Raw Protein Conformation Random Max Protein Length 300
- Raw Protein Conformation Random Max Protein Length 200
- Padded Protein Conformation Random Max Protein Length 300
- Padded Protein Conformation Random Max Protein Length 200
- Raw Protein Conformation Similarity Max Protein Length 300
- Raw Protein Conformation Similarity Max Protein Length 200
- Padded Protein Conformation Similarity Max Protein Length 300
- Padded Protein Conformation Similarity Max Protein Length 200

# How to use it?
## How was it saved?
Dataset was saved using following function:
```
import pickle as pkl
def load_pickle(full_path):
    with open(f"{full_path}.pkl", "rb") as handle:
        data_block = pkl.load(handle)
    return data_block
```
## How to load it?
Dataset can be load using simple load function:
```
import pickle as pkl
def load_pickle(full_path):
        with open(f"{full_path}.pkl", "rb") as handle:
            data_block = pkl.load(handle)
        return data_block
```
## Dataset structure
