---
layout: post
title: Happiness and Taxation 
---

![](/images/happiness_and_taxation/header.jpg)

The 20-something liberal policy concerns in the United States seem to revolve around a central theme: Scandinavia. It is well known that these countries consistently find themselves at the top of the annual [World Happiness Reports](https://en.wikipedia.org/wiki/World_Happiness_Report), and it’s easy to see why. Not only do you get free education, but you get PAID to go to University. You have access to free healthcare from the moment you’re born until you die. They all [rank very favorably as far as income inequality is concerned](https://en.wikipedia.org/wiki/List_of_countries_by_income_equality#Gini_coefficient.2C_after_taxes_and_transfers). **There’s a lot to like**. Far too bloody rainy, though (he says, living in England at the time of this writing).

The arguments against a “Scandinavian America”, however, are **valid**. The countries are much smaller than the United States, allowing greater ease of governance. Additionally, the populations are incredibly homogenous. Not that this *should* be a problem, and indeed I very truly hope to see the day that it is not, but the world still suffers from inherent biases. And perhaps most importantly, these social programs can only be supported through high taxation. Indeed, these countries have some of the [highest tax rates in the world by almost all measures](https://data.oecd.org/tax/tax-revenue.htm#indicator-table). The United States has had a [long history of thinking they pay too much tax](http://www.gallup.com/poll/1714/taxes.aspx). Never mind that they are already way on the low end of most developed nations.

But this led me to ask the question—**Is there a correlation between various taxation metrics and happiness index scores**? Well, why don’t we find out?

Wikipedia was so kind as to give me [2013 – 2015 averages for the happiness indices](https://en.wikipedia.org/wiki/World_Happiness_Report#2013-2015_averaged_ranking.5B6.5D) of various countries. I preferred more data points over a longer period of time rather than the most recent figures as a hedge of sorts. To compare these to tax data, I used the [OECD](https://data.oecd.org/tax/tax-wedge.htm#indicator-chart), which tracks a variety of metrics.

Gathering detailed tax information on all countries is completely infeasible and ultimately unhelpful (let’s not get started on how much governmental corruption there is in the world right now), so I only considered OECD countries in this analysis.

I plotted every metric the OECD tracks to happiness. They don’t all necessarily tell an interesting story, but I made the graphs so you may as well have access to them if you see something I don’t. The formatted, averaged data can be found at the bottom of the article in a CSV file.

### Overview: Happiness Correlations
Instead of making you read and interpret the proceeding graphs, here’s a table of how each taxation metric correlates to the country’s happiness index.

![](/images/happiness_and_taxation/correl-table.png)

Using the guidelines in [this post by Andrews University](https://www.andrews.edu/~calkins/math/edrm611/edrm05.htm), we obtain the following Correlation strengths:

+ **Moderate Correlation**
  + Total Tax Revenue: Per Capita
  + Personal Income: as % of GDP
  + Personal Income: as % of Total Tax
+ **Low Correlation**
  + Corporate: as % of GDP
  + Corporate: as % of Total Tax (rounding)
  + Payroll: as % of GDP
  + Payroll: as % of Total Tax
+ **Little to No Correlation**
  + Total Tax Revenue: as % of GDP
  + Property: as % of GDP
  + Property: as % of Total Tax
  + Social Security: as % of GDP
  + Wedge: % Labor Cost
+ **Low Negative Correlation**
  + Goods and Services: as % of GDP
  + Goods and Services: as % of Total Tax
  + Social Security: as % of Total Tax
So we don’t have any particularly strong correlations, but there is one particular observation I want to make regarding this overview before moving on to each metric individually. **All taxations with negative correlations to happiness are [regressive taxes](https://en.wikipedia.org/wiki/Regressive_tax)**. This means that they are a set percentage, irrespective of income. This is as opposed to progressive taxation, in which higher income individuals pay a higher percentage proportionally. We’ll explore a bit more about what these mean and additionally analyses in each respective section.

### Total Tax Revenue
![](/images/happiness_and_taxation/tax-rev-pair.png)

Happiness Correlations: 0.126 & 0.623, respectively

The OECD states “[t]otal tax revenue as a percentage of GDP indicates the share of a country’s output that is collected by the government through taxes. It can be regarded as one measure of the **degree to which the government controls the economy’s resources.**” Consequently, I was quite surprised by this low correlation. The common utopian ideal, at least as I’ve always understood it, maintains a central theme of communistic principals as a means of achieving the egalitarian ideal. But this would seem to indicate that happiness and government control of resources are not correlated. Score one for capitalism?

Even more surprising is the fact that, while % of GDP contains no correlation, the second highest correlation of all the measures can be found by looking at total tax revenue per capita. **Take Luxembourg out of the equation and the correlation jumps to .721, jumping into the high correlation classification.**

### Personal Income Tax
![](/images/happiness_and_taxation/pers-inc-pair.png)

Happiness Correlations: 0.562 & 0.634, respectively

Man, Denmark sure seems to like that upper right-hand corner of the graphs. Taking Denmark out of the correlation equations have no significant effect. Moderately positive correlations for both of these metrics. Progressive tax.

### Corporate
![](/images/happiness_and_taxation/corp-pair.png)

Happiness Correlations: 0.439 & 0.300, respectively

Small positive correlation. I think this makes sense. Too high of corporate taxation would presumably lead to less business development and less employment, which would contribute to less happiness one would think. However, this can be a large revenue pool for taxation, and many social services rely on corporate taxes. So it’s a double edged sword. Also, corporations aren’t people as we all know ([right…?](https://en.wikipedia.org/wiki/Citizens_United_v._FEC)), so they may not be too upset. Executives may worry about it, but the vast number of their employees’ happiness is not going to be severely affected by it. Most people simply serve to gain from higher corporate tax.

### Goods and Services
![](/images/happiness_and_taxation/gas-pair.png)

Happiness Correlations: -0.335 & -0.464, respectively

Ah, now this makes some sense to me. Higher taxations on goods and services means less access, generally speaking. Additionally, these taxes are completely regressive. But, not a strong negative correlation by any means. Does not appear to be a good indicator.

### Property
![](/images/happiness_and_taxation/prop-pair.png)

Happiness Correlations: 0.206 & 0.191, respectively

Safe to say there is no meaningful correlations here. I have nothing more to say on the matter.

### Social Security
![](/images/happiness_and_taxation/soc-sec-pair.png)

Happiness Correlations: -0.281 & -0.421, respectively

Meaningful? I’m not sure. But if so, it would seem that the US is not alone in an ultimately ineffective Social Security system. Or at least communication of its benefits. Hard to say.

### Payroll
![](/images/happiness_and_taxation/payroll-pair.png)

Happiness Correlations: 0.369 & 0.421, respectively

Not a lot of countries with Payroll tax, so I don’t think this is a particularly important metric. Not enough data. But if we assume validity, I am quite surprised by this result.

The US Congressional Budget Office states: “CBO assumes—as do most economists—**that employers’ share of payroll taxes is passed on to employees** in the form of lower wages than would otherwise be paid. Therefore, the amount of those taxes is included in employees’ income, and **the taxes are counted as part of employees’ tax burden**.” So this is a regressive tax on employees. I would have assumed this would have had a negative correlation. Again, not a large amount of samples.

### Wedge
![](/images/happiness_and_taxation/wedge.png)

Happiness Correlation: -0.267

The OECD defines Wedge as: “the ratio between the amount of taxes paid by an average single worker (a single person at 100% of average earnings) without children and the corresponding total labour cost for the employer. The average tax wedge measures the extent to which tax on labour income discourages employment. This indicator is measured in percentage of labour cost.”

I’m not entirely sure I understand this metric, so saying something to the effect of “it doesn’t seem surprising that discouragement of employment through taxation has at least a slight negative correlation” is about as good as it’s going to get. Let’s go with that.

### Concluding Thoughts
You can spin tax data to fit whatever story you may want, but there does seem, to me at least, that there is some information to be gleaned from this. Primarily, the progressive v. regressive tax angle is worth exploring more. Additionally, the business v. personal tax relationships are I know there is plenty more analysis to be had, so please offer up some thoughts in the comments section below!

### Data
Data can be found [here](/assets/data.csv).

To structure the data, I downloaded the CSV files for the selected years from the [OECD](https://data.oecd.org/tax/tax-revenue.htm#indicator-chart). I then deleted all columns I didn’t need and grouped the same metrics together in excel. If there was a missing year in one but not the other, I used the average of the other two years to fill in the missing information. I then created an [R Script](https://pastebin.com/iid0Uvvt) to do some further preprocessing and create the graphs.
