Predicting breast cancer from digitized images of breast mass
================
Tiffany A. Timbers </br>
2019/12/30 (updated: 2020-01-20)

# Summary

# Introduction

For this project we are trying to answer the question: given tumour
image measurements is a newly discovered tumour benign or malignant?
Answering this question is important because traditional,
non-data-driven methods for tumour diagnosis are quite subjective and
can depend on the diagnosing physicians skill as well as experience
(Street, Wolberg, and Mangasarian 1993). Furthermore, benign tumours are
not normally dangerous; the cells stay in the same place and the tumour
stops growing before it gets very large. By contrast, in malignant
tumours, the cells invade the surrounding tissue and spread into nearby
organs where they can cause serious damage. Thus, it is important to
quickly and accurately diagnose the tumour type to guide patient
treatment.

# Methods

## Data

The data set used in this project is of digitized breast cancer image
features created by Dr. William H. Wolberg, W. Nick Street, and Olvi L.
Mangasarian at the University of Wisconsin, Madison (Street, Wolberg,
and Mangasarian 1993). It was sourced from the UCI Machine Learning
Repository (Dua and Graff 2017) and can be found
[here](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+\(Diagnostic\)),
specifically [this
file](http://mlr.cs.umass.edu/ml/machine-learning-databases/breast-cancer-wisconsin/wdbc.data).
Each row in the data set represents summary statistics from measurements
of an image of a tumour sample, including the diagnosis (benign or
malignant) and several other measurements (e.g., nucleus texture,
perimeter, area, etc.). Diagnosis for each image was conducted by
physicians.

## Analysis

The k-nearest neighbors (k-nn) algorithm was used to build a
classification model to predict whether a tumour mass was benign or
malignant (found in the class column of the data set). The remaining 9
variables listed above were used as predictors in the model. The
hyperparameter \(K\) was chosen using 10-fold cross validation with
overall classification accuracy as the loss function. The R and Python
programming languages (R Core Team 2019; Van Rossum and Drake 2009) and
the following R and Python packages were used to perform the analysis:
caret (Jed Wing et al. 2019), docopt (de Jonge 2018), feather (Wickham
2019), knitr (Xie 2014), tidyverse (Wickham 2017), docopt (Keleshev
2014), os (Van Rossum and Drake 2009), feather (Wickham 2019) Pandas
(McKinney 2010). The code used to perform the analysis and create this
report can be found here:
<https://github.com/ttimbers/breast_cancer_predictor>.

# Results & Discussion

To look at whether each of the predictors might be useful to predict the
tumour class, we plotted the distributions of each predictor from the
training data set and coloured the distribution by class (benign: blue
and malignant: orange). In doing this we see that class distributions
for all of the mean and max predictors for all the measurements overlap
somewhat, but do show quite a difference in their centres and spreads.
This is less so for the standard error (se) predictors. In particular,
the standard errors of fractal dimension, smoothness, symmetry and
texture look very similar in both the distribution centre and spread.
Thus, we might choose to omit these from our
model.

<div class="figure">

<img src="../results/predictor_distributions_across_class.png" alt="Figure 1. Comparison of the empirical distributions of training data predictors between benign and malignant tumour masses." width="90%" />

<p class="caption">

Figure 1. Comparison of the empirical distributions of training data
predictors between benign and malignant tumour masses.

</p>

</div>

Using 30-fold cross validation to choose
K:

<div class="figure">

<img src="../results/accuracy_vs_k.png" alt="Figure 2. 30-fold cross validation classification accuracy as K is varied." width="40%" />

<p class="caption">

Figure 2. 30-fold cross validation classification accuracy as K is
varied.

</p>

</div>

Our prediction model performed quite well on test data, with a final
overall accuracy calculated to be 0.95. Other indicators that our model
performed well come from the confusion matrix, where it only made 7
mistakes. However all 7 mistakes were predicting a malignant tumour as
benign, given the impications this has for patients health, this model
is not good enough to yet implement in the clinic.

<table class="table" style="margin-left: auto; margin-right: auto;">

<caption>

Table 1. Confusion matrix of model performance on test
data.

</caption>

<thead>

<tr>

<th style="border-bottom:hidden" colspan="1">

</th>

<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Reference

</div>

</th>

</tr>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

B

</th>

<th style="text-align:right;">

M

</th>

</tr>

</thead>

<tbody>

<tr grouplength="2">

<td colspan="3" style="border-bottom: 1px solid;">

<strong>Predicted</strong>

</td>

</tr>

<tr>

<td style="text-align:left; padding-left: 2em;" indentlevel="1">

B

</td>

<td style="text-align:right;">

89

</td>

<td style="text-align:right;">

7

</td>

</tr>

<tr>

<td style="text-align:left; padding-left: 2em;" indentlevel="1">

M

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

46

</td>

</tr>

</tbody>

</table>

# References

<div id="refs" class="references">

<div id="ref-docopt">

de Jonge, Edwin. 2018. *Docopt: Command-Line Interface Specification
Language*. <https://CRAN.R-project.org/package=docopt>.

</div>

<div id="ref-Dua2019">

Dua, Dheeru, and Casey Graff. 2017. “UCI Machine Learning Repository.”
University of California, Irvine, School of Information; Computer
Sciences. <http://archive.ics.uci.edu/ml>.

</div>

<div id="ref-caret">

Jed Wing, Max Kuhn. Contributions from, Steve Weston, Andre Williams,
Chris Keefer, Allan Engelhardt, Tony Cooper, Zachary Mayer, et al. 2019.
*Caret: Classification and Regression Training*.
<https://CRAN.R-project.org/package=caret>.

</div>

<div id="ref-docoptpython">

Keleshev, Vladimir. 2014. *Docopt: Command-Line Interface Description
Language*. <https://github.com/docopt/docopt>.

</div>

<div id="ref-mckinney-proc-scipy-2010">

McKinney, Wes. 2010. “Data Structures for Statistical Computing in
Python.” In *Proceedings of the 9th Python in Science Conference*,
edited by Stéfan van der Walt and Jarrod Millman, 51–56.

</div>

<div id="ref-R">

R Core Team. 2019. *R: A Language and Environment for Statistical
Computing*. Vienna, Austria: R Foundation for Statistical Computing.
<https://www.R-project.org/>.

</div>

<div id="ref-Streetetal">

Street, W. Nick, W. H. Wolberg, and O. L. Mangasarian. 1993. “Nuclear
feature extraction for breast tumor diagnosis.” In *Biomedical Image
Processing and Biomedical Visualization*, edited by Raj S. Acharya and
Dmitry B. Goldgof, 1905:861–70. International Society for Optics;
Photonics; SPIE. <https://doi.org/10.1117/12.148698>.

</div>

<div id="ref-Python">

Van Rossum, Guido, and Fred L. Drake. 2009. *Python 3 Reference Manual*.
Scotts Valley, CA: CreateSpace.

</div>

<div id="ref-tidyverse">

Wickham, Hadley. 2017. *Tidyverse: Easily Install and Load the
’Tidyverse’*. <https://CRAN.R-project.org/package=tidyverse>.

</div>

<div id="ref-feather">

———. 2019. *Feather: R Bindings to the Feather ’Api’*.
<https://CRAN.R-project.org/package=feather>.

</div>

<div id="ref-knitr">

Xie, Yihui. 2014. “Knitr: A Comprehensive Tool for Reproducible Research
in R.” In *Implementing Reproducible Computational Research*, edited by
Victoria Stodden, Friedrich Leisch, and Roger D. Peng. Chapman;
Hall/CRC. <http://www.crcpress.com/product/isbn/9781466561595>.

</div>

</div>
