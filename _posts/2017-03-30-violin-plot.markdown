---
layout: post
title: "Visualizing data with Violin Plots and Python"
excerpt: "Say you are analyzing customer churn of a telecom operator. You want to visualize the distribution 
of total phone call length across those customers who stayed and those who didn't.
The good old Box and Whisker plot might do the trick. But it has its downsides - it hides the probability density of the variable. 
Can we do better?"
category: Machine Learning
tags: [exploratory-data-analysis, plot, seaborn]
comments: true
image:
  feature: violin-plot/violin-cello.jpg
---


Say you are analyzing customer churn of a telecom operator. You want to visualize the distribution 
of total phone call length across those customers who stayed and those who didn't.
The good old Box and Whisker plot might do the trick. But it has its downsides - it hides the probability density of the variable. 
Can we do better?


## Violin Plot

A violin plot allows displaying _both_ distribution _and_ probability density of a numerical variable. It's a combo of a Box Plot and a Density Plot that is rotated to show data distribution [[1]].


## An example in Python

Let's plot an example using Python, Jupyter, Pandas [[2]] and Seaborn [[3]]. We'll take this [[4]] telecom churn dataset
and plot `total day minutes` against the target variable. Let's build both a box plot and a violin plot side-by-side,
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


![Box and Whiskers vs Violin Plot]({{ site.url }}/img/violin-plot/violin-plot-vs-boxplot.jpg)

## Pros and Cons

Pros:

+ Shows summary statistics of a given variable;
+ Unlike a box plot, shows the full distribution of the data. This allows for easy spotting of multimodal data.

Cons:
- According to Wikipedia [[5]], violin plots are less known to wide audience. Therefore, their meaning may be harder to grasp.

While being relatively unknown may be something to consider, I believe we shouldn't discard violin plots on this ground alone. After all, popularity isn't the most important evaluation criterion, nor is it set in stone.
Take Miley Cyrus for example. Is she more popular nowadays than e.g. Linus Pauling? Probably. Who did more good for our society? I'll let the interested readers answer that question on their own :)

## Cool, where do I learn more?

Have a look at Seaborn violin plot documentation [[6]]. It includes more examples and is 
pretty accessible.


[1]: http://www.datavizcatalogue.com/methods/violin_plot.html
[2]: http://pandas.pydata.org/
[3]: https://seaborn.pydata.org/
[4]: https://bigml.com/user/francisco/gallery/dataset/5163ad540c0b5e5b22000383
[5]: https://en.wikipedia.org/wiki/Violin_plot
[6]: https://seaborn.pydata.org/generated/seaborn.violinplot.html?highlight=violin#seaborn.violinplot