# Laurae

Advanced High Performance Data Science Toolbox for R by Laurae

# me = wants download

```r
devtools::install_github("Laurae2/Laurae")
```

# Latest News (DD/MM/YYYY)

24/03/2017: Added **Xgboard**, an interactive dashboard for visualizing xgboost training, whether you are on computer, on your phone, on a tablet... by setting up a server accessible using a web browser (Google Chrome, Firefox...). Supports only Accuracy and Timing, more to come soon!

![xgboard](https://cloud.githubusercontent.com/assets/9083669/24310124/eef7222a-10ce-11e7-9032-53ea008461fe.gif)

04/03/2017: Added **Deep Forest** implementation in R using xgboost, which may provide similar performance versus very simple Convolutional Neural Networks (CNNs), and slightly better results than boosted models. You can find the paper [here](https://arxiv.org/pdf/1702.08835.pdf). Supported: **Complete-Random Tree Forest, Cascade Forest, Multi-Grained Scanning, Deep Forest**. You can use Gradient Boosting to get a sort of "Deep Boosting" model.

[Benchmark](https://github.com/Laurae2/Laurae/blob/master/demo/DeepForest_mnist.R) on MNIST 2,000 samples for training, 10,000 samples for testing, i7-4600U, 3-fold cross-validation (Cascade Forest with poor parameters for speed, Multi-Grained Scanning with poor parameters for speed):

| Model | Features | Accuracy | Training Time | Model Size |
| --- | ---: | ---:| ---: | --- |
| Cascade Forest (xgboost) | 784 | 89.91%<br>6th iteration | 637.264s<br>11th iteration | Forest: 274,951,008 bytes |
| Boosted Trees (xgboost) | 784 | 90.53%<br>250th iteration | 267.884s<br>300 iterations | Boost: NA |
| "Deep Forest" (xgboost)<br>=> Multi-Grained Scanning<br>=>Cascade Forest | Scan: 28x28<br>Forest: 2404 | 91.46%<br>5 iterations | Scan: 449.593s<br>Forest (8): 1135.937s | Scan: 256,419,396 bytes<br>Forest: 273,624,912 bytes |
| "Deep Boosting" (xgboost)<br>=> Multi-Grained Scanning<br>=>Boosted Trees | Scan: 28x28<br>Boost: 2404 | 92.41%<br>215 iterations | Scan: 449.593s<br>Boost (265): 852.360s | Scan: 256,419,396 bytes<br>Boost: NA |
| LeNet (MXnet + R w/ Intel MKL) | 28x28 | 94.74%<br>50 epochs | 647.638s<br>50 epochs | CNN: NA |

![Deep Forest](https://cloud.githubusercontent.com/assets/9083669/23586617/f0440732-0198-11e7-9e1e-ceff2414dad8.png)

10/02/2017: Added **Partial Dependence Analysis**, currently a skeleton but I will build more on it. It is fully working for the analysis of single observations against an amount of features you specify. The multiple observation version is not yet working when it comes to analyzing statistically the results.

30/01/2017: Added **"Lextravagenza"**, a machine learning model based on xgboost ignoring past gradient/hessian for optimization, but allowing **dynamic trees** to outperform small boosted trees.

09/01/2017: My [LightGBM PR](https://github.com/Microsoft/LightGBM/pull/177) for easy installation in R has been merged in LightGBM official repository. When I will get time to work more on it (harvest metric, harvest feature importance, save/load models), **I will update this package and get rid of the old LightGBM wrapper.** This way, one will be able to use the latest versions of LightGBM, instead of being stuck with the (old) PR 33 of LightGBM.

08/01/2017: I'm starting to work on an **automated machine learning model / stacker**.

# What is Data Science

![What is Data Science](https://cloud.githubusercontent.com/assets/9083669/20948670/8a05baec-bc15-11e6-9c7a-33419038d252.png)

# What can I do with it?

Mostly... in a nutshell:

| What? | Can you do? |
| --- | --- |
| Supervised Learning | Deep Forest implementation: Complete-Random Tree Forest, Cascade Forest, Multi-Grained Scanning, Deep Forest. <br> Automated machine learning (feature selection + hyperparamter tuning) <br> xgboost <br> LightGBM (training from binary, feature importance, prediction) <br> Rule-based model on outliers (univariate, bivariate) <br> Feature engineering assistant <br> Interactive xgboost feature importance <br> Repeated cross-validation <br> Symbolic loss function derivation <br> Interactive split feature engineering assistant <br> Laurae's Lextravagenza (dynamic boosted trees) <br> Partial dependency analysis on single observations for finding insights |
| Unsupervised Learning | Automated t-SNE |
| Automated Reporting for Machine Learning | Linear regression <br> Unbiased xgboost regression/classification |
| Interactive Analysis | Interactive loss function symbolic derivation <br> interactive "I'm Feeling Lucky" ggplot <br> Interactive 3djs/Plotly <br> Interactive Brewer's Paletttes, Xgboard |
| Optimization | Cross-Entropy optimization combined with Elite optimization |
| data.table improvements | up to 3X memory efficiency without even a minor cost in CPU time |
| Plot massive amounts of data without being slow | tableplots tableplots tableplots tableplots tableplots |
| SVMLight I/O (external package) | C++ implementation of SVMLight reading/saving for dgCMatrix (sparse column-compressed format) |

**Supervised Learning:**

* Deep Forest Implementation: first implementation in R of Complete-Random Tree Forest, Cascade Forest, Multi-Grained Scanning, and Deep Forest. Read more on this [paper](https://arxiv.org/pdf/1702.08835.pdf).
* (Soon Deprecated) Use LightGBM in R (first wrapper available in R for LightGBM) tuned for maximum I/O without using in-memory dataset moves (which is both a good and bad thing! - 10GB of data takes 4 mins of travel in a HDD) and use feature importance with smart and readable plots - I recommend using official LightGBM R Package which I contribute to
* Automated Machine Learning from a set of features and hyperparameters (provide algorithm functions, features, hyperparamters, and a stochastic optimizer does the job for you with full logging if required)
* Use a repeated cross-validated xgboost (Extreme Gradient Boosting)
* Get pretty interactive feature importance tables of xgboost ready-to-use for markdown documents
* Throw supervised rules using outliers anywhere you feel it appropriate (univariate, bivariate)
* Create cross-validated and repeated cross-validated folds for supervised learning with more options for creating them (like batch creation - those ones can be fed into my LightGBM R wrapper for extensive analysis of feature behavior)
* Feature Engineering Assistant (mostly non-linear version) using automated decision trees
* Dictionary of loss functions and ready to input into xgboost (currently: Absolute Error, Squared Error, Cubic Error, Loglikelihood Error, Poisson Error, Kullback-Leibler Error)
* Symbolic Derivaton for custom loss functions (finding gradient/hessian painlessly)
* Lextravagenza model (dynamic boosted trees) which are good for small boosting iterations, bad for high boosting iterations (good for diversity)
* Partial dependency analysis for single observation: the way to get insights on why a black box made a specific decision!

**Unsupervised Learning:**

* Auto-tune t-SNE (t-Distributed Stochastic Neighbor Embedding), but it comes already with premade hyperparameters tuned for minimal reproduction loss!

**Automated Reporting for Machine Learning:**

* Generate an in-depth automated report for linear regression with interactive elements.
* Generate an in-depth automated report for xgboost regression/classification with interactive elements, with unbiased feature importance computations

**Interactive Analysis:**

* Discover and optimize gradient and hessian functions interactively in real-time
* Plot up to 1 dependent variable, 2 independent variables, 2 conditioning variables, and 1 weighting variable for Exploratory Data Analysis using ggplot, in real-time
* Plot up to three variables for Exploratory Data Analysis using 3djs via NVD3, in real-time
* Plot several variables for Exploratory Data Analysis using 3djs via Plotly/ggplot, in real-time
* Discover rule-based (from decision trees) non-linear relationship between variables, with rules ready to be copied and pasted for data.tables
* Visualize interactively Color Brewer palettes with unlimited colors (unlike the original palettes), with ready to copy&paste color codes as vectors
* Monitor xgboost training in real time

**Optimization:**

* Do feature selection & hyperparameter optimization using Cross-Entropy optimization & Elite optimization
* Do the same optimization but with any variable (continuous, ordinal, discrete) for any function using fully personalized callbacks (which is both a great thing and a hassle for the user) and a personalized training backend (by default it uses xgboost as the predictor for next steps, you can modify it by another (un)supervised machine learning model!)
* Symbolic Derivaton for custom loss functions (finding gradient/hessian painlessly)

**Improvements & Extras:**

* Improve data.table memory efficiency by up to 3X while keeping a large part of its performance (best of both worlds? isn't that insane?)
* Improve Cross-Entropy optimization by providing a more powerful frontend (at the expense of the user's necessary knowledge) in order to converge better on feature selection & but slower on hyperparameter optimization of black boxes
* Load sparse data directly as dgCMatrix (sparse matrix)
* Plot massive amount of data in an easily readable picture
* Add unlimited colors to the Color Brewer palettes
* Add the ability to add linear equation coefficient to ggplot facets
* Add multiplot ggplot

**Sparsity SVMLight converter benchmark:**

* Benchmark to convert a dgCMatrix with 2,500,000 rows and 8,500 columns (1.1GB in memory) => 5 minutes
* I think it needs minimum hours if not days for the other existing converters for such size.
* Currently not merged on this repository: see https://github.com/Laurae2/sparsity !

**Nice pictures:**

* Partial Dependence for single observation analysis (5-variate example):

![Partial Dependence for single observation analysis](https://cloud.githubusercontent.com/assets/9083669/22832403/32b36d6c-efae-11e6-8e14-cfdc6faf0cd6.png)

* Partial Dependence for multiple observation analysis (univariate example):

![Partial Dependence for multiple observation analysis](https://cloud.githubusercontent.com/assets/9083669/22832757/94d8e94e-efaf-11e6-91a9-c38afc096b69.png)

* LightGBM Feature Importance:

![LightGBM Feature Importance](https://cloud.githubusercontent.com/assets/9083669/20763173/3e7a54a2-b729-11e6-86d5-48966ce2cd92.png)

* xgboost Interactive Feature Importance:

![xgboost Interactive Feature Importance](https://cloud.githubusercontent.com/assets/9083669/20934442/6fdc1902-bbdb-11e6-8eb4-9f382e9cd97e.png)

* Automated Reporting with pretty tables:

![Automated Reporting with pretty tables](https://cloud.githubusercontent.com/assets/9083669/21076083/d23e6d94-bf22-11e6-9b40-c718b4d5691e.png)

* Interactive Symbolic Derivation:

![Interactive Symbolic Derivation](https://cloud.githubusercontent.com/assets/9083669/21138299/b050ce68-c12d-11e6-9302-c32286ad1729.png)

* Interactive EDA using 3djs/Plotly/ggplot2:

![Interactive EDA using 3djs](https://cloud.githubusercontent.com/assets/9083669/21265690/df5b634a-c3a2-11e6-8966-0f1cef04d01b.png)

![Interactive EDA using Plotly](https://cloud.githubusercontent.com/assets/9083669/21290556/f457a2d2-c4be-11e6-89ff-1d9eae4f9477.png)

![Interactive EDA using ggplot2](https://cloud.githubusercontent.com/assets/9083669/21413139/8443d3be-c7f5-11e6-95a8-8f0e8311e7cb.png)

* Interactive Feature Engineering Assistant:

![Interactive Feature Engineering Assistant](https://cloud.githubusercontent.com/assets/9083669/21165716/78499d46-c1a1-11e6-9912-9acba65a6099.png)

* Deep Forest example:

![Deep Forest](https://cloud.githubusercontent.com/assets/9083669/23586632/54a9752c-0199-11e7-8a99-f5a7a744c048.png)

# Installing this package? (Unproper installation)

**Proper version is at the end of this page.**

If you already installed this package in the past, or you want to install this package super fast because you want the functions, run in R:

```r
devtools::install_github("Laurae2/Laurae")
```

Running in a Virtual Machine and/or have no proxy redirection from R? Use the following alternative:

```r
devtools::install_git("git://github.com/Laurae2/Laurae.git")
```

Need all R dependencies in one shot?:

```r
devtools:::install_github("ramnathv/rCharts")
install.packages("https://cran.r-project.org/src/contrib/Archive/tabplot/tabplot_1.1.tar.gz", repos=NULL, type="source")
install.packages(c("data.table", "foreach", "doParallel", "rpart", "rpart.plot", "partykit", "tabplot", "partykit", "ggplot2", "ggthemes", "plotluck", "grid", "gridExtra", "RColorBrewer", "lattice", "car", "CEoptim", "DT", "formattable", "rmarkdown", "shiny", "shinydashboard", "miniUI", "Matrix", "matrixStats", "R.utils", "Rtsne", "recommenderlab", "Rcpp", "RcppArmadillo", "mgcv", "Deriv", "outliers", "MASS", "stringi"))
devtools:::install_github("Laurae2/sparsity")
```

Getting Failed with error: `'there is no package called 'sparsity''` ? Run `install_github("Laurae2/sparsity")` or `install_git("git://github.com/Laurae2/sparsity.git")` if you wish to hide this error or if you want to use the super fast column-compressed sparse matrix (dgCMatrix) -> SVMLight converter in R.

# What you need?

If I am not missing stuff (please make a pull request if something is missing that must be added):

| Package | Requires compilation? | Which functions? |
| --- | :---: | --- |
| Microsoft/LightGBM | YES (install separately, from PR 33\*) | lgbm.train, lgbm.predict, lgbm.cv, lgbm.cv.prep, lgbm.fi, lgbm.metric, lgbm.fi.plot, LauraeML_lgbreg |
| dmlc/xgboost | YES (install separately, from PR 1855\*\*) | xgb.ncv, xgb.opt.depth, report.xgb, LauraeML_gblinear, LauraeML_gblinear_par, Lextravagenza, pred.Lextravagenza, predictor_xgb, CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred |
| Laurae2/sparsity | YES (\*\*\*) | lgbm.train, lgbm.predict, lgbm.cv, lgbm.cv.prep, *xgboard functions* |
| data.table | No | read_sparse_csv, lgbm.train, lgbm.predict, lgbm.cv, lgbm.cv.prep, lgbm.fi, lgbm.fi.plot, DTcbind, DTrbind, DTsubsample, DTcolsample, setDF, DTfillNA, DT2mat, report.lm, report.xgb, interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer, LauraeML, LauraeML_gblinear, LauraeML_gblinear_par, partial_dep.obs, partial_dep.obs_all, predictor_xgb, partial_dep.plot, partial_dep.feature, cbindlist, CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred, *xgboard functions* |
| foreach | No | LauraeML_gblinear_par |
| doParallel | No | LauraeML_gblinear_par |
| rpart | No | FeatureLookup, interactive.eda_tree |
| rpart.plot | No | FeatureLookup, interactive.eda_tree |
| partykit | No | interactive.eda_tree |
| tabplot | No | tableplot_jpg, interactive.eda_ggplot, partial_dep.plot |
| rCharts | No | interactive.eda_3djs |
| plotly | No | interactive.eda_plotly, partial_dep.plot |
| ggplot2 | No | lgbm.fi.plot, report.lm, report.xgb, interactive.eda_ggplot, partial_dep.plot, stat_smooth_func, stat_smooth_func.plotly, grid_arrange_shared_legend |
| ggthemes | No | interactive.eda_plotly |
| GGally | No | partial_dep.plot |
| plotluck | No | interactive.eda_ggplot |
| grid | No | report.lm, report.xgb, interactive.eda_tree |
| gridExtra | No | report.lm, report.xgb |
| RColorBrewer | No | interactive.eda_plotly, interactive.eda_RColorBrewer, brewer.pal_extended |
| lattice | No | report.lm, report.xgb, partial_dep.plot |
| car | No | .ExtraOpt_plot, partial_dep.plot |
| CEoptim | No | ExtraOpt, LauraeML |
| DT | No | xgb.importance.interactive, report.lm, report.xgb |
| formattable | No | report.lm, report.xgb |
| rmarkdown | No | report.lm, report.xgb, interactive.eda_tree |
| shiny | No | interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer |
| shinydashboard | No | interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer |
| miniUI | No | *xgboard functions* |
| Matrix | No | read_sparse_csv, CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred |
| matrixStats | No | report.lm, report.xgb |
| R.utils | No | rule_single, rule_double, report.lm, report.xgb, *xgboard functions* |
| Rtsne | No | tsne_grid |
| recommenderlab | No | read_sparse_csv (only when using NAs as sparse) |
| Rcpp | No | sparsity (package) |
| RcppArmadillo | No | report.lm |
| Deriv | No | SymbolicLoss, interactive.SymbolicLoss |
| outliers | No | rule_single, rule_double |
| MASS | No | interactive.eda_plotly |
| stringi | No | lightgbm.cv |
| None so far | No | kfold, nkfold, lgbm.find |

Manual installations:

- \* Mandatory version of Microsoft/LightGBM (PR 33): https://github.com/Microsoft/LightGBM/tree/9895116d9e71a91b6722ca7ef1139c946fb608bf
- \*\* dmlc/xgboost PR 1855: https://github.com/dmlc/xgboost/commit/b21e658a0251d692d4e6ff3b614893c54e7d0c7c
- \*\*\* Laurae2/sparsity: https://github.com/Laurae2/sparsity

# Installing dependencies?

* For LightGBM (use PR 33 please), please do NOT use: `git clone --recursive https://github.com/Microsoft/LightGBM` for the repository. Use my stable version which is aligned with Laurae package via `git clone --recursive https://github.com/Laurae2/LightGBM`. Then follow the installation steps (https://github.com/Microsoft/LightGBM/wiki/Installation-Guide).
* For xgboost, refer to my documentation for installing in MinGW: https://github.com/dmlc/xgboost/tree/master/R-package - If you encounter strange issues in Windows (like permission denied, etc.), please read: https://medium.com/@Laurae2/compiling-xgboost-in-windows-for-r-d0cb826786a5. Make sure you are using MinGW.
* sparsity: You must use Laurae's sparsity package (SVMLight I/O conversion) which can be found here: https://github.com/Laurae2/sparsity/blob/master/README.md - compilation simply requires writing `devtools:::install_github("Laurae2/sparsity")` (and having Rtools in Windows).
* tabplot: please use: `install.packages("https://cran.r-project.org/src/contrib/Archive/tabplot/tabplot_1.1.tar.gz", repos=NULL, type="source")`. The 1.3 version is "junk" since they added standard deviation which makes unreadable tableplots when it is too high, even if standard deviation is disabled.

# Strange errors on first run

Sometimes you will get strange errors (like a corrupted documentation database) on the first load ever on the package. Restart R to get rid of this issue. It does not show up anymore afterwards.

# Printed text is missing after interrupting LightGBM / xgboost

Write in your R console `sink()` until you get an error.

# A lot of functions that worked are giving errors.

Write in your R console `sink()` until you get an error.

# What is inside?

| Utility | Function Name(s) |
| --- | --- |
| Supervised Learning | xgboost: xgb.ncv, xgb.opt.depth <br> LightGBM: lgbm.train, lgbm.predict, lgbm.cv, lgbm.metric, lgbm.fi, lgbm.fi.plot, lgbm.find <br> Rules: rule_single, rule_double <br> Base: kfold, nkfold <br> Helpers: SymbolicLoss, FeatureLookup <br> AutoML: ExtraOpt, LauraeML <br> Laurae's Dynamic Trees: Lextravagenza, pred.Lextravagenza <br> Partial Dependence: partial_dep.obs, partial_dep.obs_all, partial_dep.plot, partial_dep.feature <br> Deep Forest: CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred |
| Unsupervised Learning | t-SNE: tsne_grid |
| Automated Reporting | report.lm, report.xgb |
| Visualizations | Interactive: interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer <br> Helpers: tableplot_jpg, brewer.pal_extended, grid_arrange_shared_legend, stat_smooth_func, stat_smooth_func.plotly, xgb.importance.interactive |
| Extreme low-memory manipulation | data.table: setDF, DTcbind, DTrbind, DTsubsample, DTcolsample, DTfillNA, cbindtable <br> CSV sparse: read_sparse_csv |

| Function Name | Type | What is it for |
| --- | --- | --- |
| Laurae_load | Dependency load | Attempts to load all Laurae dependencies. |
| tsne_grid | Dimensionality Reduction + Grid Search | Allows to grid search a seed and a perplexity interval using t-SNE, while returning the best t-SNE model along with the best iteration found, all in a fully verbose fashion. |
| read_sparse_csv | Iterated numeric sparse matrix reading | R always imports CSV as dense. This function allows to read very large CSVs in chunks by variables (or a specific subset of variables), outputting a sparse matrix with typically lower RAM usage than a dense matrix if sparsity is high enough, all in a fully verbose fashion. Sparsity can be defined as 0 or NA, while saving as RDS is available in the loading streak. |
| tableplot_jpg | Batch tableplot output to JPEG | Allows to create a tableplot which is immediately turned into JPEG in batch per variable, against a label. It allows to preview features in a more understandable fashion than eyeballing numeric values. |
| xgb.ncv | Repeated xgboost Cross-Validation | Allows to run a repeated xgboost cross-validation with fully verbosity of aggregate summaries, computation time, and ETA of computation, with fixed seed and a sink to store xgboost verbose data, and also out-of-fold predictions and external data prediction. |
| rule_single | Outlying Univariate Continuous Association Rule Finder | Allows to use an outlying univariate continuous association rule finder on data and predicts immediately. Intermediate outlying scores can be stored. High verbosity of outputs during computation.
| rule_double | Outlying Bivariate Linear Continuous Association Rule Finder | Allows to use an outlying bivariate linear continuous association rule finder on data and predicts immediately. Intermediate outlying scores cannot be stored. If a bivariate combination is ill-conditioned (sum of correlation matrix = 4), that bivariate combination is skipped to avoid a solver matrix inversion crash/freeze/interruption when trying to compute Mahalanobis distance dimensionality reduction. High verbosity of outputs during computation. Potential TO-DO: give the user the possibility to use their own dimensionality reduction function (like a truncated PCA 1-axis). |
| xgb.opt.depth | xgboost Depth Optimizer | Allows to optimize xgboost's depth parameter using simple heuristics. The learner function is customizable to fit any other model requiring to work by integer steps. Hence, it is adaptable to work on continuous 1-D features, with a large safety net you define yourself by coercing the integer to your own range. |
| lgbm.train | LightGBM trainer | Trains a LightGBM model. Full verbosity control, with logging to file possible. Allows to predict out of the box during the training on the validation set and a test set. |
| lgbm.predict | LightGBM predictor | Predicts from a LightGBM model. Use the model working directory if you lost the model variable (which is not needed to predict - you only need the correct model working directory and the model name). |
| lgbm.cv | LightGBM CV trainer | Cross-Validates a LightGBM model, returns out of fold predictions, ensembled average test predictions (if provided a test set), and cross-validated feature importance. Full verbosity control, with logging to file possible, with predictions given back as return. Subsampling is optimized to maximum to lower memory usage peaks. |
| lgbm.cv.prep | LightGBM CV preparation helper | Prepares the data for using lgbm.cv. All required data files are output, so you can run lgbm.cv with files_exist = TRUE without the need of other data preparation (which can be long sometimes). Supports SVMLight format. |
| lgbm.fi | LightGBM Feaure Importance | Computes the feature importance (Gain, Frequence) of a LightGBM model with Sum / Relative Ratio / Absolute Ratio scales. |
| lgbm.fi.plot | LightGBM Feaure Importance Plot | Pretty plots a LightGBM feature importance table from a trained model, or from a cross-validated model. Use the model for auto-plotting. Try to use different scales to see more appropriately differences in feature importance. You can also use the multipresence parameter to cross-validate features. |
| lgbm.metric | LightGBM Training Metrics | Computes the training metrics of a logged LightGBM model and finds the best iteration. |
| lgbm.find | LightGBM Path Helper | Helps you usign a GUI to find and write the correct path for input to LightGBM functions. |
| setDF | Low memory DT coercion to DF | (Already available in data.table) Coerces a data.table to data.frame using the least possible memory. Actually, it uses about 0 extra memory. |
| DTcbind | Low memory DT cbind | Column bind two data.tables using the least possible memory. With extreme settings, it uses only one column extra of memory, and the peak is reached when hitting the largest RAM intensive column (which is not much when you have 1,000+ columns). Compared to cbind, this reduce peak memory usage by 3X, and sometimes by more. |
| DTrbind | Low memory DT rbind | Row bind two data.tables using the least possible memory. With extreme settings, it uses only one column extra of memory, and the peak is reached when hitting the largest RAM intensive column (which is not much when you have 1,000+ columns). Compared to rbind, this reduce peak memory usage by 3X, and sometimes by more. |
| DTsubsample | Low memory DT subsampling | Subsample a data.table using the least possible memory. It should not do lower memory usage than direct subsampling. Sometimes, you can get a slight efficiency of up to 5%. |
| DTcolsample | Low memory DT column sampling | Column sample a data.table using the least possible memory. Impact is major versus a FROM clause in data.table, but it is more a convenience function for NULLing and COPYing the data.table / modify in-memoory (versus a NULL loop, the performance and memory difference should be non existant). |
| DTfillNA | Low memory DT Missing Value filling | Fills the missing values of a data.table using the least possible memory. Compared to direct usages (DT[is.na(DT)] <- value), this function consumes up to 3X less (and typically 2X less). You can even create a new data.table or overwrite the original one. Also, this function works on data.frame, and can even overwrite the original data.frame. |
| DT2mat | Low memory DT to Matrix | Converts a data.table to a matrix using the least possible memory, and way faster than using as.matrix. |
| kfold | k-fold Cross-Validation | Creates folds for cross-validation. |
| nkfold | n-repeated k-fold Cross-Validation | Creates folds for repeated cross-validation. |
| ExtraOpt | Cross-Entropy -based Hybrid Optimization | Combines Cross-Entropy optimization and Elite optimization in order to optimize mixed types of variable (continuous, ordinal, discrete). The frontend is fully featured and requires the usage of callbacks in order to be usable. Example callbacks are provided. A demo trainer, a demo estimator, a demo predictor, and a demo plotter are provided as reference callbacks to customize. The optimization backend is fully customizable, allowing you to switch the optimizer (default is xgboost) to any other (un)supervised machine learning model! |
| FeatureLookup | Non-linear Feature Engineering Assistant | Allows to run a cross-validated decision tree using your own specified depth, amount of surrogates, and best potential lookups in order to to create new features based on the resulting decision tree at your own will. |
| SymbolicLoss | Symbolic Derivation of Loss Functions | Attemps to compute the exact 1st and 2nd derivatives of the loss function provided, along of a reference function if you provide one. The functions returned are ready to be used. Graphics are also added to help the user. |
| xgb.importance.interactive | Interactive xgboost Feature Importance | Allows to print an interactive xgboost feature importance table, ready to be used in markdown documents and HTML documents to be shared. |
| report.lm | Automated HTML Reporting for Linear Regression | Automatically creates a report for linear regression (C++ backend). Allows data normalization, NA cleaning, rank deficiency checking, pretty printed machine learning performance statistics (R, R^2, MAE, MSE, RMSE, MAPE), pretty printed feature multiplicative coefficients, plotting statistics, analysis of variance (ANOVA), adjusted R^2, degrees of freedom computation... |
| report.xgb | Automated HTML Reporting for Linear Regression | Automatically creates a report for linear regression (C++ backend). Allows data normalization, NA cleaning, rank deficiency checking, pretty printed machine learning performance statistics (R, R^2, MAE, MSE, RMSE, MAPE, AUC, Logloss, optimistic Kappa, optimistic F1 Score, optimistic MCC, optimistic TPR, optimistic TNR, optimistic FPR, optimistic FNR), pretty printed feature (unbiased/biased) importance, plotting statistics, plotting of machine learning performance statistic evolution vs probability... |
| interactive.SymbolicLoss | Interactive Dashboard for Derivation of Loss Functions | Creates an interactive dashboard which allows you to work on up to 4 loss functions with their gradient and hessian, which are typically used in numerical optimization tasks. Resists to errors (keeps running even when you input errors). |
| interactive.eda_ggplot | Interactive Dashforboard for Exploratory Data Analysis using ggplot2 | Creates an interactive dashboard which allows to work on the data set you want (from the global environment) by plotting up to 3 variables simultaneously, using a smart detection of variables to choose the best appropriate plot via ggplot and plotluck. Resists to errors (keeps running even when you input errors). |
| interactive.eda_tree | Interactive Dashboard for Non-linear Feature Engineering Assistant | Creates an interactive dashboard which allows to run a cross-validated decision tree using the same settings as the Non-Linear Feature Engineering Assistant, but with an interactive interface and printable rules ready to copy and paste into data.tables. |
| interactive.eda_3djs | Interactive Dashboard for Exploratory Data Analysis using d3js | Creates an interactive dashboard which allows to work on the data set you want (from the global environment) by plotting up to 3 variables using 3djs. Not recommended and it is better to use interactive.eda_plotly. Supposed to resist to errors (keeps running even when you input errors), but this is not always true (the window unexpectedly closes sometimes when you input a very very bad setup). |
| interactive.eda_plotly | Interactive Dashboard for Exploratory Data Analysis using d3js via Plotly | Creates an interactive dashboard which allows to work on the data set you want (from the global environment) by plotting several variables using 3djs via Plotly (can use ggplot2 via Plotly via d3js). This is the recommended way for interactive charts. Not all plots are available, but support for scatter, bar, pie, histogram, histogram2d, box, contour, heatmap, polar, scatter3d, and surface plots is provided. Supposed to resist to errors (keeps running even when you input errors), but this is not always true (the window unexpectedly closes sometimes when you input a very very bad setup). Performs also on-demand supervised/unsupervised clustering for continuous to discrete data. |
| brewer.pal_extended | Color Brewer Palette Extended | Extends the original Color Brewer palettes by providing unlimited colors unlike the original palettes. |
| interactive.eda_RColorBrewer | Interactive Dashboard for Finding the Perfect Color Brewer Palette | Creates an interactive dashboard which allows you to search visually for the best Color Brewer palette for your own taste. Not only everything is shown in real-time just by editing a field, but a copy&paste output is ready to be pasted into R for further usage. You are greeted with a pyramid. |
| LauraeML | Automated Machine Learning | (VERY EXPERIMENTAL) Provides a function for doing automated machine learning (optimize features, optimize hyperparameters) using a stochastic optimizer (Cross-Entropy optimization). It does not use a Bayesian optimizer, therefore sampling is random every each optimization iterations and is much slower (for the benefits of finding which features to keep). Full logging is provided which allows you find out the best features and their loss (ex: loss vs number of features used). Still a lot of TO-DO (best would be "throw all in a single function without more than 5 arguments, get results back"). <br> Functions: LauraeML_gblinear, LauraeML_gblinear_par, LauraeML_lgbreg |
| Lextravagenza | Laurae's Dynamic Boosted Trees | (EXPERIMENTAL, working) Trains a dynamic boosted trees whose depth is defined by a range instead of a single value, without any past gradient/hessian memory. It outperforms xgboost for a small amount of boosting iterations, but xgboost is better for longer trainings. However, dynamism comes at a price: you need a validation set (for dynamism) and a testing set (for early stopping). You can use pred.Lextravagenza to predict from it. |
| grid_arrange_shared_legend | Multiplot ggplot | Allows to add multiple ggplot2 plots in one page, with a common legend. |
| stat_smooth_func | ggplot equation formula | (For non-Plotly routines only) Prints the formula used for linear regression in ggplot plots. Works with facetting. |
| stat_smooth_func.plotly | ggplot equation formula | (For Plotly routines only)Prints the formula used for linear regression in ggplot plots. Works with facetting, but you should hover the mouse to check for strange placements (hovering one statistic will reveal the others). |
| partial_dep.obs | Partial Dependence, Single Observation analysis | Performs a single observation analysis using the provided data in order to check the evolution of the label to predict when the feature values are changed, keeping all other features invariant. This is great if you want to analyze why an observation got XYZ value according to some factors. |
| partial_dep.obs_all | Partial Dependence, Multiple Observation analysis | Performs a univariate multiple observation analysis using the provided data in order to check the evolution of the label to predict when the feature values are changed, keeping all other features invariant. |
| partial_dep.plot | Partial Dependence, Plotting | Allows to plot the content of partial dependence analysis. You can use lattice, ggplot2, car, base, or tableplots. Use Plotly for interactive analysis. |
| partial_dep.feature | Partial Dependence, Statistical checking | Performs statistical tests to check for validity of impact of a feature against a specified variable. |
| cbindlist | data.table rbindlist for columns | Allows to perform rbindlist on list of vectors. |
| CRTreeForest | Complete-Random Tree Forest | Trains a Complete-Random Tree Forest model which is used in Cascade Forests from Deep Forests. You can use CRTreeForest_pred to predict from it. |
| CascadeForest | Cascade Forest | Trains a Cascade Forest model which is the equivalent of a Multilayer Perceptron / Neural Network. Adding MGScanning before it makes it become a Deep Forest. Performance is very similar to LeNet (untested against other implementations yet), which is a convolutional neural network (CNN). You can use CascadeForest_pred to predict from it. |
| MGScanning | Multi-Grained Scanning | Trains a Multi-Grained Scanning model which is, when used as features for a Cascade Forest, turns it into a Deep Forest. You can use MGScannning_pred to predict from it. |
| xgboard.run | Xgboard Dashboard (run) | Runs Xgboard Dashboard using the IP and port you specify and opens a window in a new browser (if asked to). By default, it uses `127.0.0.1:6700`. You can use IP `0.0.0.0` for broadcasting in your Intranet. |
| xgboard.init | Xgboard Dashboard (init) | Initialize an environment for xgboost. |
| xgboard.time | Xgboard Dashboard (reset) | Resets the time environment for xgboost. |
| xgboard.dump | Xgboard Dashboard (dump) | Performs dumping of metrics when passed in an evaluation metric. |
| xgboard.xgb | Xgboard Dashboard (eval_metric) | (Easy) wrapper for the evaluation metric to pass to xgboost. |
| xgboard.eval.error | Xgboard Dashboard (metric) | Evaluates the best threshold for maximum binary accuracy and return both accuracy and threshold. |
| xgboard.eval.logloss | Xgboard Dashboard (metric) | Evaluates the logartihmic loss for binary classification. |

# TO-DO:

* ~~Add a super fast matrix to data.table converter~~
* ~~Refactor LightGBM code~~
* ~~Better handling of LightGBM arguments~~
* ~~Better handling of LightGBM files~~
* Fuse Laurae2/sparsity 's SVMLight converter/reader and Laurae2/Laurae
* ~~Add Differential Evolution algorithm for feature selection and hyperparameter simultaneous optimization (add another backend via another interface as it typically takes a lot of time for both)~~ (cancelled)
* ~~(Attempt to) Add automated non-linear feature creation using decision trees~~ (cancelled)
* Provide more for LauraeML
* Provide dynamic shrinkage for Lextravagenza for maximally overfitting validation data

# To add:

* ~~xgboost grid search~~ (LauraeML)
* ~~xgboost unbalanced large dataset learning~~ (cancelled)
* ~~large sparse matrix loader for categorical data~~ (cancelled)
* Categorical to Numeric converter: h2o's autoencoder, mxnet's autoencoder, t-SNE, Generalized Low Rank Models, largeVis, FeatureHashing - along with testing performance using xgboost
* Logloss brute force calibration
* Prediction Analyzer (analyze any type of model predictions, currently only binary)
* Automated Feature Creator (create automatically features using linear (^1), quadratic (^2), cubic (^3), quartic (^4), mean, and standard deviation of different random features as inputs) - all with a GUI to interrupt without losing data with full verbosity of search
* Automated Feature Analyzer (analyze created features and test against randomness of improval) - all with verbosity
* Leave-one-out encoding (encodes any categorical using a continuous variable such as the label or a feature)
* AND MANY MORE...

# Extra contributors:

* @fakyras for the base R code for LightGBM.

# Installing this package? (Proper installation)

If you need the modeling packages, you are going to need LightGBM and xgboost compiled. Also, xgboost requires to be installed afterwards as a R package. Using drat or CRAN version is not guaranteed to work with my package.

Linux users can skip xgboost (https://github.com/dmlc/xgboost/tree/master/R-package) and LightGBM (https://github.com/Microsoft/LightGBM/wiki/Installation-Guide) installation steps, as they are straightforward (compile source).

Windows users need MinGW (architecture x86_64) and Visual Studio 2015 Community (or any working version, starting from 2013). Prepare at least 10 GB.

## xgboost (~1 GB in Windows)

This applies to **Windows only**. Linux users can just compile "out of the box" xgboost with the gcc tool chain and install easily the package in R.

Check first if you have RTools. If not, download a proper version here: https://cran.r-project.org/bin/windows/Rtools/

Check also whether you installed Git Bash or not. If not, install Git Bash (https://git-for-windows.github.io/).

Make sure you installed MinGW (mandatory) for x86_64 architecture.

Run in R: `system('gcc -v')`

* If you don't see MinGW, then edit the PATH variable appropriately so MinGW is FIRST.
* If you see MinGW, open Git Bash and run:

```bash
mkdir C:/xgboost
cd C:/xgboost
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost
git submodule init
git submodule update
alias make='mingw32-make'
cd dmlc-core
make
cd ../rabit
make lib/librabit_empty.a
cd ..
cp make/mingw64_min.mk config.mk
make
```

This should compile xgboost perfectly out of the box on Windows. If you get an error at the last "make", it means you are not using MinGW or you messed up something in the steps.

Now, fire up an R session and run this:

```r
setwd('C:/xgboost/xgboost/R-package')
library(devtools)
install()
```

If you get a "permission denied" error, go to C:\xgboost\xgboost\R-package, right-click on the “src” folder, select “Properties”:

* Under the “Security” tab, click “Edit”
* Click “Full control” to all group or user names (click on each group, click Full control for each)
* Click OK twice
* Right-click on the “src” folder, select “Properties”
* Under the “Security” tab, click “Advanced”
* Check “Replace all child object permission entries with inheritable permission entries from this object” (it is the last box at the bottom left of the opened tab).
* Click OK twice
* Run again `install()` in the R console

And you should have now xgboost compiled in Windows.

Check quickly that xgboost works:

```r
library(xgboost)
set.seed(11111)
n=100
ncov=4
z=matrix(replicate(n,rnorm(ncov)),nrow=n)
alpha=c(-1,0.5,-0.25,-0.1)
za=z%*%alpha
p=exp(za)/(1+exp(za))
t=rbinom(n,1,p)
xgb.train(list(objective="binary:logitraw"), xgb.DMatrix(data=z,label=t), nrounds=10)
```

## LightGBM installation (~10 GB in Windows)

* Deprecated soon: I recommend to use the official LightGBM R package I contribute to, it is a one-liner install in R and you do not even need Visual Studio (but only Rtools). LightGBM in Laurae's package will be deprecated soon. *

This applies to **Windows only**. Linux users can just compile "out of the box" LightGBM with the gcc tool chain

LightGBM use Visual Studio (2013 or higher) to build in Windows. If you do not have Visual Studio, follow this: download Visual Studio 2015 Community. It is free. When installing Visual Studio Community, use the default installation method. Otherwise, you might have random errors on the UI if you try a minimal installation. Prepare at least 8GB of free drive space. Install it with the Visual C++ additions (custom install, select the first box which has 3 subboxes - it should say you will install the Windows SDK blablabla - ignore the update failure error at the end).

Once you are done installing Visual Studio 2015 Community, reboot your computer.

Now, or if you skipped the installation step, clone the latest (CLEARLY UNRECOMMENDED) LightGBM repository by doing in Git Bash:

```r
cd C:/xgboost
git clone --recursive https://github.com/Microsoft/LightGBM
```

If you want the stable (RECOMMENDED) version aligned to Laurae package, use `git clone --recursive https://github.com/Laurae2/LightGBM` instead. You have 99%+ guarantee to have a non-working version if you use the fully bleeding edge devel version of LightGBM with this package (well, most of the things work but it is refusing to train on data most of the times, even via direct command line).

Now the steps:

* Under C:/xgboost/LightGBM/windows, double click LightGBM.sln to open it in Visual Studio.
* Accept any warning pop up about project versioning issues (Upgrade VC++ Compiler and Libraries --> OK).
* Wait one minute for the loading.
* On the Solution Explorer, click "Solution 'LightGBM' (1 project)"
* On the bottom right tab (Properties), change the "Active config" to "Release|x64" (default is "Debug_mpi|x64")
* Compile the solution by pressing Ctrl+Shift+B (or click Build > Build Solution).
* Should everything be correct, you now have LightGBM compiled under C:\xgboost\LightGBM\windows\x64\Release

If you get an error while building (Windows SDK version blabla), then you will need the correct SDK for your OS. Start Visual Studio from scratch, click "New Project", select "Visual C++" and click "Install Visual C++ 2015 Tools for Windows Desktop". Then, attempt to build LightGBM.

If Visual Studio fails to load the "project", delete LightGBM folder and clone LightGBM repository again in Git Bash. If it still does not compile in Visual Studio, try adjusting the PATH to include the appropriate Windows SDK path. Restart Visual Studio and try compiling again. Another way: uninstall Visual Studio (using the installer), reboot, and reinstall using Custom install (and select all Visual C++ things, it must be the first box with 3 subboxes to check - which will tell you it will install the SDK etc.). Then, you should be able to compile it perfectly.

Once you compiled it (and after you installed everything else you need, like the Laurae package), create a folder named "test" in "C:/" (or any appropriate folder you have), and try to run the following in R (you will get two prompts: the first for the "temporary" directory you created, and the second for the LightGBM executable to select):

```r
# Make sure you have data.table in case
setwd(choosedir(caption = "Select the temporary folder"))
library(Laurae)
library(stringi)

DT <- data.table(Split1 = c(rep(0, 50), rep(1, 50)), Split2 = rep(c(rep(0, 25), rep(0.5, 25)), 2))
DT$Split5 <- rep(c(rep(0, 5), rep(0.05, 5), rep(0, 10), rep(0.05, 5)), 4)
label <- as.numeric((DT$Split2 == 0) & (DT$Split1 == 0) & (DT$Split3 == 0) & (DT$Split4 == 0) | ((DT$Split2 == 0.5) & (DT$Split1 == 1) & (DT$Split3 == 0.25) & (DT$Split4 == 0.1) & (DT$Split5 == 0)) | ((DT$Split1 == 0) & (DT$Split2 == 0.5)))

trained <- lgbm.train(y_train = label,
                      x_train = DT,
                      bias_train = NA,
                      application = "binary",
                      num_iterations = 1,
                      early_stopping_rounds = 1,
                      learning_rate = 1,
                      num_leaves = 16,
                      min_data_in_leaf = 1,
                      min_sum_hessian_in_leaf = 1,
                      tree_learner = "serial",
                      num_threads = 1,
                      lgbm_path = lgbm.find(),
                      workingdir = getwd(),
                      validation = FALSE,
                      files_exist = FALSE,
                      verbose = TRUE,
                      is_training_metric = TRUE,
                      save_binary = TRUE,
                      metric = "binary_logloss")
```

## tabplot

To have "more readable" tableplots for visualizations, you will need to install an old version of the tabplot package. You can do this by running in your R console:

```r
install.packages("https://cran.r-project.org/src/contrib/Archive/tabplot/tabplot_1.1.tar.gz", repos=NULL, type="source")
```

## Other packages

You can install the other packages by running in your R console:

```r
install.packages(c("data.table", "foreach", "doParallel", "rpart", "rpart.plot", "partykit", "tabplot", "partykit", "ggplot2", "ggthemes", "plotluck", "grid", "gridExtra", "RColorBrewer", "lattice", "car", "CEoptim", "DT", "formattable", "rmarkdown", "shiny", "shinydashboard", "miniUI", "Matrix", "matrixStats", "R.utils", "Rtsne", "recommenderlab", "Rcpp", "RcppArmadillo", "mgcv", "Deriv", "outliers", "MASS", "stringi"))
devtools:::install_github("ramnathv/rCharts")
devtools:::install_github("Laurae2/sparsity")
```

## Laurae

You can now install the Laurae package and use the fully fledged version of it.

```r
devtools::install_github("Laurae2/Laurae")
```

Running in a Virtual Machine and/or have no proxy redirection from R? Use the following alternative:

```r
devtools::install_git("git://github.com/Laurae2/Laurae.git")
```

Getting a package error while running install_github/install_git which is not "could not connect to server"? Make sure you have the package outlined in the error, which is required by devtools.

* (Soon Deprecated) Use LightGBM in R (first wrapper available in R for LightGBM) tuned for maximum I/O without using in-memory dataset moves (which is both a good and bad thing! - 10GB of data takes 4 mins of travel in a HDD) and use feature importance with smart and readable plots - I recommend using official LightGBM R Package which I contribute to
* Automated Machine Learning from a set of features and hyperparameters (provide algorithm functions, features, hyperparamters, and a stochastic optimizer does the job for you with full logging if required)
* Use a repeated cross-validated xgboost (Extreme Gradient Boosting)
* Get pretty interactive feature importance tables of xgboost ready-to-use for markdown documents
* Throw supervised rules using outliers anywhere you feel it appropriate (univariate, bivariate)
* Create cross-validated and repeated cross-validated folds for supervised learning with more options for creating them (like batch creation - those ones can be fed into my LightGBM R wrapper for extensive analysis of feature behavior)
* Feature Engineering Assistant (mostly non-linear version) using automated decision trees
* Dictionary of loss functions and ready to input into xgboost (currently: Absolute Error, Squared Error, Cubic Error, Loglikelihood Error, Poisson Error, Kullback-Leibler Error)
* Symbolic Derivaton for custom loss functions (finding gradient/hessian painlessly)
* Lextravagenza model (dynamic boosted trees) which are good for small boosting iterations, bad for high boosting iterations (good for diversity)
* Partial dependency analysis for single observation: the way to get insights on why a black box made a specific decision!

**Unsupervised Learning:**

* Auto-tune t-SNE (t-Distributed Stochastic Neighbor Embedding), but it comes already with premade hyperparameters tuned for minimal reproduction loss!

**Automated Reporting for Machine Learning:**

* Generate an in-depth automated report for linear regression with interactive elements.
* Generate an in-depth automated report for xgboost regression/classification with interactive elements, with unbiased feature importance computations

**Interactive Analysis:**

* Discover and optimize gradient and hessian functions interactively in real-time
* Plot up to 1 dependent variable, 2 independent variables, 2 conditioning variables, and 1 weighting variable for Exploratory Data Analysis using ggplot, in real-time
* Plot up to three variables for Exploratory Data Analysis using 3djs via NVD3, in real-time
* Plot several variables for Exploratory Data Analysis using 3djs via Plotly/ggplot, in real-time
* Discover rule-based (from decision trees) non-linear relationship between variables, with rules ready to be copied and pasted for data.tables
* Visualize interactively Color Brewer palettes with unlimited colors (unlike the original palettes), with ready to copy&paste color codes as vectors

**Optimization:**

* Do feature selection & hyperparameter optimization using Cross-Entropy optimization & Elite optimization
* Do the same optimization but with any variable (continuous, ordinal, discrete) for any function using fully personalized callbacks (which is both a great thing and a hassle for the user) and a personalized training backend (by default it uses xgboost as the predictor for next steps, you can modify it by another (un)supervised machine learning model!)
* Symbolic Derivaton for custom loss functions (finding gradient/hessian painlessly)

**Improvements & Extras:**

* Improve data.table memory efficiency by up to 3X while keeping a large part of its performance (best of both worlds? isn't that insane?)
* Improve Cross-Entropy optimization by providing a more powerful frontend (at the expense of the user's necessary knowledge) in order to converge better on feature selection & but slower on hyperparameter optimization of black boxes
* Load sparse data directly as dgCMatrix (sparse matrix)
* Plot massive amount of data in an easily readable picture
* Add unlimited colors to the Color Brewer palettes
* Add the ability to add linear equation coefficient to ggplot facets
* Add multiplot ggplot

**Sparsity SVMLight converter benchmark:**

* Benchmark to convert a dgCMatrix with 2,500,000 rows and 8,500 columns (1.1GB in memory) => 5 minutes
* I think it needs minimum hours if not days for the other existing converters for such size.
* Currently not merged on this repository: see https://github.com/Laurae2/sparsity !

**Nice pictures:**

* Partial Dependence for single observation analysis (5-variate example):

![Partial Dependence for single observation analysis](https://cloud.githubusercontent.com/assets/9083669/22832403/32b36d6c-efae-11e6-8e14-cfdc6faf0cd6.png)

* Partial Dependence for multiple observation analysis (univariate example):

![Partial Dependence for multiple observation analysis](https://cloud.githubusercontent.com/assets/9083669/22832757/94d8e94e-efaf-11e6-91a9-c38afc096b69.png)

* LightGBM Feature Importance:

![LightGBM Feature Importance](https://cloud.githubusercontent.com/assets/9083669/20763173/3e7a54a2-b729-11e6-86d5-48966ce2cd92.png)

* xgboost Interactive Feature Importance:

![xgboost Interactive Feature Importance](https://cloud.githubusercontent.com/assets/9083669/20934442/6fdc1902-bbdb-11e6-8eb4-9f382e9cd97e.png)

* Automated Reporting with pretty tables:

![Automated Reporting with pretty tables](https://cloud.githubusercontent.com/assets/9083669/21076083/d23e6d94-bf22-11e6-9b40-c718b4d5691e.png)

* Interactive Symbolic Derivation:

![Interactive Symbolic Derivation](https://cloud.githubusercontent.com/assets/9083669/21138299/b050ce68-c12d-11e6-9302-c32286ad1729.png)

* Interactive EDA using 3djs/Plotly/ggplot2:

![Interactive EDA using 3djs](https://cloud.githubusercontent.com/assets/9083669/21265690/df5b634a-c3a2-11e6-8966-0f1cef04d01b.png)

![Interactive EDA using Plotly](https://cloud.githubusercontent.com/assets/9083669/21290556/f457a2d2-c4be-11e6-89ff-1d9eae4f9477.png)

![Interactive EDA using ggplot2](https://cloud.githubusercontent.com/assets/9083669/21413139/8443d3be-c7f5-11e6-95a8-8f0e8311e7cb.png)

* Interactive Feature Engineering Assistant:

![Interactive Feature Engineering Assistant](https://cloud.githubusercontent.com/assets/9083669/21165716/78499d46-c1a1-11e6-9912-9acba65a6099.png)

# Installing this package? (Unproper installation)

**Proper version is at the end of this page.**

If you already installed this package in the past, or you want to install this package super fast because you want the functions, run in R:

```r
devtools::install_github("Laurae2/Laurae")
```

Running in a Virtual Machine and/or have no proxy redirection from R? Use the following alternative:

```r
devtools::install_git("git://github.com/Laurae2/Laurae.git")
```

Need all R dependencies in one shot?:

```r
devtools:::install_github("ramnathv/rCharts")
install.packages("https://cran.r-project.org/src/contrib/Archive/tabplot/tabplot_1.1.tar.gz", repos=NULL, type="source")
install.packages(c("data.table", "foreach", "doParallel", "rpart", "rpart.plot", "partykit", "tabplot", "partykit", "ggplot2", "ggthemes", "plotluck", "grid", "gridExtra", "RColorBrewer", "lattice", "car", "CEoptim", "DT", "formattable", "rmarkdown", "shiny", "shinydashboard", "miniUI", "Matrix", "matrixStats", "R.utils", "Rtsne", "recommenderlab", "Rcpp", "RcppArmadillo", "mgcv", "Deriv", "outliers", "MASS", "stringi"))
devtools:::install_github("Laurae2/sparsity")
```

Getting Failed with error: `'there is no package called 'sparsity''` ? Run `install_github("Laurae2/sparsity")` or `install_git("git://github.com/Laurae2/sparsity.git")` if you wish to hide this error or if you want to use the super fast column-compressed sparse matrix (dgCMatrix) -> SVMLight converter in R.

# What you need?

If I am not missing stuff (please make a pull request if something is missing that must be added):

| Package | Requires compilation? | Which functions? |
| --- | :---: | --- |
| Microsoft/LightGBM | YES (install separately, from PR 33\*) | lgbm.train, lgbm.predict, lgbm.cv, lgbm.cv.prep, lgbm.fi, lgbm.metric, lgbm.fi.plot, LauraeML_lgbreg |
| dmlc/xgboost | YES (install separately, from PR 1855\*\*) | xgb.ncv, xgb.opt.depth, report.xgb, LauraeML_gblinear, LauraeML_gblinear_par, Lextravagenza, pred.Lextravagenza, predictor_xgb, CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred |
| Laurae2/sparsity | YES (\*\*\*) | lgbm.train, lgbm.predict, lgbm.cv, lgbm.cv.prep |
| data.table | No | read_sparse_csv, lgbm.train, lgbm.predict, lgbm.cv, lgbm.cv.prep, lgbm.fi, lgbm.fi.plot, DTcbind, DTrbind, DTsubsample, setDF, DTfillNA, report.lm, report.xgb, interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer, LauraeML, LauraeML_gblinear, LauraeML_gblinear_par, partial_dep.obs, partial_dep.obs_all, predictor_xgb, partial_dep.plot, partial_dep.feature, cbindlist, CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred |
| foreach | No | LauraeML_gblinear_par |
| doParallel | No | LauraeML_gblinear_par |
| rpart | No | FeatureLookup, interactive.eda_tree |
| rpart.plot | No | FeatureLookup, interactive.eda_tree |
| partykit | No | interactive.eda_tree |
| tabplot | No | tableplot_jpg, interactive.eda_ggplot, partial_dep.plot |
| rCharts | No | interactive.eda_3djs |
| plotly | No | interactive.eda_plotly, partial_dep.plot |
| ggplot2 | No | lgbm.fi.plot, report.lm, report.xgb, interactive.eda_ggplot, partial_dep.plot, stat_smooth_func, stat_smooth_func.plotly, grid_arrange_shared_legend |
| ggthemes | No | interactive.eda_plotly |
| GGally | No | partial_dep.plot |
| plotluck | No | interactive.eda_ggplot |
| grid | No | report.lm, report.xgb, interactive.eda_tree |
| gridExtra | No | report.lm, report.xgb |
| RColorBrewer | No | interactive.eda_plotly, interactive.eda_RColorBrewer, brewer.pal_extended |
| lattice | No | report.lm, report.xgb, partial_dep.plot |
| car | No | .ExtraOpt_plot, partial_dep.plot |
| CEoptim | No | ExtraOpt, LauraeML |
| DT | No | xgb.importance.interactive, report.lm, report.xgb |
| formattable | No | report.lm, report.xgb |
| rmarkdown | No | report.lm, report.xgb, interactive.eda_tree |
| shiny | No | interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer |
| shinydashboard | No | interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer |
| Matrix | No | read_sparse_csv, CRTreeForest, CRTreeForest_pred, CascadeForest, CascadeForest_pred, MGScanning, MGScanning_pred |
| matrixStats | No | report.lm, report.xgb |
| R.utils | No | rule_single, rule_double, report.lm, report.xgb |
| Rtsne | No | tsne_grid |
| recommenderlab | No | read_sparse_csv (only when using NAs as sparse) |
| Rcpp | No | sparsity (package) |
| RcppArmadillo | No | report.lm |
| Deriv | No | SymbolicLoss, interactive.SymbolicLoss |
| outliers | No | rule_single, rule_double |
| MASS | No | interactive.eda_plotly |
| stringi | No | lightgbm.cv |
| None so far | No | kfold, nkfold, lgbm.find |

Manual installations:

- \* Mandatory version of Microsoft/LightGBM (PR 33): https://github.com/Microsoft/LightGBM/tree/9895116d9e71a91b6722ca7ef1139c946fb608bf
- \*\* dmlc/xgboost PR 1855: https://github.com/dmlc/xgboost/commit/b21e658a0251d692d4e6ff3b614893c54e7d0c7c
- \*\*\* Laurae2/sparsity: https://github.com/Laurae2/sparsity

# Installing dependencies?

* For LightGBM (use PR 33 please), please do NOT use: `git clone --recursive https://github.com/Microsoft/LightGBM` for the repository. Use my stable version which is aligned with Laurae package via `git clone --recursive https://github.com/Laurae2/LightGBM`. Then follow the installation steps (https://github.com/Microsoft/LightGBM/wiki/Installation-Guide).
* For xgboost, refer to my documentation for installing in MinGW: https://github.com/dmlc/xgboost/tree/master/R-package - If you encounter strange issues in Windows (like permission denied, etc.), please read: https://medium.com/@Laurae2/compiling-xgboost-in-windows-for-r-d0cb826786a5. Make sure you are using MinGW.
* sparsity: You must use Laurae's sparsity package (SVMLight I/O conversion) which can be found here: https://github.com/Laurae2/sparsity/blob/master/README.md - compilation simply requires writing `devtools:::install_github("Laurae2/sparsity")` (and having Rtools in Windows).
* tabplot: please use: `install.packages("https://cran.r-project.org/src/contrib/Archive/tabplot/tabplot_1.1.tar.gz", repos=NULL, type="source")`. The 1.3 version is "junk" since they added standard deviation which makes unreadable tableplots when it is too high, even if standard deviation is disabled.

# Strange errors on first run

Sometimes you will get strange errors (like a corrupted documentation database) on the first load ever on the package. Restart R to get rid of this issue. It does not show up anymore afterwards.

# Printed text is missing after interrupting LightGBM / xgboost

Write in your R console `sink()` until you get an error.

# A lot of functions that worked are giving errors.

Write in your R console `sink()` until you get an error.

# What is inside?

| Utility | Function Name(s) |
| --- | --- |
| Supervised Learning | xgboost: xgb.ncv, xgb.opt.depth, xgb.importance.interactive <br> LightGBM: lgbm.train, lgbm.predict, lgbm.cv, lgbm.metric, lgbm.fi, lgbm.fi.plot, lgbm.find <br> Rules: rule_single, rule_double <br> Base: kfold, nkfold <br> Helpers: SymbolicLoss, FeatureLookup, ExtraOpt, LauraeML, Lextravagenza, pred.Lextravagenza |
| Unsupervised Learning | t-SNE: tsne_grid |
| Automated Reporting | report.lm, report.xgb |
| Visualizations | tableplot_jpg, interactive.SymbolicLoss, interactive.eda_ggplot, interactive.eda_tree, interactive.eda_3djs, interactive.eda_plotly, interactive.eda_RColorBrewer |
| Extreme low-memory manipulation | data.table: setDF, DTcbind, DTrbind, DTsubsample, DTfillNA <br> CSV sparse: read_sparse_csv |

| Function Name | Type | What is it for |
| --- | --- | --- |
| Laurae_load | Dependency load | Attempts to load all Laurae dependencies. |
| tsne_grid | Dimensionality Reduction + Grid Search | Allows to grid search a seed and a perplexity interval using t-SNE, while returning the best t-SNE model along with the best iteration found, all in a fully verbose fashion. |
| read_sparse_csv | Iterated numeric sparse matrix reading | R always imports CSV as dense. This function allows to read very large CSVs in chunks by variables (or a specific subset of variables), outputting a sparse matrix with typically lower RAM usage than a dense matrix if sparsity is high enough, all in a fully verbose fashion. Sparsity can be defined as 0 or NA, while saving as RDS is available in the loading streak. |
| tableplot_jpg | Batch tableplot output to JPEG | Allows to create a tableplot which is immediately turned into JPEG in batch per variable, against a label. It allows to preview features in a more understandable fashion than eyeballing numeric values. |
| xgb.ncv | Repeated xgboost Cross-Validation | Allows to run a repeated xgboost cross-validation with fully verbosity of aggregate summaries, computation time, and ETA of computation, with fixed seed and a sink to store xgboost verbose data, and also out-of-fold predictions and external data prediction. |
| rule_single | Outlying Univariate Continuous Association Rule Finder | Allows to use an outlying univariate continuous association rule finder on data and predicts immediately. Intermediate outlying scores can be stored. High verbosity of outputs during computation.
| rule_double | Outlying Bivariate Linear Continuous Association Rule Finder | Allows to use an outlying bivariate linear continuous association rule finder on data and predicts immediately. Intermediate outlying scores cannot be stored. If a bivariate combination is ill-conditioned (sum of correlation matrix = 4), that bivariate combination is skipped to avoid a solver matrix inversion crash/freeze/interruption when trying to compute Mahalanobis distance dimensionality reduction. High verbosity of outputs during computation. Potential TO-DO: give the user the possibility to use their own dimensionality reduction function (like a truncated PCA 1-axis). |
| xgb.opt.depth | xgboost Depth Optimizer | Allows to optimize xgboost's depth parameter using simple heuristics. The learner function is customizable to fit any other model requiring to work by integer steps. Hence, it is adaptable to work on continuous 1-D features, with a large safety net you define yourself by coercing the integer to your own range. |
| lgbm.train | LightGBM trainer | Trains a LightGBM model. Full verbosity control, with logging to file possible. Allows to predict out of the box during the training on the validation set and a test set. |
| lgbm.predict | LightGBM predictor | Predicts from a LightGBM model. Use the model working directory if you lost the model variable (which is not needed to predict - you only need the correct model working directory and the model name). |
| lgbm.cv | LightGBM CV trainer | Cross-Validates a LightGBM model, returns out of fold predictions, ensembled average test predictions (if provided a test set), and cross-validated feature importance. Full verbosity control, with logging to file possible, with predictions given back as return. Subsampling is optimized to maximum to lower memory usage peaks. |
| lgbm.cv.prep | LightGBM CV preparation helper | Prepares the data for using lgbm.cv. All required data files are output, so you can run lgbm.cv with files_exist = TRUE without the need of other data preparation (which can be long sometimes). Supports SVMLight format. |
| lgbm.fi | LightGBM Feaure Importance | Computes the feature importance (Gain, Frequence) of a LightGBM model with Sum / Relative Ratio / Absolute Ratio scales. |
| lgbm.fi.plot | LightGBM Feaure Importance Plot | Pretty plots a LightGBM feature importance table from a trained model, or from a cross-validated model. Use the model for auto-plotting. Try to use different scales to see more appropriately differences in feature importance. You can also use the multipresence parameter to cross-validate features. |
| lgbm.metric | LightGBM Training Metrics | Computes the training metrics of a logged LightGBM model and finds the best iteration. |
| lgbm.find | LightGBM Path Helper | Helps you usign a GUI to find and write the correct path for input to LightGBM functions. |
| setDF | Low memory DT coercion to DF | (Already available in data.table) Coerces a data.table to data.frame using the least possible memory. Actually, it uses about 0 extra memory. |
| DTcbind | Low memory DT cbind | Column bind two data.tables using the least possible memory. With extreme settings, it uses only one column extra of memory, and the peak is reached when hitting the largest RAM intensive column (which is not much when you have 1,000+ columns). Compared to cbind, this reduce peak memory usage by 3X, and sometimes by more. |
| DTrbind | Low memory DT rbind | Row bind two data.tables using the least possible memory. With extreme settings, it uses only one column extra of memory, and the peak is reached when hitting the largest RAM intensive column (which is not much when you have 1,000+ columns). Compared to rbind, this reduce peak memory usage by 3X, and sometimes by more. |
| DTsubsample | Low memory DT subsampling | Subsample a data.table using the least possible memory. It should not do lower memory usage than direct subsampling. Sometimes, you can get a slight efficiency of up to 5%. |
| DTfillNA | Low memory DT Missing Value filling | Fills the missing values of a data.table using the least possible memory. Compared to direct usages (DT[is.na(DT)] <- value), this function consumes up to 3X less (and typically 2X less). You can even create a new data.table or overwrite the original one. Also, this function works on data.frame, and can even overwrite the original data.frame. |
| kfold | k-fold Cross-Validation | Creates folds for cross-validation. |
| nkfold | n-repeated k-fold Cross-Validation | Creates folds for repeated cross-validation. |
| ExtraOpt | Cross-Entropy -based Hybrid Optimization | Combines Cross-Entropy optimization and Elite optimization in order to optimize mixed types of variable (continuous, ordinal, discrete). The frontend is fully featured and requires the usage of callbacks in order to be usable. Example callbacks are provided. A demo trainer, a demo estimator, a demo predictor, and a demo plotter are provided as reference callbacks to customize. The optimization backend is fully customizable, allowing you to switch the optimizer (default is xgboost) to any other (un)supervised machine learning model! |
| FeatureLookup | Non-linear Feature Engineering Assistant | Allows to run a cross-validated decision tree using your own specified depth, amount of surrogates, and best potential lookups in order to to create new features based on the resulting decision tree at your own will. |
| SymbolicLoss | Symbolic Derivation of Loss Functions | Attemps to compute the exact 1st and 2nd derivatives of the loss function provided, along of a reference function if you provide one. The functions returned are ready to be used. Graphics are also added to help the user. |
| xgb.importance.interactive | Interactive xgboost Feature Importance | Allows to print an interactive xgboost feature importance table, ready to be used in markdown documents and HTML documents to be shared. |
| report.lm | Automated HTML Reporting for Linear Regression | Automatically creates a report for linear regression (C++ backend). Allows data normalization, NA cleaning, rank deficiency checking, pretty printed machine learning performance statistics (R, R^2, MAE, MSE, RMSE, MAPE), pretty printed feature multiplicative coefficients, plotting statistics, analysis of variance (ANOVA), adjusted R^2, degrees of freedom computation... |
| report.xgb | Automated HTML Reporting for Linear Regression | Automatically creates a report for linear regression (C++ backend). Allows data normalization, NA cleaning, rank deficiency checking, pretty printed machine learning performance statistics (R, R^2, MAE, MSE, RMSE, MAPE, AUC, Logloss, optimistic Kappa, optimistic F1 Score, optimistic MCC, optimistic TPR, optimistic TNR, optimistic FPR, optimistic FNR), pretty printed feature (unbiased/biased) importance, plotting statistics, plotting of machine learning performance statistic evolution vs probability... |
| interactive.SymbolicLoss | Interactive Dashboard for Derivation of Loss Functions | Creates an interactive dashboard which allows you to work on up to 4 loss functions with their gradient and hessian, which are typically used in numerical optimization tasks. Resists to errors (keeps running even when you input errors). |
| interactive.eda_ggplot | Interactive Dashforboard for Exploratory Data Analysis using ggplot2 | Creates an interactive dashboard which allows to work on the data set you want (from the global environment) by plotting up to 3 variables simultaneously, using a smart detection of variables to choose the best appropriate plot via ggplot and plotluck. Resists to errors (keeps running even when you input errors). |
| interactive.eda_tree | Interactive Dashboard for Non-linear Feature Engineering Assistant | Creates an interactive dashboard which allows to run a cross-validated decision tree using the same settings as the Non-Linear Feature Engineering Assistant, but with an interactive interface and printable rules ready to copy and paste into data.tables. |
| interactive.eda_3djs | Interactive Dashboard for Exploratory Data Analysis using d3js | Creates an interactive dashboard which allows to work on the data set you want (from the global environment) by plotting up to 3 variables using 3djs. Not recommended and it is better to use interactive.eda_plotly. Supposed to resist to errors (keeps running even when you input errors), but this is not always true (the window unexpectedly closes sometimes when you input a very very bad setup). |
| interactive.eda_plotly | Interactive Dashboard for Exploratory Data Analysis using d3js via Plotly | Creates an interactive dashboard which allows to work on the data set you want (from the global environment) by plotting several variables using 3djs via Plotly (can use ggplot2 via Plotly via d3js). This is the recommended way for interactive charts. Not all plots are available, but support for scatter, bar, pie, histogram, histogram2d, box, contour, heatmap, polar, scatter3d, and surface plots is provided. Supposed to resist to errors (keeps running even when you input errors), but this is not always true (the window unexpectedly closes sometimes when you input a very very bad setup). Performs also on-demand supervised/unsupervised clustering for continuous to discrete data. |
| brewer.pal_extended | Color Brewer Palette Extended | Extends the original Color Brewer palettes by providing unlimited colors unlike the original palettes. |
| interactive.eda_RColorBrewer | Interactive Dashboard for Finding the Perfect Color Brewer Palette | Creates an interactive dashboard which allows you to search visually for the best Color Brewer palette for your own taste. Not only everything is shown in real-time just by editing a field, but a copy&paste output is ready to be pasted into R for further usage. You are greeted with a pyramid. |
| LauraeML | Automated Machine Learning | (VERY EXPERIMENTAL) Provides a function for doing automated machine learning (optimize features, optimize hyperparameters) using a stochastic optimizer (Cross-Entropy optimization). It does not use a Bayesian optimizer, therefore sampling is random every each optimization iterations and is much slower (for the benefits of finding which features to keep). Full logging is provided which allows you find out the best features and their loss (ex: loss vs number of features used). Still a lot of TO-DO (best would be "throw all in a single function without more than 5 arguments, get results back"). <br> Functions: LauraeML_gblinear, LauraeML_gblinear_par, LauraeML_lgbreg |
| Lextravagenza | Laurae's Dynamic Boosted Trees | (EXPERIMENTAL, working) Trains a dynamic boosted trees whose depth is defined by a range instead of a single value, without any past gradient/hessian memory. It outperforms xgboost for a small amount of boosting iterations, but xgboost is better for longer trainings. However, dynamism comes at a price: you need a validation set (for dynamism) and a testing set (for early stopping). You can use pred.Lextravagenza to predict from it. |
| grid_arrange_shared_legend | Multiplot ggplot | Allows to add multiple ggplot2 plots in one page, with a common legend. |
| stat_smooth_func | ggplot equation formula | (For non-Plotly routines only) Prints the formula used for linear regression in ggplot plots. Works with facetting. |
| stat_smooth_func.plotly | ggplot equation formula | (For Plotly routines only)Prints the formula used for linear regression in ggplot plots. Works with facetting, but you should hover the mouse to check for strange placements (hovering one statistic will reveal the others). |
| partial_dep.obs | Partial Dependence, Single Observation analysis | Performs a single observation analysis using the provided data in order to check the evolution of the label to predict when the feature values are changed, keeping all other features invariant. This is great if you want to analyze why an observation got XYZ value according to some factors. |
| partial_dep.obs_all | Partial Dependence, Multiple Observation analysis | Performs a univariate multiple observation analysis using the provided data in order to check the evolution of the label to predict when the feature values are changed, keeping all other features invariant. |
| partial_dep.plot | Partial Dependence, Plotting | Allows to plot the content of partial dependence analysis. You can use lattice, ggplot2, car, base, or tableplots. Use Plotly for interactive analysis. |
| partial_dep.feature | Partial Dependence, Statistical checking | Performs statistical tests to check for validity of impact of a feature against a specified variable. |
| cbindlist | data.table rbindlist for columns | Allows to perform rbindlist on list of vectors. |
| CRTreeForest | Deep Forest - Complete-Random Tree Forest | Trains a Complete-Random Tree Forest model which is used in Cascade Forests from Deep Forests. |
| CascadeForest | Deep Forest - Cascade Forest | Trains a Cascade Forest model which is the equivalent of a Multilayer Perceptron / Neural Network. Adding MGScanning before it makes it become a Deep Forest. Performance is very similar to LeNet (untested against other implementations yet), which is a convolutional neural network (CNN). |
| MGScanning | Deep Forest - Multi-Grained Scanning | Trains a Multi-Grained Scanning model which is, when used as features for a Cascade Forest, turns it into a Deep Forest. |

# TO-DO:

* ~~Add a super fast matrix to data.table converter~~
* ~~Refactor LightGBM code~~
* ~~Better handling of LightGBM arguments~~
* ~~Better handling of LightGBM files~~
* Fuse Laurae2/sparsity 's SVMLight converter/reader and Laurae2/Laurae
* ~~Add Differential Evolution algorithm for feature selection and hyperparameter simultaneous optimization (add another backend via another interface as it typically takes a lot of time for both)~~ (cancelled)
* ~~(Attempt to) Add automated non-linear feature creation using decision trees~~ (cancelled)
* Provide more for LauraeML
* Provide dynamic shrinkage for Lextravagenza for maximally overfitting validation data

# To add:

* ~~xgboost grid search~~ (LauraeML)
* ~~xgboost unbalanced large dataset learning~~ (cancelled)
* ~~large sparse matrix loader for categorical data~~ (cancelled)
* Categorical to Numeric converter: h2o's autoencoder, mxnet's autoencoder, t-SNE, Generalized Low Rank Models, largeVis, FeatureHashing - along with testing performance using xgboost
* Logloss brute force calibration
* ~~Prediction Analyzer (analyze any type of model predictions, currently only binary)~~
* Automated Feature Creator (create automatically features using linear (^1), quadratic (^2), cubic (^3), quartic (^4), mean, and standard deviation of different random features as inputs) - all with a GUI to interrupt without losing data with full verbosity of search
* Automated Feature Analyzer (analyze created features and test against randomness of improval) - all with verbosity
* Leave-one-out encoding (encodes any categorical using a continuous variable such as the label or a feature)
* AND MANY MORE...

# Extra contributors:

* @fakyras for the base R code for LightGBM.

# Installing this package? (Proper installation)

If you need the modeling packages, you are going to need LightGBM and xgboost compiled. Also, xgboost requires to be installed afterwards as a R package. Using drat or CRAN version is not guaranteed to work with my package.

Linux users can skip xgboost (https://github.com/dmlc/xgboost/tree/master/R-package) and LightGBM (https://github.com/Microsoft/LightGBM/wiki/Installation-Guide) installation steps, as they are straightforward (compile source).

Windows users need MinGW (architecture x86_64) and Visual Studio 2015 Community (or any working version, starting from 2013). Prepare at least 10 GB.

## xgboost (~1 GB in Windows)

This applies to **Windows only**. Linux users can just compile "out of the box" xgboost with the gcc tool chain and install easily the package in R.

Check first if you have RTools. If not, download a proper version here: https://cran.r-project.org/bin/windows/Rtools/

Check also whether you installed Git Bash or not. If not, install Git Bash (https://git-for-windows.github.io/).

Make sure you installed MinGW (mandatory) for x86_64 architecture.

Run in R: `system('gcc -v')`

* If you don't see MinGW, then edit the PATH variable appropriately so MinGW is FIRST.
* If you see MinGW, open Git Bash and run:

```bash
mkdir C:/xgboost
cd C:/xgboost
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost
git submodule init
git submodule update
alias make='mingw32-make'
cd dmlc-core
make
cd ../rabit
make lib/librabit_empty.a
cd ..
cp make/mingw64_min.mk config.mk
make
```

This should compile xgboost perfectly out of the box on Windows. If you get an error at the last "make", it means you are not using MinGW or you messed up something in the steps.

Now, fire up an R session and run this:

```r
setwd('C:/xgboost/xgboost/R-package')
library(devtools)
install()
```

If you get a "permission denied" error, go to C:\xgboost\xgboost\R-package, right-click on the “src” folder, select “Properties”:

* Under the “Security” tab, click “Edit”
* Click “Full control” to all group or user names (click on each group, click Full control for each)
* Click OK twice
* Right-click on the “src” folder, select “Properties”
* Under the “Security” tab, click “Advanced”
* Check “Replace all child object permission entries with inheritable permission entries from this object” (it is the last box at the bottom left of the opened tab).
* Click OK twice
* Run again `install()` in the R console

And you should have now xgboost compiled in Windows.

Check quickly that xgboost works:

```r
library(xgboost)
set.seed(11111)
n=100
ncov=4
z=matrix(replicate(n,rnorm(ncov)),nrow=n)
alpha=c(-1,0.5,-0.25,-0.1)
za=z%*%alpha
p=exp(za)/(1+exp(za))
t=rbinom(n,1,p)
xgb.train(list(objective="binary:logitraw"), xgb.DMatrix(data=z,label=t), nrounds=10)
```

## LightGBM installation (~10 GB in Windows)

* Deprecated soon: I recommend to use the official LightGBM R package I contribute to, it is a one-liner install in R and you do not even need Visual Studio (but only Rtools). LightGBM in Laurae's package will be deprecated soon. *

This applies to **Windows only**. Linux users can just compile "out of the box" LightGBM with the gcc tool chain

LightGBM use Visual Studio (2013 or higher) to build in Windows. If you do not have Visual Studio, follow this: download Visual Studio 2015 Community. It is free. When installing Visual Studio Community, use the default installation method. Otherwise, you might have random errors on the UI if you try a minimal installation. Prepare at least 8GB of free drive space. Install it with the Visual C++ additions (custom install, select the first box which has 3 subboxes - it should say you will install the Windows SDK blablabla - ignore the update failure error at the end).

Once you are done installing Visual Studio 2015 Community, reboot your computer.

Now, or if you skipped the installation step, clone the latest (CLEARLY UNRECOMMENDED) LightGBM repository by doing in Git Bash:

```r
cd C:/xgboost
git clone --recursive https://github.com/Microsoft/LightGBM
```

If you want the stable (RECOMMENDED) version aligned to Laurae package, use `git clone --recursive https://github.com/Laurae2/LightGBM` instead. You have 99%+ guarantee to have a non-working version if you use the fully bleeding edge devel version of LightGBM with this package (well, most of the things work but it is refusing to train on data most of the times, even via direct command line).

Now the steps:

* Under C:/xgboost/LightGBM/windows, double click LightGBM.sln to open it in Visual Studio.
* Accept any warning pop up about project versioning issues (Upgrade VC++ Compiler and Libraries --> OK).
* Wait one minute for the loading.
* On the Solution Explorer, click "Solution 'LightGBM' (1 project)"
* On the bottom right tab (Properties), change the "Active config" to "Release|x64" (default is "Debug_mpi|x64")
* Compile the solution by pressing Ctrl+Shift+B (or click Build > Build Solution).
* Should everything be correct, you now have LightGBM compiled under C:\xgboost\LightGBM\windows\x64\Release

If you get an error while building (Windows SDK version blabla), then you will need the correct SDK for your OS. Start Visual Studio from scratch, click "New Project", select "Visual C++" and click "Install Visual C++ 2015 Tools for Windows Desktop". Then, attempt to build LightGBM.

If Visual Studio fails to load the "project", delete LightGBM folder and clone LightGBM repository again in Git Bash. If it still does not compile in Visual Studio, try adjusting the PATH to include the appropriate Windows SDK path. Restart Visual Studio and try compiling again. Another way: uninstall Visual Studio (using the installer), reboot, and reinstall using Custom install (and select all Visual C++ things, it must be the first box with 3 subboxes to check - which will tell you it will install the SDK etc.). Then, you should be able to compile it perfectly.

Once you compiled it (and after you installed everything else you need, like the Laurae package), create a folder named "test" in "C:/" (or any appropriate folder you have), and try to run the following in R (you will get two prompts: the first for the "temporary" directory you created, and the second for the LightGBM executable to select):

```r
# Make sure you have data.table in case
setwd(choosedir(caption = "Select the temporary folder"))
library(Laurae)
library(stringi)

DT <- data.table(Split1 = c(rep(0, 50), rep(1, 50)), Split2 = rep(c(rep(0, 25), rep(0.5, 25)), 2))
DT$Split5 <- rep(c(rep(0, 5), rep(0.05, 5), rep(0, 10), rep(0.05, 5)), 4)
label <- as.numeric((DT$Split2 == 0) & (DT$Split1 == 0) & (DT$Split3 == 0) & (DT$Split4 == 0) | ((DT$Split2 == 0.5) & (DT$Split1 == 1) & (DT$Split3 == 0.25) & (DT$Split4 == 0.1) & (DT$Split5 == 0)) | ((DT$Split1 == 0) & (DT$Split2 == 0.5)))

trained <- lgbm.train(y_train = label,
                      x_train = DT,
                      bias_train = NA,
                      application = "binary",
                      num_iterations = 1,
                      early_stopping_rounds = 1,
                      learning_rate = 1,
                      num_leaves = 16,
                      min_data_in_leaf = 1,
                      min_sum_hessian_in_leaf = 1,
                      tree_learner = "serial",
                      num_threads = 1,
                      lgbm_path = lgbm.find(),
                      workingdir = getwd(),
                      validation = FALSE,
                      files_exist = FALSE,
                      verbose = TRUE,
                      is_training_metric = TRUE,
                      save_binary = TRUE,
                      metric = "binary_logloss")
```

## tabplot

To have "more readable" tableplots for visualizations, you will need to install an old version of the tabplot package. You can do this by running in your R console:

```r
install.packages("https://cran.r-project.org/src/contrib/Archive/tabplot/tabplot_1.1.tar.gz", repos=NULL, type="source")
```

## Other packages

You can install the other packages by running in your R console:

```r
install.packages(c("data.table", "foreach", "doParallel", "rpart", "rpart.plot", "partykit", "tabplot", "partykit", "ggplot2", "ggthemes", "plotluck", "grid", "gridExtra", "RColorBrewer", "lattice", "car", "CEoptim", "DT", "formattable", "rmarkdown", "shiny", "shinydashboard", "miniUI", "Matrix", "matrixStats", "R.utils", "Rtsne", "recommenderlab", "Rcpp", "RcppArmadillo", "mgcv", "Deriv", "outliers", "MASS", "stringi"))
devtools:::install_github("ramnathv/rCharts")
devtools:::install_github("Laurae2/sparsity")
```

## Laurae

You can now install the Laurae package and use the fully fledged version of it.

```r
devtools::install_github("Laurae2/Laurae")
```

Running in a Virtual Machine and/or have no proxy redirection from R? Use the following alternative:

```r
devtools::install_git("git://github.com/Laurae2/Laurae.git")
```

Getting a package error while running install_github/install_git which is not "could not connect to server"? Make sure you have the package outlined in the error, which is required by devtools.
