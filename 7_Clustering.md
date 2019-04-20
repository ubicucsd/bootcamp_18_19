### SSH address: @ec2-18-218-72-125.us-east-2.compute.amazonaws.com
### Talk to Mark if you do not have an ec2 account yet

scp ubuntu@ec2-18-218-72-125.us-east-2.compute.amazonaws.com:/home/ubuntu/clustering_lesson/foo.pdf .

#### Preliminary note:

This lesson will force you to look through documentation and fill in the blanks on some of the functions. I know I could have given you the full code, but I think that more is learned when you are forced to interact with the code to some extent. Note that in Python syntax, you will have to use the dot (period) to indicate when you are going from a general to specific scope. For example, there is a package called numpy, with a module called random, with a function called seed. The seed function is called by typing out ```np.random.seed()```, telling python where exactly it needs to look. 

# A little bit on Clustering

#### Skills: Familiarity with sklearn package and an understanding of why clustering is useful in bioinformatics

1. General Description of clustering and why it is important in bioinformatics

### General Factoids

**Clustering:** The process of partitioning a dataset into groups based on shared unkown characteristics. In other words, we are looking for patterns in data where we do not necessarily know the patterns to look for ahead of time. 

**In:** N points, usually in the form of a matrix(each row is a point). 

**In:** A distance function to tell us how similar two points are. The most intuitive distance function is [euclidean distance](http://rosalind.info/glossary/euclidean-distance/). The type of distance measure you use can vary depending on the type of data you are using. 

**Out:** K groups, each containing points which are similar to each other in some way. Some algorithms cluster for a preset number K, others figure it out as they go along. 

### Example Bioinformatics Applications: 

1. Finding what genes are up and down regulated under certain conditions. Imagine you have a matrix, where each point is a set of gene expression recorded for a variety of conditions. If two points are close to each other, that means they had similar expression levels throughout those conditions. 

2. Discerning different species present in a sample of unkown contents. This can be done with an algorithm that does not have a preditermined amount of clusters. An example application is taking HIV sequences from a patient, clustering them, and filtering clusters under a certain size to find the sequences of prevalent strains within the patient.

3. Finding evolutionary relationships between samples using hierarchical clustering. The earlier on two centers were combined, the closer their corresponding points are from an evolutionary perspective. 

## Clustering Methods

In this class, I want to demonstrate the difference between different clustering algorithms. To start with, we need data that will make these differences very obvious. 

First off, copy the file ```/home/ubuntu/clustering_lesson/clust.py``` into your own directory. 

Start by creating some blobs using numpy's random normal generator. First, create a seed for the random number generator with ```np.random.seed()```. This will make a blob centered around 5 with a stdev of 2 in the form of a 1000\*2 array: ```clust1 = np.random.normal(5, 2, (1000,2))```. Make a few blobs with centers between 0 and 20 (keep the array dimensions the same). Now, use ```set1=np.concatenate()``` to bring the blobs into one structure.

The figure we can use to contrast the blobs is some circular point layouts. Make two concentric circles with ```set2=datasets.make_circles(n_samples=1000, factor=.5, noise=.05)[0]```

Finally, use the provided ```cluster_plots()``` function with the two sets you have generated to generate some pretty plots. **Note:** this will save your plots to a pdf file in your current directory, the name of which can be changed (look at the argument called *name*!) You'll have to scp the file over to your computer to view it. 

<details>
  <summary>Forgot how to scp? click here</summary>
```
scp username@ec2-18-218-72-125.us-east-2.compute.amazonaws.com:/home/username/path /localpath/
Do not forget to replace the paths and username!
```
</details></br>

There are a few approaches to clustering, let us look into 3 of them for now. 

### 1. K-means

  I. Select K centers. This can be done a variety of ways, the easiest of which is to select a random point, find the farthest point from that and select it, find the furthest point from the previous and so on. 
  
  II. Assign each point to the center nearest to it. 
  
  III. For each center, take all the points attached to it and take their average to create a new center for that cluster.
  
  IV. Reassign all points to their nearest center and continue reassigning + averaging until the iteration when nothing changes
  
  Code to apply K-means clustering to set1 is below, don't forget to replace k with the number of blops you made above. Do the same for set2, but now set k=2.   There are two circles, right? It seems like each circle might share a characteristics within itself, so it would be nice if the computer could cluster the circles into 2 partitions. 
  ```
  kmeans_dataset1 = cluster.KMeans(n_clusters=k).fit_prediction(set1)
  cluster_plots(set1, set2, kmeans_dataset1, kmeans_dataset2)
  ```
  
### 2. Agglomerative Hierarchical 

   I. Start with every point being its very own cluster center. 
   
   II. Find the two centers which are closest to each other and combine them into one cluster. The new center is the average of the two previous ones. 
   
   III. Continue combining the closest centers until all points are under a single cluster. 
   
   Let's look at the blobs and circles we made again. Look at the [documentation page for agglomerative clustering](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AgglomerativeClustering.html) and figure out the proper calls for the two datasets (syntax is very similar to what you did for k-means). 
   
   Unfortunately, this still does not solve our circlular cluster issue. For that, we can ask the sklearn package to build a graph out of our circles which restricts the amount of nearest neighbors a point can cluster with. 
   
   ```
   #this line is missing a parameter - how would you set the number of nearest neighbors to 6?
   connect = kneighbors_graph(dataset2, include_self=False)
   
   #in this line, you need to set linkage to complete, number of clusters to 2, and set connectivity equal to the graph 
   #on the previous line
   hc_dataset2_connectivity = cluster.AgglomerativeClustering().fit_predict(dataset2)
   ```
   
   Use ```cluster_plots()``` to graph the plot resulting from the regular AgglomerativeClustering beside the graph that plots the connected AgglomerativeClustering. As you may have guessed, this fixes the circle problem. 
   
### 3. Expectation Maximization


## Dirichlet Process Means Clustering

Now that you have learned some terminology so you know how to Google information about clusters, let's practice Python by making our own clustering algorithm. 

The dirichlet process is just a method of clustering without knowing the number of clusters ahead of time. Something like this algorithm may be used for example 2 in the list of clustering related bioinformatics problems. Here are the steps:
 
\t  I. Add the first point in your data as the first center
  
\t  II. Iterate through all of the points in your data, calculating the distance between the current point and all existing centers. 
  
   A. If the point falls within a certain threshold distance of the center, add that point to that center's cluster
  
   B. If the point does not fall within a certain threshold distance of the center, add that point to the list of centers
    
  III. Once you have gone through the Dirichlet Process, you do the means part. Redifine the centers of each cluster to be the average of all points in the cluster, like you would in most standard clustering algorithms. 
  
  IV. Repeat steps II and III either until an iteration provides no change in the assignment of points to centers, or a maximum number of cycles is reached. 
  
I provided a starting file at ```/home/ubuntu/clustering_lesson/dmp.py``` to get the ball rolling 