---
layout: post
title: political affiliation is an eigenvector problem
---

### *on optimizing network modularity*

<p align="center">
<figure>
<img src="/images/largenetwork.webp" alt="network"/>
    <figcaption></figcaption>
</figure>
</p>

Consider the following problems:

* You have a data on a large collection of politically active Twitter users and their followers . Can you classify people based on how similar their political ideologies are? [^1]

* You are a streaming service with information on users' viewing 
preferences. Can you find categories of people with similar tastes in order to 
fine-tun your recommendations to them?[^2]



* You have a protein-protein interaction network. Can you 
find polypeptide chains which are responsible for 
generating a certain biological process? [^3]

* You have a database of drug-gene interactions. Can you find
pharacological pathways by looking at clusters of genes 
and drugs?[^4]




Note that the task in all of these problems 
is fundamentally the same - we have network of nodes, 
and a collection of edges
between them. We want sort to the network into a 
collection of groups, identified with some characteristic, such that nodes within a group are more likely 
to be connected to each other, 
and less likely 
to be connected to  nodes outside their group. To do so, first, we must find a way of measuring how 
good a particular sorting is, and then, we must find the 
optimal sorting.
This task, known as 
modularity maximization, is NP-complete[^5].
 This purpose 
of this post is to describe a clever heuristic 
to solve it in $O(n\log(n)$ time!

## Modularity

Take an arbitrary graph whose nodes are each identified by 
some finite set $i=\{1,2,3,...\}$. We say that the graph 
is assortative provided that we expect that nodes of the 
same type are relatively likely to be connected compared 
to nodes of some different type. For example, consider a
graph of people, where a connection represents familiarity 
between two individuals. One potiential assortative 
characteristic would be the language they speak.



<p align="center">
<figure>
<img src="/images/badgraphs.png" alt="network"/>
    <figcaption>These two graphs are identical, but labeling and rerrangement makes its divisons clear</figcaption>
</figure>
</p>


Not all English speakers talk to each other 
and some Chinese speakers talk to Arabic speakers, so 
none of the boundaries are absolute - and yet, there are 
clearly natural groups which form. 

We can measure the modularity of a graph through the following process:

1. If edges were randomly selected, what percent of total edges would 
we expect to be between nodes of the same type?
2. What percent of total edges are actually between nodes of the same type?
3. Subtract the actual value from the expected value

Recall that for a graph with $n$ vertices, we define its adjacency matrix $A$ as an $n \times n$ matrix where 
$A_{ij}=1$ if there exists an edge between $i$ and $j$ , 
and $A_{ij}=0$ if there doesn't.Additionally, we 
define the Kronecker delta $\delta_{i,j}$ as equalling 
0 if $i \neq j$ and 1 if $i=j$.

First, we find the expected value. Let $i,j$ be 
two arbitrary nodes, let  $g_i,g_j$ be the type of these nodes, 
and let $k_i,k_j$ be degree of these nodes.


If we randomly place an edge, what are the odds 
of it being connected to $i$ and $j$? Clearly, it should be 
equal to the odds of a random edge being connected to $i$ times 
the odds of a random edge being connected to $j$. Recall 
that  a graph with $m$ edges has a total degree of $2m$, so 
this value is equal to $\frac{k_i}{2m} * \frac{k_j}{2m}$. Because we are only 
interested in edges between nodes of the same type, 
we multiply this value by the Kronecker delta, sum over 
all $i,j$ in the graph, and divide by $2$ to account for double 
counting. As such, the total number of expected edges between groups 
is:

$$\frac{1}{2} \sum_{i,j}\frac{k_ik_j}{2m} \delta_{g_ig_j} $$

Next, we find the actual number of edges between groups. To 
find this, all we have to do is sum over the entries of entries 
of the adjacency matrix, again multiplying by the Kronecker 
delta and dividing by 2:



$$ \frac{1}{2}\sum_{ij} A_{ij} \delta_{g_ig_j}$$

To find the modularity, we finally subtract these two values 
and divide by the total number of edges $m$:

$$\frac{1}{2m} \sum_{ij} (A_{ij} - \frac{k_ik_j}{2m}) \delta_{g_ig_j} $$ 

We can clean this expression up by defining two quantities:

$$ B_{ij} = (A_{ij} - \frac{k_ik_j}{2m}) $$



[^1]:<a href="https://arxiv.org/pdf/2204.07436.pdf">https://arxiv.org/pdf/2204.07436.pdf</a>
[^2]:<a href="https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7363828">https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7363828</a>
[^3]:<a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8430217/">https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8430217/</a>
[^4]:<a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8099108/#B30">https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8099108/#B30</a>
[^5]:<a href="hhttps://arxiv.org/pdf/physics/0608255.pdf">https://arxiv.org/pdf/physics/0608255.pdf</a>
