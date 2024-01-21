# Social Network Analysis Project

This project explores social network data to derive insights and patterns using R.

## Overview

The objective is to analyze the given social network dataset and understand the relationships between individuals, identifying key influencers, and visualizing the network structure.

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/social-network-analysis-project.git
   cd social-network-analysis-project
# Code
#Social Network Analysis
install.packages("igraph")
library(igraph)
g<-graph(c(1,2,2,3,3,4,4,1),directed = F,n=7)
plot(g,vertex.color="green",vertex.size = 40, edge.color = 'red')
g[]
g1<- graph(c("Diksha","Nivedita","Utkarsh","Reet","Teesha","Jatin","Nikhil","Aakarsh","Sumit","Bulandi"),directed = F)

plot(g1,vertex.color="green",vertex.size = 40, edge.color = 'red')
g1
#Network Measures
degree(g1,mode='all')
degree(g1,mode='in')
degree(g1,mode='out')
diameter(g1,directed=F,weights=NA)
edge_density(g1,loops = F)
ecount(g1)/(vcount(g1)*(vcount(g1)-1))
reciprocity(g1)
closeness(g1,mode='all',weights=NA)
betweenness(g1,directed=T,weights=NA)


data<- read.csv(file.choose(),header=T)
y<-data.frame(data$first,data$second)

#create Network
net<-graph.data.frame(y,directed=T)
V(net)
E(net)
V(net)$label<-V(net)$name
V(net)$degree<- degree(net)

#Histogram of node degree
hist(V(net)$degree,col='green',main='Histogram of Node Degree',ylab = 'Frequency',xlab='Degree of Vertices')

#Network Analysis
set.seed(222)
plot(net,vertex.color='green',vertext.size=2,edge.arrow.size=0.1,vertex.label.cex=0.8)

#Highlights and Layouts

plot(net,vertex.color=rainbow(52),vertex.size=V(net)$degree*0.4,edge.arrow.size=0.1,layout=layout.fruchterman.reingold)
plot(net,vertex.color=rainbow(52),vertex.size=V(net)$degree*0.4,edge.arrow.size=0.1,layout=layout.graphopt)
plot(net,vertex.color=rainbow(52),vertex.size=V(net)$degree*0.4,edge.arrow.size=0.1,layout=layout.kamada.kawai)

#Hub and Authorities
hs<- hub_score(net)$vector
as<- authority.score(net)$vector
par(mfrow=c(1,2))
set.seed(123)
plot(net,vertex.size=hs*30,main='Hubs',vertex.color=rainbow(52),edge.arrow.size=0.1,layout=layout.kamada.kawai)
set.seed(123)
plot(net,vertex.size=hs*30,main='Authorities',vertex.color=rainbow(52),edge.arrow.size=0.1,layout=layout.kamada.kawai)
par(mfrow=c(1,1))

#Community detection
net<-graph.data.frame(y,directed=F)
cnet<-cluster_edge_betweenness(net)
plot(cnet,net,vertex.size=10,vertex.label.cex=0.8)

