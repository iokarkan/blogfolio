---
layout: post
title: "Suprisingly intuitive recommender systems"
tags: machine learning recommender surprise
---

Service or product recommendations happen to be major applications of Machine Learning that are tightly woven with our every day user experience online, especially social networks and media consumption. Simultaneously, it has been one of the directions that I have not had the chance to explore yet, so I decided to pursue an intuitive understanding and to put together this little introduction.

### Ratings Matrix

The first part in the process of producing a recommendation in any application is to formulate the goal, then understand and organise available information. The goal, in this case, is to increase engagement for the main protagonist of the application, the user, and, as a consequence, increase the consumption of whatever the application has to offer. The well-established rationale is that the probability of satisfactory (both for the user and for the owner of the app) navigation and interaction with the application is higher when the choices available throughout the user experience are aligned with the user's true desires and needs.

True knowledge of the desires and needs of the users are inferred by the available data. In fact, they are reasonably assumed to be correlated, to some degree, to the various user interactions. Note that the correlations are either explicit (e.g. actual reviews provided by the users) or implicit (e.g. number of times the user has considered or performed a selection). Although the former hold much more sway over whether a recommendation is valid, the latter are far more likely to be harvested on scale and on time. It is the work of any data scientist, then, to discover the most accurate implicit predictor, or formulate one out of existing implicit building
blocks. 

The grid representation of the users and the corresponding implicit and/or explicit ratings is the Ratings Matrix. The actual values that the Ratings Matrix will contain depend on the approach used on deciding how to select the factors will produce recommendations. In general, there are the following three approaches:

- Knowledge-based filtering
  - Provide recommendations based on widely accepted or explorative heuristics regarding the user and their selection
- Content-based filtering
  - Utilize a set of features from a product along with information on the user's preferences to reach a conclusion for
recommendation
- Collaborative filtering
  - Correlate the likelihood that a user will select a product based on the choices of other users that share their taste

The first two approaches are potentially based on either biased or one-dimensional approaches. In practice, the third one seems more
trustworthy and can offer the much needed element of surprise! More about that later...

In a hypothetical scenario where a web developer has implemented all kinds of user feedback metrics into an electronics
e-shop, one could arrange a Ratings Matrix like so:


| | | Products | |
| | 🎧 | 🖥 | ... |
| Users |                                         |                        Opinions                        |
| ----- | :-------------------------------------: | :----------------------------------------------------: |
| 👩     |                    👍                    |                           😀                            | ... |
| 👨🏻     | <span class="text-green-500">4/5</span> |                           ❤️                            | ... |
| 👨🏾     |                    👎🏽                    | No rating → <span class="italic">Viewed 5 times</span> | ... |
| ...   |                   ...                   |                          ...                           | ... |


Note that since there was no kind of feedback from 👨🏾 regarding 🖥, a data scientist can try to fall-back to counting
the views of the product page. We can also write the following equation for a specific value in the Ratings Matrix:

$$ r_{👩🎧} = 👍 $$

However, it is quite chaotic to try and make sense of a lot of different metrics, let alone metrics that can span
different sets of values. Normally, one can constrain themselves to having a simple YES/NO metric (the thumbs-up or down
works!). 

Regarding collaborative filtering, the wikipedia page for [collaborative filtering](https://en.wikipedia.org/wiki/Collaborative_filtering) has a
fantastic gif that I just have to steal:

<div class="md:grid md:grid-cols-2">
  <div class="m-auto">
    <ul>
      <li>A graph is first produced from the feedback taken by the various user interactions.</li>
      <li>The graph is then transformed to a Ratings Matrix.</li>
      <li>From this Ratings Matrix, we can filter and keep the most similar users, and fill-in the gaps by comparison.
      </li>
    </ul>
  </div>
  <img class="m-auto" src="{{site.baseurl}}/assets/gif/Collaborative_filtering.gif">
</div>

Exploiting similarities using Machine Learning algorithms has led to very strong results in recommendation tasks, and it
is shown below how this can be implemented to systematize the production of a recommendation.

### Python's `surprise` module

A Python standard for scientific computation is the open-source [`scipy`](https://scipy.org/) module. Personally, I
realized this
is a go-to when looking up what is the recommended way to randomly sample from specific distributions, and easily get
results for special distribution functions, such as the inverse cumulative distribution function (iCDF), all of which
`scipy` covers in a very easy an intuitive out-of-the-box way.


<div class="md:grid md:grid-cols-2">
  <div class="">
    Scipy also serves as a basis module, a foundation for libraries aiming to cover more specialized use cases.
    One of the most popular frameworks uses the scipy backbone to provide essentials for Machine Learning. Of course,
    this is the infamous <a href="https://scikit-learn.org/stable/"><span
        class="font-semibold italic">scikit-learn</span></a> package. This module derives its name from
    the word "scikit", which is exactly what is used for modules building on top of scipy. Another is <a
      href="https://scikit-image.org/"><span class="font-semibold italic">scikit-image</span></a>, for
    computer vision and related processing.
  </div>
  <div class="bg-slate-200 sm:m-auto w-max p-10 xs:mx-auto xs:mt-4 rounded-full text-center">
    SciKit = SciPy Toolkit
  </div>
</div>

The main idea behind scikits is that, while focusing on a use case, they should be integrating well with other important
libraries in the Python
ecosystem, like numpy, pandas and matplotlib, and, of course, scipy! For the use case of building recommender systems,
it comes to no [`surprise`](https://surpriselib.com/) that there exists a "Simple Python RecommendatIon System Engine"
scikit! Quoting from its home page, it was
developed with the following in mind:

>- Give users perfect control over their experiments. To this end, a strong emphasis is laid on documentation, which we
have tried to make as clear and precise as possible by pointing out every detail of the algorithms.
>- Alleviate the pain of Dataset handling. Users can use both built-in datasets (Movielens, Jester), and their own
custom datasets.
>- Provide various ready-to-use prediction algorithms such as baseline algorithms, neighborhood methods, matrix
factorization-based ( SVD, PMF, SVD++, NMF), and many others. Also, various similarity measures (cosine, MSD, pearson…)
are built-in.
>- Make it easy to implement new algorithm ideas.
>- Provide tools to evaluate, analyse and compare the algorithms' performance. Cross-validation procedures can be run
very easily using powerful CV iterators (inspired by scikit-learn excellent tools), as well as exhaustive search over a
set of parameters.

#### Surprise's training data

For pedagogical purposes, it is in particular quite handy that `surprise` offers built-in datasets. We can try to look
into how a dataset for a recommendation engine looks like.

Loading a dataset has been made as simple as a single method call:

```Python
from surprise import Dataset
data = Dataset.load_builtin("ml-100k")
```

We have just loaded an `<class 'surprise.dataset.DatasetAutoFolds'>` object. If we call the `ratings_file` method we can
  see that there is an auxiliary internal file `u.data` containing the actual representation used behind this data file,
  looking
  something
  like `user; item ; rating ; timestamp`:
  ```None
  196 242 3 881250949
  86 302 3 891717742
  22 377 1 878887116
  ...
  ```

  You may ask, what is the source of this data? It is the
  [movielens](https://files.grouplens.org/datasets/movielens/ml-25m-README.html) dataset (specifically the [100k variant](https://grouplens.org/datasets/movielens/)), consisting of:

  >... 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 25000095
  ratings and 1093360 tag applications across 62423 movies...

  but here undersampled at roughly 0.4% to keep 100k rows of 943 users on 1682 movies. The original data contains
  several more files with more information on the users providing feedback, the details of the movies rated and more.

  The fact is that the `u.data` file, despite not being a grid, contains the available values of the user-item Ratings Matrix!

### An intuitive formulation

  It seems to all boil down to applying an estimation for the rating to put in the Ratings Matrix for a user-item pair. An intuitive way seems to construct the recommendation based on item-item similarity, meaning that we believe that, for example, a user will give a similar rating to two similar items. The formula for the prediction can be drafted to interpolate between the available ratings given by the user, and create a value for a new item (adapted from Yehuda Koren's work - see below):

  $$ \hat{r}_{ui} = \sum_{j \in S} w^u_{ij}r_{uj} $$

  where:

  - $\hat{r}_{ui}$ is the predicted recommendation for user $u$ and item $i$
  - $S$ is a set of items $i$ that are rated similarly by a user $u$
  - $w_{ij}$ are interpolation weights

As it's critical to estimate the similar items across our entire set of users and items, we employ a straight-forward measure of similarity, the [Pearson correlation coefficient](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient), and we can further adjust this with a regularization parameter, to only allow propagation of influences from items for which a lot of ratings exist. Thus, we can consider substituting the interpolation weights with the correlation coefficient.

Out of all items, though, we want to predict $\hat{r}_{ui}$ using those items that are most similar to the specific $i$. Thus, we also need a way to select this specific cluster of items, and a straightforward way to do so is using the [k-Nearest Neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) algorithm.

In the end, we can give the prediction $\hat{r}_{ui}$ as a weighted average of the user's ratings of the similar items, also introducing bias terms:

$$ \hat{r}_{ui} =  b_{ui} + \frac{\sum_{j \in S} \rho^u_{ij} \left(r_{uj} - b_{uj}\right)}{\sum_{j \in S} \rho^u_{ij}} $$

The bias parameter introduced is $b_{ui} = \mu + b_u + b_i$, characterizing our available dataset of user-items, by combining the average rating, the bias in the ratings given by a user $u$ (i.e. $b_{u}$) and the bias of a specific item $i$ (i.e. $b_{i}$). These can be computed by a simultaneous least squares fit from the available dataset.

Finally, a "shrinkage" $\lambda$ parameter is also used along with the correlation definition, to avoid values without many ratings to impact the correlation:

$$ \rho_{ij} \rightarrow \frac{n_{ij}}{n_{ij} + \lambda} \rho_{ij} $$

with $n_{ij}$ equal to the number of users who rated both $i$ and $j$ items.

### Implementation with `surprise`

  So how does `suprise` perform its job? In true scikit nature, it has built-in classes and methods to seamlessly handle
  the computation of correlations between the users and items needed for the application of collaborative filtering, providing the familiar `predict`, `fit` and `test` methods, as well as `train_test_split`!
  
  After a brief (and, admittedly, sparse) mathematical modeling, it is encouraging to see how effortless it is to put together all that we have considered, and we can try to evaluate the performance of our modeling, consisting of:

- baseline estimations
- Pearson similarity correlations
- a kNN item set

by computing the root mean squared error (RMSE) of the predicted ratings on a test set.

Using the `suprise` well-written docs, a sample code for the above can be constructed:

```Python
# imports
from surprise import Dataset, KNNBaseline
from surprise.model_selection import train_test_split
from surprise.accuracy import rmse

# fetch data
data = Dataset.load_builtin("ml-100k")

# split train test using surprise's namespace
trainset, testset = train_test_split(data, test_size=0.25)

# define the algorithm's bias and similarity estimattions
# baseline: use least squares with two regularization parameters
bsl_opts = {
    "method": "als", "n_epochs": 1, "reg_u": 10, "reg_i": 25
}

# similarity: item-item Pearson correlation with shrinkage
sim_opts = {
    "name": "pearson",
    "shrinkage": 100, # shrinkage
    "user_based": False,  # compute  similarities between items
}
# define the algorithm object, utilizing at most 20 neighbors
algo = KNNBaseline(k=20, min_k=1, sim_options=sim_opts, bsl_options=bsl_opts)

# train the algorithm on the trainset, and predict ratings for the testset
algo.fit(trainset)
predictions = algo.test(testset)

# then compute RMSE
loss = rmse(predictions)
```

The result is printed in the console:

```Python
Estimating biases using als...
Computing the pearson similarity matrix...
Done computing similarity matrix.
user: 145 item: 680 r_ui = 3.00 est = 2.96 {'actual_k': 20, 'was_impossible': False}
RMSE: 0.9626
```

Inspecting on of the prediction and the `u.item` file shows that the model believes user #145 would rate the (iconic, if you ask me)  1997 movie "Kull the Conqueror" with a score of 2.96, when in fact the true rating by the user was a 3.00! It is also shown that the algorithm considered 20 neighbors to predict on the specific item, as desired.

Of course, this is just scratching the surface, there's plenty more to see and even more coming, since recommender systems will continue to improve as they are a key ingredient to improving user experience.

<!-- https://surprise.readthedocs.io/en/stable/prediction_algorithms.html#similarity-measures-configuration -->
### Additional reading

  - "Factor in the Neighbors: Scalable and Accurate Collaborative Filtering", a [review](https://courses.ischool.berkeley.edu/i290-dm/s11/SECURE/a1-koren.pdf) by Yehuda Koren. Notably, it is seen early in the article that this blog post focuses on the so-called neighborhood model for recommendations!
  - "Recommender systems and their ethical challenges", an ethics-oriented [review](https://link.springer.com/content/pdf/10.1007/s00146-020-00950-y.pdf?pdf=button) by Silvia Milano, Mariarosaria Taddeo and Luciano Floridi.
  <!-- - The original proceedings [paper](https://proceedings.neurips.cc/paper/2007/file/d7322ed717dedf1eb4e6e52a37ea7bcd-Paper.pdf) by Ruslan Salakhutdinov and Andriy Mnih at NeurIPS 2007, describing Probabilistic Matrix Factorization in Recommender systems. -->
  <!-- - Data Academy [video](https://www.youtube.com/watch?v=4g8IVU9w3bg) of a course explaining the matrix factorization as related to recommender systems. -->

<!-- https://sifter.org/~simon/journal/20061211.html -->