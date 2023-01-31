---
layout: post
title: political affiliation is an eigenvector problem
---
### on optimizing network modularity

<p align="center">
<figure>
<img src="/images/largenetwork.png" alt="isolated"/>
    <figcaption></figcaption>
</figure>
</p>

Consider the following problems:

* You have a data on a large collection politically active Twitter users and their followers . Can you identify and classify people based on how similar their political ideologies are? [^1]

* You are a streaming service with information on users' viewing 
preferences. Can you find categories of people with similar tastes in order to 
fine-tun your recommendations to them?[^2]



* You are an organization responsible for distributing electrical power 
to peoples homes. With an increasing number of consumers 
generating their own renewable energy and selling it back, 
can you  partition the grid into communities as to minimize power losses? [^3]

* You have a database of drug-gene interactions. Can you 
find clusters of genes and drugs which correspond to some 
pharmacological pathway?[^4]




Note that the task in all of these problems 
is fundamentally the same - you have network of nodes, 
and a collection of edges
between them. Is there a way to divide the network into a 
collection of groups, identified with some characteristic, such that nodes are comparatively likely 
to be connected to other nodes inside their group, 
and comparatively dislikely 
to be connected to  nodes outside their group.


[^1]:https://arxiv.org/pdf/2204.07436.pdf
[^2]:https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7363828
[^3]:https://arxiv.org/pdf/2112.08300.pdf
[^4]:https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8099108/#B30