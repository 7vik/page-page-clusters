# Page Page Clusters
A group of graph clustering algorithms (written in Python), profiled over on the Facebook Large Page-Page Network.

## Problem Statement
Check [statement.pdf](https://github.com/7vik/page-page-clusters/blob/master/statement.pdf)

## Dataset Description
Check [SNAP Facebook Large Page-Page Dataset](https://snap.stanford.edu/data/facebook-large-page-page-network.html).

This is a visualization of the sparse dataset:

<img src="https://github.com/7vik/page-page-clusters/blob/master/img/visual.png" width="500" height="300">

And this is a histogram of the class distribution:

<img src="https://github.com/7vik/page-page-clusters/blob/master/img/class-distribution.png" width="500" height="300">

## Methodology
Read through the IPython Notebooks inside `src` in the following order:
- [visual.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/visual.ipynb)
- [girvan-newman.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/girvan-newman.ipynb)
- [kmeans.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/kmeans.ipynb)
- [graphnets.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/graphnets.ipynb)
- [graphconv.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/graphconv.ipynb)


## Dataset Citation:
> B. Rozemberczki, C. Allen and R. Sarkar. Multi-scale Attributed Node Embedding. 2019.
 ```
        @misc{rozemberczki2019multiscale,
            title={Multi-scale Attributed Node Embedding},
            author={Benedek Rozemberczki and Carl Allen and Rik Sarkar},
            year={2019},
            eprint={1909.13021},
            archivePrefix={arXiv},
            primaryClass={cs.LG}
        }
```    
