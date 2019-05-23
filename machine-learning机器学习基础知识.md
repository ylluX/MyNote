# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [基本概念](#基本概念)
   * [灵敏度/特异度](#灵敏度特异度)
   * [损失函数(Loss function)/代价函数(成本函数)(Cost function)](#损失函数loss-function代价函数成本函数cost-function)
   * [分类/回归](#分类回归)
   * [哑变量](#哑变量)
* [模型](#模型)
   * [Scikit-Learn中文文档](#scikit-learn中文文档)
   * [数据预处理(归一化)](#数据预处理归一化)
   * [数据标准化(Normalization)](#数据标准化normalization)
   * [不均衡数据集处理](#不均衡数据集处理)
   * [核密度函数](#核密度函数)
   * [PCA](#pca)
   * [逻辑回归](#逻辑回归)
   * [非线性回归](#非线性回归)
   * [梯度下降](#梯度下降)
   * [SVM](#svm)
   * [HMM](#hmm)
   * [贝叶斯](#贝叶斯)
   * [随机森林](#随机森林)
* [深度学习](#深度学习)
   * [TensorFlow](#tensorflow)
* [分布](#分布)
   * [泊松分布](#泊松分布)
* [学习资料](#学习资料)
   * [视频资料](#视频资料)
   * [深度学习](#深度学习)
<!--te-->

----

# 基本概念

## 灵敏度/特异度

[Sensitivity and specificity](https://en.wikipedia.org/wiki/Sensitivity_and_specificity)

* 真阳性率(true positive rate, TPR)，又称为灵敏度(sensitivity)，即有病诊断阳性的概率   TPR = TP/(TP+FN)
* 真阴性率(true negative rate)，又称为特异度(specificity, SPC), 即无病诊断阴性的概率   SPC = TN/(TN+FP)
* 假阳性率(false positive rate, FPR)，又称为"误诊率"   FPR = FP/(FP+TN) = 1 - SPC
* 假阴性率(false negative rate, FNR)，又称为"漏诊率"   FNR = FN/(TP+FN) = 1 - TPR
* 阳性预测值(positive predictive value, PPV), 即诊断为阳性中有病的概率    PPV = TP/(TP+FP)
* 隐性预测值(negative predictive value, NPV), 即诊断为阴性中无病的概率    NPV = TN/(TN+FN)
* 准确率(accuracy)  = (TP+TN) / (TP+TN+FP+FN)
* 精确率(precision): P = TP / (TP+FP)
* 召回率(recall): R = TP / (TP+FN)

灵敏度：实际有病的人正确判断为真阳性的比例

特异度：实际无病的人正确判断为真阴性的比例


## 损失函数(Loss function)/代价函数(成本函数)(Cost function)

损失函数(Loss function)是定义在单个训练样本上的，也就是就算一个样本的误差，比如我们想要分类，就是预测的类别和实际类别的区别，
是一个样本的哦，用**L**表示

代价函数(Cost function)是定义在整个训练集上面的，是所有样本的误差的总和的平均，也就是损失函数的总和的平均，用**J**表示，有没
有这个平均其实不会影响最后的参数的求解结果。


## 分类/回归

* [机器学习中的回归(regression)与分类(classification)问题](https://blog.csdn.net/wspba/article/details/61927105)
* [回归(regression)与分类(classification)的区别](https://blog.csdn.net/u011630575/article/details/58676160)

输入变量与输出变量均为连续变量的预测问题是回归问题。输出变量为有限个离散变量的预测问题成为分类问题。

分类模型和回归模型本质一样，分类模型是将回归模型的输出离散化。

如果从training角度来看，分类模型和回归模型的目标函数不同，分类常见的是 log loss(对数损失函数), hinge loss(铰链损失函数), 
而回归是 square loss(平方损失函数)。


## 哑变量

* [回归模型中的哑变量](https://blog.csdn.net/xiezhen_zheng/article/details/80598258)


----


# 模型

## Scikit-Learn中文文档

* [Scikit-Learn中文文档](http://sklearn.apachecn.org/#/docs/5)

**scikit-learn算法选择**

![原文](https://scikit-learn.org/stable/_static/ml_map.png)
![中文](https://img-blog.csdn.net/20170624105439491?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ3VhbmdfbWFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

**API**

***sklearn.base: 基类和通用函数***

基类

* `base.BaseEstimator`	Base class for all estimators in scikit-learn
* `base.BiclusterMixin`	Mixin class for all bicluster estimators in scikit-learn
* `base.ClassifierMixin`	Mixin class for all classifiers in scikit-learn.
* `base.ClusterMixin`	Mixin class for all cluster estimators in scikit-learn.
* `base.DensityMixin`	Mixin class for all density estimators in scikit-learn.
* `base.RegressorMixin`	Mixin class for all regression estimators in scikit-learn.
* `base.TransformerMixin`	Mixin class for all transformers in scikit-learn.

通用函数

* `base.clone(estimator[, safe])`	Constructs a new estimator with the same parameters.
* `base.is_classifier(estimator)`	Returns True if the given estimator is (probably) a classifier.
* `base.is_regressor(estimator)`	Returns True if the given estimator is (probably) a regressor.
* `config_context(**new_config)`	Context manager for global scikit-learn configuration
* `get_config()`	Retrieve current values for configuration set by set_config
* `set_config([assume_finite, working_memory])`	Set global scikit-learn configuration
* `show_versions()`	Print useful debugging information


***sklearn.calibration：概率校正***

* `calibration.CalibratedClassifierCV([…])`	Probability calibration with isotonic regression or sigmoid.
* `calibration.calibration_curve(y_true, y_prob)`	Compute true and predicted probabilities for a calibration curve.

***sklearn.cluster：聚类***

收集了常见的无监督聚类算法

类

* `cluster.AffinityPropagation([damping, …])`	Perform Affinity Propagation Clustering of data.
* `cluster.AgglomerativeClustering([…])`	Agglomerative Clustering
* `cluster.Birch([threshold, branching_factor, …])`	Implements the Birch clustering algorithm.
* `cluster.DBSCAN([eps, min_samples, metric, …])`	Perform DBSCAN clustering from vector array or distance matrix.
* `cluster.FeatureAgglomeration([n_clusters, …])`	Agglomerate features.
* `cluster.KMeans([n_clusters, init, n_init, …])`	K-Means clustering
* `cluster.MiniBatchKMeans([n_clusters, init, …])`	Mini-Batch K-Means clustering
* `cluster.MeanShift([bandwidth, seeds, …])`	Mean shift clustering using a flat kernel.
* `cluster.SpectralClustering([n_clusters, …])`	Apply clustering to a projection to the normalized laplacian.

函数

* `cluster.AffinityPropagation([damping, …])`	Perform Affinity Propagation Clustering of data.
* `cluster.AgglomerativeClustering([…])`	Agglomerative Clustering
* `cluster.Birch([threshold, branching_factor, …])`	Implements the Birch clustering algorithm.
* `cluster.DBSCAN([eps, min_samples, metric, …])`	Perform DBSCAN clustering from vector array or distance matrix.
* `cluster.FeatureAgglomeration([n_clusters, …])`	Agglomerate features.
* `cluster.KMeans([n_clusters, init, n_init, …])`	K-Means clustering
* `cluster.MiniBatchKMeans([n_clusters, init, …])`	Mini-Batch K-Means clustering
* `cluster.MeanShift([bandwidth, seeds, …])`	Mean shift clustering using a flat kernel.
* `cluster.SpectralClustering([n_clusters, …])`	Apply clustering to a projection to the normalized laplacian.


***sklearn.cluster.bicluster：双聚类***

* `SpectralBiclustering([n_clusters, method, …])`	Spectral biclustering (Kluger, 2003).
* `SpectralCoclustering([n_clusters, …])`	Spectral Co-Clustering algorithm (Dhillon, 2001).


***sklearn.compose：综合评估***

* `compose.ColumnTransformer(transformers[, …])`	Applies transformers to columns of an array or pandas DataFrame.
* `compose.TransformedTargetRegressor([…])`	Meta-estimator to regress on a transformed target.
* `compose.make_column_transformer(…)`	Construct a ColumnTransformer from the given transformers.


***sklearn.covariance：协方差评估***

* `covariance.EmpiricalCovariance([…])`	Maximum likelihood covariance estimator
* `covariance.EllipticEnvelope([…])`	An object for detecting outliers in a Gaussian distributed dataset.
* `covariance.GraphicalLasso([alpha, mode, …])`	Sparse inverse covariance estimation with an l1-penalized estimator.
* `covariance.GraphicalLassoCV([alphas, …])`	Sparse inverse covariance w/ cross-validated choice of the l1 penalty.
* `covariance.LedoitWolf([store_precision, …])`	LedoitWolf Estimator
* `covariance.MinCovDet([store_precision, …])`	Minimum Covariance Determinant (MCD): robust estimator of covariance.
* `covariance.OAS([store_precision, …])`	Oracle Approximating Shrinkage Estimator
* `covariance.ShrunkCovariance([…])`	Covariance estimator with shrinkage
* `covariance.empirical_covariance(X[, …])`	Computes the Maximum likelihood covariance estimator
* `covariance.graphical_lasso(emp_cov, alpha[, …])`	l1-penalized covariance estimator
* `covariance.ledoit_wolf(X[, assume_centered, …])`	Estimates the shrunk Ledoit-Wolf covariance matrix.
* `covariance.oas(X[, assume_centered])`	Estimate covariance with the Oracle Approximating Shrinkage algorithm.
* `covariance.shrunk_covariance(emp_cov[, …])`	Calculates a covariance matrix shrunk on the diagonal


***sklearn.cross_decomposition: 交叉分解***

* `cross_decomposition.CCA([n_components, …])`	CCA Canonical Correlation Analysis.
* `cross_decomposition.PLSCanonical([…])`	PLSCanonical implements the 2 blocks canonical PLS of the original Wold algorithm [Tenenhaus 1998] p.204, referred as PLS-C2A in [Wegelin 2000].
* `cross_decomposition.PLSRegression([…])`	PLS regression
* `cross_decomposition.PLSSVD([n_components, …])`	Partial Least Square SVD


***sklearn.datasets: 数据集***

导入器

* `datasets.clear_data_home([data_home])`	Delete all the content of the data home cache.
* `datasets.dump_svmlight_file(X, y, f[, …])`	Dump the dataset in svmlight / libsvm file format.
* `datasets.fetch_20newsgroups([data_home, …])`	Load the filenames and data from the 20 newsgroups dataset (classification).
* `datasets.fetch_20newsgroups_vectorized([…])`	Load the 20 newsgroups dataset and vectorize it into token counts (classification).
* `datasets.fetch_california_housing([…])`	Load the California housing dataset (regression).
* `datasets.fetch_covtype([data_home, …])`	Load the covertype dataset (classification).
* `datasets.fetch_kddcup99([subset, data_home, …])`	Load the kddcup99 dataset (classification).
* `datasets.fetch_lfw_pairs([subset, …])`	Load the Labeled Faces in the Wild (LFW) pairs dataset (classification).
* `datasets.fetch_lfw_people([data_home, …])`	Load the Labeled Faces in the Wild (LFW) people dataset (classification).
* `datasets.fetch_olivetti_faces([data_home, …])`	Load the Olivetti faces data-set from AT&T (classification).
* `datasets.fetch_openml([name, version, …])`	Fetch dataset from openml by name or dataset id.
* `datasets.fetch_rcv1([data_home, subset, …])`	Load the RCV1 multilabel dataset (classification).
* `datasets.fetch_species_distributions([…])`	Loader for species distribution dataset from Phillips et.
* `datasets.get_data_home([data_home])`	Return the path of the scikit-learn data dir.
* `datasets.load_boston([return_X_y])`	Load and return the boston house-prices dataset (regression).
* `datasets.load_breast_cancer([return_X_y])`	Load and return the breast cancer wisconsin dataset (classification).
* `datasets.load_diabetes([return_X_y])`	Load and return the diabetes dataset (regression).
* `datasets.load_digits([n_class, return_X_y])`	Load and return the digits dataset (classification).
* `datasets.load_files(container_path[, …])`	Load text files with categories as subfolder names.
* `datasets.load_iris([return_X_y])`	Load and return the iris dataset (classification).
* `datasets.load_linnerud([return_X_y])`	Load and return the linnerud dataset (multivariate regression).
* `datasets.load_sample_image(image_name)`	Load the numpy array of a single sample image
* `datasets.load_sample_images()`	Load sample images for image manipulation.
* `datasets.load_svmlight_file(f[, n_features, …])`	Load datasets in the svmlight / libsvm format into sparse CSR matrix
* `datasets.load_svmlight_files(files[, …])`	Load dataset from multiple files in SVMlight format
* `datasets.load_wine([return_X_y])`	Load and return the wine dataset (classification).
* `datasets.mldata_filename(dataname)`	DEPRECATED: mldata_filename was deprecated in version 0.20 and will be removed in version 0.22


样本产生器

* `datasets.clear_data_home([data_home])`	Delete all the content of the data home cache.
* `datasets.dump_svmlight_file(X, y, f[, …])`	Dump the dataset in svmlight / libsvm file format.
* `datasets.fetch_20newsgroups([data_home, …])`	Load the filenames and data from the 20 newsgroups dataset (classification).
* `datasets.fetch_20newsgroups_vectorized([…])`	Load the 20 newsgroups dataset and vectorize it into token counts (classification).
* `datasets.fetch_california_housing([…])`	Load the California housing dataset (regression).
* `datasets.fetch_covtype([data_home, …])`	Load the covertype dataset (classification).
* `datasets.fetch_kddcup99([subset, data_home, …])`	Load the kddcup99 dataset (classification).
* `datasets.fetch_lfw_pairs([subset, …])`	Load the Labeled Faces in the Wild (LFW) pairs dataset (classification).
* `datasets.fetch_lfw_people([data_home, …])`	Load the Labeled Faces in the Wild (LFW) people dataset (classification).
* `datasets.fetch_olivetti_faces([data_home, …])`	Load the Olivetti faces data-set from AT&T (classification).
* `datasets.fetch_openml([name, version, …])`	Fetch dataset from openml by name or dataset id.
* `datasets.fetch_rcv1([data_home, subset, …])`	Load the RCV1 multilabel dataset (classification).
* `datasets.fetch_species_distributions([…])`	Loader for species distribution dataset from Phillips et.
* `datasets.get_data_home([data_home])`	Return the path of the scikit-learn data dir.
* `datasets.load_boston([return_X_y])`	Load and return the boston house-prices dataset (regression).
* `datasets.load_breast_cancer([return_X_y])`	Load and return the breast cancer wisconsin dataset (classification).
* `datasets.load_diabetes([return_X_y])`	Load and return the diabetes dataset (regression).
* `datasets.load_digits([n_class, return_X_y])`	Load and return the digits dataset (classification).
* `datasets.load_files(container_path[, …])`	Load text files with categories as subfolder names.
* `datasets.load_iris([return_X_y])`	Load and return the iris dataset (classification).
* `datasets.load_linnerud([return_X_y])`	Load and return the linnerud dataset (multivariate regression).
* `datasets.load_sample_image(image_name)`	Load the numpy array of a single sample image
* `datasets.load_sample_images()`	Load sample images for image manipulation.
* `datasets.load_svmlight_file(f[, n_features, …])`	Load datasets in the svmlight / libsvm format into sparse CSR matrix
* `datasets.load_svmlight_files(files[, …])`	Load dataset from multiple files in SVMlight format
* `datasets.load_wine([return_X_y])`	Load and return the wine dataset (classification).
* `datasets.mldata_filename(dataname)`	DEPRECATED: mldata_filename was deprecated in version 0.20 and will be removed in version 0.22


***sklearn.decomposition: 矩阵分解***

* `decomposition.DictionaryLearning([…])`	Dictionary learning
* `decomposition.FactorAnalysis([n_components, …])`	Factor Analysis (FA)
* `decomposition.FastICA([n_components, …])`	FastICA: a fast algorithm for Independent Component Analysis.
* `decomposition.IncrementalPCA([n_components, …])`	Incremental principal components analysis (IPCA).
* `decomposition.KernelPCA([n_components, …])`	Kernel Principal component analysis (KPCA)
* `decomposition.LatentDirichletAllocation([…])`	Latent Dirichlet Allocation with online variational Bayes algorithm
* `decomposition.MiniBatchDictionaryLearning([…])`	Mini-batch dictionary learning
* `decomposition.MiniBatchSparsePCA([…])`	Mini-batch Sparse Principal Components Analysis
* `decomposition.NMF([n_components, init, …])`	Non-Negative Matrix Factorization (NMF)
* `decomposition.PCA([n_components, copy, …])`	Principal component analysis (PCA)
* `decomposition.SparsePCA([n_components, …])`	Sparse Principal Components Analysis (SparsePCA)
* `decomposition.SparseCoder(dictionary[, …])`	Sparse coding
* `decomposition.TruncatedSVD([n_components, …])`	Dimensionality reduction using truncated SVD (aka LSA).
* `decomposition.dict_learning(X, n_components, …)`	Solves a dictionary learning matrix factorization problem.
* `decomposition.dict_learning_online(X[, …])`	Solves a dictionary learning matrix factorization problem online.
* `decomposition.fastica(X[, n_components, …])`	Perform Fast Independent Component Analysis.
* `decomposition.sparse_encode(X, dictionary[, …])`	Sparse coding


***sklearn.discriminant_analysis: 判别分析***

* `discriminant_analysis.LinearDiscriminantAnalysis([…])`	Linear Discriminant Analysis
* `discriminant_analysis.QuadraticDiscriminantAnalysis([…])`	Quadratic Discriminant Analysis


***sklearn.dummy: 虚假估计***

***sklearn.ensemble:组合方法***

***sklearn.feature_extraction: 特征提取***

* `feature_extraction.DictVectorizer([dtype, …])`	Transforms lists of feature-value mappings to vectors.
* `feature_extraction.FeatureHasher([…])`	Implements feature hashing, aka the hashing trick.

从图片中

* `feature_extraction.image.extract_patches_2d(…)`	Reshape a 2D image into a collection of patches
* `feature_extraction.image.grid_to_graph(n_x, n_y)`	Graph of the pixel-to-pixel connections
* `feature_extraction.image.img_to_graph(img[, …])`	Graph of the pixel-to-pixel gradient connections
* `feature_extraction.image.reconstruct_from_patches_2d(…)`	Reconstruct the image from all of its patches.
* `feature_extraction.image.PatchExtractor([…])`	Extracts patches from a collection of images

从文本中

* `feature_extraction.text.CountVectorizer([…])`	Convert a collection of text documents to a matrix of token counts
* `feature_extraction.text.HashingVectorizer([…])`	Convert a collection of text documents to a matrix of token occurrences
* `feature_extraction.text.TfidfTransformer([…])`	Transform a count matrix to a normalized tf or tf-idf representation
* `feature_extraction.text.TfidfVectorizer([…])`	Convert a collection of raw documents to a matrix of TF-IDF features.


***sklearn.feature_selection: 特征选择***

* `feature_selection.GenericUnivariateSelect([…])`	Univariate feature selector with configurable strategy.
* `feature_selection.SelectPercentile([…])`	Select features according to a percentile of the highest scores.
* `feature_selection.SelectKBest([score_func, k])`	Select features according to the k highest scores.
* `feature_selection.SelectFpr([score_func, alpha])`	Filter: Select the pvalues below alpha based on a FPR test.
* `feature_selection.SelectFdr([score_func, alpha])`	Filter: Select the p-values for an estimated false discovery rate
* `feature_selection.SelectFromModel(estimator)`	Meta-transformer for selecting features based on importance weights.
* `feature_selection.SelectFwe([score_func, alpha])`	Filter: Select the p-values corresponding to Family-wise error rate
* `feature_selection.RFE(estimator[, …])`	Feature ranking with recursive feature elimination.
* `feature_selection.RFECV(estimator[, step, …])`	Feature ranking with recursive feature elimination and cross-validated selection of the best number of features.
* `feature_selection.VarianceThreshold([threshold])`	Feature selector that removes all low-variance features.
* `feature_selection.chi2(X, y)`	Compute chi-squared stats between each non-negative feature and class.
* `feature_selection.f_classif(X, y)`	Compute the ANOVA F-value for the provided sample.
* `feature_selection.f_regression(X, y[, center])`	Univariate linear regression tests.
* `feature_selection.mutual_info_classif(X, y)`	Estimate mutual information for a discrete target variable.
* `feature_selection.mutual_info_regression(X, y)`	Estimate mutual information for a continuous target variable.


***sklearn.gaussian_process: 高斯过程***

* `gaussian_process.GaussianProcessClassifier([…])`	Gaussian process classification (GPC) based on Laplace approximation.
* `gaussian_process.GaussianProcessRegressor([…])`	Gaussian process regression (GPR).

核：

* `gaussian_process.kernels.CompoundKernel(kernels)`	Kernel which is composed of a set of other kernels.
* `gaussian_process.kernels.ConstantKernel([…])`	Constant kernel.
* `gaussian_process.kernels.DotProduct([…])`	Dot-Product kernel.
* `gaussian_process.kernels.ExpSineSquared([…])`	Exp-Sine-Squared kernel.
* `gaussian_process.kernels.Exponentiation(…)`	Exponentiate kernel by given exponent.
* `gaussian_process.kernels.Hyperparameter`	A kernel hyperparameter’s specification in form of a namedtuple.
* `gaussian_process.kernels.Kernel`	Base class for all kernels.
* `gaussian_process.kernels.Matern([…])`	Matern kernel.
* `gaussian_process.kernels.PairwiseKernel([…])`	Wrapper for kernels in sklearn.metrics.pairwise.
* `gaussian_process.kernels.Product(k1, k2)`	Product-kernel k1 * k2 of two kernels k1 and k2.
* `gaussian_process.kernels.RBF([length_scale, …])`	Radial-basis function kernel (aka squared-exponential kernel).
* `gaussian_process.kernels.RationalQuadratic([…])`	Rational Quadratic kernel.
* `gaussian_process.kernels.Sum(k1, k2)`	Sum-kernel k1 + k2 of two kernels k1 and k2.
* `gaussian_process.kernels.WhiteKernel([…])`	White kernel.


***sklearn.isotonic:保序回归***

***sklearn.impute: Impute***

***sklearn.kernel_approximation：核近似***

实现了几种基于傅里叶变换的近似核特征映射。

* `kernel_approximation.AdditiveChi2Sampler([…])`	Approximate feature map for additive chi2 kernel.
* `kernel_approximation.Nystroem([kernel, …])`	Approximate a kernel map using a subset of the training data.
* `kernel_approximation.RBFSampler([gamma, …])`	Approximates feature map of an RBF kernel by Monte Carlo approximation of its Fourier transform.
* `kernel_approximation.SkewedChi2Sampler([…])`	Approximates feature map of the “skewed chi-squared” kernel by Monte Carlo approximation of its Fourier transform.


***sklearn.kernel_ridge：核岭回归***

* `kernel_ridge.KernelRidge([alpha, kernel, …])`	Kernel ridge regression.


***sklearn.linear_model：广义线性模型***

实现了广义线性模型。它包括岭回归、贝叶斯回归、Flasso估计和弹性网络估计。它还实现了随机梯度下降相关算法。

* `linear_model.ARDRegression([n_iter, tol, …])`	Bayesian ARD regression.
* `linear_model.BayesianRidge([n_iter, tol, …])`	Bayesian ridge regression
* `linear_model.ElasticNet([alpha, l1_ratio, …])`	Linear regression with combined L1 and L2 priors as regularizer.
* `linear_model.ElasticNetCV([l1_ratio, eps, …])`	Elastic Net model with iterative fitting along a regularization path.
* `linear_model.HuberRegressor([epsilon, …])`	Linear regression model that is robust to outliers.
* `linear_model.Lars([fit_intercept, verbose, …])`	Least Angle Regression model a.k.a.
* `linear_model.LarsCV([fit_intercept, …])`	Cross-validated Least Angle Regression model.
* `linear_model.Lasso([alpha, fit_intercept, …])`	Linear Model trained with L1 prior as regularizer (aka the Lasso)
* `linear_model.LassoCV([eps, n_alphas, …])`	Lasso linear model with iterative fitting along a regularization path.
* `linear_model.LassoLars([alpha, …])`	Lasso model fit with Least Angle Regression a.k.a.
* `linear_model.LassoLarsCV([fit_intercept, …])`	Cross-validated Lasso, using the LARS algorithm.
* `linear_model.LassoLarsIC([criterion, …])`	Lasso model fit with Lars using BIC or AIC for model selection
* `linear_model.LinearRegression([…])`	Ordinary least squares Linear Regression.
* `linear_model.LogisticRegression([penalty, …])`	Logistic Regression (aka logit, MaxEnt) classifier.
* `linear_model.LogisticRegressionCV([Cs, …])`	Logistic Regression CV (aka logit, MaxEnt) classifier.
* `linear_model.MultiTaskLasso([alpha, …])`	Multi-task Lasso model trained with L1/L2 mixed-norm as regularizer.
* `linear_model.MultiTaskElasticNet([alpha, …])`	Multi-task ElasticNet model trained with L1/L2 mixed-norm as regularizer
* `linear_model.MultiTaskLassoCV([eps, …])`	Multi-task Lasso model trained with L1/L2 mixed-norm as regularizer.
* `linear_model.MultiTaskElasticNetCV([…])`	Multi-task L1/L2 ElasticNet with built-in cross-validation.
* `linear_model.OrthogonalMatchingPursuit([…])`	Orthogonal Matching Pursuit model (OMP)
* `linear_model.OrthogonalMatchingPursuitCV([…])`	Cross-validated Orthogonal Matching Pursuit model (OMP).
* `linear_model.PassiveAggressiveClassifier([…])`	Passive Aggressive Classifier
* `linear_model.PassiveAggressiveRegressor([C, …])`	Passive Aggressive Regressor
* `linear_model.Perceptron([penalty, alpha, …])`	Read more in the User Guide.
* `linear_model.RANSACRegressor([…])`	RANSAC (RANdom SAmple Consensus) algorithm.
* `linear_model.Ridge([alpha, fit_intercept, …])`	Linear least squares with l2 regularization.
* `linear_model.RidgeClassifier([alpha, …])`	Classifier using Ridge regression.
* `linear_model.RidgeClassifierCV([alphas, …])`	Ridge classifier with built-in cross-validation.
* `linear_model.RidgeCV([alphas, …])`	Ridge regression with built-in cross-validation.
* `linear_model.SGDClassifier([loss, penalty, …])`	Linear classifiers (SVM, logistic regression, a.o.) with SGD training.
* `linear_model.SGDRegressor([loss, penalty, …])`	Linear model fitted by minimizing a regularized empirical loss with SGD
* `linear_model.TheilSenRegressor([…])`	Theil-Sen Estimator: robust multivariate regression model.
* `linear_model.enet_path(X, y[, l1_ratio, …])`	Compute elastic net path with coordinate descent
* `linear_model.lars_path(X, y[, Xy, Gram, …])`	Compute Least Angle Regression or Lasso path using LARS algorithm [1]
* `linear_model.lasso_path(X, y[, eps, …])`	Compute Lasso path with coordinate descent
* `linear_model.logistic_regression_path(X, y)`	Compute a Logistic Regression model for a list of regularization parameters.
* `linear_model.orthogonal_mp(X, y[, …])`	Orthogonal Matching Pursuit (OMP)
* `linear_model.orthogonal_mp_gram(Gram, Xy[, …])`	Gram Orthogonal Matching Pursuit (OMP)
* `linear_model.ridge_regression(X, y, alpha[, …])`	Solve the ridge equation by the method of normal equations.


***sklearn.manifold: Manifold Learning***


***sklearn.metrics:度量(模型评估)***

分类模型度量指标

* `metrics.accuracy_score(y_true, y_pred[, …])`	Accuracy classification score.
* `metrics.auc(x, y[, reorder])`	Compute Area Under the Curve (AUC) using the trapezoidal rule
* `metrics.average_precision_score(y_true, y_score)`	Compute average precision (AP) from prediction scores
* `metrics.balanced_accuracy_score(y_true, y_pred)`	Compute the balanced accuracy
* `metrics.brier_score_loss(y_true, y_prob[, …])`	Compute the Brier score.
* `metrics.classification_report(y_true, y_pred)`	Build a text report showing the main classification metrics
* `metrics.cohen_kappa_score(y1, y2[, labels, …])`	Cohen’s kappa: a statistic that measures inter-annotator agreement.
* `metrics.confusion_matrix(y_true, y_pred[, …])`	Compute confusion matrix to evaluate the accuracy of a classification
* `metrics.f1_score(y_true, y_pred[, labels, …])`	Compute the F1 score, also known as balanced F-score or F-measure
* `metrics.fbeta_score(y_true, y_pred, beta[, …])`	Compute the F-beta score
* `metrics.hamming_loss(y_true, y_pred[, …])`	Compute the average Hamming loss.
* `metrics.hinge_loss(y_true, pred_decision[, …])`	Average hinge loss (non-regularized)
* `metrics.jaccard_similarity_score(y_true, y_pred)`	Jaccard similarity coefficient score
* `metrics.log_loss(y_true, y_pred[, eps, …])`	Log loss, aka logistic loss or cross-entropy loss.
* `metrics.matthews_corrcoef(y_true, y_pred[, …])`	Compute the Matthews correlation coefficient (MCC)
* `metrics.precision_recall_curve(y_true, …)`	Compute precision-recall pairs for different probability thresholds
* `metrics.precision_recall_fscore_support(…)`	Compute precision, recall, F-measure and support for each class
* `metrics.precision_score(y_true, y_pred[, …])`	Compute the precision
* `metrics.recall_score(y_true, y_pred[, …])`	Compute the recall
* `metrics.roc_auc_score(y_true, y_score[, …])`	Compute Area Under the Receiver Operating Characteristic Curve (ROC AUC) from prediction scores.
* `metrics.roc_curve(y_true, y_score[, …])`	Compute Receiver operating characteristic (ROC)
* `metrics.zero_one_loss(y_true, y_pred[, …])`	Zero-one classification loss.

回归模型度量指标

* `metrics.explained_variance_score(y_true, y_pred)`	Explained variance regression score function
* `metrics.mean_absolute_error(y_true, y_pred)`	Mean absolute error regression loss
* `metrics.mean_squared_error(y_true, y_pred[, …])`	Mean squared error regression loss
* `metrics.mean_squared_log_error(y_true, y_pred)`	Mean squared logarithmic error regression loss
* `metrics.median_absolute_error(y_true, y_pred)`	Median absolute error regression loss
* `metrics.r2_score(y_true, y_pred[, …])`	R^2 (coefficient of determination) regression score function.

多标签秩度量指标

* `metrics.coverage_error(y_true, y_score[, …])`	Coverage error measure
* `metrics.label_ranking_average_precision_score(…)`	Compute ranking-based average precision
* `metrics.label_ranking_loss(y_true, y_score)`	Compute Ranking loss measure

聚类度量指标

* `metrics.adjusted_mutual_info_score(…[, …])`	Adjusted Mutual Information between two clusterings.
* `metrics.adjusted_rand_score(labels_true, …)`	Rand index adjusted for chance.
* `metrics.calinski_harabaz_score(X, labels)`	Compute the Calinski and Harabaz score.
* `metrics.davies_bouldin_score(X, labels)`	Computes the Davies-Bouldin score.
* `metrics.completeness_score(labels_true, …)`	Completeness metric of a cluster labeling given a ground truth.
* `metrics.cluster.contingency_matrix(…[, …])`	Build a contingency matrix describing the relationship between labels.
* `metrics.fowlkes_mallows_score(labels_true, …)`	Measure the similarity of two clusterings of a set of points.
* `metrics.homogeneity_completeness_v_measure(…)`	Compute the homogeneity and completeness and V-Measure scores at once.
* `metrics.homogeneity_score(labels_true, …)`	Homogeneity metric of a cluster labeling given a ground truth.
* `metrics.mutual_info_score(labels_true, …)`	Mutual Information between two clusterings.
* `metrics.normalized_mutual_info_score(…[, …])`	Normalized Mutual Information between two clusterings.
* `metrics.silhouette_score(X, labels[, …])`	Compute the mean Silhouette Coefficient of all samples.
* `metrics.silhouette_samples(X, labels[, metric])`	Compute the Silhouette Coefficient for each sample.
* `metrics.v_measure_score(labels_true, labels_pred)`	V-measure cluster labeling given a ground truth.

双度量指标

* `metrics.pairwise.additive_chi2_kernel(X[, Y])`	Computes the additive chi-squared kernel between observations in X and Y
* `metrics.pairwise.chi2_kernel(X[, Y, gamma])`	Computes the exponential chi-squared kernel X and Y.
* `metrics.pairwise.cosine_similarity(X[, Y, …])`	Compute cosine similarity between samples in X and Y.
* `metrics.pairwise.cosine_distances(X[, Y])`	Compute cosine distance between samples in X and Y.
* `metrics.pairwise.distance_metrics()`	Valid metrics for pairwise_distances.
* `metrics.pairwise.euclidean_distances(X[, Y, …])`	Considering the rows of X (and Y=X) as vectors, compute the distance matrix between each pair of vectors.
* `metrics.pairwise.kernel_metrics()`	Valid metrics for pairwise_kernels
* `metrics.pairwise.laplacian_kernel(X[, Y, gamma])`	Compute the laplacian kernel between X and Y.
* `metrics.pairwise.linear_kernel(X[, Y, …])`	Compute the linear kernel between X and Y.
* `metrics.pairwise.manhattan_distances(X[, Y, …])`	Compute the L1 distances between the vectors in X and Y.
* `metrics.pairwise.pairwise_kernels(X[, Y, …])`	Compute the kernel between arrays X and optional array Y.
* `metrics.pairwise.polynomial_kernel(X[, Y, …])`	Compute the polynomial kernel between X and Y:
* `metrics.pairwise.rbf_kernel(X[, Y, gamma])`	Compute the rbf (gaussian) kernel between X and Y:
* `metrics.pairwise.sigmoid_kernel(X[, Y, …])`	Compute the sigmoid kernel between X and Y:
* `metrics.pairwise.paired_euclidean_distances(X, Y)`	Computes the paired euclidean distances between X and Y
* `metrics.pairwise.paired_manhattan_distances(X, Y)`	Compute the L1 distances between the vectors in X and Y.
* `metrics.pairwise.paired_cosine_distances(X, Y)`	Computes the paired cosine distances between X and Y
* `metrics.pairwise.paired_distances(X, Y[, metric])`	Computes the paired distances between X and Y.
* `metrics.pairwise_distances(X[, Y, metric, …])`	Compute the distance matrix from a vector array X and optional Y.
* `metrics.pairwise_distances_argmin(X, Y[, …])`	Compute minimum distances between one point and a set of points.
* `metrics.pairwise_distances_argmin_min(X, Y)`	Compute minimum distances between one point and a set of points.
* `metrics.pairwise_distances_chunked(X[, Y, …])`	Generate a distance matrix chunk by chunk with optional reduction


***sklearn.mixture: 高斯混合模型***

* `mixture.BayesianGaussianMixture([…])`	Variational Bayesian estimation of a Gaussian mixture.
* `mixture.GaussianMixture([n_components, …])`	Gaussian Mixture.

***sklearn.model_selection:模型选择***

参见交叉验证，调整模型超参数，学习曲线

分束器类

* `model_selection.GroupKFold([n_splits])`	K-fold iterator variant with non-overlapping groups.
* `model_selection.GroupShuffleSplit([…])`	Shuffle-Group(s)-Out cross-validation iterator
* `model_selection.KFold([n_splits, shuffle, …])`	K-Folds cross-validator
* `model_selection.LeaveOneGroupOut()`	Leave One Group Out cross-validator
* `model_selection.LeavePGroupsOut(n_groups)`	Leave P Group(s) Out cross-validator
* `model_selection.LeaveOneOut()`	Leave-One-Out cross-validator
* `model_selection.LeavePOut(p)`	Leave-P-Out cross-validator
* `model_selection.PredefinedSplit(test_fold)`	Predefined split cross-validator
* `model_selection.RepeatedKFold([n_splits, …])`	Repeated K-Fold cross validator.
* `model_selection.RepeatedStratifiedKFold([…])`	Repeated Stratified K-Fold cross validator.
* `model_selection.ShuffleSplit([n_splits, …])`	Random permutation cross-validator
* `model_selection.StratifiedKFold([n_splits, …])`	Stratified K-Folds cross-validator
* `model_selection.StratifiedShuffleSplit([…])`	Stratified ShuffleSplit cross-validator
* `model_selection.TimeSeriesSplit([n_splits, …])`	Time Series cross-validator

分束器函数

* `model_selection.check_cv([cv, y, classifier])`	Input checker utility for building a cross-validator
* `model_selection.train_test_split(*arrays, …)`	Split arrays or matrices into random train and test subsets

超参优化

* `model_selection.GridSearchCV(estimator, …)`	Exhaustive search over specified parameter values for an estimator.
* `model_selection.ParameterGrid(param_grid)`	Grid of parameters with a discrete number of values for each.
* `model_selection.ParameterSampler(…[, …])`	Generator on parameters sampled from given distributions.
* `model_selection.RandomizedSearchCV(…[, …])`	Randomized search on hyper parameters.
* `model_selection.fit_grid_point(X, y, …[, …])`	Run fit on one set of parameters.

模型验证

* `model_selection.cross_validate(estimator, X)`	Evaluate metric(s) by cross-validation and also record fit/score times.
* `model_selection.cross_val_predict(estimator, X)`	Generate cross-validated estimates for each input data point
* `model_selection.cross_val_score(estimator, X)`	Evaluate a score by cross-validation
* `model_selection.learning_curve(estimator, X, y)`	Learning curve.
* `model_selection.permutation_test_score(…)`	Evaluate the significance of a cross-validated score with permutations
* `model_selection.validation_curve(estimator, …)`	Validation curve.


***sklearn.multiclass: 多类多标签分类***

* `multiclass.OneVsRestClassifier(estimator[, …])`	One-vs-the-rest (OvR) multiclass/multilabel strategy
* `multiclass.OneVsOneClassifier(estimator[, …])`	One-vs-one multiclass strategy
* `multiclass.OutputCodeClassifier(estimator[, …])`	(Error-Correcting) Output-Code multiclass strategy


***sklearn.multioutput: 多输出回归和分类***

* `multioutput.ClassifierChain(base_estimator)`	A multi-label model that arranges binary classifiers into a chain.
* `multioutput.MultiOutputRegressor(estimator)`	Multi target regression
* `multioutput.MultiOutputClassifier(estimator)`	Multi target classification
* `multioutput.RegressorChain(base_estimator[, …])`	A multi-label model that arranges regressions into a chain.


***sklearn.naive_bayes: 朴素贝叶斯***

* `naive_bayes.BernoulliNB([alpha, binarize, …])`	Naive Bayes classifier for multivariate Bernoulli models.
* `naive_bayes.GaussianNB([priors, var_smoothing])`	Gaussian Naive Bayes (GaussianNB)
* `naive_bayes.MultinomialNB([alpha, …])`	Naive Bayes classifier for multinomial models
* `naive_bayes.ComplementNB([alpha, fit_prior, …])`	The Complement Naive Bayes classifier described in Rennie et al.


***sklearn.neighbors：近邻法***

* `neighbors.BallTree`	BallTree for fast generalized N-point problems
* `neighbors.DistanceMetric`	DistanceMetric class
* `neighbors.KDTree`	KDTree for fast generalized N-point problems
* `neighbors.KernelDensity([bandwidth, …])`	Kernel Density Estimation
* `neighbors.KNeighborsClassifier([…])`	Classifier implementing the k-nearest neighbors vote.
* `neighbors.KNeighborsRegressor([n_neighbors, …])`	Regression based on k-nearest neighbors.
* `neighbors.LocalOutlierFactor([n_neighbors, …])`	Unsupervised Outlier Detection using Local Outlier Factor (LOF)
* `neighbors.RadiusNeighborsClassifier([…])`	Classifier implementing a vote among neighbors within a given radius
* `neighbors.RadiusNeighborsRegressor([radius, …])`	Regression based on neighbors within a fixed radius.
* `neighbors.NearestCentroid([metric, …])`	Nearest centroid classifier.
* `neighbors.NearestNeighbors([n_neighbors, …])`	Unsupervised learner for implementing neighbor searches.
* `neighbors.kneighbors_graph(X, n_neighbors[, …])`	Computes the (weighted) graph of k-Neighbors for points in X
* `neighbors.radius_neighbors_graph(X, radius)`	Computes the (weighted) graph of Neighbors for points in X


***sklearn.neural_network: 神经网络模型***

* `neural_network.BernoulliRBM([n_components, …])`	Bernoulli Restricted Boltzmann Machine (RBM).
* `neural_network.MLPClassifier([…])`	Multi-layer Perceptron classifier.
* `neural_network.MLPRegressor([…])`	Multi-layer Perceptron regressor.


***sklearn.preprocessing: 预处理和标准化***

* `preprocessing.Binarizer([threshold, copy])`	Binarize data (set feature values to 0 or 1) according to a threshold
* `preprocessing.FunctionTransformer([func, …])`	Constructs a transformer from an arbitrary callable.
* `preprocessing.KBinsDiscretizer([n_bins, …])`	Bin continuous data into intervals.
* `preprocessing.KernelCenterer()`	Center a kernel matrix
* `preprocessing.LabelBinarizer([neg_label, …])`	Binarize labels in a one-vs-all fashion
* `preprocessing.LabelEncoder`	Encode labels with value between 0 and n_classes-1.
* `preprocessing.MultiLabelBinarizer([classes, …])`	Transform between iterable of iterables and a multilabel format
* `preprocessing.MaxAbsScaler([copy])`	Scale each feature by its maximum absolute value.
* `preprocessing.MinMaxScaler([feature_range, copy])`	Transforms features by scaling each feature to a given range.
* `preprocessing.Normalizer([norm, copy])`	Normalize samples individually to unit norm.
* `preprocessing.OneHotEncoder([n_values, …])`	Encode categorical integer features as a one-hot numeric array.
* `preprocessing.OrdinalEncoder([categories, dtype])`	Encode categorical features as an integer array.
* `preprocessing.PolynomialFeatures([degree, …])`	Generate polynomial and interaction features.
* `preprocessing.PowerTransformer([method, …])`	Apply a power transform featurewise to make data more Gaussian-like.
* `preprocessing.QuantileTransformer([…])`	Transform features using quantiles information.
* `preprocessing.RobustScaler([with_centering, …])`	Scale features using statistics that are robust to outliers.
* `preprocessing.StandardScaler([copy, …])`	Standardize features by removing the mean and scaling to unit variance
* `preprocessing.add_dummy_feature(X[, value])`	Augment dataset with an additional dummy feature.
* `preprocessing.binarize(X[, threshold, copy])`	Boolean thresholding of array-like or scipy.sparse matrix
* `preprocessing.label_binarize(y, classes[, …])`	Binarize labels in a one-vs-all fashion
* `preprocessing.maxabs_scale(X[, axis, copy])`	Scale each feature to the [-1, 1] range without breaking the sparsity.
* `preprocessing.minmax_scale(X[, …])`	Transforms features by scaling each feature to a given range.
* `preprocessing.normalize(X[, norm, axis, …])`	Scale input vectors individually to unit norm (vector length).
* `preprocessing.quantile_transform(X[, axis, …])`	Transform features using quantiles information.
* `preprocessing.robust_scale(X[, axis, …])`	Standardize a dataset along any axis
* `preprocessing.scale(X[, axis, with_mean, …])`	Standardize a dataset along any axis
* `preprocessing.power_transform(X[, method, …])`	Power transforms are a family of parametric, monotonic transformations that are applied to make data more Gaussian-like.


***sklearn.semi_supervised：半监督学习***

* `semi_supervised.LabelPropagation([kernel, …])`	Label Propagation classifier
* `semi_supervised.LabelSpreading([kernel, …])`	LabelSpreading model for semi-supervised learning


***sklearn.svm: 支持向量机***

评估器

* `svm.LinearSVC([penalty, loss, dual, tol, C, …])`	Linear Support Vector Classification.
* `svm.LinearSVR([epsilon, tol, C, loss, …])`	Linear Support Vector Regression.
* `svm.NuSVC([nu, kernel, degree, gamma, …])`	Nu-Support Vector Classification.
* `svm.NuSVR([nu, C, kernel, degree, gamma, …])`	Nu Support Vector Regression.
* `svm.OneClassSVM([kernel, degree, gamma, …])`	Unsupervised Outlier Detection.
* `svm.SVC([C, kernel, degree, gamma, coef0, …])`	C-Support Vector Classification.
* `svm.SVR([kernel, degree, gamma, coef0, tol, …])`	Epsilon-Support Vector Regression.
* `svm.l1_min_c(X, y[, loss, fit_intercept, …])`	Return the lowest bound for C such that for C in (l1_min_C, infinity) the model is guaranteed not to be empty.

低级方法

* `svm.libsvm.cross_validation`	Binding of the cross-validation routine (low-level routine)
* `svm.libsvm.decision_function`	Predict margin (libsvm name for this is predict_values)
* `svm.libsvm.fit`	Train the model using libsvm (low-level method)
* `svm.libsvm.predict`	Predict target values of X given a model (low-level method)
* `svm.libsvm.predict_proba`	Predict probabilities


***sklearn.tree: 决策树***

* `tree.DecisionTreeClassifier([criterion, …])`	A decision tree classifier.
* `tree.DecisionTreeRegressor([criterion, …])`	A decision tree regressor.
* `tree.ExtraTreeClassifier([criterion, …])`	An extremely randomized tree classifier.
* `tree.ExtraTreeRegressor([criterion, …])`	An extremely randomized tree regressor.
* `tree.export_graphviz(decision_tree[, …])`	Export a decision tree in DOT format.


***sklearn.utils: 通用程序***


* `utils.testing.mock_mldata_urlopen(*args, …)`	Object that mocks the urlopen function to fake requests to mldata.
* `utils.arrayfuncs.cholesky_delete`	
* `utils.arrayfuncs.min_pos`	Find the minimum value of an array over positive values
* `utils.as_float_array(X[, copy, force_all_finite])`	Converts an array-like to an array of floats.
* `utils.assert_all_finite(X[, allow_nan])`	Throw a ValueError if X contains NaN or infinity.
* `utils.bench.total_seconds(delta)`	helper function to emulate function total_seconds,
* `utils.check_X_y(X, y[, accept_sparse, …])`	Input validation for standard estimators.
* `utils.check_array(array[, accept_sparse, …])`	Input validation on an array, list, sparse matrix or similar.
* `utils.check_consistent_length(*arrays)`	Check that all arrays have consistent first dimensions.
* `utils.check_random_state(seed)`	Turn seed into a np.random.RandomState instance
* `utils.class_weight.compute_class_weight(…)`	Estimate class weights for unbalanced datasets.
* `utils.class_weight.compute_sample_weight(…)`	Estimate sample weights by class for unbalanced datasets.
* `utils.deprecated([extra])`	Decorator to mark a function or class as deprecated.
* `utils.estimator_checks.check_estimator(Estimator)`	Check if estimator adheres to scikit-learn conventions.
* `utils.extmath.safe_sparse_dot(a, b[, …])`	Dot product that handle the sparse matrix case correctly
* `utils.extmath.randomized_range_finder(A, …)`	Computes an orthonormal matrix whose range approximates the range of A.
* `utils.extmath.randomized_svd(M, n_components)`	Computes a truncated randomized SVD
* `utils.extmath.fast_logdet(A)`	Compute log(det(A)) for A symmetric
* `utils.extmath.density(w, **kwargs)`	Compute density of a sparse vector
* `utils.extmath.weighted_mode(a, w[, axis])`	Returns an array of the weighted modal (most common) value in a
* `utils.gen_even_slices(n, n_packs[, n_samples])`	Generator to create n_packs slices going up to n.
* `utils.graph.single_source_shortest_path_length(…)`	Return the shortest path length from source to all reachable nodes.
* `utils.graph_shortest_path.graph_shortest_path`	Perform a shortest-path graph search on a positive directed or undirected graph.
* `utils.indexable(*iterables)`	Make arrays indexable for cross-validation.
* `utils.multiclass.type_of_target(y)`	Determine the type of data indicated by the target.
* `utils.multiclass.is_multilabel(y)`	Check if y is in a multilabel format.
* `utils.multiclass.unique_labels(*ys)`	Extract an ordered array of unique labels
* `utils.murmurhash3_32`	Compute the 32bit murmurhash3 of key at seed.
* `utils.resample(*arrays, **options)`	Resample arrays or sparse matrices in a consistent way
* `utils.safe_indexing(X, indices)`	Return items or rows from X using indices.
* `utils.safe_mask(X, mask)`	Return a mask which is safe to use on X.
* `utils.safe_sqr(X[, copy])`	Element wise squaring of array-likes and sparse matrices.
* `utils.shuffle(*arrays, **options)`	Shuffle arrays or sparse matrices in a consistent way
* `utils.sparsefuncs.incr_mean_variance_axis(X, …)`	Compute incremental mean and variance along an axix on a CSR or CSC matrix.
* `utils.sparsefuncs.inplace_column_scale(X, scale)`	Inplace column scaling of a CSC/CSR matrix.
* `utils.sparsefuncs.inplace_row_scale(X, scale)`	Inplace row scaling of a CSR or CSC matrix.
* `utils.sparsefuncs.inplace_swap_row(X, m, n)`	Swaps two rows of a CSC/CSR matrix in-place.
* `utils.sparsefuncs.inplace_swap_column(X, m, n)`	Swaps two columns of a CSC/CSR matrix in-place.
* `utils.sparsefuncs.mean_variance_axis(X, axis)`	Compute mean and variance along an axix on a CSR or CSC matrix
* `utils.sparsefuncs.inplace_csr_column_scale(X, …)`	Inplace column scaling of a CSR matrix.
* `utils.sparsefuncs_fast.inplace_csr_row_normalize_l1`	Inplace row normalize using the l1 norm
* `utils.sparsefuncs_fast.inplace_csr_row_normalize_l2`	Inplace row normalize using the l2 norm
* `utils.random.sample_without_replacement`	Sample integers without replacement.
* `utils.validation.check_is_fitted(estimator, …)`	Perform is_fitted validation for estimator.
* `utils.validation.check_memory(memory)`	Check that memory is joblib.Memory-like.
* `utils.validation.check_symmetric(array[, …])`	Make sure that array is 2D, square and symmetric.
* `utils.validation.column_or_1d(y[, warn])`	Ravel column or 1d numpy array, else raises an error
* `utils.validation.has_fit_parameter(…)`	Checks whether the estimator’s fit method supports the given parameter.
* `utils.testing.assert_in`	Just like self.assertTrue(a in b), but with a nicer default message.
* `utils.testing.assert_not_in`	Just like self.assertTrue(a not in b), but with a nicer default message.
* `utils.testing.assert_raise_message(…)`	Helper function to test the message raised in an exception.
* `utils.testing.all_estimators([…])`	Get a list of all estimators from sklearn.




## 数据预处理(归一化)

* [处理离散型特征和连续型特征共存的情况 归一化 论述了对离散特征进行one-hot编码的意义](https://blog.csdn.net/lujiandong1/article/details/49448051)
* [利用python对包含离散型特征和连续型特征的数据进行预处理](https://blog.csdn.net/wotui1842/article/details/80697444)

拿到获取的原始特征，必须对每一特征分别进行归一化，比如，特征A的取值范围是[-1000,1000]，
特征B的取值范围是[-1,1].如果使用logistic回归，w1*x1+w2*x2，因为x1的取值太大了，所以x2
基本起不了作用。所以，必须进行特征的归一化，每个特征都单独进行归一化。

**连续型特征归一化的常用方法**

1. 线性放缩到[-1,1]
2. 线性放缩到[-1,1]

**离散型特征的处理方法**

离散型特征就是该特征对应的值不能进行大小比较，比如：职业，性别，国家等等

对于离散的特征基本就是按照one-hot编码，该离散特征有多少取值，就用多少维来表示该特征。
为什么使用one-hot编码来处理离散型特征，这是有理由的，不是随便拍脑袋想出来的！！！具体原因，
分下面几点来阐述： 

1. 使用one-hot编码，将离散特征的取值扩展到了欧式空间，离散特征的某个取值就对应欧式空间的某个点。
2. 将离散特征通过one-hot编码映射到欧式空间，是因为，在回归，分类，聚类等机器学习算法中，
特征之间距离的计算或相似度的计算是非常重要的，而我们常用的距离或相似度的计算都是在欧式
空间的相似度计算，计算余弦相似性，基于的就是欧式空间。
3. 离散型特征使用one-hot编码，确实会让特征之间的距离计算更加合理。比如，有一个离散型特征，
代表工作类型，该离散型特征，共有三个取值，不使用one-hot编码，其表示分别是x_1 = (1), 
x_2 = (2), x_3 = (3)。两个工作之间的距离是，(x_1, x_2) = 1, d(x_2, x_3) = 1, d(x_1, x_3) = 2。
那么x_1和x_3工作之间就越不相似吗？显然这样的表示，计算出来的特征的距离是不合理。那如果使用
one-hot编码，则得到x_1 = (1, 0, 0), x_2 = (0, 1, 0), x_3 = (0, 0, 1)，那么两个工作之间的距
离就都是sqrt(2).即每两个工作之间的距离是一样的，显得更合理
4. 将离散型特征进行one-hot编码的作用，是为了让距离计算更合理，但如果特征是离散的，并且不用
one-hot编码就可以很合理的计算出距离，那么就没必要进行one-hot编码，比如，该离散特征共有1000
个取值，我们分成两组，分别是400和600,两个小组之间的距离有合适的定义，组内的距离也有合适的定
义，那就没必要用one-hot 编码
 
离散特征进行one-hot编码后，编码后的特征，其实每一维度的特征都可以看做是连续的特征。就可以跟对
连续型特征的归一化方法一样，对每一维特征进行归一化。比如归一化到[-1,1]或归一化到均值为0,方差为1

基于树的方法是不需要进行特征的归一化，例如随机森林，bagging 和 boosting等。基于参数的模型或基
于距离的模型，都是要进行特征的归一化。


## 数据标准化(Normalization)

* [Quantile Normalization](https://en.wikipedia.org/wiki/Quantile_normalization)
* [quantile normalization on pandas dataframe](https://stackoverflow.com/questions/37935920/quantile-normalization-on-pandas-dataframe)


## 不均衡数据集处理

* [不平衡数据集下的SVM算法研究](https://blog.csdn.net/u011414200/article/details/47310795)
* [数据不均衡问题的解决](https://blog.csdn.net/sunflower_sara/article/details/81055033)
* [SVM训练时候样本不均衡怎么设置惩罚项](https://blog.csdn.net/qq_22625309/article/details/76256381?locationNum=8&fps=1)

从技术角度上说，任何在不同类之间展现出不等分布的样本集都应该被认为是不均衡的，并且应该展现出
明显的不平衡特征。具体来说，这种不均衡形式被称为类间不均衡，常见的多数类与少数类比例是100:1，
1000:1，10000:1

有时对少数类错分情况的后果很严重，比如癌症患者被误诊为健康人。所以需要的分类器应该是在不严重
损失多数类精度的情况下，在少数类上获得尽可能高的精度

同时也暗示着使用单一的评价准则，例如全局精度或是误差率，是不能给不均衡问题提供足够的评价信息。
因此利用含有更多信息的评价指标，例如接收机特性曲线、精度-recall曲线和代价曲线

样本不均衡的程度不是阻碍分类学习的唯一因素，样本集的复杂度也是导致分类性能恶化的重要因素，
另外相对不平衡比例的增大也可能使分类性能进一步恶化 。其中样本集复杂度是广义的术语，它包括重叠、
缺少代表性样本、类别间分离程度小等

```
在sklearn的SVC中，可用通过class_weight参数来处理不均衡数据集，该参数的值为字典类型或者
'balanced'字符串，默认为None.

每个类别分别设置不同的惩罚参数C，如果没有给，则会给所有类别都给C=1，即前面参数指出的参数C.
如果给定参数'balanced'，则使用y的值自动调整与输入数据中的类频率成反比的权重。
```


在statsmodels.api.Logit中没有weight参数，我们可以使用采样技术进行解决：

* [从重采样到数据合成：如何处理机器学习中的不平衡分类问题？](https://blog.csdn.net/xiaokang06/article/details/76546418)
* [Over-sampling(过采样) - imblearn](https://imbalanced-learn.readthedocs.io/en/stable/over_sampling.html)
* [Under-sampling(欠采样)](https://imbalanced-learn.readthedocs.io/en/stable/under_sampling.html)



## 核密度函数

* [核密度估计 Kernel Density Estimation(KDE)](https://blog.csdn.net/unixtch/article/details/78556499)

![核函数的图形](https://img-blog.csdn.net/20171116222009645?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdW5peHRjaA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## PCA

* [Python scikit-learn 学习笔记—PCA+SVM人脸识别](https://blog.csdn.net/leo_is_ant/article/details/45766315)
* **[PCA主成分分析学习总结](https://zhuanlan.zhihu.com/p/32412043)** [#]

pca降维的原理是:**“将协方差矩阵化为对角阵的过程。而协方差矩阵的值反映的是不同波段之间数据的相关性，即协方差。
对角化后的协方差矩阵除了主对角线上的元素外，都是零。所以说，特征之间的相关性被去除了”。**

* [协方差与协方差矩阵](https://www.cnblogs.com/terencezhou/p/6235974.html)
* [协方差矩阵和对角阵理解](https://blog.csdn.net/ngmanhei/article/details/47109057)

* **[特征值和特征向量的几何意义](https://blog.csdn.net/qq_36653505/article/details/82025971)** (#)

引用《线性代数的几何意义》的描述：**“矩阵乘法对应了一个变换，是把任意一个向量变成另一个方向或长度都大多不同的新向量。
在这个变换的过程中，原向量主要发生旋转、伸缩的变化。如果矩阵对某一个向量或某些向量只发生伸缩变换，不对这些向量产生
旋转的效果，那么这些向量就称为这个矩阵的特征向量，伸缩的比例就是特征值”**。对于实对称矩阵来说，不同特征值对应的特征
向量必定正交;我们也可以说，一个变换矩阵的所有特征向量组成了这个变换矩阵的一组基。

其实，经过数学上的推导的，我们就可以知道，特征值对应的特征向量就是理想中想取得正确的坐标轴，而特征值就等于数据在旋转
之后的坐标上对应维度上的方差。

PCA：选取特征值最高的k个特征向量来表示一个矩阵，从而达到降维分析+特征显示的方法.

* **[奇异值分解(SVD)原理与在降维中的应用](https://www.cnblogs.com/pinard/p/6251584.html)** (###)
* [奇异值分解（SVD）原理](https://blog.csdn.net/u013108511/article/details/79016939) (#)
* [矩阵的对角化（Diagonalizing a Matrix ）](https://blog.csdn.net/danieljianfeng/article/details/22171581)

对角性和可逆性:

	1. 对角性与特征向量有关，如果存在n个线性无关的特征向量，则矩阵可对角化。
	2. 可逆性与特征值有关，如果存在特征值为0，则矩阵不可逆。


**python-PCA**

* [sklearn_PCA实践](https://blog.csdn.net/Huangyi_906/article/details/76438885)

```
class sklearn.decomposition.PCA(n_components=None, copy=True, whiten=False, svd_solver=’auto’, 
tol=0.0, iterated_power=’auto’, random_state=None)
其中参数：
	n_components=None：指定降维后的维数。如果给定数在（0,1）之间，则为降维后占原维数的百分比。
	       默认自动选择。[最大值不得超过min(m,n)]
属性：
	components_ : 主成分组数 [shape为(k,n), 每一行代表一个主成分] 主成分矩阵(V)是原始矩阵的正交基。
	n_components_ : 一个整数，指示主成分有多少个元素。
	explained_variance_: 各成分所能解释的方差量。
	explained_variance_ratio_: 每个主成分占方差比例
	noise_variance_: 采用概率PCA模型估计的噪声协方差
	singular_values_: 各主成分的奇异值
	mean_: 每个特征的平均值
方法：
	fit(X): 训练模型
	transform(X): 执行降维
	fit_transform(X): 训练并降维
	inverse_transform(X): 逆向操作，把降维的数据逆向转换回原来数据。
说明:
	X: 原始数据矩阵(m x n)
	m: 原始数据的行数,代表样本
	n: 原始数据的列数,代表特征
	k: 为降维后的特征数(维度)
	V: 原始数据X的正交基
	Z：降维后的数据
其它：

```


**怎样排除引起最大方差的前n个因素的影响？**

我们可以使用PCA先对原始数据X进行拟合，再恢复到原始维度，获得X的近似X1，X-X1即为噪音数据：

* **[PCA及绘制降维与恢复示意图](https://blog.csdn.net/SHU15121856/article/details/84646874)** (##)
* **[How to reverse PCA and reconstruct original variables from several principal components?](https://stats.stackexchange.com/questions/229092/how-to-reverse-pca-and-reconstruct-original-variables-from-several-principal-com)** (##)
* **[Relationship between SVD and PCA. How to use SVD to perform PCA?](https://stats.stackexchange.com/questions/134282/relationship-between-svd-and-pca-how-to-use-svd-to-perform-pca)** (###)


**PCA使用协方差矩阵(covariance matrix)来计算特征值和特征向量； 如果要使用相关矩阵(correlation matrix )，
原始数据需要做中心化处理(减去平均值)和标准化处理(除以标准差)；，当恢复数据时，需要反向处理(乘以标准化
和加上平均值)**


> PCA reconstruction=PC scores * Eigenvectors^T + Mean

```
from sklearn.decomposition import PCA

pca = PCA(svd_solver='full')
pca.fit(X)                    # X.shape (m,n)
X1 = pca.transform(X)[:, 1:]  # 对X进行线性变换，并扔掉第一维的数据(引起主要方差的因素的值), shape:(m, k-1)
U = pca.components_[1:, :]    # 扔掉第一个主成分 shape:(k-1, n)
X_appr = X1.dot(U)            # 还原到原来的维度 shape:(m, n)
X_appr += pca.mean_           # 回复数据
```

或者通过奇异值分解来排除 

```
M = X.mean(axis=0) 
U, S, VT = np.linalg.svd((X-M), full_matrices=False) # 先centered,再svd 
expvar = (S ** 2) / (X.shape[0] - 1)  # 计算各主成分对方差的贡献 
self._exp_var_ratio = expvar / expvar.sum()  # 计算各主成分对方差的贡献率 
S[:n] = 0   # 去除前n个主成分的影响 
S_ = np.zeros((U.shape[1], VT.shape[0])) 
np.fill_diagonal(S_, S) 
X_ = U.dot(S_).dot(VT) + M 
return X_
```



**奇异值分解**

如果特征和样本量都很大，那么计算协方差会很耗时，此时我们可以借助奇异值分解来绕过计算协方差而直接得到特征值
和特征向量。

> U, D, V = SVD(X)
>
X: (m x n)  原始矩阵
U: (m x m)  左奇异矩阵(一组正交基)
D: (m x n)  奇异值矩阵(对角线为特征值,其余为0)
V: (n x n)  右奇异矩阵(一组正交基) 
>
当m < n 时，PCA主成分等于V；
当m > n时， PCA主成分不等于V，也不能等于U，不知道等于啥

```
>>> X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
>>> U, D, V = np.linalg.svd(X)
>>> V  # 特征向量
array([[ 0.83849224,  0.54491354],
       [ 0.54491354, -0.83849224]])
>>> D  # 特征值
array([6.30061232, 0.54980396])
>>> pca = PCA()
>>> pca.fit(X)
>>> pca.components_
array([[ 0.83849224,  0.54491354],
       [ 0.54491354, -0.83849224]])

>>> U, D, V = np.linalg.svd(X.T)
>>> V
array([[ 0.21956688,  0.35264795,  0.57221483, -0.21956688, -0.35264795, -0.57221483],
       [-0.53396977,  0.45713538, -0.07683439,  0.53396977, -0.45713538,  0.07683439],
       [-0.48030985, -0.30371038,  0.75680405,  0.03329824,  0.20989771,  0.24319595],
       [ 0.45219595, -0.31508521,  0.17257785,  0.79735166,  0.03007049, -0.17257785],
       [ 0.02811389,  0.61879559,  0.0706181 ,  0.1693501 ,  0.7600318 , -0.0706181 ],
       [ 0.48030985,  0.30371038,  0.24319595, -0.03329824, -0.20989771,  0.75680405]])
>>> pca = PCA()
>>> pca.fit(X.T)
>>> pca.components_
array([[ 0.  ,  0.5 ,  0.5 ,  0.  , -0.5 , -0.5 ],
       [ 0.5 ,  0.75, -0.25,  0.  ,  0.25,  0.25]])
```



## 逻辑回归

* [逻辑回归（Logistic Regression, LR）简介](https://blog.csdn.net/jk123vip/article/details/80591619)
* [逻辑回归的理解](https://blog.csdn.net/t46414704152abc/article/details/79574003)
* [logistic回归与判别分析](https://www.jianshu.com/p/8afbf60156d2)
* [逻辑回归（Logistic Regression）](https://blog.csdn.net/liulina603/article/details/78676723)
* [逻辑回归的常见面试点总结](https://www.cnblogs.com/ModifyRong/p/7739955.html)
* [逻辑回归模型及LBFGS的Sherman Morrison(SM) 公式推导](https://blog.csdn.net/langb2014/article/details/48915425)

* [医学研究中的logistic模型精讲](https://wenku.baidu.com/view/70c12ec916fc700aba68fcc2.html)

* [你应该要掌握的7种回归分析方法](https://blog.csdn.net/lynnucas/article/details/47948639)

逻辑回归虽然名字叫做回归，但实际上却是一种分类学习方法。 

线性回归完成的是回归拟合任务，而对于分类任务，我们同样需要一条线，但不是去拟合每个数据点，而是把不同类别的样本区分
开来。

对于二分类问题，y∈{0,1}，1表示正例，0表示负例。逻辑回归是在线性函数θ<sup>T</sup>x输出预测实际值的基础上，
寻找一个假设函数hθ(x)=g(θ<sup>T</sup>x)，将实际值映射到到0，1之间，如果hθ(x)>=0.5，则预测y=1，及y属于正例；
如果hθ(x)<0.5，则预测y=0，即y属于负例。

逻辑回归中选择对数几率函数（logistic function）作为激活函数，对数几率函数是Sigmoid函数（形状为S的函数）的重要代表


## 非线性回归

* [python指数、幂数拟合curve_fit](https://blog.csdn.net/yefengzhichen/article/details/52767733)
* [Python机器学习之非线性回归-多项式回归](https://carrylaw.github.io/bml/2017/10/13/ml02/) 代码很清晰

非线性回归相较于线性回归而言，总带有一丢丢复杂的神秘感。关于线性回归模型相信各位已耳熟能详，
因此这里主要讨论非线性回归模型。其实非线性回归中很大一部分是基于多项式的回归模型，即利用曲
线方程代替直线方程拟合坐标图上各点，使得各点到曲线的距离总和最短。 

  一元m次多项式回归方程为：

![](https://raw.githubusercontent.com/carrylaw/IMG/master/img_ml/sucai02.png)

  二元二次多项式回归方程为：

![](https://raw.githubusercontent.com/carrylaw/IMG/master/img_ml/sucai03.png)

多项式回归的最大优点就是可以通过增加x的高次项对实测点进行逼近，直至满意为止。事实上，
多项式回归可以处理很大一类非线性问题，它在分析中占有重要的地位，因为任何一个函数都可以分段用多项式来逼近。 

举一个房屋价格与房屋尺寸非线性拟合的实例

```
# python -version 3.5+   
import matplotlib.pyplot as plt    
import numpy as np    
from sklearn import linear_model   
from sklearn.preprocessing import PolynomialFeatures   

# 读取数据集
datasets_X = [] #建立datasets_X储存房屋尺寸数据
datasets_Y = [] #建立datasets_Y储存房屋成交价格数据
fr = open('E:\\prices.txt', 'r', encoding='utf-8') #指定prices.txt数据集所在路径
lines = fr.readlines() #读取一整个文件夹
for line in lines: #逐行读取，循环遍历所有数据
    items = line.strip().split(",") #变量之间按逗号进行分隔
    datasets_X.append(int(items[0])) #读取的数据转换为int型
    datasets_Y.append(int(items[1]))

# 数据预处理
length = len(datasets_X)
datasets_X = np.array(datasets_X).reshape([length, 1]) #将datasets_X转化为数组
datasets_Y = np.array(datasets_Y)
minX = min(datasets_X) #以数据datasets_X的最大值和最小值为范围，建立等差数列，方便后续画图
maxX = max(datasets_X)
X = np.arange(minX, maxX).reshape([-1, 1])

# 数据建模
poly_reg = PolynomialFeatures(degree=2) #degree=2表示二次多项式
X_poly = poly_reg.fit_transform(datasets_X) #构造datasets_X二次多项式特征X_poly
lin_reg_2 = linear_model.LinearRegression() #创建线性回归模型
lin_reg_2.fit(X_poly, datasets_Y) #使用线性回归模型学习X_poly和datasets_Y之间的映射关系

# 查看回归系数
print('Coefficients:',lin_reg_2.coef_)
# 查看截距项
print('intercept:',lin_reg_2.intercept_)  

# 数据可视化
plt.scatter(datasets_X, datasets_Y, color='orange')   
plt.plot(X, lin_reg_2.predict(poly_reg.fit_transform(X)), color='blue')   
plt.xlabel('Area')   
plt.ylabel('Price')   
plt.show()

```


## 梯度下降

* [深入浅出--梯度下降法及其实现](https://www.jianshu.com/p/c7e642877b0e)
* [一文看懂常用的梯度下降算法](https://blog.csdn.net/u013709270/article/details/78667531/)
* [最清晰的讲解各种梯度下降法原理与Dropout](https://baijiahao.baidu.com/s?id=1613121229156499765&wfr=spider&for=pc)

## SVM

* [SVM支持向量机分类模型SVC理论+python sklean.svm实践](https://blog.csdn.net/SummerStoneS/article/details/78551757)
* [SVM详解(包含它的参数C为什么影响着分类器行为)-scikit-learn拟合线性和非线性的SVM](https://blog.csdn.net/xlinsist/article/details/51311755)
* [用实验理解SVM的核函数和参数](https://blog.csdn.net/sigai_csdn/article/details/80693951)
* [sklearn-SVC实现与类参数](https://www.cnblogs.com/xiaotan-code/p/6700290.html)

**核映射与核函数**

* [核函数的由来](https://blog.csdn.net/huang1024rui/article/details/51510611)

通过核函数，支持向量机可以将特征向量映射到更高维的空间中，使得原本线性不可分的数据在映射之后的
空间中变得线性可分。假设原始向量为x，映射之后的向量为z，这个映射为：

> z = φ(x)

在实现时不需要直接对特征向量做这个映射，而是用核函数对两个特征向量的内积进行变换，这样做等价于
先对向量进行映射然后再做内积：

> K(x<sub>i</sub>, x<sub>j</sub>) = K(x<sub>i</sub><sup>T</sup>x<sub>j</sub>) = φ(x<sub>i</sub>)<sup>T</sup>φ(x<sub>j</sub>)

在这里K为核函数。常用的非线性核函数有多项式核，高斯核（也叫径向基函数核，RBF）。下表列出了各种
核函数的计算公式：

| 核函数 | 计算公式 |
| ---- | ---- |
| 线性核(linear) | K(x<sub>i</sub>, x<sub>j</sub>) = x<sub>i</sub><sup>T</sup>x<sub>j</sub> |
| 多项式核(poly) | K(x<sub>i</sub>, x<sub>j</sub>) = (γx<sub>i</sub><sup>T</sup>x<sub>j</sub> + b)<sup>d</sup> |
| 径向基函数(高斯)核(RBF) | K(x<sub>i</sub>, x<sub>j</sub>) = exp(-γ\|\|x<sub>i</sub> - x<sub>j</sub>\|\|<sup>2</sup>) |
| sigmoid核 | K(x<sub>i</sub>, x<sub>j</sub>) = tanh(γx<sub>i</sub><sup>T</sup>x<sub>j</sub> + b) |


其中，γ(核系数, gamma), b(独立项, coef0)，d(深度, degree)为人工设置的参数，d是一个正整数，为正实数，b为非负实数。

尽管最佳核函数的选择一般与问题自身有关，但对普遍问题还是有规律可循的，建议初学者在通常情况下，
优先考虑径向基核函数（RBF）.主要基于以下考虑：

1. 作为一种对应于非线性映射的核函数，RBF 能够处理非线性可分的问题

2. 线性核函数时 RBF 核函数的一种特例，即通过适当地选择参数 (γ,C)(γ,C)，RBF 核函数总可以得到与错误代价参数 
C 的线性核函数相同的效果，反之当然不成立

3. 在选择某些参数的情况下，Sigmoid 核函数的行为也类似于 RBF 核函数,而且选择 Sigmoid 核函数就有 2 个与之有
关的参数 b、c 需要确定。

4. 多项式核函数需要计算内积，而这有可能产生溢出之类的计算问题。


**罚分因子**

C越大，我们越倾向于没有松弛变量，即模型会尽可能分对每一个点，反之，C越小，模型的泛化能力越强。


## HMM

* [一文搞懂HMM（隐马尔可夫模型）](https://www.cnblogs.com/skyme/p/4651331.html)
* [隐马尔可夫模型（一）](https://www.cnblogs.com/bigmonkey/p/7230668.html)
* [隐马尔可夫模型](https://blog.csdn.net/u011630575/article/details/79140106)
* [隐马尔可夫模型攻略](http://www.leexiang.com/hidden-markov-model)
* [HMM模型和Viterbi算法](https://www.cnblogs.com/Denise-hzf/p/6612212.html)
* [Python实现HMM的前向-后向算法和维特比算法](https://blog.csdn.net/vincent1y/article/details/84768598)

* [每日一生信--用隐马尔可夫模型建立预测模型](http://blog.sina.com.cn/s/blog_670445240101iqrp.html)

**隐马尔可夫模型作了两个基本假设**

1. 齐次马尔可夫性假设，即假设隐藏的马尔可夫链在任意时刻t的状态只依赖于其前一时刻的状态，与其他时刻的状态及观测无关。
2. 观测独立性假设，即假设任意时刻的观测只依赖于该时刻的马尔可夫链的状态，与其他观测及状态无关。

**隐马尔可夫模型的5个要素**

`隐含状态`，`可见状态`，隐含状态间的`转移概率`，隐含态到可见态的`发射概率`(输出概率)，以及隐含状态的`初始概率`

**隐马尔可夫模型5元组**

一个 HMM 可用一个5元组 { N, M, π，A，B } 表示，其中：

* N 表示隐藏状态的数量，我们要么知道确切的值，要么猜测该值；
* M 表示可观测状态的数量，可以通过训练集获得；
* π={πi} 为初始状态概率；代表的是刚开始的时候各个隐藏状态的发生概率；
* A={aij}为隐藏状态的转移矩阵；N*N维矩阵，代表的是第一个状态到第二个状态发生的概率；
* B={bij}为混淆矩阵，N*M矩阵，代表的是处于某个隐状态的条件下，某个观测发生的概率。

**隐马尔可夫模型的3个基本问題**

1. 概率计算问题。给定模型和观测序列,计算在模型下观测序列出现的概率。 [遍历法、向前算法、向后算法]
2. 学习问题。己知观测序列,估计模型参数，使得在该模型下观测序列概率最大。 [鲍姆-韦尔奇算法(EM算法)]
即用极大似然估计的方法估计参数。
3. 预测问题，也称为解码（decoding)问题。已知模型和观测序列，求对给定观测序列条件概率最大的状态序列。
即给定观测序列，求最有可能的对应的状态序列。[近似算法、维特比算法(Viterbi)]

**维特比算法**

* [HMM模型和Viterbi算法](https://www.cnblogs.com/Denise-hzf/p/6612212.html)
* [每日一生信--用隐马尔可夫模型建立预测模型](http://blog.sina.com.cn/s/blog_670445240101iqrp.html)
* [小白给小白详解维特比算法(一)](https://blog.csdn.net/athemeroy/article/details/79339546)
* [小白给小白详解维特比算法(二)](https://blog.csdn.net/athemeroy/article/details/79342048)


## 贝叶斯

* [贝叶斯公式由浅入深大讲解—AI基础算法入门](https://www.cnblogs.com/zhoulujun/p/8893393.html)
* [怎么简单理解贝叶斯公式？](https://www.zhihu.com/question/51448623/answer/175907274)


## 随机森林

* [机器学习算法---随机森林实现（包括回归和分类）](https://blog.csdn.net/jiede1/article/details/78245597)


----

# 深度学习

## TensorFlow

* [五分钟带你入门TensorFlow](https://www.jianshu.com/p/2ea7a0632239)
* [TensorFlow 机器学习：TensorFlow 基础](https://blog.csdn.net/and_w/article/details/80228243)
* [干货-史上最全的Tensorflow学习资源汇总](https://blog.csdn.net/fendouaini/article/details/79885721)
* [Simple and ready-to-use tutorials for TensorFlow](https://github.com/osforscience/TensorFlow-Course#why-use-tensorflow)

* [可视化信息理论(Visual Information Theory) （上）](https://blog.csdn.net/li_ximin/article/details/72364696?utm_source=blogxgwz1)

----

# 分布

[各种分布的公式及关系](http://www.math.wm.edu/~leemis/2008amstat.pdf)


## 泊松分布

* [如何通俗理解泊松分布？](https://blog.csdn.net/ccnt_2012/article/details/81114920)

----

# 学习资料

## 视频资料

* 斯坦福大学机器学习-吴恩达, [学习笔记](https://blog.csdn.net/hujingshuang/article/category/3277895)
* [吴恩达老师的机器学习和深度学习课程个人笔记](https://github.com/fengdu78/Coursera-ML-AndrewNg-Notes)

## 深度学习

* [github-apachecn/AiLearning (12044 Star)](https://github.com/apachecn/AiLearning)
* [良心推荐：机器学习入门资料汇总及学习建议（2018版）](https://mp.weixin.qq.com/s?__biz=Mzg5NzAxMDgwNg==&mid=2247484000&idx=1&sn=92f198b840073e79e1a267d15a48a279&chksm=c0791f79f70e966fccd525bc2ecb11d328a12f566ccdc781132ffeeb41c484c1f7757db03911&mpshare=1&scene=1&srcid=0415mIj7jMQtloDMwK0AK0bv&key=f6869c76f8fd06b8a6d822fd10ecfac0697204a8d235aff9db21e4bda74c247e25d32c07bf415f8d65a07ccaeab92ffa96a320034f98d7c938f405bde1fc4b24923ce93730071dfcc2936fbce8c1d189&ascene=1&uin=MjQ4MTQ1NDg4Mw%3D%3D&devicetype=Windows+10&version=62060728&lang=zh_CN&pass_ticket=gUwf80IY9bbYJwc333gYdD0OP8S6sMBUN4dtMY%2Fi0EKPTWn3IuyCk%2BoIi924zIUC)
* [干货 | 机器学习入门方法和资料合集](https://mp.weixin.qq.com/s?__biz=MzI3ODgwODA2MA==&mid=2247486377&idx=1&sn=e275eb251f3ec4b9fecbe3ec49402448&chksm=eb501f3adc27962c39ba45260f78ad7ce6525587eaf84836d89f817a724598f80ce5f5281418&mpshare=1&scene=1&srcid=0424WGgc62TpsPvrJ6ioDuBC&key=7c2de03dd17390131dd1a56115dfa8eca8b4d582f9e97281be9c2344906e92125be117db058369a20d60578c220d4f03ca506681107a57da53f84c37aa158a467854801f43e444bb2ad7eded9064f8ad&ascene=1&uin=MjQ4MTQ1NDg4Mw%3D%3D&devicetype=Windows+10&version=62060728&lang=zh_CN&pass_ticket=gUwf80IY9bbYJwc333gYdD0OP8S6sMBUN4dtMY%2Fi0EKPTWn3IuyCk%2BoIi924zIUC)
