# GSS Explorations in R

I came across this chart from John Burn-Murdoch in a post asserting that ["progressives have a birth rate problem"](https://x.com/jburnmurdoch/status/1961388402449744241):
![](./ideology_fertility/jbm_fertility_ideology.png)

> For all the talk of a general fall in births, the drop is overwhelmingly driven by people on the left having fewer kids. By ceding the topic of family and children to the right, progressives risk ushering in a more conservative world.

As both a self-identified progressive and a parent, the sweeping generalization in the figure, as well as the moralizing tone of the accompanying tweet, struck a chord. I grew up around many peers who faithfully inherited their parents' political views, mostly on the right. While most of my friends from college are progressives, few of them have children.

## looking for alternative explanations
My first reaction to JBM's figure was to rationalize alternative explanations. For instance, liberals are more likely than conservatives to live in high-cost urban areas, so affordability might be a factor constraining parenthood.

My explorations are ongoing-- ultimately, I'll post whatever conclusions I reach [on my blog](https://aaronjbecker.com), whether they support or refute the claims advanced by JBM and other more explicitly conservative commentators.

**This is a work in progress.**

My preferred language is unquestionably Python, but my curiosity about the GSS dataset drove me into the arms of R. When it comes to statistical analysis based on survey data, R is a much more natural fit, and its package ecosystem even includes [data loaders for the GSS data](https://github.com/kjhealy/gssr).

I haven't used R extensively in more than a decade, so I'm leaning on Claude while I come up to speed.