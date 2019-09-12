 The Directed acyclic graph(DAG) displays assumptions about the relationship between variables (often called nodes in the context of graphs). DAGs are good at expressing causal generative models.  The basic definition of DAG can be found [here](https://en.wikipedia.org/wiki/Directed_acyclic_graph). 

In this project, we perform the following tasks:
1. generate a random directed acyclic graph with V number of vertices and E number of edges.
2. visualize the graph.
3. enumerate all directed paths between two vertices for a given DAG.
4. Generate data based on the graph in the following fashion:
  - Any variable without any parent are random variable following Gaussian distribution with mean 0 standard deviation of 1.
  - any variable with parents are the sum of their parents plus a Gaussian noise term with mean 0 and standard deviation of 1. generate 2000 random datasets
5. Feature selection.
   - Target variable for prediction: randomly pick a variable that have more than one neighbor as the target of prediction.
   - Features: all other variables that are not the target are potential predictors/features.
   - Feature selection and regression algorithm: use your favorite methods for feature selection and regression. You can use a pre-existing implementation.
   - Validation: use 80% samples for training and 20% sample for validation.
   - Performance metric: use your favorite metric(s)
   - Report: what features are selected by the feature selector?



   
