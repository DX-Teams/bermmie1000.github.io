# Unsuperivsed Learning (비지도 학습)
[출처](http://www.mit.edu/~9.54/fall14/slides/Class13.pdf)
## Clustering (군집)
1. Introduction to clustering
1. K-means
1. Bag of words (dictionary learning)
1. Hierarchical clustering
1. Competitive learning (SOM)

### 1. Introduction to clustering
#### 군집화(Clustering)란?
- 레이블 되어있지 않은 데이터가 유사한 집단으로 나누어진 구성을 cluster라 함
- a cluster는 데이터끼리 _similar_ 한 것이며 다른 clusters와는 _dissimilar_ 데이터의 무리임

![clusters](..\\assets\\images\\clustering\\clusters.png)

#### Clustering을 위해 무엇이 필요한가?
1. Proximity measure (근접도 평가)
    - Similarity measure $s(x_i, x_k)$:
        - 유사도 평가
        - large if $x_i, x_k$ are similar
    - dissimilarity(or distance) measure $d(x_i, x_k)$:
        - 비유사도 평가
        - small if $x_i, x_k$ are similar
2. Criterion function (평가 함수)를 통한 clustering 평가

![goodbad](..\\assets\\images\\clustering\\goodbad.PNG)

3. Clustering 계산을 위한 알고리즘
- 예를 들어 평가 함수 최적화

#### Distance (dissimilarity) measures
_거리 (비유사도) 평가_
- __Euclidean distance__
    - ![euclide](..\\assets\\images\\clustering\\euclidean.PNG)
    - \[ d(x_i, x_j) = \sqrt{\sum_{k=1}^{d}(x_i^{(k)} - x_j^{(k)})^2} \]
    - translation invariant

- __Manhattan (city block) distance__
    - ![manhattan](..\\assets\\images\\clustering\\manhattan.PNG)
    - \[ d(x_i, x_j) = \sum_{k=1}^{d}|x_i^{(k)} - x_j^{(k)}| \]
    - approximation to Euclidean distance, cheaper to compute

#### Cluster evaluation
- __Inter-cluster cohesion__ (compactness):
    - Cohesion(응집력) measures how near the data points in a cluster are to the cluster centroid.
    - Sum of squared error (SSE) is a commonly used measure.
- __Inter-cluster separation__ (isolation):
    - Separation means that different cluster centroids should be far away from one another.
- In most applications, expert judgments are still the key

#### How man clusters?
![howmany](..\\assets\\images\\clustering\\howmany.PNG)

- Possible approaches
    1. fix the number of clusters to __k__
    1. find the best clustering according to the criterion function (number of clusters may vary)

#### Clustering techniques
![clusterings](..\\assets\\images\\clustering\\clusterings.PNG)

``` console
Clustering
│
├─ Hierarchical
│       ├─ Divisive
│       └─ Agglomerative
│
├─ Partitional
│       ├─ Centroid
│       ├─ Model Based
│       ├─ Graph Theoretic
│       └─ Spectral
│
└─ Bayesian
        ├─ Decision Based
        └─ Nonparametric
```

- __Hierarchical(계층적)__ algorithms:
    - 계층적 알고리즘은 이전에 설정된 클러스터를 사용하여 연속적인(successive) cluster를 찾습니다. 이러한 알고리즘은 응집(bottom-up) 되거나 분열(top-down) 될 수 있습니다.

- __Partitional(분할)__ algorithms:
    - 분할 알고리즘은 일반적으로 모든 클러스터를 한 번에 결정하지만 계층 적 클러스터링에서 분할 알고리즘으로 사용할 수도 있습니다.

- __Bayesian(베이지안)__ algorithms:
    - 베이지안 알고리즘은 데이터의 모든 파티션 모음에 대해 사후 분포를 생성하려고합니다.

### 2. K-Means clustering
![kmeans](..\\assets\\images\\clustering\\kmeans.PNG)

- K-means (MacQueen, 1967) is a parirional clustering algorithm
- Let the set of data points D be $\{\vec{x_1}, \vec{x_2}, ..., \vec{x_n}\}$,
    where $\vec{x_i}=(x_{i1}, x_{i2}, ..., x_{ir})$ is a vectoer in $X \subseteq R^{r} $ and $r$ is the number of dimensions.
- The K-means algorithm partitions the given data into $k$ clusters:
    - Each cluster has a cluster center, called centroid.
    - $k$ is specified by the user

#### K-means algorithm
- Given $k$, the _k-means_ algorithm works as follows:
    1. Choose $k$ (random) data points (seeds) to be the initial centroids, cluster centers
    1. Assign each data point to closest centroid
    1. Re-compute the centroids using the current cluster memberships
    1. If a convergence criterion is not met, repeat steps 2 and 3

#### K-means convergence (stopping) criterion
- no (or minimum) re-assignments of data points to different clusters, _or_
- no (or minimum) change of centroids, _or_
- minimum decrease in the __sum of squared error__ (SSE),
    - $ SSE = \sum_{j=1}^k \sum_{x\in C_j} d(\vec{x}, \vec{m_j})^2 $
    - $ C_j $ is the $j$th cluster,
    - $ \vec{m_j}$ is the centroid of cluster $C_j$ (the mean vector of all the data points in $C_j$),
    - $d(\vec{x}, \vec{m_j})$ is the (Eucledian) distance between data point $x$ and centroid $\vec{m_j}.$

#### K-means clustering example
##### step 1
![step1](..\\assets\\images\\clustering\\step1.PNG)
##### step 2
![step2](..\\assets\\images\\clustering\\step2.PNG)
##### step 3
![step3](..\\assets\\images\\clustering\\step3.PNG)
##### step 4
![step4](..\\assets\\images\\clustering\\step4.PNG)
##### step 5
![step5](..\\assets\\images\\clustering\\step5.PNG)
##### step 6
![step6](..\\assets\\images\\clustering\\step6.PNG)

#### Why use K-means?
- Strengths:
    - Simple: easy to understand and to implement
    - Efficient: Time complexity: $O(tkn)$,
        - where $n$ is the number of data points,
        - $k$ is the number of clusters, and
        - $t$ is the number of iterations.
    - Since both $k$ and $t$ are small, $k$-means is considered a linear algorithm.
- K-means is the most popular clustering algorithm.
- Note that:
    - it terminates at a local opimum if SSE is used.
    - The global optimum is hard to find due to complexity.

#### Weaknesses of K-means
- The algorithm is only applicable if the mean is defined.
    - Fro categorical data, $k$-mode - the centroid is represented by most frequent values.
- The user needs to specify k.
- The algorithm is sensitive to outliers
    - Outliers are data points that are very far away from other data points
    - Outliers could be errors in the data recording or some special data points with very different values.

#### Outliers
![outliers](..\\assets\\images\\clustering\\outliers.PNG)
##### Dealing with outliers
- Remove some data points that are much further away from the centroids than other data points
    - To be safe, we may want to monitor these possible outliers over a few iterations and then decide to remove them.
- Perform random sampling: by choosing a small subset of the data points, the chance of selecting an outlier is much smaller
    - Assign the rest of the data points to the clusters by distance or similarity comparison, or classification

#### Sensitivity to initial seeds

![seeds](..\\assets\\images\\clustering\\seeds.PNG)

#### Special data structures
- The $k$-means algorithm is not suitable for discovering clusters that are not hyper-ellipsoids (or hyper-spheres).

![specialDS](..\\assets\\images\\clustering\\specialDS.PNG)

#### K-means summary
- Despite weaknesses, $k$-means is still the most popular algorithm due to its simplicity and efficieny
- No clear evidence that any other clustering algorithm performs better in general
- Comparing different clustering algorithms is a difficult task. No one knows the correct clusters!