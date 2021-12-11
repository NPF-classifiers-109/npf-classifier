Our group decided to split up and evaluate a diverse set of machine learning models in order
to compare and determine the best one for this particular data set. We wanted to include at 
least one non-parametric learning method, since there are many real world phenomena that 
stubbornly resist constricting themselves to underlying models or probability distributions.
For our non-parametric method, we settled on the decision tree, as it is one of the most 
powerful while also being relatively easy to interpret. It also handles large datasets 
gracefully, especially when it comes to the number of features. One of the defining 
characteristics of the dataset from the beginning has been the large number of features, 
which makes feature selection practically a requirement for most statistical learning 
techniques, such as the glm. Even if there was actually an underlying linear model utilizing 
all of the features in the dataset, we might not even be able to compute it in a reasonable 
amount of time given the sheer number of features. But, as the number of features goes up 
and feature selection becomes more important, feature selection also becomes more difficult 
because the potential options grow larger and larger. There is not only the question of “what 
features” but also “how many features”, and a fair amount of subjectivity can start becoming 
involved at this point as there is no one objective way to answer this question. However, the 
decision tree algorithm handles all of the feature selection itself, so none of that becomes 
a concern. We can just feed all of our feature data for every observation into the algorithm, 
and through the course of building the tree, the features that give the most information 
will rise to the top of the tree and inform the initial decisions. In fact, by looking at the 
features near the top of the tree, we can even use the decision tree to perform our feature 
selection for other statistical learning algorithms, choosing to use only the features that the 
decision tree carried to the top. The one major thing to look out for is potential overfitting, 
since a decision tree grown large enough can fit any set of training data perfectly at the 
expense of generalizability. This can be avoided by restricting the tree’s depth and carefully 
pruning the tree once it is grown, and validating the trees using a test/train split. Fortunately, 
despite the fact that we have only one training dataset, it is quite large so it is easy to make 
robust datasets for both training and testing.
