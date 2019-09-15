 ## About the Directed acyclic graph(DAG) 
Bayes network, belief network, decision network, Bayes model or probabilistic directed acyclic graphical model is a probabilistic graphical model that represents a set of variables and their conditional dependencies via a directed acyclic graph(DAG).  DAG displays assumptions about the relationship between variables (often called nodes in the context of graphs). DAGs are good at expressing causal generative models.  The basic definition of DAG can be found [here](https://en.wikipedia.org/wiki/Directed_acyclic_graph). 

## What to do
In this project, we perform the following tasks:
1. generate a random directed acyclic graph with V number of vertices and E number of edges.
2. visualize the graph.
3. enumerate all directed paths between two vertices for a given DAG.
4. Generate data based on the graph in the following fashion:
   - Any variable without any parent are random variable following Gaussian distribution with mean 0 standard deviation of 1.
   - any variable with parents are the sum of their parents plus a Gaussian noise term with mean 0 and standard deviation of 1. 
   - generate 2000 random datasets
5. Feature selection.
   - Target variable for prediction: randomly pick a variable that have more than one neighbor as the target of prediction.
   - Features: all other variables that are not the target are potential predictors/features.
   - Feature selection and regression algorithm: use your favorite methods for feature selection and regression. You can use a pre-existing implementation.
   - Validation: use 80% samples for training and 20% sample for validation.
   - Performance metric: use your favorite metric(s)
   - Report: what features are selected by the feature selector?
   
## Main results:
 1.  Graphviz is used to visualize the DAG graph.
 2.  LassoCV is used to generate the lieanear regression model. SelectFromModel is used to select the dominant features.
 3.  By analysis on our numerical data, we reached the following rules: 
     1. Collect all direct parents and children for the target, call it S1
     2. For all the children, combine all their parents into a collection (except target itself), call it S2.
     3. Get rid of those elements in S1 that have odd number of children in the children set of target.
     4. Combine the remaining set in 3 with S2.
     
     to get the main feature nodes for each target node. Those feature nodes are efficienct to determine the target node in the sense that the R^2 score is high from the resultant model. They are also robust for a given graph in that they won't change with respect to different random realization of dataset. These rules has been succesfully tested for general target nodes for 100 randomly generated graph with 20 nodes and 20 directed edges.  
     
## Theoretical understanding:
       - Shown here is a typical DAG graph:
![alt text][logo]

[logo]: https://github.com/yongjinjiang/DirectedAcyclicGraph/blob/master/DAG1.png "Logo Title Text"
![foo]( https://github.com/yongjinjiang/DirectedAcyclicGraph/blob/master/DAG1.png  "title")
   

   



   
