# Predicting-Movie-Ratings-on-MovieLens

When trying to predict a user's rating over an unseen movie, 2 main approaches jump in mind: Collaborative and Content-based recommendations. For this challenge, iv'e chosen to explore both methods in order to try to find the optimal solution.

However, some restrictions must be kept in mind. But first, lets describe the problem and used data:

### Objective

Predict a user's rating over an unseen movie with either a *high (>=4.0)* or low *(< 4.0)* score, becoming a binary problem.

### Data

Kaggle's **20M MovieLens** data. It contains an approximate of 20M rows of user-movie-rating, with about **138.5k** unique Users and **26.7k** unique Movies. Extra files contained in data are:

* genome_scores.csv: contains movie-tag relevance data.
* genome_tags.csv: contains tag descriptions.
* link.csv: contains identifiers that can be used to link to other sources.
* movie.csv: contains movie information.
* rating.csv: contains ratings of movies by users.
* tag.csv: contains tags applied to movies by users.

### Approached Solutions:

The chosen approaches were selected on an empirical basis and by their mentions on literature.

* The first approach to predict user's rating relays on a content based (item based) focus, under the algorithms listed below: 
    * Simple Logistic Regression
    * Xgboost

* The second approach relays on a very used alternative over recommendations problems, which is **Binary Matrix Factorization (BMF)**

## *Considerations*

* Despite recommender systems also work under content-based approaches (recommending the top N most similar movies by computing movie to movie similarity). It impiesy a correlation between movies features and the output might not end up giving the rating a user may give to it. Thus, collaborative filtering results a more useful technique for this specific task.

* If the 20M MovieLens is given in this challenge, extracting an **X%** of data to work with may end in disrpting the challenge nature itself. For this reason, i've ommited some approaches i could have use but the computational power required was beyond my personal computer. Such approaches are listed bellow:
    * Using Tags as features: Only **1.96%** of the rated movies have an attached tag. By considering this feature (which may be representative on a less dense scenario though) we would ommit a huge amount of the given data for the challenge, despite accuracy over that % may result high.
    * Using word embedding techniques over the given features (if we used them) such as clustering words on a pre-trained model (GloVe word embedding, for instance) may require up to 30GB of free memory just to extract and apply the mapping to the words presen on tags.

* By binarysing data, we're not dealing with unbalanced classes. Instead, we have a very uniformely distribution between 0 & 1 classes, with 50% & 50% respectively.
* Note how the BMF method gets any prediction by using elementwise multiplication from the corresponding embeddings (feature matrices) and then sum to get the prediction $u_i m_j$. This avoids creating the dense matrix $U \times M^T$, hugely saving space allocation and processing requirements.


### Future work (if time is given)

* Explore content-based/collaborative hybrid approaches by using both movies & users similarity as the predictive base.
* Explore different ML techniques on the Logistic Regression, such as binary trees, SVM, deep learning...
* Try to merge variables such as common paired genres on movies, which bight reflect a real life case.
* Research on parallel computation on high memory consuming processes into the code, such as computing sparse matrixes, extracting mapping vectors.
* Reducing exploring space (not by %, but by importance of data) i.e. dropping users with excesive ratings (outlier user) and/or movies rated by a very low number of users (outlier movie).
* Try (For Logistic Regression) categorical variables encoding (assign a unique continuos value to each unique value) instead of one-hot encoding them and see if there's a signifficant difference.
* Xgboost algorithm may worth waiting training with deeper depht and different learning_rate. However, this is one of the most time-consuming algorithms, taking up to 1 hour to train, thus it not feasible to explore such options at this very specific exercise.
* Using k-fold validation on by performing random selection on validation set.

### Final Remarks.

* *Everithing can some way or another be improved*. Specially in our field, with data modeling, new technologies arise every second and bay worth the time investement on tuning and improving our modeling outputs.
* From the algorithms evaluated here, we got the below listed outcomes on the evaluation data set:
    * Baseline (simple mean value): **50%** accuracy (sames as tossing the coin). 
    * Logistic Regression: **57%** accuracy.
    * XgBoost: 
    * BInary Matrix Factorization: **58.2%** accuracy.

> ### Total spent time on this exercise $\approx$ 7 hours (training included).
