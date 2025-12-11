## John Burn-Murdoch
"progressives have a birth rate problem": https://x.com/jburnmurdoch/status/1961388402449744241
![](jbm_fertility_ideology.png)
But is this a "correlation is not causation" situation? What if political affiliation here is just a proxy for residence in a high-cost area, since progressives tend to live in urban areas and coastal states? The "problem" then would be not with individual progressives but rather with the communities where they live, which make family life difficult and unaffordable.
If you control for region and/or cost of living, does the relationship still hold? Would it be possible to answer this question using microdata? GSS microdata with geographic information is only available through an application process because it's considered "sensitive". https://gss.norc.org/get-the-data.html It does seem like "region" is available in the public data.

> REGION (and its age 16 corresponding variable REG16) now only reflects the four census regions, and not the nine census divisions, being more accurate to its variable name. This change is due to updates in the disclosure review process (see Disclosure Review and Limitation). Moving forward, a new variable DIVISION will be available via the sensitive data process to look at the nine census divisions.


This implies that we may be able to find data at the census division level in a recent (though not latest) release? I don't need the most current data or ongoing monitoring to answer this question, since JBM's chart shows a trend that has been in place for several decades (since 1980).

Can query the data here, which does include census divisions as of 12/8/2025:
(note reference to release version 1)
https://sda.berkeley.edu/sdaweb/analysis/?dataset=gss24rel1

Assumed filters to reproduce JBM's chart:
* All adults age 35+?
* There's some amount of pooling across survey years being applied; I don't have the exact number, but pooling 7 survey instances (centered) results in lines that are broadly consistent.

## package installation and notes
We can use the `gssr` R package to download the full GSS dataset; by pinning a particular version, we can retrieve data that contains US Census divisions (version 0.7.0).
Commit SHA is `ed90704`, full line is `remotes::install_github("kjhealy/gssr@ed90704")`

[This blog post](https://blog.thecoatlessprofessor.com/programming/cpp/r-compiler-tools-for-rcpp-on-macos/index.html) explains how to install the R compiler tools for Rcpp on macOS, which is required for some `tidyverse` packages. Includes links to version-appropriate installers for dependencies like `gnufortran`.

## Related sources
JBM cites this blog post in his FT article: https://ifstudies.org/blog/the-conservative-fertility-advantage

The Institute for Family Studies blog post references this X post that plots a correlation between state-level political affiliation and fertility rate, from 2018: https://x.com/fuxianyi/status/1325550119677173760?s=20

## variables to look at
* `childs`: Number of children
* `finalter`: During the last few years, has your financial situation been getting better, worse, or has it stayed the same?
* `parsol`: Compared to your parents when they were the age you are now, do you think your own standard of living now
is much better, somewhat better, about the same, somewhat worse, or much worse than theirs was?
* `conbus`: (I am going to name some institutions in this country. As far as the people running these institutions are
concerned, would you say you have a great deal of confidence, only some confidence, or hardly any
confidence at all in them?) Major companies
* `conlegis`: (I am going to name some institutions in this country. As far as the people running these institutions are
concerned, would you say you have a great deal of confidence, only some confidence, or hardly any
confidence at all in them?) Congress
* `conmedic`: (I am going to name some institutions in this country. As far as the people running these institutions are
concerned, would you say you have a great deal of confidence, only some confidence, or hardly any
confidence at all in them?) Medicine
* `sexeduc`: Would you be for or against sex education in the public schools?
* `spanking`: Do you strongly agree, agree, disagree, or strongly disagree that it is sometimes necessary to discipline a child
with a good, hard spanking?
* `fear`: Is there any area right around here--that is, within a mile--where you would be afraid to walk alone at night?
* `relpersn`: To what extent do you consider yourself a religious person? Are you very religious, moderately religious,
slightly religious, or not religious at all?
* `sprtprsn`: To what extent do you consider yourself a spiritual person? Are you very spiritual, moderately spiritual,
slightly spiritual, or not spiritual at all?
* `notsmart`: (In your day-to-day life how often have any of the following things happened to you?) People act as if they
think you are not smart.
* `goodlife`: The way things are in America, people like me and my family have a good chance of improving our standard
of living -- do you agree or disagree?
* `meovrwrk`: Family life often suffers because men concentrate too much on their work.