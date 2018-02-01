---
title: Debugging unnaturally high correlations. When theory turns to practice
layout: post
category: posts
published: true
---


I could have named the title better and kept it more informative but then it would force  me to give away the suspense. This post is about a day at work, which left me grinning like a monkey, but at the same time embarassed in front of my CTO, Varun.

*Personality scores?*

Aspiring Minds's main product, AMCAT, is this huge array of standardized adaptive tests which are used in hiring talent by corporates. One of these tests is the Personality test, which has 5-6 submodules. 

I was supposed to pull out personality scores to support the candidate dataset I was working on to assess the current labour market in India. More on that later.  

There was some issue with the scores I had with me before and hence I had to freshly pull them out from the database which stored them in a serialized PHP dump. The horror. I wrote a hacky PHP script and got the results out after a few iterations.

Personality scores comprised of 6 modules,
 - nuero
 - extraversion
 - open to experience
 - agreeableness
 - conscientiousness
 - polychronicity (not interested, a lot of missing values)
 
I was excited to see whether they correlate to salariy of a candidate, so the first thing which I decided to see was the correlation matrix.

![corrs.PNG]({{site.baseurl}}/images/corrs.PNG)

The correlations with salary were decent, but the intercorrelations between the modules was way too high. I didn't want to add highly correlated features to the regression model and hence this was a red flag. I sent the matrix to Varun (Boss).

> There is something wrong with the data you've pulled, they shouldn't be so highly correlated. Can you plot the scatter/hexbin between these modules?

I started thinking. Was this irregularity an outcome of my PHP prowess. Or something else? Were the correlations Varun had seen before, the one he was expecting, based on scores before they were converted to zScores? I chose to believe the latter. 

I quickly started Googling, revisiting the pearson correlation formula and wether it would get affected by zScore. Well, it wouldn't. Z-scores linearly transform the data, and pearson's correlation remains the same as non-normalized data.
 
Damn. So it isn't this. 

I was eyeballing the data and found that there were a couple of rows which had all personality zScores as 0. What are the odds, the candidate was the exact mean in all the tests. The perfect average Joe.

So maaaaaaybe, its my PHP code. I was querying the db, taking the serialized object, unserializing it (yawn), and checking for a particular *dictionary* called zScores, using *isSet* and then storing the module scores if the *isSet* condition is met.


The bug was their zScores associative arrays existed, but they didn't have any score variables inside them.
So the *isSet* passed, but the zScore['pscore'] weren't getting any values. Typically, Python would break and throw an error. But PHP was throwing Notices which was shamelessly ignoring as long as the code worked. 

So the 0 values were supposed to be *nans*. I did the needful.

There were around a thousand in 12 thousand, all zero rows in the data, but would they be enough to make the correlation so high? The correlation virtually didn't change after removing the zeros. Why? The data I was working on was zScore normalized. The mean of the sample data is close to zero. Hence x - xmean terms of the correlation formula were hardly contributing anything in the first place. Well atleast that is sorted.

Argh. Problem still not solved. So I just decided to plot the scatters and hexbins and send them to Varun.

I opened a IPython notebook (which I loooove btw).


	data.plot(kind='scatter', x = 'agreeable', y = 'conscient')
	plt.title('agreeable vs conscient')
	plt.xlim((-7,7))
	plt.ylim((-7,7))

![a and c scatter.png]({{site.baseurl}}/images/a and c scatter.png)


	data.plot(kind='hexbin', x='agreeable', y='conscient', gridsize=400)
	plt.title('agreeable to conscient')
	plt.ylim((-3,3))
	plt.xlim((-3,3))

![a and c hex.png]({{site.baseurl}}/images/a and c hex.png)

I sent the plots to Varun.

> These don't look scatters of data which are showing .9 correlations. Something is odd. Are you sure you calculating the right correls?

Well, I tried them on Excel too. Same values.

What is wrong. Argh.

Why don't they look like scatters which are 0.9? Maybe because I have zoomed into them so much (the xlims) they don't like a straight line. Maybe if I zoom out, they will appear to be a line.

So, I replotted the scatters without the xlims.


	data.plot(kind='scatter', x = 'agreeable', y = 'conscient')
	plt.title('agreeable vs conscient')

![a and c scatter full.png]({{site.baseurl}}/images/a and c scatter full.png)

Now, yes, I guess you probably already figured the problem and are laughing at my naivety. I will make it better for you. I didn't. To me on zooming out, the dense cluster of data did look like a line. I went to Shashank's (moi manager) bay and told him, don't you think on zooming out it looks like a line? Isn't the 0.9 justified. I wasn't thinking. I had gone whack.

Shashank just kept looking at me. 
> What are those points out there?

I don't know. I **saw** them before. Probably buggy. Don't except someone to be 40 deviations away from the mean. Just a few points. Ignored them before. 

He just kept looking at me.

Oh.
###OH
##OH
#OH!

Fuck! I started grinning. Do you know what JUST happened?! Do you know what happened here? We just fell for the Anscombe's Quartet. WHOA.

For those who aren't introduced to these 4 chaps, Anscombe's Quartet contains 4 data sets which have almost the same descriptive stats like mean, variance and correlations but on plotting are very different from each other.

[Wikipedia](https://en.wikipedia.org/wiki/Anscombe%27s_quartet)
![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Anscombe%27s_quartet_3.svg/800px-Anscombe%27s_quartet_3.svg.png)

A part of me was feeling embarassed. But the other major part of me was fucking excited! I was grinning like a fucking idiot. I couldn't believe. Its like a phenomenon happened to me. It was classic Anscombe. 

The points which were at the 40+ range were skewing the correlation. You can imagine a line passing right through the center of the dense cluster near the origin to the small cluster of heavily biasing (1 percenters :P) badasses sitting at the 40+ range. It is similar to the *X4* picture in the above diagram.
They were bloating up the (x - xmean)(y-ymean) moment in the correlation formula.

My bestfriend had shared the wiki link of Anscombe's Quartet with me just a few weeks back, and I was amazed by it then. But then I forgot about it. But meeting one of the cases in the wild? Whoa. It was like a rite of passage. The last time I was similarly excited was when my Pandas code when out of memory for the first time. The first time I broke RAM memory while dealing with data. That was a special feeling. 

Lessons learned:
 - I was too much into the problem to think clearly, I should have probably taken a walk and tried to clear my head. 
 - Should have been careful with my PHP script especially when I am not used to it.
 - Shouldn't have ignored the outliers and put the limits on data before atleast once visualizing them in their entirety.
 - Shouldn't hold any assumptions about data.

But fuck it, I was tricked by the Anscombe's Quartet in the wild. It was worth the embarassment :D

Ps. So, I emailed Varun my final conclusion, an email which couldn't decide if it was embarassed or excited.

His reply,
> ARGH
