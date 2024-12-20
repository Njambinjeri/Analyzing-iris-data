## Analyzing-iris-data 
### Preview


This famous (Fisher's or Anderson's) iris data set gives the measurements in centimeters of the variables sepal length and width and petal length and width, respectively, for 50 flowers from each of 3 species of iris. The species are Iris setosa, versicolor, and virginica.


### tools

 - R script

```R script
#load data from R 
library(datasets)
 data(iris)
 
 #understanding the data
 
#view data
View(iris)
#view the first 5 rows of the data
head(iris,5)
#view the last 5 rows of the data
tail(iris,5)
#summary statistics of the data
summary(iris)
#summary statistics of a specific data
summary(iris$Sepal.Length)


#data visualization of the data

#General scatter plot of all the variables
plot(iris)
plot(iris, col="blue")
#plot specific data
plot(iris$Sepal.Length,iris$Sepal.Width, col="orange",xlab = "sepal length",ylab="sepal width",main = "sepal length vs sepal width")

#histogram
hist(iris$Sepal.Length, col="red")

#show the Box plots for 4 variables as a function of 3 classes

install.packages("ggplot2")
library(ggplot2)
# see the data one more time before creating a MEGA BOXPLOT
View(iris)
plot1<-ggplot(iris,aes(x=Species,y=Sepal.Width))+geom_boxplot()+
  geom_point()
plot1
plot2<-ggplot(iris,aes(x=Species,y=Sepal.Length))+geom_boxplot()+
  geom_point()
plot2
plot3<-ggplot(iris,aes(x=Species,y=Petal.Width))+geom_boxplot()+
  geom_point()
plot3
plot4<-ggplot(iris,aes(x=Species,y=Petal.Length))+geom_boxplot()+
  geom_point()
plot4
# to merge the 4  box plots 
install.packages("gridExtra")
library(gridExtra)
grid.arrange(plot1,plot2,plot3,plot4,ncol=4)

#build a classification model

#check data for missing values
sum(is.na(iris))
#Assigning seed number(100) to allow a constant result when code is run
set.seed(100)
#perform a stratified split of data set
install.packages("caret")
library(caret)
TrainingIndex<-createDataPartition(iris$Species,p=0.8,list=FALSE)
TrainingSet<-iris[TrainingIndex,]
TestingSet<-iris[-TrainingIndex,]

#creating plots of Training Set and Testing Set
p1<-ggplot(TrainingSet,aes(Sepal.Length,Petal.Length,color=Species))+
  geom_point()+
  scale_color_manual(values=c("#135029","#E1AD01","#E2725B"))+
  ggtitle("Training Set")
p1
p2<-ggplot(TestingSet,aes(Sepal.Length,Petal.Length,color=Species))+
  geom_point()+
  scale_color_manual(values=c("#135029","#E1AD01","#E2725B"))+
  ggtitle("Testing Set")
p2
#show the plots side by side
multi_plot<-grid.arrange(p1,p2,ncol=2)
multi_plot
#The setosa and virginica has quite similar distribution
```



### Data visualisation
