
### What is Active Learning?
In this section, we take a closer look at what active learning is and how it works within MindMeld.

Active Learning is an approach to continuously and iteratively pick data that is most informative for the models to train on from a pool of data-points. By choosing these informative data-points, active learning provides a higher chance of improving the accuracy of the model with fewer training examples. If the pool of data-points is unannotated, active learning also greatly reduces the number of queries that need manual annotation. MindMeld provides this inbuilt functionality to select these must-have queries from existing data or additional logs and datasets to get the best out of your conversational applications.

MindMeld's NLP pipeline consists of a hierarchy of classifier and tagger models for domain, intent, entity and role classification. Each classifier takes as input the query text and extracted features to generate a probability distribution for the corresponding classes in the hierarchy. These probability distributions can be strong indicators of the classifier's confidence in its prediction and can be useful in determining whether the query needs further reflection.

Say for a query A from the logs, the classifier assigns a probability of 0.95 or 95% to the selected class (i.e, the highest probability class) in the domain classifier and the remaining 5% is distributed amongst the rest of the domains. This indicates a high confidence by the classifier in its prediction. Whereas, for a query B, if the classifier assigns a probability 0.5 for the selected class, it would indicate a lower confidence in its prediction. Based on these confidence values, certain active learning strategies will select query B over query A which can be annotated and added to the training data. Once the classifier is trained with this additional data, it has a higher chance of performing better on similar confusable queries. Later sections explain how different strategies use these confidence scores to select important queries.

There are two phases in MindMeld's active learning pipeline. One, for configuring the best hyperparameters (such as the optimal strategy) for the pipeline and the other, for selecting the most important subset of queries from logs given the optimal configuration. These phases are referred to as Strategy Tuning and Query Selection respectively. Before diving deeper into these phases, let us take a look at the configuration file for setting up MindMeld's active learning pipeline.