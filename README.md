# Spam Filtering with Naive Bayes Classifier

## Introduction
This project implements a simple Spam Filter using the Naive Bayes Classifier. The Naive Bayes algorithm is a probabilistic classifier that applies Bayes' theorem with strong independence assumptions between features. It is particularly suited for spam filtering by evaluating the likelihood of certain words appearing in spam versus non-spam emails.

## Dataset description:
The data in this project was taken from [Exercise 6: Naive Bayes - Machine Learning - Andrew Ng](http://openclassroom.stanford.edu/MainFolder/DocumentPage.php?course=MachineLearning&doc=exercises/ex6/ex6.html).

In this example, the data has been processed, and is a subset of the [Ling-Spam dataset](https://www.kaggle.com/datasets/mandygu/lingspam-dataset).

This data set includes a total of 960 English emails, separated into training and testing sets at a ratio of 700:260, 50% of each set are spam emails.

The data in this dataset has been handled quite nicely. The processing rules are as follows:

1. **Eliminate stop word**: Words that appear frequently such as 'and', 'the', 'of', ... are removed.

2. **Lemmatization** : Words with the same 'root' are brought into the same category. For example, 'include', 'includes', 'included' are all referred to as 'include'. All words have also been converted to lower case (not capital case).

3. **Remove non-words** : Numbers, punctuation, 'tabs' characters, 'newline' characters have been removed.

Below is an example of a non-spam email, **before being processed**:
```
Subject: Re: 5.1344 Native speaker intuitions
  
The discussion on native speaker intuitions has been extremely interesting, 
but I worry that my brief intervention may have muddied the waters. I take 
it that there are a number of separable issues. The first is the extent to
which a native speaker is likely to judge a lexical string as grammatical 
or ungrammatical per se. The second is concerned with the relationships 
between syntax and interpretation (although even here the distinction may 
not be entirely clear cut). 
```

and after being processed :
```
re native speaker intuition discussion native speaker intuition extremely 
interest worry brief intervention muddy waters number separable issue first 
extent native speaker likely judge lexical string grammatical ungrammatical 
per se second concern relationship between syntax interpretation although 
even here distinction entirely clear cut
```

And here is an example of email spam after being processed :
```
financial freedom follow financial freedom work ethic extraordinary desire 
earn least per month work home special skills experience required train 
personal support need ensure success legitimate homebased income 
opportunity put back control finance life ve try opportunity past 
fail live promise
```

We see that in this paragraph there are words such as: financial, extraordinary, earn, opportunity, ... which are words often found in spam emails.

In the folder **ex6DataPrepared.zip** , we see the files:
```
test-features.txt
test-labels.txt
train-features-50.txt
train-features-100.txt
train-features-400.txt
train-features.txt
train-labels-50.txt
train-labels-100.txt
train-labels-400.txt
train-labels.txt
```
Corresponding to files containing data of the training set and test set. The file train-features-50.txt contains data from a condensed training set with only a total of 50 training emails.

Each file \*labels\*.txt contains many lines, each line is a 0 or 1 character indicating the email is non-spam or spam.

Each file \*features\*.txtcontains many lines, each line has 3 numbers, for example:
```
1 564 1
1 19 2
```
where the first number is the index of the email, starting from 1; The second number is the order of the words in the dictionary (2500 words in total); The third number is the number of that word in the email in question. The first line says that in the first email, the 564th word in the dictionary appears once. Saving data like this helps save memory because an email usually does not contain all the words in the dictionary but only a small amount, we only need to save non-zero values.

If we represent the feature vector of each email as a row vector of dictionary length (2500), then the first line says that the 564th component of this vector is equal to 1. Similarly, the 19th component of this vector equal to 1. If not present, other components are defaulted to 0.

Based on this information, we can proceed with programming with the sklearn library.

## Results


