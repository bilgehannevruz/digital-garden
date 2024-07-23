---
Created: 2024-02-13T17:38
URL: https://towardsdatascience.com/how-to-build-a-graph-based-neural-network-for-anomaly-detection-in-6-steps-a7dc47723788
---
# How to Build a Graph-based Neural Network for Anomaly Detection in 6 Steps

## Learn to build a Graph Convolutional Network that can handle heterogeneous graph data for link prediction

![[2SAaKdVJ0n0he3AKaPcIzNA.jpeg]]

![[1CJe3891yB1A1mzMdqemkdg.jpeg]]

[Claudia Ng](https://ds-claudia.medium.com/?source=post_page-----a7dc47723788--------------------------------)

·

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fba2da7b3b9c8&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fhow-to-build-a-graph-based-neural-network-for-anomaly-detection-in-6-steps-a7dc47723788&user=Claudia+Ng&userId=ba2da7b3b9c8&source=post_page-ba2da7b3b9c8----a7dc47723788---------------------post_header-----------)

Published in

[Towards Data Science](https://towardsdatascience.com/?source=post_page-----a7dc47723788--------------------------------)

·

17 min read

·

12 hours ago

Image from [Pixabay](https://pixabay.com/vectors/linked-connected-network-team-men-152575/)

![[1Lb_4cCQckr6i7aDoJ2SN5w.png]]

This article is a detailed technical deep dive into how to build a powerful model for anomaly detection with graph data containing entities of different types (heterogeneous graph data).

The model you will learn about is based on the paper titled “[Interaction-Focused Anomaly Detection on Bipartite Node-and-Edge-Attributed Graphs](https://engineering.grab.com/files/GraphBEAN_IJCNN_2023.pdf)” presented by Grab, an Asian tech company, at the 2023 International Joint Conference on Neural Networks (IJCNN) conference.

This Graph Convolutional Network (GCN) model can handle heterogeneous graph data, meaning that nodes and edges are of different types. These graphs are structurally complex as they represent relationships between different types of entities or nodes.

GCNs that can handle heterogeneous graph data is an active area of research. The convolutional operations in the model have been adapted to address challenges around handling different node types and their relationships in a heterogeneous graph.

In contrast, homogeneous graphs involve nodes and edges of the same type. This type of graph is structurally simpler. An example of a homogeneous graph include LinkedIn connections, where all nodes represent individuals and edges exist between individuals if they are connected.

The example you will see here applies Grab’s GraphBEAN model (**B**ipartite Node-and-**E**dge-**A**ttributed **N**etworks) to a Kaggle [dataset](https://www.kaggle.com/datasets/rohitrox/healthcare-provider-fraud-detection-analysis/data?select=Train_Beneficiarydata-1542865627584.csv) on healthcare provider fraud. (This dataset is currently licensed CC0: Public Domain on Kaggle. Please note that this dataset might not be accurate, and it’s used in this article only for demonstration purposes). The dataset contains multiple csv files with claims and insights on inpatient data, outpatient data, and beneficiary data.

I will demonstrate how to build a GCN to predict healthcare provider fraud using the inpatient dataset and train set containing `ProviderID`and a label column (`PotentialFraud`).

While graph data can be difficult to visualize in tabular form, like the csv files, you can make interesting…