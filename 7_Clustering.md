### SSH address: @ec2-18-218-72-125.us-east-2.compute.amazonaws.com
### Talk to Mark if you do not have an ec2 account yet

# Clustering

#### Skills: More Python and hopefully an understanding of why clustering is useful in bioinformatics

1. General Description of clustering and why it is important in bioinformatics

### General Factoids

**Clustering:** The process of partitioning a dataset into groups based on shared unkown characteristics. In other words, we are looking for patterns in data where we do not necessarily know the patterns to look for ahead of time. 

**In:** N points, usually in the form of a matrix(each row is a point). 

**In:** A distance function to tell us how similar two points are. The simplest is [euclidean distance](http://rosalind.info/glossary/euclidean-distance/)

**Out:** K groups, each containing points which are similar to each other in some way. Some algorithms cluster for a preset number K, others figure it out as they go along. 

### Methods

There are a few approaches to clustering, let us look into 3 of them for now. 

1. 

### A few examples of Bioinformatics applications: 

1. Finding what genes are up and down regulated under certain conditions. Imagine you have a matrix, where each point is a set of gene expression recorded for a variety of conditions. If two points are close to each other, that means they had similar expression levels throughout those conditions. 

2. 

2. Get an example dataset and have them learn a few different methods with sklearn on python

3. Example from Ben lab + an article example or something

4. Challenge exercise can be a 181-like assignment to implement a type of clustering (such as soft clustering) 
