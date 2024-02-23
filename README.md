# Cancer_Patient_Prediction_Classifier
Using a Classifier devleoped from Pomeroy et al., a classifier for the survival of cancer patients is built using leave-one-out analysis and k-nearest neighbors. Fisher's exact test and Matthews' correlation coefficient are used to assess statistical significance and variance between predicted and actual values respectively


Medulloblastoma is one of the most common malignant brain tumor conditions during childhood. The paper "Prediction of central nervous system embryonal tumor outcome based on gene expression" by Pomeroy et al aims to show that the "clinical outcome of children with medulloblastomas is highly predictable" based on gene expression profiles of their tumors taken at diagnosis [1].

# Predictions and Analysis
## Fisher’s Exact Test 
Fisher’s test is a measure of how likely an observed confusion matrix is to be observed entirely by chance. 

### Directionality
A bidirectional fishers test was chosen since we are interested in assessing if there is a significant association between two categorical variables. The significance level for this analysis is 0.05 as was used in Pomeroy et. al. Also, the confusion matrix in Pomeroy et al. is “two-tailed”.

### Null Hypothesis
There is no association between the variables, and the alternative hypothesis is that there is an association in either “direction”. 

### Significance

In the first run, without selecting the optimal genes, the p-value from Fisher’s exact test is less than the assigned significant level, the null hypothesis can be rejected using this model rejected, and one may conclude that there is an association in the data. 
First Run: See supplementary PDF and in Appendix 1: ‘20166126_PDF_Run1.pdf’

The second run has a slightly different setup and selects the optimal genes before doing leave-one-out and k-nearest neighbor analysis. The p-value was not under the significance level set above so the null-hypothesis cannot be rejected even though it was close.
Second Run: See supplementary PDF and in Appendix 2: ‘20166126_PDF_Run2.pdf’

### Results & Comparison to Pomeroy et. al
For the first run Fisher’s exact test gives a value of 0.034 (Appendix 1, 6th line from bottom) which is less than 0.05. The p-value for the second run is 0.07 (Appendix 2, 2nd line from bottom) which is greater than 0.05. 
In Pomeroy et al., the confusion matrix indicates a ‘two tailed p value’ of 0.000197 which is significantly lower. While this is more desirable, the first run still reasonably satisfies the same significant value. The second run does not.

### Comparison of Runs
This overall indicates the importance of choosing the dataset. While the code is almost identical and theoretically better with the selection of optimal genes for a classifier, garbage in garbage out still greatly affects the results. To improve results, a more careful selection of patients to put in the train set could improve results.

## Mattews’ Correlation Coefficient Phi
Matthews’ coefficient is a measure of association for nominal variables. For this problem, we have a binary classification between a response to the cytotoxic cocktail or not. In a range of -1 to 1, Phi corresponds to a negative or positive correlation where a positive correlation represents that the prediction agrees with the actual value. 

### Confusion Matrix Discussion
It's crucial to strike a balance between accuracy for both positive and negative classes. Maximizing accuracy for one class may come at the expense of accuracy for the other. Depending on the application, one might prioritize different metrics or use a composite metric like the Matthews coefficient to consider both types of errors.
In this medical application, correctly identifying positive instances (True Positives) is crucial as crucial as negative instances (True Negative). Medical professionals would be just as interested in figuring out who would respond to the treatment as who would not.

### Confusion Matrix Results
In the first run, Phi is calculated as 0.43 which indicates a moderate positive correlation. In the second run, Phi is calculated to be -0.36 which indicates a moderate negative correlation. These both indicate means that for the respective data sets, the chosen classifier predicts the outcomes in the test with moderate in both directions. Moreover, in this application, both directions are useful as a doctor could infer from both which patients would positively and who would negatively react to the cocktail. Pomeroy et al. found a Phi value of 0.507 which is very close to the Phi calculated for this model which has a similar magnitude to the results calculated by the models.

## Result Stability
This code is designed to select a completely new set of patients for the training and testing data sets every time the model is run. These data sets are completely random selections. Sometimes Phi values approach 0 and Fisher’s coefficient is 1.0. This is the worst-case scenario indicating that predictions are no better than random and that null hypothesis (there is no association) cannot be rejected. Other times results such as the ones discussed above are achieved. It is difficult to reproduce similar results across different data sets underscoring the importance of choosing good training and testing sets. Garbage in, garbage out. More work could be done to optimize stability and improve the model. 

## Conclusion
Overall, from the results from the runs support Pomeroy et al. in their claim hypothesis clinical outcome of children with medulloblastomas is highly predictable. This was done using machine learning, specifically leave-one-out and k-nearest neighbors’ analysis. Upon rigorously separating the gene expression data for 60 patients into training and testing datasets, reasonably accurate results were obtained. Selecting the optimal patients and genes to use proves to be critical when creating a classifier. Increasing the number of patients datasets and improving the model would further support the claim.



# References
[1]	S. L. Pomeroy et al., “Prediction of central nervous system embryonal tumour outcome based on gene expression,” Nature, vol. 415, no. 6870, pp. 436–442, Jan. 2002, doi: 10.1038/415436a.

