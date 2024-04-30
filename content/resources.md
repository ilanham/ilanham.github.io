---
title: Resources
date: "2024-04-17T12:23:41-04:00"
draft: false
---

This page is between an *X Awesome List* you'd find on GitHub and a browser bookmarks export to HTML. Some are pages I don't want to forget but can't find in my stack of bookmarks/Notion DB.

### Data
- [A 2020 Reader's Guide to The Data Warehouse Toolkit](https://www.holistics.io/blog/how-to-read-data-warehouse-toolkit/)
  - If you're working with a more traditional on-premises data warehouse, you likely work with fact & dimension tables. There's plenty still relevant, but some stuff doesn't apply in the current cloud/distributed era.

### SQL Server
- [Take Care When Scripting Batches - Michael J Swart](https://michaeljswart.com/2014/09/take-care-when-scripting-batches/)
  - I use a technique in this blog post pretty often when I'm A) working on SQL Server and B) need to update massive tables with minimal locking. This post has a [follow-up sequel](https://michaeljswart.com/2022/09/batching-follow-up/) that explains more variations. Most of these examples are specific to SQL Server, but would likely apply when using a B+Tree structure.
- [Table Partitioning in SQL Server - The Basics - Catherine Wilhelmsen](https://www.cathrinewilhelmsen.net/table-partitioning-in-sql-server/)
  - There might be more blog posts written about SQL Server's implementation of Table Partitioning than instances of partitioned tables. For me, this has been my go-to refresher when I need to remind myself how the range boundaries work.
- [Microsoft SQL Server Versions List](https://sqlserverbuilds.blogspot.com)
  - For a while, this was the defacto source of updates released for SQL Server. Microsoft made an official version with a similar layout (see below), but I still reference this when I need to see the different CVE's included with a Cumulative Update. Infrequent, but sometimes useful.
- [Latest updates and version history for SQL Server - Microsoft Learn](https://learn.microsoft.com/en-us/troubleshoot/sql/releases/download-and-install-latest-updates)
  - Aforementioned official update release list. Use this when needing to look up official releases and builds.
- [SQL Server Terms Translated into PostgreSQL](https://www.red-gate.com/blog/sql-server-terms-translated-into-postgresql)
  - Helpful when learning PostgreSQL and coming from SQL Server.

### Python
- [Python F-Strings Number Formatting Cheat Sheet - Brian Allan](https://cheatography.com/brianallan/cheat-sheets/python-f-strings-number-formatting/)
- [Python Charts by R Coder](https://python-charts.com)
  - A nice gallery of different chart types and sample code for the different visualization libraries in the Python ecosystem (pick your favorite).
- [Pandas Tutor](https://pandastutor.com)
  - From the page: "Pandas Tutor lets you write Python pandas code in your browser and see how it transforms your data step-by-step." I also like there's a complimentary version for R code too.

### R
- [Rseek](https://rseek.org)
  - If you've had to search for a single item related to the R programming language in a search engine, you know how tough that is. Use this instead.
- [Tidy Data Tutor](https://tidydatatutor.com)
  - Same as Pandas Tutor above, only for the tidyverse.
- [R Charts by R Coder](https://r-charts.com)
  - Similar to Python Charts above, but for R code and libraries.
- [GitHub: rstudio/cheatsheets](https://github.com/rstudio/cheatsheets/tree/main)
  - GH repo of [https://posit.co/resources/cheatsheets](https://posit.co/resources/cheatsheets)

### Regular Expressions
- [RexEgg Cheat Sheet](https://www.rexegg.com/regex-quickstart.html)
  - I don't know if this is the best site out there for Regular Expressions, but it's what I used to learn it roughly 10 years ago, and I still come back to it to remember lookarounds when I forget the syntax (again)
- [RegExr](https://regexr.com)
  - A web-based regular expression parser. I use this to sanity check my capture strings in case something isn't working locally.