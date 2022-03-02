.. _code_directive:

-------------------------------------

Cross validation and hyperparameter tuning
'''''''''''''''''''''''''''''''''''''''''''

*Cross validation* and *hyperparameter tuning* are two tasks that we do together in the data pipeline.
*Cross validation* is the process of training learners using one set of data and testing it using a different set. We set a default of **5-fold crossvalidation** to evalute our results.
*Parameter tuning* is the process of selecting the values for a model’s parameters that maximize the accuracy of the model.

.. _grid_search_cross_validation:

.. figure:: ../figs/grid_search_cross_validation.png

 
Training and testing
--------------------

The model *sees* and *learns* from the data. To ensure stability in the model and results, we devide the data set into three parts with different sizes, namely: train-set, test-set and validation-set.
Each set has a different role, and is explained below.

Validation dataset
    20% of all the data is used when the ``hgboost`` determined the best model  using the train and test sets.
    This will provide an unbiased result of the final model fit on the training dataset.

Train dataset
    After excluding the validation set, we take 80% of the data to fit the model. The model sees and learns from this data.

Test dataset
    The remaining 20% of the data training data is to evaluate the learned model and provides an unbiased evaluation of a model fit after tuning model hyperparameters.
    Evalution is performed in a 5-fold crossvalidation approach.


The use of a validation set is optional. When setting ``val_size=None`` in :func:`hgboost.hgboost.hgboost`, there are more samples included in the train/testset for parameter hyperoptimizatoin.
The use of the test set is not optional. The test_size should be larger then 0 :func:`hgboost.hgboost.hgboost` to make sure we derive a robust model.
Note that ``val_size`` can be set to very low sizes but keep in mind that this would lead in a poorly (over)trained models.


Hyperparameter optimization
---------------------------

In ``hgboost`` we incorporated hyperparameter optimization using a ``hyperopt``. The goal is to evaluate the value of the combination of parameters in the learning process.

We evaluate in total thousands of parameter combinations in the learning process.
To ensure stability, the k-fold crossvalidation comes into play which leads to even more evaluations. To keep the computation costs low, we can decide to only cross-validate the top k detected models
using the parameter ``top_cv_evals=10`` in :func:`hgboost.hgboost.hgboost`. By default, we enable parallel processing.
Each fit is scored based on the desired evaluation metric and the parameters of the best fit are used.

The specific list of parameter used for tuning are lised in section **classification** and **regression**.


.. raw:: html

	<hr>
	<center>
		<script async type="text/javascript" src="//cdn.carbonads.com/carbon.js?serve=CEADP27U&placement=erdogantgithubio" id="_carbonads_js"></script>
	</center>
	<hr>
