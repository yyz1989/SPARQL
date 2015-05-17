SPARQL client for R
===================

### Introduction

This is an upgraded SPARQL client for R. The original package can be found at **[cran/SPARQL](https://github.com/cran/SPARQL)** authored by **Willem Robert van Hage (willem.van.hage at synerscope.com)**, with the lastest release published as R library at **[CRAN](http://cran.r-project.org/web/packages/SPARQL/index.html)** at the end of 2013. official reference manual can also be found at the same page.

Compared to the original version, this one is capable of firing SPARQL queries through HTTP POST request, in case that the query body exceeds the length limit of an HTTP GET request at the SPARQL endpoint side. In order to get compatible with the original version and minimize code changes, the trigger to use POST method is wrapped into an existing parameter *curl_args*, as shown in the examples. *curl_args* is indeed an arguments list passing to Curl and the trigger statement *style="post"* also looks like a Curl argument used to send POST requests. However, here this setting is only used for convention, and this statement will be removed from the argument list before sent to Curl. What really makes the query to be sent by POST is using *postForm* instead of *getURL*.

### Examples

*Query by GET*

    d <- SPARQL(url="http://services.data.gov.uk/reference/sparql",
                query="SELECT * WHERE { ?s ?p ?o . } LIMIT 10",
                ns=c('time','<http://www.w3.org/2006/time#>'))

*Query by POST*

    d <- SPARQL(url="http://services.data.gov.uk/reference/sparql",
                query="SELECT * WHERE { ?s ?p ?o . } LIMIT 10",
                ns=c('time','<http://www.w3.org/2006/time#>'),
                curl_args=list(style="post"))
