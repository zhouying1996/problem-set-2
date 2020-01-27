# Problem Set 2: Uncertainty, Holdouts, and Bootstrapping

## Fork the repository

Fork the repository for the problem set 2, `problem-set-2` (https://github.com/macss-ml20/problem-set-2). _Remember, all final submissions should be a single rendered PDF with code produced in-line._ Also, don't forget to **open the pull request** once you've committed your final submission to your forked repository. It needs to be merged back into the course master branch to be considered "submitted". See the syllabus for details.

## Joe Biden and Validation

[Joe Biden](https://en.wikipedia.org/wiki/Joe_Biden) was the 47th Vice President of the United States. He was the subject of [many memes](http://distractify.com/trending/2016/11/16/best-of-joe-and-obama-memes), [attracted the attention of Leslie Knope](https://www.youtube.com/watch?v=NvbMB_GGR6s), and [experienced a brief surge in attention due to photos from his youth](http://www.huffingtonpost.com/entry/joe-young-hot_us_58262f53e4b0c4b63b0c9e11).

The goal here is to fit a regression model predicting feelings toward Biden, and then implement a couple validation techniques to evaluate the original findings. The validation techniques include the simple holdout approach and the bootstrap. **Note**: we are *not* covering cross validation (LOOCV or k-fold) in this problem set, as these topics are covered in the following week.

#### The 2008 NES Data

The `nes2008.csv` data contains a paired down selection of features from the full [2008 American National Election Studies survey](http://www.electionstudies.org/). These data will allow you to test competing factors that may influence attitudes towards Joe Biden. The variables are coded as follows:

* `biden` - feeling thermometer ranging from 0-100. Feeling thermometers are a common metric in survey research used to gauge attitudes or feelings of "warmth" towards individuals and institutions. They range from 0-100, with 0 indicating extreme "coldness" and 100 indicating extreme "warmth."
* `female` - 1 if respondent is female, 0 if respondent is male
* `age` - age of respondent in years
* `educ` - number of years of formal education completed by respondent
* `dem` - 1 if respondent is a Democrat, 0 otherwise
* `rep` - 1 if respondent is a Republican, 0 otherwise

For this exercise we consider the following functional form,

$$Y = \beta_0 + \beta_{1}X_1 + \beta_{2}X_2 + \dots + \beta_{p}X_p  + \epsilon,$$

where $Y$ is the Joe Biden feeling thermometer, and $[X_1 \dots X_p]$ are the predictive features, including age, gender, education, Democrat, and Republican. The reason for including both `dem` and `rep` party affiliation features is to allow for capturing the preferences of Independents, which must be left out to serve as the baseline category, otherwise we would encounter perfect multicollinearity.

#### The Questions

1. (10 points) Estimate the MSE of the model using the traditional approach. That is, fit the linear regression model using the _entire_ dataset and calculate the mean squared error for the _entire_ dataset. Present and discuss your results at a simple, high level.

2. (30 points) Calculate the test MSE of the model using the simple holdout validation approach.
    * (5 points) Split the sample set into a training set (50%) and a holdout set (50%). **Be sure to set your seed prior to this part of your code to guarantee reproducibility of results.**
    * (5 points) _Fit_ the linear regression model using _only_ the _training_ observations.
    * (10 points) Calculate the _MSE_ using _only_ the _test_ set observations.
    * (10 points) How does this value compare to the training MSE from question 1? Present numeric comparison and discuss a bit.

3. (30 points) Repeat the simple validation set approach from the previous question 1000 times, using 1000 different splits of the observations into a training set and a test/validation set. Visualize your results as a sampling distribution ( *_hint_*: think histogram or density plots). Comment on the results obtained.

4. (30 points) Compare the estimated parameters and standard errors from the original model in question 1 (the model estimated using _all of the available data_) to parameters and standard errors estimated using the bootstrap ($B = 1000$). Comparison should include, at a minimum, both numeric output as well as discussion on differences, similarities, etc. Talk also about the conceptual use and impact of bootstrapping.
