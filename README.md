---
title: "README"
author: "Dar Nettler & Carmela Davidovsky"
date: "December 31, 2017"
output: html_document
---
# First Question
You can find the full code here
First we will see the graph we made [here](https://github.com/carmelad912/ex3/blob/master/Q1/Q1.Rmd)    

![first graph](https://github.com/carmelad912/ex3/blob/master/Q1/1-first%20graph.PNG)  

## First Part
### In Betweenness
```{r}
which.max(betweenness(g, v=V(g), directed = FALSE, weights=NULL, nobigint = FALSE, normalized = FALSE))
```
we got that **sloan** is the most central.    

![betweenes](https://github.com/carmelad912/ex3/blob/master/Q1/1-betweenes.PNG) 

### In Closeness
```{r}
which.max(closeness(g, v=V(g), mode = c("out", "in", "all", "total"),
  weights = NULL, normalized = FALSE))
```
we got that **torres** is the most central.  

![closeness](https://github.com/carmelad912/ex3/blob/master/Q1/1-closeness.PNG) 
### In Eigenvector
```{r}
which.max(eigen_centrality(g)$vector)
```
we got that **karev** is the most central.  

![eigevector](https://github.com/carmelad912/ex3/blob/master/Q1/1-eigenvector.PNG) 


## Second Part
### First algorithm: Girvan-Newman community detection
This is a divisive method that works on undirected unweighted networks. It is based on calculating for each edge its **edge betweeness-** the number of shortest path going through this edge.

It then iteratively removes the edge with the highest betweeness score, until reaching some threshold.

The remaining connected vertices are communities (clusters).
#### The colored graphs
```{r}
gc <-  edge.betweenness.community(g)
```

```{r}
#Store cluster ids for each vertex
memb <- membership(gc)
head(memb)
```

```{r}
plot(g, vertex.size=5, 
     vertex.color=memb, asp=FALSE)
```
![first algo graph](https://github.com/carmelad912/ex3/blob/master/Q1/1-first%20algo%20graph.PNG)  

#### Number of communities and their size
the number of communitis is 7:
```{r}
gc
```

![number of communities graph](https://github.com/carmelad912/ex3/blob/master/Q1/1-first%20num.PNG)

The sizes of the communities are:
```{r}
sizes(gc)
```
![sizes of communities graph](https://github.com/carmelad912/ex3/blob/master/Q1/1-first%20sizes.PNG)

#### Modularity
The modularity is 0.58:
```{r}
max(gc$modularity)
```
![modularity](https://github.com/carmelad912/ex3/blob/master/Q1/1-first%20modularity.PNG)

### Second algorithm: Walktrap community detection
Tries to find densely connected subgraphs, also called communities in a graph via random walks. The idea is that short random walks tend to stay in the same community.

#### The colored graphs
```{r}
# Remove self-loops is exist
g <- simplify(g)
gc2 <-  fastgreedy.community(g)
```

```{r}
plot(g,  vertex.size=5,
     vertex.color=membership(gc2), asp=FALSE)
```
![second algo graph](https://github.com/carmelad912/ex3/blob/master/Q1/1-second%20algo%20graph.PNG)

#### Number of communities and their size
the number of communitis is 6:
```{r}
gc2
```

![number of communities](https://github.com/carmelad912/ex3/blob/master/Q1/1-second%20num.PNG)

The sizes of the communities are:
```{r}
sizes(gc2)
```
![sizes of communities](https://github.com/carmelad912/ex3/blob/master/Q1/1-second%20sizes.PNG)

#### Modularity
The modularity is 0.59:
```{r}
max(gc2$modularity)
```
![modularity](https://github.com/carmelad912/ex3/blob/master/Q1/1-second%20modularity.PNG)

# Second Question
Since we're both regular watchers and fans of grey's anatomy, we decided to continue with the theme of grey's anatomy in this part of the assignment.

Using twitter's API we requested 1,500 tweets that include the hashtag "#GreysAnatomy".
Then, we extracted the hashtags from each tweet using the "stringr" package and regex in order to see what people are associating with the show  
Our graph consist of the hashtags from the extracted tweets as vertices. Two vertices share an edge if both hashtags appeared in the same tweet.

For example: if the fallowing tweet was extracted:  
**the hottest guys in #GreysAnatomy are #McDreamy #McSteamy #McVet**    
the graph vertices will be: McDreamy, McSteamy and McVet  
and the graph edges: McDreamy--McSteamy, McDreamy-McVet McSteamy--McVet.

You can find the full code [here](https://github.com/carmelad912/ex3/blob/master/Q2/Q2.Rmd).
You can find the csv file with the results we cheked [here](https://github.com/carmelad912/ex3/blob/master/Q2/1500.csv).
the graph we got after collecting the data:
![first graph](https://github.com/carmelad912/ex3/blob/master/Q2/2-first%20graph.PNG)

## First Part
### In Betweenness
```{r}
which.max(betweenness(graphy, v=V(graphy), directed = FALSE, weights=NULL, nobigint = FALSE, normalized = FALSE))
```
we got that **#scandal** is the most central.  

![betweeness](https://github.com/carmelad912/ex3/blob/master/Q2/2-betweenes.PNG)

### In Closeness
```{r}
which.max(closeness(graphy, v=V(graphy), mode = c("out", "in", "all", "total"),
  weights = NULL, normalized = FALSE))
```
we got that **#scandal** is the most central.  

![closeness](https://github.com/carmelad912/ex3/blob/master/Q2/2-closeness.PNG)

### In Eigenvector
```{r}
which.max(eigen_centrality(graphy)$vector)
```
we got that **#japril** is the most central.  

![eigenvector](https://github.com/carmelad912/ex3/blob/master/Q2/2-eigenvector.PNG)

## Second Part
### First algorithm: Girvan-Newman community detection
#### The colored graphs
```{r}
gc <-  edge.betweenness.community(graphy)
```

```{r}
#Store cluster ids for each vertex
memb <- membership(gc)
head(memb)
```

```{r}
tkplot(graphy,layout=layout.kamada.kawai, vertex.color=memb, asp=FALSE)
```
![first algo graph](https://github.com/carmelad912/ex3/blob/master/Q2/2-first%20algo%20graph.PNG)

#### Number of communities and their size
the number of communitis is 48:
```{r}
gc
```
![number of communities](https://github.com/carmelad912/ex3/blob/master/Q2/2-first%20num.PNG)

The sizes of the communities are:
```{r}
sizes(gc)
```

![sizes of communities](https://github.com/carmelad912/ex3/blob/master/Q2/2-first%20sizes.PNG)

#### Modularity
The modularity is 0.92:
```{r}
max(gc$modularity)
```

![modularity](https://github.com/carmelad912/ex3/blob/master/Q2/2-first%20modularity.PNG)

### Second algorithm: Walktrap community detection

#### The colored graphs
```{r}
# Remove self-loops is exist
graphy <- simplify(graphy)
gc2 <-  fastgreedy.community(graphy)
```

plotting the graph:
```{r}
tkplot(graphy,layout=layout.kamada.kawai, vertex.color=membership(gc2),asp=FALSE)
```

![second algo graph](https://github.com/carmelad912/ex3/blob/master/Q2/2-second%20algo%20graph.PNG)

#### Number of communities and their size
the number of communitis is 48:
```{r}
gc2
```

![number of communities](https://github.com/carmelad912/ex3/blob/master/Q2/2-second%20num.PNG)

The sizes of the communities are:
```{r}
sizes(gc2)
```

![sizes of communities](https://github.com/carmelad912/ex3/blob/master/Q2/2-second%20sizes.PNG)

#### Modularity
The modularity is 0.92:
```{r}
max(gc2$modularity)
```
![modularity](https://github.com/carmelad912/ex3/blob/master/Q2/2-second%20modularity.PNG)
