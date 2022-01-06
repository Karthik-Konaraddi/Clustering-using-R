library(tidyverse) #data manipulation
library(modeest) #for mfv to calculate mode
library(factoextra) #clustering algorithms & visualization
library(cluster) #clustering algorithms
library(dplyr) #For data filter
library(caret) # For using dummy function

pros <- read.csv("C://prospect.csv")
data<-pros
data<-data.frame(data)


#Excluding the location and ID variable
data<-select(data,-c(ID,LOC)) 

#Taking care of NA values
data$AGE[is.na(data$AGE)]<-mfv(data$AGE)
data$INCOME[is.na(data$INCOME)]<-mfv(data$INCOME)
data$SEX[data$SEX==""]<-mfv(data$SEX)
data$MARRIED[is.na(data$MARRIED)]<-mfv(data$MARRIED)
data$OWNHOME[is.na(data$OWNHOME)]<-mfv(data$OWNHOME)
data$FICO..700[is.na(data$FICO..700)]<-mfv(data$FICO..700)
data$SEX<-as.factor(data$SEX)
data$CLIMATE<-as.factor(data$CLIMATE)
data$SEX<-ifelse(data$SEX=="M",1,0)



#To remove any missing value that might be present in the data
data <- na.omit(data)

#For normalizing the data in AGE and INCOME VARIABLE
data$AGE <- data$AGE / max(data$AGE)
data$INCOME <- data$INCOME / max(data$INCOME)

#Creating dummy variables for CLIMATE 
alldata = select(data, -CLIMATE)
dummy <- dummyVars(~ CLIMATE, data=data)

newdata <- data.frame(predict(dummy, newdata = data))
data<- cbind(newdata,alldata)




#As we don't want the clustering algorithm to depend to an arbitrary variable unit, 
#we start by scaling/standardizing the data using the R function 

df <- data

set.seed(1234)

#We can compute k-means in R with the kmeans function. Here will group the data into 
#12 clusters (centers = 12). The kmeans function also has an nstart option that attempts multiple initial 
#configurations and reports on the best one. For example, adding nstart = 25 will generate 25 initial configurations. 
#This approach is often recommended
#For k=4 Clusters, Variation between clusters is 47.1%
km1<-kmeans(df,4,nstart=25)
km1

#For getting the summary of each cluster characteristics
cluster1 <- df[which( km1$cluster == 1),]
summary(cluster1)
cluster2 <- df[which( km1$cluster == 2),]
summary(cluster2)
cluster3 <- df[which( km1$cluster == 3),]
summary(cluster3)
cluster4 <- df[which( km1$cluster == 4),]
summary(cluster4)


#If we print the results we'll see that our groupings resulted in 12 cluster. 
#We see the cluster centers (means) for the 12 groups across the Seven variables. 
#We also get the cluster assignment for each observation 

fviz_cluster(km1,data = df,geom="points")
#This provides a nice illustration of the clusters. 
#If there are more than two dimensions (variables) fviz_cluster will perform 
#principal component analysis (PCA) and plot the data points according to the 
#first two principal components that explain the majority of the variance.

#Alternatively, we used standard pairwise scatter plots to illustrate the clusters 
#compared to the original variables.

df %>%
  as_tibble() %>%
  mutate(cluster = km1$cluster,
         state = row.names(data)) %>%
  ggplot(aes(AGE, INCOME,SEX,MARRIED,OWNHOME,LOC,CLIMATE, color = factor(cluster), label = state)) +
  geom_point()

#Because the number of clusters (k) must be set before we start the algorithm, it is often advantageous to use several different values of k and examine the differences in the results. 
#We can execute the same process for 5, 6, 7, 8, 9 and 10 clusters, 
#and the results are shown in the figure

#For k=5 Clusters, Variation between clusters is 53.2%
k5 <- kmeans(df, centers = 5, nstart = 25)
#For k=6 Clusters, Variation between clusters is 57.3%
k6 <- kmeans(df, centers = 6, nstart = 25)
#For k=7 Clusters, Variation between clusters is 60%
k7 <- kmeans(df, centers = 7, nstart = 25)
#For k=8 Clusters, Variation between clusters is 63.1%
k8 <- kmeans(df, centers = 8, nstart = 25)
#For k=9 Clusters, Variation between clusters is 66.1%
k9 <- kmeans(df, centers = 9, nstart = 25)
#For k=10 Clusters, Variation between clusters is 69.8%
k10 <- kmeans(df, centers = 10, nstart = 25)


#the process to compute the "average silhoutte method" has been wrapped up in a single function 
#(fviz_nbclust)

fviz_nbclust(df, kmeans, method = "silhouette")

# "average silhoutte method" suggested 10 as the number of optimal clusters.


#For finding the best k value
mydata<-df
wss<-(nrow(mydata)-1)*sum(apply(mydata,2,var))
for(i in 1:15)
  wss[i]<-sum(kmeans(mydata, centers = i)$withinss)
plot(1:15,wss,type = "b",xlab = "Number of clusters", ylab = "Within groups sum of squares", pch=20, cex=2)

#silhouette(Euclidean)
avg_sil<-function(k)
{
  kmModel<-kmeans(df, centers = k, nstart =100 )
  ss<-silhouette(kmModel$cluster, dist(df))
  mean(ss[,3])
}

#The average silhoutte measure for best k=10 is 0.36
avg_sil(10)

