# Clustering-using-R

### Used the K-means method to cluster the prospects dataset. Set the number of clusters to four.

K-means clustering with 4 clusters of sizes 879, 1663, 854, 1199
**Below are the cluster means**
 
 
![image](https://user-images.githubusercontent.com/15854238/148449557-d90d179f-9d39-4228-b3a1-f16195cd3d69.png)

**Below are cluster variances**
C1: 836.3733 
C2: 1199.8230  
C3: 841.6978  
C4: 854.9522

**Below is the cluster plot:**

![image](https://user-images.githubusercontent.com/15854238/148449609-73345ecf-a871-4ebe-bb0a-e2505245dd07.png)

**For each of the four clusters, below are the characteristics of members of that cluster.**

**In Cluster1:**
•	Number of points in cluster 1 is 879.
•	The Ratio of males and females is close to ratio 483:396, the number of males is more than females.
•	More than 50% of the people are married.
•	Average age is 56	
•	Average income is 38K

**In Cluster2:**
•	Number of points in cluster 2 is 1663
•	The Ratio of males and females is close to ratio 814:849, the number of females is more than males.
•	Around 46% of the people are married.
•	Average age is 58
•	Average income is 38K.

**In Cluster3:**
•	Number of points in cluster 3 is 854.
•	The Ratio of males and females is close to ratio 495:359, the number of males is more than females.
•	Around 57% of the people are married.
•	Average age is 58
•	Average income is 39K.

**In Cluster4:**
•	Number of points in cluster 4 is 1199.
•	The Ratio of males and females is close to ratio 660:539, the number of males is more than females.
•	Around 74% of the people are married.
•	Average age is 60.
•	Average income is 47K.

We could see that the cluster 4 has more average numbers in terms of age and income compared to other clusters. 

**Best Value of K for this dataset** 

For k=5 Clusters, Variation between clusters is 53.2%
For k=6 Clusters, Variation between clusters is 57.3%
For k=7 Clusters, Variation between clusters is 60%
For k=8 Clusters, Variation between clusters is 63.1%
For k=9 Clusters, Variation between clusters is 66.1%
#For k=10 Clusters, Variation between clusters is 69.8%

From the above exploration we could see that the Variation between clusters for k=10 is the highest hence we take this as the best k for data set.

**Silhouette measure of the clusters obtained by best k**
Below plot depicts the variation between clusters. After k=10 clusters the variation within the group is stable. 

![image](https://user-images.githubusercontent.com/15854238/148450079-f0ee0090-5213-4e42-9de1-0a8d8a34a6a1.png)

![image](https://user-images.githubusercontent.com/15854238/148450101-d57144cf-a45c-4efd-bf2a-8177bf5e28d0.png)

**The Average silhouette value for the best value of k=10 is 0.36. Above plot depicts the same.**

