# MyGNNotes

## Neural Message Passing

1. A graph contains nodes and edges. Nodes have embeddings -- features and values of the features.  
2. Graphs can't be plotted in co-ordinate space for classification by drawing decision boundary.
3. Our goal is to ***assign meaningful co-ordinates*** to the nodes of a graph so that we can then ***easily*** create decision boundaries (rather than having to draw complicated boundaries) across the nodes for downstream classification.
    1. We want to compute ***neighbourhood-aware embeddings***  i.e., the embeddings of a node reflect the neighbourhood of the node.
    2. We use the ***message passing framework*** to achieve this goal.
4. ***Message Passing Framework:***
    1. Messages are the embeddings from the neighbouring nodes.
    2. Messages from all the neighbouring nodes are aggregated to compute a new embedding.
    3. The steps of message passing and aggregation can be iterated multiple times to update this new embedding.

Given a graph, GCN uses a graph convolution operation to obtain node embeddings layer by layer—at each layer, the embedding of a node is obtained by gathering the embeddings of its neighbors, followed by one or a few layers of linear transformations and nonlinear activations. The final layer embedding is then used for some end tasks. For instance, in node classification problems, the final layer embedding is passed to a classifier to predict node labels, and thus the parameters of GCN can be trained in an end-to-end manner.

5. GNN tasks:
    1. **Node-level task**: Regression of an attribute of a node or predict the class of a node in the given graph
    2. **Edge-level task**: Infer the existence of an edge between two existing nodes in an incomplete graph or regression/prediction of an attribute of an edge in a graph 
    3. **Graph-level task**: Classify a graph or regression/clustering task over an entire graph. The model learns to classify graphs using three main steps:
        1. Embed nodes using several rounds of message passing.
        2. Aggregate these node embeddings into a single graph embedding (called readout layer). In the code below, the average of node embeddings is used (global mean pool).
        3. Train a classifier based on graph embeddings.
            
           
![Screenshot (380)](https://user-images.githubusercontent.com/114074746/226182024-32760c06-f35d-4749-a77c-ad3524dfbb53.png)


6. GNNs are trained with batches of graphs instead of individual graphs. This is done as follows:
    1. Stack adjacency matrices in a diagonal manner leading to a large graph with multiple isolated subgraphs.
    2. Concatenate node features and the target.

![Screenshot (378)](https://user-images.githubusercontent.com/114074746/226179142-451948ae-372d-4ff5-aeae-edab15e923ac.png)

7. How can edge features be used when training the model? If we take the example of GCN, it can easily be done by replacing the zeros and ones of the adjacency matrix with the edge weights.

![Screenshot (382)](https://user-images.githubusercontent.com/114074746/226182186-9a84e435-0636-442e-9c3a-1fc8efbec6ec.png)

8. Explainability of GNNs:
    i. Getting good performance is one thing, but having confidence in the prediction to take action is another. To trust the prediction of a model, one can examine the reasons why the model generated it. Sometimes, these explanations can be more important than the results themselves as they reveal the hidden patterns that the model has detected and better guide the decision-making. For graphs, explicability is about three questions: 
        i. **Which nodes and features were relevant to making the prediction?** 
        ii. **How relevant were they?** 
        iii. **How relevant were the node and edge features of the graph?**

    ii. Instance-level methods, that provide explanations at the level of individual predictions
    iii. Model-level approaches, that give explanations at the level of the whole model
  
