# NLP Product Sentiment

**Author**: [Matt LeRoi](mailto:mcleroi@gmail.com) 

# Overview

Twitter offers a unique opportunity to get the publicly available opinions of a great many people about a wide variety of topics. It is, unfortunately, not organized neatly for easy digestion, and therefore requires analysis to sort, process, and gain useful information from an enormous volume of tweets.

# Business Understanding

A stealth tech company is building a new product. Having failed a previous attempt at covert corporate espionage, they have hired me to gather positive public comments made on Twitter about Google and Apple products to help them understand people's favorite aspects of those products to incorporate them into their new product. The tool will flag tweets as either positive or non-positive (could be neutral or negative) for deeper analysis. The company has stated that they would like to flag as many positive tweets as possible while minimizing false positives (tweets incorrectly labeled as positive).

# Data
The csv file has ~9000 tweets, each labeled by a human reviewer as positive, neutral, or negative. ~1/3 are positive and ~2/3 are either neutral or negative. The accuracy of these labels is limited by the judgement of the humans who labeled the list, as well as the vagaries of emotion generally. Also, this data's applicability to current technology and current language/slang trends may be limited by the fact that it is now over 10 years old.

# Modeling

Two models were created for this project: a logistic regression model and a decision tree classifier. These two were chosen because they can both handle making binary classification outcome predictions. Without knowing the type of relationship between the independent variables and the outcome (i.e. linear or more complex) beforehand, both models were created and compared. A baseline logistic regression model was created, then the data was scaled and oversampled (to combat the unbalanced data, since only 15% of customers churned). The baseline decision tree classifier was then created with various criteria and refined with hypertuning. During the tuning phase, a subset of the data was used for training and another set for validation. Once the parameters were set, the final evaluation was done using a final test set that wasn’t used during any of the training or tuning.

# Evaluation

The goal of this project is financial, to increase profits for SyriaTel. The recall and precision scores are relevant, as we are trying to identify as many of the churning customers as possible (recall rate) while limiting the number of customers we reach out to unnecessarily (precision rate). To combine these two scores, I have taken the estimate provided by SyraiTel to directly calculate the actual financial impact to the company. Each correctly identified churning customer (True Positive, TP) is worth $80 on average, and every person SyriaTel reaches out to (True Positive plus False Positive, TP+FP) costs $20. The final evaluation criterion is then: $80TP + $20*(TP+FP), which is the total profit (or loss) of the experiment.


# Conclusion

The final logistic regression model achieved a profit of $1300, correctly identifying 35 out of 101 churning customers, with 40 falsely identified churning customers. This is a positive result, literally, with a positive dollar value associated with it, but identifying roughly a third of the churning customers is not nearly as accurate as I would like.

The final hypertuned decision tree classifier model outperformed the logistic regression model, achieving a profit of $4180 after hypertuning, correctly identifying 75 out of 101 churning customers, with 16 falsely identified churning customers. 

## Limitations

The available data covers a small number of customers in one geographical area and only includes basic usage and account data. It appears that there is enough to be useful, but more detailed data could be extremely helpful to refine the model further. Also, the financial evaluation is based on rough estimates, so further experimentation can refine the evaluation criteria.

## Recommendations

The model provided should yield positive results. Broader data, however, covering more of SyriaTel’s customers and containing more varied and detailed information, should help refine the model. Also, a few insights from how the classification tree was built:

Customers with high usage and no voice mail plan churned at a very high rate, ~90%. I recommend looking into this group further. Is this line only used for a specific purpose and then closed? These could be high value customers since their usage is high, so the rewards for solving their high churn rate could be great.

Customers with low usage and high customer service calls churned at a high rate, unsurprisingly. Looking for patterns in customer service calls may lead to better customer engagement with more usage and greater retention.

Finally, customers with low usage, few customer service calls, and no international plan stayed at a relatively high rate. Generally speaking, customers with higher usage churned at a higher rate in several points in the tree. It may be worth looking into pricing strategies that reward greater use rather than a flat per-minute rate. This could help retain the high value customers and prompt other customers to use the service more.

![Classification_tree.png](./images/Classification_tree.png)

## For More Information

See the full analysis in the [Jupyter Notebook](./notebook.ipynb).

For additional info, contact Matt LeRoi at [mcleroi@gmail.com](mailto:mcleroi@gmail.com)

```
├── images
├── data
├── README.md
└── noteboook.ipynb
``` 
