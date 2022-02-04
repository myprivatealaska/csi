1. While we have 500 mln reads per year, we don't know the traffic pattern - it could be  
   exponential - this is something to consider when estimating RPS
2. What are some points along the spectrum from "one server" to "highly available setup across multiple  
   AZ"?
   - Move DB to a different machine
   - Introduce a caching layer
   - Add a load balancer  
3. How to quickly validate back-of-the-envelope estimations?
   - Provision a PostgreSQL instance in the cloud, write a simple program to insert/read from the tables  
    benchmarking the time
   - Use iotop util
   - Run PostgreSQL with some tracing options to see how many IOPS is needed for a write  
   - Load testing webserver with scripts
        - https://k6.io/
        - https://github.com/tsenart/vegeta
4. Learnings from Stack Overflow:
   http://highscalability.com/stack-overflow-architecture
   
    
