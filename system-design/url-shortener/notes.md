1. What if traffic only comes in during work hours? Should we plan for more QPS?
2. Pushback: here's what it would cost to do this or that. (AWS costs, engineering costs)
3. What kind of blowup can happen (disk) ? Look into the I/O estimates more! 
 _Considering disk I/O we can only serve 200 link requests per sec. on one machine_ 
4.By the time you generate a million links, you'll start to see collisions. (Birthday paradox)
5 Bitly actually uses an offline generation service

General Recommendations
1. Walk thru the lifecycle of a request
2. What features/SLOs are we supporting, various tradeoffs
3. Talk about the data shape. indexes
4. What are the biggest risks/unknowns
5. How much will that cost?

