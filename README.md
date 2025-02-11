![ShinyLearner logo](gui/shinylearnerweb/www/Logo_Small.jpg)

[![Build Status](https://travis-ci.org/srp33/ShinyLearner.svg?branch=master)](https://travis-ci.org/srp33/ShinyLearner)

## Introduction

*ShinyLearner* enables scientists to benchmark machine-learning classification algorithms in a flexible and tidy manner.

## Background

[Classification](https://en.wikipedia.org/wiki/Statistical_classification) algorithms are used in many scientific and industrial settings to assign individuals (or "instances" or "samples") to specific categories. A classic example is the challenge of classifying [iris flowers](https://en.wikipedia.org/wiki/Iris_flower_data_set) to their correct species based on visually observable variables ("features"), such as petal length, petal width, sepal length, and sepal width. Rather than examine these features individually, classification algorithms seek to identify multivariate patterns that discriminate the categories. Classification has been applied in various contexts, including computational biology, speech recognition, computer vision, spam filtering, credit scoring, etc. See more [here](https://en.wikipedia.org/wiki/Statistical_classification#Application_domains).

Typically, a classification algorithm is applied to a dataset that contains many instances of each category, and the algorithm identifies patterns that differ among the groups. To evaluate the algorithm's ability to distinguish among individuals in the groups, the algorithm is applied to new data instances. If the algorithm accurately predicts the category to which these new instances belong, the algorithm may be suitable for broader application. Different research applications require different levels of accuracy before these algorithms are suitable for broader application. However, in many cases, even small improvements in accuracy can provide large benefits. Accordingly, researchers seek to identify ways to optimize prediction accuracy.

Hundreds of classification algorithms have been developed. Each algorithm has different properties, which may make it more or less suitable for particular applications. However, due to the large number of algorithms, it is difficult to know which algorithms should be applied in specific settings. In addition, most algorithms support "hyperparameters" (or settings), which the user can configure and which may affect the algorithm's accuracy dramatically. Thus it is also difficult to know which hyperparameters should be used in a given setting.

One way to address this problem is to perform benchmark comparisons across multiple algorithms and hyperparameters and to identify what works best in particular settings. In this way, algorithm(s) and hyperparameters can be selected in an evidence-based manner. (Care must be taken to avoid biases when performing such benchmarks; see [Word of Caution](https://github.com/srp33/ShinyLearner/blob/master/Word_of_Caution.md).)

The open-source community have developed several machine-learning software libraries that implement classification algorithms. Scientists can freely use these resources. However, several barriers make it difficult to perform large-scale benchmark comparisons across classification algorithms. For one, each software library supports only a subset of available classification algorithms; thus to perform a comprehensive comparison, it is useful to compare algorithms that have been implemented in multiple software libraries. Although most machine-learning libraries allow users to execute analyses programmatically—thus supporting reproducibility and enabling greater flexibility—different machine-learning libraries are implemented in different programming languages and often require esoteric input-data formats. In addition, output formats are not standardized, thus requiring custom efforts to parse and interpret the results. Furthermore, it is crucial to ensure that benchmark evaluations are performed across algorithms in a consistent and robust manner, yet different machine-learning libraries use different techniques for evaluating algorithm performance. Finally, to install third-party machine-learning libraries, researchers must install specific software dependencies, and these requirements often differ by software version and operating system.

We developed *ShinyLearner*, open-source software, to address these problems. ShinyLearner acts as a software "wrapper" for existing machine-learning libraries, including [scikit-learn](http://scikit-learn.org/stable), [weka](http://www.cs.waikato.ac.nz/ml/weka), and [mlr](https://mlr-org.github.io/mlr/). Each of these libraries was written in a different programming language (Python, Java, and R, respectively). Scientists who use these tools interface with them in a way that is specific to each library. For example, to use *scikit-learn* or *mlr*, users need to write code in the particular programming languages supported by these tools. Although *weka* provides a graphical user interface (in addition to a programming interface), users may find it difficult to extract and analyze predictions provided by this tool or to execute analyses at scale. A wide variety of classification algorithms are supported by these tools, and there is some overlap across these libraries; however, many algorithms are implemented in only one of these packages. Therefore, to gain access to all the algorithms that a researcher may wish to use, he/she may need to work with multiple libraries. Additionally, if a scientist wanted to compare algorithms implemented in multiple libraries, considerable effort would be required. ShinyLearner makes this easy!

## Features

Below is a list of key features that ShinyLearner supports.

#### Cross-platform support, easy to install

ShinyLearner can be executed on Windows, Mac, or Linux operating systems. ShinyLearner integrates several third-party, machine-learning libraries into a single software package. Users need not install these individual machine-learning libraries or their dependencies. ShinyLearner and all its dependencies are encapsulated within a [Docker container](https://hub.docker.com/r/srp33/shinylearner). Accordingly, once a user has installed the [Docker software](https://www.docker.com), she/he can install ShinyLearner and perform an analysis using a single command!

#### Easy to execute

ShinyLearner commands are executed via a [command-line interface](https://en.wikipedia.org/wiki/Command-line_interface) so that long-running analyses can be performed on a computer cluster or in the cloud. However, these commands can become a bit long and complex. Thus to make it easier to build these commands, we have created a Web application that enables our users to construct ShinyLearner commands more easily (see [http://shinylearner.byu.edu/shinylearnerweb/](http://shinylearner.byu.edu/shinylearnerweb/)). The user specifies input-data files, algorithms, hyperparameters, and a validation strategy. ShinyLearner takes care of the rest.

#### No computer programming is required

The third-party machine-learning libraries incorporated into ShinyLearner are written in a variety of programming languages. However, ShinyLearner users do not need to write any computer code to execute analyses with ShinyLearner.

#### Flexible inputs and standardized outputs

ShinyLearner supports commonly used [input-data formats](https://github.com/srp33/ShinyLearner/blob/master/InputFormats.md). It then translates these input data to the formats required by individual algorithms. To request that we support any additional formats, please [contact us](https://github.com/srp33/ShinyLearner/blob/master/Contact.md).

Output files are consistently formatted using the "[tidy data](http://vita.had.co.nz/papers/tidy-data.pdf)" approach. Therefore, these files can be imported directly into third-party analytic tools, such as Microsoft Excel or [R](http://www.r-project.org). [Output files](https://github.com/srp33/ShinyLearner/blob/master/OutputFiles.md) indicate predictions for each data instance as well a variety of evaluation metrics, including accuracy, sensitivity, specificity, positive predictive value, AUROC, etc. [see Metrics.md](https://github.com/srp33/ShinyLearner/blob/master/Metrics.md).

ShinyLearner uses [one-hot encoding](https://www.quora.com/What-is-one-hot-encoding-and-when-is-it-used-in-data-science) to transform categorical variables. (If desired, this can be turned off using the --ohe argument.)

#### Many algorithms

Over 50 classification algorithms and 16 feature selection algorithms from various third-party libraries have been incorporated into ShinyLearner [see Algorithms.md](https://github.com/srp33/ShinyLearner/blob/master/Algorithms.md). ShinyLearner also supports a variety of hyperparameter combinations for classification algorithms that support such.

#### Extensible

Additional algorithms can be [incorporated into ShinyLearner](https://github.com/srp33/ShinyLearner/blob/master/IncorporatingNewAlgorithms.md) in a few simple steps, irrespective of the programming language in which the algorithms were developed. Thus developers of classification algorithms can make their algorithms accessible to the research community without the need to develop a computational framework around the algorithm. We believe this feature will help to bridge a gap between the machine-learning research community and other communities where these algorithms are applied.

#### Reliable

Each time new code (or scripts) have been committed to the ShinyLearner code repository, a [Travis CI continuous-integration build](https://travis-ci.org/srp33/ShinyLearner) is triggered. This build compiles the code and runs tests to verify that each third-party algorithm executes properly via ShinyLearner.

#### Multiple validation strategies

ShinyLearner supports [k-fold cross validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics)#k-fold_cross-validation) and [Monte-carlo cross validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics)#Repeated_random_sub-sampling_validation). For either option, algorithms, hyperparameters, features, and the number of features can be optimized via internal cross-validation folds. This process can be repeated for many iterations as a way to assess consistency.

## Getting Started

To get started in using ShinyLearner, please read [these instructions](https://github.com/srp33/ShinyLearner/blob/master/GettingStarted.md).
