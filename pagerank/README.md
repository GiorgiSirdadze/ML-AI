# PageRank Implementation

Okay, so I had to implement PageRank, which is basically how Google figures out which web pages are important.  It's all about links and how they connect pages.  I did it in a few different ways:

## 1. `transition_model(corpus, page, damping_factor)`

This function is like the heart of the whole thing. It figures out the probability of going from one page to another.

* **What it does:** It takes a web page (`page`) and a bunch of other pages (`corpus`) and tells you the chances of clicking on a link to get to another page.
* **How I did it:**
    * I made a dictionary (`probs`) to store the probabilities.
    * If the current page has links, I use those as possible destinations.
    * If it doesn't (a "dangling" page), I say you could go anywhere.
    * Then, I calculate the probabilities: there's a chance you'll jump to a random page (`1 - damping_factor`), and a chance you'll follow a link (`damping_factor`).  I split the link-following chance evenly among the links.

## 2. `sample_pagerank(corpus, damping_factor, n)`

This is a way to estimate PageRank by simulating a bunch of random "web surfers" clicking around.

* **What it does:** It simulates people clicking links and counts how often they land on each page.
* **How I did it:**
    * I start on a random page.
    * I loop `n` times, and each time:
        * I use `transition_model` to figure out where to go next.
        * I randomly choose the next page based on those probabilities.
        * I keep track of how many times each page is visited.
    * Then, I normalize the counts to get the PageRank scores.

## 3. `iterate_pagerank(corpus, damping_factor)`

This is the more "proper" way to calculate PageRank, by repeatedly updating the PageRank values until they stabilize.

* **What it does:** It calculates the PageRank by iteratively updating the scores until they don't change much.
* **How I did it:**
    * I start by giving all pages the same initial PageRank.
    * I keep looping until the PageRank values don't change much anymore (using a `threshold`).
    * In each loop, I calculate a new PageRank for each page based on the PageRank of the pages that link to it.
    * I handle "dangling" pages (pages with no links) by evenly distributing their PageRank.
    * I stop when the PageRank values converge.

## Honestly...

* The `iterate_pagerank` method is probably more accurate.
* The `sample_pagerank` method is faster for large datasets.
* I'm still figuring out all the little details of PageRank, like how to handle different link structures.
