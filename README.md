Model Evaluation: The Curve, and What It Cannot Tell You

Objective

I tested how the choice of metric and the cost of a missed positive affect which classifier I would use.

Methodology

I simulated 8,000 cases and held out a stratified test set. Positives made up 11.8% of the test rows.

I drew ROC and precision-recall curves for logistic regression. I compared logistic regression with boosted trees using 500 paired bootstrap samples, scoring both models on the same rows each time.

I used out-of-fold predictions on the training rows to choose a threshold when a miss cost ten times as much as a false alarm. I then measured the cost on the held-out rows and repeated the comparison for ratios from 2:1 to 50:1.

I wrote roc_point() to measure the share of negatives and the share of positives flagged at a specified threshold. In the extension, I added an interaction and a squared term to the simulated outcome and repeated the model comparison.

Key findings

Logistic regression had a ROC AUC of 0.8468 and an average precision of 0.4651. Boosted trees had an AUC of 0.8431. The AUC difference was +0.0038, with a paired 95% interval of [−0.0020, +0.0094]. Either model could have a small ranking advantage on the original outcome.

At a 10:1 cost ratio, my training-selected logistic threshold was 0.0905. Its test cost was 0.4692 per case, about half the 0.9437 at the default threshold of 0.5. At the selected threshold, the false positive rate was 0.296 and the true positive rate was 0.823. Boosted trees had the lower observed cost at 5:1. Logistic regression cost less at every other ratio I tried.

With the nonlinear outcome, logistic AUC fell to 0.7130 and boosted-tree AUC reached 0.9080. The difference was −0.1950, with a paired 95% interval of [−0.2284, −0.1618]. Here the comparison favored boosted trees across the entire interval.
