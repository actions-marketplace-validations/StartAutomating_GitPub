---

title: Publish GitPubJekyll creates summary pages
author: StartAutomating
sourceURL: https://github.com/StartAutomating/GitPub/issues/42
tag: enhancement
---
# Publish-GitPubJekyll creates summary pages

Jekyll's great, and yet it doesn't do _everything_ right.

One thing that's annoying out of the box is the fact that a Jekyll site does not have a summary page for posts in a given year, month, or day.

This means that segments of a given post's URL do not work.

Luckily, this is something we can work around.

Jekyll allows us to create pages with a permalink in their front matter.

This allows us to create each URL segment, provided we know all of the years, months, and days we have posts.

In order to this, we actually need a fair number of additional parameters on Publish-GitPubJekyll.

However, only one parameter should be required to make this work.

If -NoSummary is not found, Publish-GitPubJekyll should look thru all of the files that meet start with YYYY-mm-DD (collecting all posts by date).  Then, Publish-GitPubJekyll should go thru each post date and generate a file.

The files should be generated according to three parameters:

|Parameter|Aliases|
|-|-|
|-YearlySummary|-YearSummary, -AnnualSummary|
|-MonthlySummary|-MonthSummary|
|-DailySummary|-DaySummary|

These parameters should have pretty decent defaults, so you shouldn't really need to think about this when using GitPub.  However, if you wanted to override these parameters with your own custom summaries, here's how you'd do so.

You can override these parameters a few different ways:

* In your GitHub action's .PublishParameters input,
* In the -Parameters parameter for Publish-GitHub
* Directly providing them to Publish-GitPubJekyll


For every day, month, and year there is a post, these summary files will be generated by expanding the string content of these parameters.  This means if you wanted to provide a PowerShell variable or expression here, you could.  By default, Publish-GitPubJekyll will define $Year $Month and $Day (as a "yyyy", "MM", "dd").

To prove things are working as they should, here are some live examples on GitPub's own GitHub Page

* [all posts in 2022](https://gitpub.start-automating.com/2022/)
* [all posts in October 2022](https://gitpub.start-automating.com/2022/10)
* [all posts on October 10th, 2022](https://gitpub.start-automating.com/2022/10/10)

Happy Posting