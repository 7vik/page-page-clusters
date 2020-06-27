# Graph Clustering Experiments Report
This is a report/summary of a group of graph clustering algorithms (written in Python), profiled over on the Facebook Large Page-Page Network.

## Problem Statement
Check [statement.pdf](https://github.com/7vik/page-page-clusters/blob/master/statement.pdf)

## Dataset Description
Check [SNAP Facebook Large Page-Page Dataset](https://snap.stanford.edu/data/facebook-large-page-page-network.html).

This is a visualization of the sparse dataset:

<img src="https://github.com/7vik/page-page-clusters/blob/master/img/visual.png" width="500" height="300">

And this is a histogram of the class distribution:

<img src="https://github.com/7vik/page-page-clusters/blob/master/img/class-distribution.png" width="500" height="300">

## Summary of Experiments and Results

For network data visualization and basic graph operations, we can use a number of libraries. I have used networkX.
All visualizations with analysis are available at [visual.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/visual.ipynb).

The problem of graph clustering for social network graphs like page-page naturally moulds into one of community detection. 
There are a number of community detection algorithms. I tested the Girvan Newman's Algorithm. More algorithmic details are there in the research paper (1).

The algorithm's steps for community detection are summarized below:
- The betweenness of all existing edges in the network is calculated first.
- The edge(s) with the highest betweenness are removed.
- The betweenness of all edges affected by the removal is recalculated.
- The above two steps are repeated until no edges remain.

This algorithm worked really well on a sample graph, but on the large page-page dataset, I could not get it to run with my processing power. 
The code is available in [girvan-newman.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/girvan-newman.ipynb)

Next I tried the most common clustering algorithm: KMeans Clustering.
K-Means Clustering: Start with all vertices in different clusters and merge pairs of clusters that minimize a given linkage distance (Euclidean by default). 
We'll test the sklearn implementation of this seminal research paper (2) on the page-page dataset.

Note: We will pass the adjacency matrix rows as features to KMeans, with the untested hypothesis that samples from the same cluster would be closer to each other on this feature space.
The code is available at [kmeans.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/kmeans.ipynb).

The results were unsuccessful, and thus the hypothesis was incorrect.

After visualizing the graph data and trying two classical approaches to clustering, we'll move on to try some ML based approaches.

I've never done graph ML before. [This](https://medium.com/octavian-ai/how-to-get-started-with-machine-learning-on-graphs-7f0795c83763) article was a really comfortable starting point into the field.
One difference we can see in the `page-page` data vs usual graph NN data is that here, the nodes don't have features. 
Just a `page_type` from `1-4` that acts as the target in the usual node classification problem.

To model graphs as neural nets, we need embeddings for each layer of the graph. This image helps understand how weights are used to define these embeddings. More details in [this](https://towardsdatascience.com/program-a-simple-graph-net-in-pytorch-e00b500a642d) blog.

![img](https://miro.medium.com/max/1400/1*THVRB8-wHODA3yDUykasIg.png)

GCNs (Graph Convolutional Networks) almost always prove to perform better than vanilla Graph Networks. 
I'm not reading about the theoretical details of how they work (except the main embedding equation) for now, and will be trying out PyTorch Geometric's implementation to see how they perform later.

Note to self: Read up more about GCNs [here](https://tkipf.github.io/graph-convolutional-networks/), and the papers linked with this.

- (3) is the seminal paper on Graph Convolutional Nets.

More theory and code for graph convnets is available at [graphnets.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/graphnets.ipynb)
and [graphconv.ipynb](https://github.com/7vik/page-page-clusters/blob/master/src/graphconv.ipynb).

We try to use neural networks on graphs using the DGL library. 
It will follow the implementation of a GCN using PyTorch backend. 
First I'm trying it out on an inbuilt dataset from the DGL Library , and later will apply it to the page-page dataset.

The algorithm works well on the inbuilt dataset, and it will require some tweaking to feed the page-page dataset to it.

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
## Reference to Research Papers:

1. [Girvan-Newman Community Detection Algorithm](https://www.pnas.org/content/99/12/7821)
2. [K-Means Clustering](https://cs.nyu.edu/~roweis/csc2515-2006/readings/lloyd57.pdf)
3. [Graph Convolutional Networks](https://arxiv.org/abs/1609.02907)
