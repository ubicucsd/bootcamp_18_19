### SSH address: @ec2-18-218-72-125.us-east-2.compute.amazonaws.com
### Talk to Mark if you do not have an ec2 account yet

scp ubuntu@ec2-18-218-72-125.us-east-2.compute.amazonaws.com:/home/ubuntu/clustering_lesson/foo.pdf .

scp username@ec2-18-218-72-125.us-east-2.compute.amazonaws.com:/home/username/path /localpath/


# Clustering

#### Skills: Familiarity with sklearn package and an understanding of why clustering is useful in bioinformatics

1. General Description of clustering and why it is important in bioinformatics

### General Factoids

**Clustering:** The process of partitioning a dataset into groups based on shared unkown characteristics. In other words, we are looking for patterns in data where we do not necessarily know the patterns to look for ahead of time. 

**In:** N points, usually in the form of a matrix(each row is a point). 

**In:** A distance function to tell us how similar two points are. The simplest is [euclidean distance](http://rosalind.info/glossary/euclidean-distance/)

**Out:** K groups, each containing points which are similar to each other in some way. Some algorithms cluster for a preset number K, others figure it out as they go along. 

### Methods

In this class, I want to demonstrate the difference between different clustering algorithms. To start with, we need data that will make these differences very obvious. 

First off, copy the file ```/home/ubuntu/clustering_lesson/```

Start by creating some blobs using numpy's random normal generator. First, create a seed for the random number generator with ```np.random.seed()```. This will make a blob centered around 5 with a stdev of 2 in the form of a 1000\*2 array: ```clust1 = np.random.normal(5, 2, (1000,2))```. Make a few blobs with centers between 0 and 20 (keep the array dimensions the same). Now, use ```set1=np.concatenate()``` to bring the blobs into one structure.

The figure we can use to contrast the blobs is some circular point layouts. Make two concentric circles with ```set2=datasets.make_circles(n_samples=1000, factor=.5, noise=.05)[0]```

Finally, use the provided ```cluster_plots()``` function with the two sets you have generated to generate some pretty plots. **Note:** this will save your plots to a pdf file in your current directory, the name of which can be changed (look at the argument called *name*!) You'll have to scp the file over to your computer to view it. 

<details>
  <summary>Forgot how to scp? click here</summary>
  
```python
scp username@ec2-18-218-72-125.us-east-2.compute.amazonaws.com:/home/username/path /localpath/
Do not forget to replace the paths and username!
````
</details></br>

There are a few approaches to clustering, let us look into 3 of them for now. 

### 1. K-means

  I. Select K centers. This can be done a variety of ways, the easiest of which is to select a random point, find the farthest point from that and select it, find the furthest point from the previous and so on. 
  
  II. Assign each point to the center nearest to it. 
  
  III. For each center, take all the points attached to it and take their average to create a new center for that cluster.
  
  IV. Reassign all points to their nearest center and continue reassigning + averaging until the iteration when nothing changes
  
  

### A few examples of Bioinformatics applications: 

1. Finding what genes are up and down regulated under certain conditions. Imagine you have a matrix, where each point is a set of gene expression recorded for a variety of conditions. If two points are close to each other, that means they had similar expression levels throughout those conditions. 

2. 

2. Get an example dataset and have them learn a few different methods with sklearn on python

3. Example from Ben lab + an article example or something

4. Challenge exercise can be a 181-like assignment to implement a type of clustering (such as soft clustering) 
