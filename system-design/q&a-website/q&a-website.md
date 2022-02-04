# Question and Answer Website

## Functional requirements
    - A user should be able to post a question and see it on the website almost immediately (1-2s)  
      It's fine if it takes up to 5s to become visible to other users
    - A user should be able to upvote/downvote the answer/question
    - A user should be able to see most popular, most recent questions on the home page

## Technical requirements
    - 10 mln users (after a year)
    - it's a read-heavy application. We expect 500 mln reads per year
    - 5 mln questions and 20 mln answers (after a year)
    - questions/answers should be 2 pages max
    - restricted to one geographic location
    - * can you do it with your own hardware - not utilizing AWS etc.

## Analysis
    A page of text is approx 2KB. On average, a question or answer would not exceed 1 page.  
    Let's say an object - either q or a - is 2KB. To store 5 mln Q and 20 mln A we will need   
    25 mln * 2KB = 50 000 000 KB = 50 GB of text data. To give ourselves some wiggle room, let's provision  
    100 GB. We might wanna store some user metadata, upvotes, etc. This could easily fit on one HDD. We still  
    want to maintain a backup copy of the data, so we will need at least 2 HDDs

    Let's estimate bandwidth. Considering that we need to support 500 mln reads per year, that would be ~16QPS.
    Let's say we also have 8QPS for write requests. To be on the safe side and account for spikes in traffic, let's  
    prepare for 100 QPS. The request size is approx 2KB so the throughput we're looking for here is 2KB*100 = 0.2 MBps  
    
    

    

    
    
    
    



