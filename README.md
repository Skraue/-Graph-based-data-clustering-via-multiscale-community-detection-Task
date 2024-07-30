# Graph-based-data-clustering-via-multiscale-community-detection-Task (Master thesis experiment)
This project conveys my optimised code for this method applied to a benchmark breast cancer data set. This method was replicated on both real and synthetic data and compared with other novel clustering methods to analyse performance, to provide recommendations in the field of clustering, as part of my master thesis experiments. 

Method Description

This is a novel clustering method developed by Zijing Liu & Mauricio Barahona, that detects the most robust clusters in a data set via graph based multiscale community detection.
Communities or clusters, are computed using an adaptation of the K nearest neighbours graph to model the connectivity of the nodes in the data set. A matrix representation of the graph is then encoded and applied to a markov stability framework. A markov chain is used to model the graphs connectivity by considering the probabilities that a random walker will transition between node, and is encoded as a matrix. Time is used a resolution parameter in this method to compute a transition matrix of probabilities that convey the markov process over a continuous time period. The transition matrix conveys the probabilities that a random walker will transition to a particular state with regards to a continuous time period. This transition matrix is then used as the input parameter for the Louvain algorithm, which detects the most robust clusters. The quality of the partitions is gauged via a markov stability metric, calculated for each partition at a given time, as well as a metric used to gauge the dissimilarity between partitions known as the variation of information. Using these metrics, the number of robust partitions is computed for the data set, each step is annotated and demonstrated accordingly in this project. 


Detailed Explanation of Method Framework and Theory

The framework of this method used to determine the number of clusters in a data set is as follows:

1) Construct an applied version of the K- nearest neighbour graph.

Applied version uses Tyrus Berry and Timothy Sauer's ('Consistent Manifold Representation for Topological Data Analysis' paper) delta metric, as a tuning parameter to construct the KNN graph by accounting for the both the global and local features of the graph, whereas the original KNN considers only the local features.
The a pair of nodes in the graph is connected using the following condition: d(x,y) < δ d(x,x_k)d(y,y_k) as referenced in the provided code.

2) Compute a matrix encoding of the graph

The graph connectivity is modelled using an adjacency matrix A, consisting of 0's and 1's in matrix notation, with 0 denoting no connection and 1 conveying a connection between nodes (edge). The diagonal degree matrix D is computed by summing the degree of each node in the graph which is conveyed along the matrix diagonal. Using matrices A and D, the matrix denoting the markov chain M is then computed by the product of the inverse of D and A.M is conveys the transition matrix which is a square matrix of the probabilities that the random walker will transition between the nodes, where 1 represents a certain transition and 0, no probability of transitioning. 

3) Create a matrix representation a model for a markov process

The Markov stability framework uses a random process (a random walk) to determine the strength or quality of the communities constructed via graph construction. 
These communities are conveyed as a set of connected nodes where the connections within communities are dense and the connections between different communities are sparse. A markov chain is diffused across the network and observed at different times (t). Time is used as a resolution parameter in this method to scan across communities at different times in the markov network. For large values of t, global properties of the networks structure are uncovered as few communities are present, and for smaller values of t, more communities can be detected to convey more local information about the graph.
In this study the markov stability metric (denoted as g) is represented as a numerical value, for which its magnitude coveys the strength of the communities at a given time. Using the vector representation for the markov process enables to derive the markov stability metric as the output of an algorithm, for better interpretability.

4) Compute the transition matrix P(t)

The transition matrix is the matrix representation model of the markov chain diffused across the network denoted as P(t). It encodes the transition probabilities of the Markov chain, representing the probability of moving from one state to another for each possible state. This is observed in continuous time and is used for the input of the Louvain algorithm at a specific range of time t.

5) Run the Louvain algorithm at specific times 

The Louvain algorithm computes the most robust partitions of the graph by optimising a quality metric. The markov stability metric is calculated alongside each partition for the specified markov time. A larger markov stability measure is observed for the optimised partitions, as well as a low measure for the variation of information metric, which conveys large dissimilarity between partitions. In this code the time frame that represented the optimised partitions ranges from 1250 - 1300 seconds and 10 readings are observed for the algorithm. To find the optimal time frame, different time ranges were inputted into the algorithm and experimented with (this was done in the 6th block of code), starting from a high number of seconds as using a small number of seconds will convey local features as opposed to the global ones. Consistent readings for partitions, markov stability and variation of information demonstrate that the network has stabilised. 

6) Run the Louvain algorithm multiple times at the selected optimal value for time
   
Once the optimal partitions have been observed for the markov time period, the time in seconds, that corresponds to the robust partitions is run several times on the Louvain algorithm to check for stability. The stability of the output conveys a robust partition. It's worth noting that since the processes is observed over a continuous time frame, and the graph structure/ communities stabilise quickly, there exists multiple time frames for which the partitions outputted are robust. The correct number of partitions is the key value to be determined for this process, the quality metrics observed at each time frame to confirm robustness. 

 
