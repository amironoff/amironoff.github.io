---
layout: post
title: "Visualizing data with Violin Plots"
excerpt: "Say you are analyzing customer churn. You want to visualize the distribution 
of total phone call length across those customers who stayed and those who didn't.
You think of using the good old Box and Whisker plot. But that doesn't give you the probability density of the variable. 
What do you do?"
category: Machine Learning
tags: [exploratory-data-analysis, plot, seaborn]
comments: true
image:
  feature: violin-plot/violin-plot-vs-boxplot.jpg
---

Say you are analyzing customer churn of a telecom operator. You want to visualize the distribution 
of total phone call length across those customers who stayed and those who didn't.
You think of using the good old Box and Whisker plot. But that doesn't give you the probability density of the variable. 
What do you do?

## Violin Plot

A violin plot allows displaying _both_ distribution _and_ probability density of a numerical variable.  
It is a combination of a Box Plot and a Density Plot that is rotated to show data distribution [[1]].

## A Python example

Let's plot an example using Python, Jupyter, Pandas [[2]] and Seaborn [[3]]. We'll take this [[4]] telecom churn dataset
and plot `total day minutes` against the target variable. To show what a violin plot brings to the table,
let's build both a box plot and a violin plot side-by-side,
so that you can compare the descriptive power of each.

{% highlight python %}

%pylab inline
import pandas as pd
import seaborn as sns
df = pd.read_csv("data/telecom-churn.csv")
_, axes = plt.subplots(1, 2, sharey=True, figsize=(12,6))

sns.boxplot(x='churn', y='total day minutes', data=df, ax=axes[0]);
sns.violinplot(x='churn', y='total day minutes', data=df, ax=axes[1]);

{% endhighlight %}

Here is the result:
<br />
![Box and Whiskers vs Violin Plot]({{ site.url }}/img/violin-plot/violin-plot-vs-boxplot.jpg)


## Alternatives

TBD

## Pros and Cons

TBD

[1]: http://www.datavizcatalogue.com/methods/violin_plot.html
[2]: http://pandas.pydata.org/
[3]: https://seaborn.pydata.org/
[4]: https://bigml.com/user/francisco/gallery/dataset/5163ad540c0b5e5b22000383