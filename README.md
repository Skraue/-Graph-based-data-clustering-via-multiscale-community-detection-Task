# Graph-based-data-clustering-via-multiscale-community-detection-Task
This method was a novel clustering method that detected clusters in data via graph based multiscale community detection. This method was replicated on both real and synthetic data and compared with other novel clustering methods to analyse performance to provide recommendations in the field of clustering, as part of my master thesis experiments. 
The framework used Markov logic to model the connectivity of the graphs structure in matrix form, for which a multiscale community
 detection framework was applied to obtain a solution as an output of an algorithm. The multi scale element of this Markov stability framework enabled to scan for communities across different levels of resolutions to determine robust clusterings that are not sensitive to the parameters used in the graph constructions. 
 To do this, a graph was constructed to capture global features of a data set by diffusing a markov chain across the data to detect communities. Time was then used a resolution paramter to scan across the network to identify the measure that constituted to the most robust clusterings. When the number of partitions stabilised, the robustness was detemied by a high value of markov stability metric and a low value for the variation of information metric, which conveyed the dissimilarty between communites. 
 For the markov time, multiple iterations were run to determine the stability of the network which would then give the number of clusters for the data set.

 
