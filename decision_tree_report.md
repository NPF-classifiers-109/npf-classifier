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
For the initial testing of the decision tree classifier, the standard data cleaning that the group decided on for all models was used. Fortunately, since the data was already very clean (no missing data, etc.) to begin with, all that needed to be done was the removal of the “partlybad” column and creation of a new categorical binary column to classify observations as “event” or “non-event”. Then, the features and classifications were separated, and an even test/train split was applied to both dataframes. A decision tree classifier with a max depth of 3 (to prevent overfitting) was trained on the training data, and then scored for accuracy on the test data. Generally, the performance was quite good, with accuracies in the range of 0.76 to 0.82.
There are several extensions of the decision tree algorithm that can be used to further increase the accuracy. The most notable is the “Random Forest” approach, which caught our eye because it was called one of the most powerful classifiers available during a lecture. Just like the basic decision tree algorithm, the Random Forest algorithm is relatively easy to understand: a whole “forest” of different “trees” is grown during training, and the output is whatever the majority of trees decide to classify an observation as. The trees are created by taking random samples and constructing the trees based on different parts of the training set, analogous to K-fold cross validation used with other statistical learning methods. This method helps to reduce one of the major sources of error in decision trees, which is overfitting. By training trees on different portions of the training set and essentially averaging across many different trees, the variance is lowered and overfitting is more easily avoided. The only major downside is that the model itself becomes hard to interpret (as now you’re dealing with potentially dozens of trees instead of just one), though not quite as opaque as the “black-box” methods seen in deep learning. This downside does not affect us much since our goal is simply to make a classifier that is as accurate as possible, regardless of what the method or the model is.

The Random Forest classifier was tested using the same cleaned data and test/train split from the original decision tree classifier. The forests generated consisted of 100 trees (bumped up from the default of 10, on the recommendation of a warning that said the default in the next version was going to be 100). The max number of features per tree was set to “sqrt”, which bases the number of features on the square root of the total features. Lower numbers of features means lower variance, so setting the max features this low is in line with our goals. No max depth value was provided, however, since we don’t really have to be concerned anymore with overfitting in each individual tree. The accuracies from the Random Forest classifier were quite a bit better than just the decision tree classifier, ranging from 0.87 to 0.89, a gain of almost 0.1 on average. At these accuracies, it is likely difficult to find any better classifier, unless there is some “true” model that could be uncovered through other modelling techniques, such as the glm. From what we have seen with our testing, this is unlikely to be the case though.

