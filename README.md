# Spam Filtering with Naive Bayes Classifier

## Introduction
This project implements a simple Spam Filter using the Naive Bayes Classifier. The Naive Bayes algorithm is a probabilistic classifier that applies Bayes' theorem with strong independence assumptions between features. It is particularly suited for spam filtering by evaluating the likelihood of certain words appearing in spam versus non-spam emails.

## Dataset Description:
The data for this project was sourced from [Exercise 6: Naive Bayes - Machine Learning - Andrew Ng](http://openclassroom.stanford.edu/MainFolder/DocumentPage.php?course=MachineLearning&doc=exercises/ex6/ex6.html) and is a subset of the [Ling-Spam dataset](https://www.kaggle.com/datasets/mandygu/lingspam-dataset).

This dataset includes a total of 960 English emails, divided into training and testing sets with a ratio of 700:260. Each set contains 50% spam emails.

The dataset has been preprocessed as follows:

1. **Eliminate Stop Words**: Commonly occurring words such as 'and', 'the', 'of', etc., have been removed.

2. **Lemmatization**: Words that share the same root have been grouped together. For instance, 'include', 'includes', and 'included' are all converted to 'include'. All words have also been converted to lowercase.

3. **Remove Non-Words**: Numerical digits, punctuation, tab characters, and newline characters have been removed.

Below is an example of a non-spam email **before being processed**:
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

And after being processed:
```
re native speaker intuition discussion native speaker intuition extremely 
interesting worry brief intervention muddy waters number separable issue 
first extent native speaker likely judge lexical string grammatical 
ungrammatical per se second concern relationship between syntax 
interpretation although even here distinction not entirely clear cut
```

Here is an example of an email classified as spam after processing:
```
financial freedom follow financial freedom work ethic extraordinary desire 
earn at least per month work from home no special skills or experience 
required we train provide personal support needed to ensure your success 
legitimate home-based income opportunity take back control of your finances 
life you've tried opportunities in the past that didn't live up to their 
promises
```

Notice the presence of words such as 'financial', 'extraordinary', 'earn', and 'opportunity', which are commonly found in spam emails.

Within the folder **ex6DataPrepared.zip**, we find files including:
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
These correspond to the data for the training and testing sets. The file `train-features-50.txt` contains data from a condensed training set of only 50 emails.

Each `*labels*.txt` file contains multiple lines, with each line consisting of a single character, 0 or 1, indicating whether the email is non-spam or spam, respectively.

Each `*features*.txt` file contains multiple lines, each with three numbers, for example:
```
1 564 1
1 19 2
```
The first number is the index of the email, starting from 1; the second number is the position of the word in the dictionary (which contains a total of 2500 words); the third number is the frequency of that word in the specific email. The first line indicates that in the first email, the 564th word in the dictionary appears once. This sparse data representation is memory efficient as emails typically contain only a small subset of the dictionary's words, and only non-zero occurrences are stored.

If we represent the feature vector of each email as a row vector of the dictionary length (2500), then the first line indicates that the 564th component of this vector is 1. Similarly, the 19th component is 2. Components not mentioned default to 0.

With this information, we can proceed with the implementation using the `sklearn` library.

## Results


