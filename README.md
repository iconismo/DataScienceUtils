# Data Science Utils: Frequently Used Methods for Data Science
[![License: MIT](https://img.shields.io/github/license/idanmoradarthas/DataScienceUtils)](https://opensource.org/licenses/MIT)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/idanmoradarthas/DataScienceUtils)
[![GitHub issues](https://img.shields.io/github/issues/idanmoradarthas/DataScienceUtils)](https://github.com/idanmoradarthas/DataScienceUtils/issues)
[![Documentation Status](https://readthedocs.org/projects/datascienceutils/badge/?version=latest)](https://datascienceutils.readthedocs.io/en/latest/?badge=latest)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/data-science-utils)
![PyPI - Wheel](https://img.shields.io/pypi/wheel/data-science-utils)
[![PyPI version](https://badge.fury.io/py/data-science-utils.svg)](https://badge.fury.io/py/data-science-utils)
[![Anaconda-Server Badge](https://anaconda.org/idanmorad/data-science-utils/badges/version.svg)](https://anaconda.org/idanmorad/data-science-utils)
[![Build Status](https://travis-ci.org/idanmoradarthas/DataScienceUtils.svg?branch=master)](https://travis-ci.org/idanmoradarthas/DataScienceUtils)
[![Coverage Status](https://coveralls.io/repos/github/idanmoradarthas/DataScienceUtils/badge.svg?branch=master)](https://coveralls.io/github/idanmoradarthas/DataScienceUtils?branch=master)


Data Science Utils extends the Scikit-Learn API and Matplotlib API to provide simple methods that simplify task and 
visualization over data. 

# Code Examples and Documentation
**Let's see some code examples and outputs.** 

**You can read the full documentation with all the code examples from:
[https://datascienceutils.readthedocs.io/en/latest/](https://datascienceutils.readthedocs.io/en/latest/)**

In the documentation you can find more methods and more examples.

The API of the package is build to work with Scikit-Learn API and Matplotlib API. Here is an example of a typical 
workflow sequence with scikit-learn, matplotlib and data-science-utils:
### Plot Confusion Matrix
```python
from matplotlib import pyplot
from sklearn.model_selection import train_test_split
from sklearn.multiclass import OneVsRestClassifier
from sklearn import svm

from ds_utils.metrics import plot_confusion_matrix


x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=.5)

# Create a simple classifier
classifier = OneVsRestClassifier(svm.LinearSVC())
classifier.fit(x_train, y_train)
y_pred = classifier.predict(x_test)

plot_confusion_matrix(y_test, y_pred, [0, 1, 2])
pyplot.show()
```
The following image will be shown:

![multi label classification confusion matrix](https://raw.githubusercontent.com/idanmoradarthas/DataScienceUtils/master/tests/baseline_images/test_metrics/test_print_confusion_matrix.png)

**see full example [here](https://datascienceutils.readthedocs.io/en/latest/metrics.html#plot-confusion-matrix).**

### Generate Decision Paths
```python
from sklearn.tree import DecisionTreeClassifier

from ds_utils.xai import generate_decision_paths
    

# Create decision tree classifier object
clf = DecisionTreeClassifier(max_depth=3)

# Train model
clf.fit(x, y)
print(generate_decision_paths(clf, feature_names, target_names.tolist(), 
                              "iris_tree"))
```
The following text will be printed:
```
def iris_tree(petal width (cm), petal length (cm)):
    if petal width (cm) <= 0.8000:
        # return class setosa with probability 0.9804
        return ("setosa", 0.9804)
    else:  # if petal width (cm) > 0.8000
        if petal width (cm) <= 1.7500:
            if petal length (cm) <= 4.9500:
                # return class versicolor with probability 0.9792
                return ("versicolor", 0.9792)
            else:  # if petal length (cm) > 4.9500
                # return class virginica with probability 0.6667
                return ("virginica", 0.6667)
        else:  # if petal width (cm) > 1.7500
            if petal length (cm) <= 4.8500:
                # return class virginica with probability 0.6667
                return ("virginica", 0.6667)
            else:  # if petal length (cm) > 4.8500
                # return class virginica with probability 0.9773
                return ("virginica", 0.9773)
```

**see full example [here](https://datascienceutils.readthedocs.io/en/latest/xai.html#generate-decision-paths).**

### Extract Significant Terms from Subset
Based on the [elasticsearch significant_text aggregation](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-significantterms-aggregation.html#_scripted).

```python
import pandas

from ds_utils.strings import extract_significant_terms_from_subset

corpus = ['This is the first document.', 'This document is the second document.',
          'And this is the third one.', 'Is this the first document?']
data_frame = pandas.DataFrame(corpus, columns=["content"])
# Let's differentiate between the last two documents from the full corpus
subset_data_frame = data_frame[data_frame.index > 1]
terms = extract_significant_terms_from_subset(data_frame, subset_data_frame, 
                                               "content")

```
And the following table will be the output for ``terms``:

|third|one|and|this|the |is  |first|document|second|
|-----|---|---|----|----|----|-----|--------|------|
|1.0  |1.0|1.0|0.67|0.67|0.67|0.5  |0.25    |0.0   |

**see full example [here](https://datascienceutils.readthedocs.io/en/latest/strings.html#significant-terms).**

Excited?

Read about all the modules here and see more methods and abilities (such as drawing a decision tree and more): 
* [Metrics](https://datascienceutils.readthedocs.io/en/latest/metrics.html) - The module of metrics contains methods that help to calculate and/or visualize evaluation performance of an algorithm.
* [Preprocess](https://datascienceutils.readthedocs.io/en/latest/preprocess.html) - The module of preprocess contains methods that are processes that could be made to data before training.
* [Strings](https://datascienceutils.readthedocs.io/en/latest/strings.html) - The module of strings contains methods that help manipulate and process strings in a dataframe.
* [Visualization Aids](https://datascienceutils.readthedocs.io/en/latest/visualization_aids.html) - The module of visualization aids contains methods that visualize by drawing or printing ML output.
* [XAI](https://datascienceutils.readthedocs.io/en/latest/xai.html) - The module of xai contains methods that help explain a model decisions.

## Contributing
Interested in contributing to Data Science Utils? Great! You're welcome,  and we would love to have you. We follow 
the [Python Software Foundation Code of Conduct](http://www.python.org/psf/codeofconduct/) and 
[Matplotlib Usage Guide](https://matplotlib.org/tutorials/introductory/usage.html#coding-styles).

No matter your level of technical skill, you can be helpful. We appreciate bug reports, user testing, feature 
requests, bug fixes, product enhancements, and documentation improvements.

Thank you for your contributions!

## Find a Bug?
Check if there's already an open [issue](https://github.com/idanmoradarthas/DataScienceUtils/issues) on the topic. If 
needed, file an issue.

## Open Source
Data Science Utils license is [MIT License](https://opensource.org/licenses/MIT). 

## Installing Data Science Utils
Data Science Utils is compatible with Python 3.6 or later. The simplest way to install Data Science Utils and its 
dependencies is from PyPI with pip, Python's preferred package installer:
```bash
pip install data-science-utils
```
Note that this package is an active project and routinely publishes new releases with more methods.  In order to 
upgrade Data Science Utils to the latest version, use pip as follows:
```bash
pip install -U data-science-utils
```
Alternatively you can install from source by cloning the repo and running:
```bash
git clone https://github.com/idanmoradarthas/DataScienceUtils.git
cd DataScienceUtils
python setup.py install
```
Or install using pip from source:
```bash
pip install git+https://github.com/idanmoradarthas/DataScienceUtils.git
```
If you're using Anaconda, you can install using conda:
```bash
conda install -c idanmorad data-science-utils
```