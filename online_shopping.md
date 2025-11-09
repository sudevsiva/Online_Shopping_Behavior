# Online_Shopping_Behavior
Decision Tree model to predict Age_Group based on online shopping data

data('online_Shopping_Behavior_Dataset')
View(Online_Shopping_Behavior_Dataset)
OSBD<-Online_Shopping_Behavior_Dataset
OSBD
obj=OSBD[,c("Age_Group","Average_Monthly_Spend (INR)","Payment_Method","Purchase_Frequency")]

table(obj$Age_Group)
train_index=createDataPartition(obj$Age_Group,p=0.8,list=FALSE)
train_data=obj[train_index, ]
test_data=obj[-train_index,]
sapply(train_data, length)
summary(train_data)

model <- rpart(Age_Group ~ `Average_Monthly_Spend (INR)`, data = train_data)
rpart.plot(model)
treepred=predict(model,test_data,type='class')
con=confusionMatrix(treepred,test_data$Age_Group)
con
accuracy=con$overall["Accuracy"]
accuracy
