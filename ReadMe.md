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

## notes on tools
This is more for my information, a collection of notes regarding R usage in VSCode/Cursor.

### Jupyter notebooks
Generally I like Jupyter notebooks, largely because they combine markdown, execution code, and *cell outputs*, which makes them an easy format to parse into a blog post. In contrast, R Markdown files don't include cell outputs-- some tools like RStudio will render outputs like visualizations inline with the code, but the outputs aren't part of the file itself. 

* While the Jupyter VSCode extension does allow using an R kernel, there's no data viewer support and variables are not listed like they are with Python notebooks. There was an [issue regarding this in the VSCode extension repo](https://github.com/microsoft/vscode-jupyter/issues/5264), but it died due to lack of interest. 
    * This appears to be due to an underlying issue with the IRKernel, because variables are also not visible when launching jupyter lab in a browser.
* [All of the Quarto examples regarding `.ipynb` files assume you're using Python.](https://quarto.org/docs/tools/vscode/notebook.html)

### output rendering in VSCode/Cursor
Running R Markdown files in VSCode/Cursor renders outputs like tables to the terminal; plots are rendered to temporary `png` files unless the [httpgd backend](https://github.com/nx10/httpgd) is installed, which currently needs to be installed from github via `remotes` (at least on my machine). The `httpgd` rendering backend allows figures to be resized, but doesn't respect the figure sizes set in the R Markdown file code block comments, which is a net negative because it makes it harder to determine exact positioning in the final rendered output.

R Markdown files in notebook mode may include persistent outputs that are stored locally in a separate file, but it doesn't seem like this format works with the VSCode R extension?


### tools: conclusion
It seems like there's no way around having to use RStudio for interactive development and Cursor/VSCode for AI assistance. It's the only environment that properly respects figure sizes; it's annoying that inline outputs are cleared whenever the file is externally modified (e.g. by an AI agent in Cursor/Claude Code), but that doesn't clear the RStudio working session's memory, so re-generating outputs is not awful.