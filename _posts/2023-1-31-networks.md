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
generating some biological process? [^3]

* You have a database of drug-gene interactions. Can you find
pharacological pathways by looking at clusters of genes 
and drugs?[^4]




Note that the task in all of these problems 
is fundamentally the same - you have network of nodes, 
and a collection of edges
between them. We want divide the network into a 
collection of groups, identified with some characteristic, such that nodes are comparatively likely 
to be connected to other nodes inside their group, 
and comparatively dislikely 
to be connected to  nodes outside their group. This purpose 
of this post is to describe a clever way of doing 
so(in $O((m+n)\log(n)$ time!)


[^1]:https://arxiv.org/pdf/2204.07436.pdf
[^2]:https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7363828
[^3]:https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8430217/
[^4]:https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8099108/#B30