# Social-Network-Graph-Link-Prediction
## step by step procedure to solve this case study

Social Network Graph Link Prediction

- first we import some Libraries
- using networkx liberari load the data with out header
- we observe that the data set contain only two features those are 'scorce_node' and 'destination_node'
- we Mappling this problem into supervised lerning problem
- we use perfomance matrix for this problem are f1 score and confusion matrix

- this data set contains only directed edges
- we do some EDA on graph type features
- Type: DiGraph
- Number of nodes: 1862220
- Number of edges: 9437519
- Average in degree:   5.0679
- Average out degree:   5.0679

## EDA

> ##### No of followers for each person

- we observe that very few have more connections
- 99% of nodes are have just lessthen 40 connections
- 99.9 percentile is 112

> ##### No of people each person is following

- we observe that very few have more connections
- 99% of nodes are have just lessthen 40 following
- 99.9 percentile is 123

- No of persons those are not following anyone are 274512 and % is 14.741115442858524

- No of persons having zero followers are 188043 and % is 10.097786512871734


> ##### both followers + following

- we observe that very few have more connections
- 99% of nodes are have just lessthen 79
- 99.9 percentile is 221

- Min of no of followers + following is 1334291  persons having minimum no of followers + following
- Max of no of followers + following is 15791  persons having maximum no of followers + following
- No of persons having followers + following less than10 are 1320326
- No of weakly connected components 45558 weakly connected components wit 2 nodes 32195

## Posing a problem as classification problem


> ##### Generating some edges which are not present in graph for supervised learning

- Generated Bad links from graph which are not in graph and whose shortest path is greater than 2.

> ##### Training and Test data split

- Removed edges from Graph and used as test data and after removing used that graph for creating features for Train and test data
- we done 80:20 split as train and test data

- Data points in train data (15100030, 2)
- Data points in test data (3775008, 2)
- Shape of traget variable in train (15100030,)
- Shape of traget variable in test (3775008,)

## Featurization

> ##### Similaity measures

- Jucard Distance

\begin{equation}
j = \frac{|X\cap Y|}{|X \cup Y|} 
\end{equation}

- Cosine distance

\begin{equation}
CosineDistance = \frac{|X\cap Y|}{|X|\cdot|Y|} 
\end{equation}

>##### Ranking Measures

- PageRank computes a ranking of the nodes in the graph G based on the structure of the incoming links.

- Page Ranking

- 

> ##### Other Graph Features

- Shortest path

- checking for same community

- adamic/Adar index

$$A(x,y)=\sum_{u \in N(x) \cap N(y)}\frac{1}{log(|N(u)|)}$$

- Is persion was following back

- Katz Centrality

- Hits Score


## Adding new set of features

__we will create these each of these features for both train and test data points__
<ol>
<li>Weight Features
    <ul>
        <li>weight of incoming edges</li>
        <li>weight of outgoing edges</li>
        <li>weight of incoming edges + weight of outgoing edges</li>
        <li>weight of incoming edges * weight of outgoing edges</li>
        <li>2*weight of incoming edges + weight of outgoing edges</li>
        <li>weight of incoming edges + 2*weight of outgoing edges</li>
    </ul>
</li>
<li>Page Ranking of source</li>
<li>Page Ranking of dest</li>
<li>katz of source</li>
<li>katz of dest</li>
<li>hubs of source</li>
<li>hubs of dest</li>
<li>authorities_s of source</li>
<li>authorities_s of dest</li>
</ol>

- SVD features for both source and destination

- Add another feature called Preferential Attachment with followers and followees data of vertex. you can check about Preferential Attachment in below link http://be.amazd.com/link-prediction/ 

- Add feature called svd_dot. you can calculate svd_dot as Dot product between sourse node svd and destination node svd features. you can read about this in below pdf https://storage.googleapis.com/kaggle-forum-message-attachments/2594/supervised_link_prediction.pdf
    

# Modeling

- we are hyperparameter tuning for XG boost with all these features

- we get best train and test accureces

- Train f1 score 0.9892563978754224

- Test f1 score 0.9256446597423477

- we check the error metric using confusion matrics

> ######### importent features


- hubs_s

- page_rank_d

- svd_dot

- katz-d

- katz-s

- so...on
