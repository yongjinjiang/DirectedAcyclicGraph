 ## Directed acyclic graph(DAG) 
Directed acyclic graph(DAG) is the graph to describe Bayes network(or belief network, decision network) in which a set of variables and their conditional dependencies is shown.  DAG displays assumptions about the relationship between variables (often called nodes in the context of graphs) and are good at expressing causal generative models.  The basic definition of DAG can be found [here](https://en.wikipedia.org/wiki/Directed_acyclic_graph). 

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
   
## Main approaches&results:
 1.  Graphviz is used to visualize the DAG graph.
 2.  LassoCV is used to generate the lieanear regression model. SelectFromModel is used to select the dominant features.
 3.  By analysis on our numerical data, we reached the following rules: 
     1. Collect all direct parents and children for the target, call it S1
     2. For all the children, combine all their parents into a collection (except target itself), call it S2.
     3. Get rid of those elements in S1 that have odd number of children in the children set of target.
     4. Combine the remaining set in 3 with S2.
     
to get the main feature nodes for each target node. Those feature nodes are efficienct to determine the target node in the sense that the R^2 score is high from the resultant model. They are also robust for a given graph in that they won't change with respect to different random realization of dataset. These rules has been succesfully tested for general target nodes for 100 randomly generated graph with 20 nodes and 20 directed edges.  
     
As an example, for the following graph,
     <img src="./DAG1.png " width="900" height="400">
if we pick 19th node as targe, the selected nodes are: [0, 7, 8, 9]; pick 9th node as target, the selected nodes are: [0, 7, 8, 19]; pick 0th node as target,  the selected nodes are: [1, 7, 8, 9, 18, 19].  these are pure S1+S2 case defined by first two rules. Furthermore, if we pick 17th node as the target, the selected feature nodes are: [2, 3, 8, 15]. Note 10th node is avoided, even though it is a child of 17th node. Such cases are described by the last two rules described on above. 
     
## Theoretical understanding:
The features chosen by the rules actually forms a set called "Markov blanket" of the target node. This set sheilds the target from outside world, i,e., once the features in the set is set, it will fully determines the random distribution of the target.  Other features outside the markov blanket would be conditionally independent of the target. The usual definition of Markov blanket for a node A is the set of nodes composed of A's parents, A's children, and A's children's other parents. This is described by S1+S2 on above. T

There are some exceptions. In some cases, a child or parent of the target can at the same time be parent of other children. This will cause some relation confusion. Such confusion can lead to rule modifications(hence rules 3 and 4). For example, in the graph DAG1, for target=17, the choosen set of features=[2,3,8,15]. It's noteworthy that 10 is not chosen.


This modification can be theoretically understood by [D-separation](https://www.youtube.com/watch?v=yDs_q6jKHb0&t=112s) of Baysian network. Look at the three nodes, 17--10--3, which formed a causal chain. If 10 is chosen, then 17 and 3 would become conditionally independent, which is undesirable. At first glance, it seems strange that 15 is selected while 10 is discarded. However, let look at 17--10--15, which forms a V-strucure, or a common effect structure. It is known that if the central effect node 10 and its descendants are all not selected, then 15 and 17 would be independent.  However, 3 is selected and it's the child of 10. So, 15 and 17 is correlated. So, in this way, the discard of 10 can be understood.  



  

   
