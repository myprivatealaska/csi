### Image Hosting Service

## Functional Requirements
- Users should be able to upload an image however large and share it with others
- After some time a user should be able to see different versions of their image - thumbnail size,   
  small, medium, large, original. 
- Expiration time ~1year

## Technical Requirements
- 0.5 mln image uploads per day
- 5 mln views per day
- Latency 
    - 10 sec before an uploaded image is shareable
    - 300 ms p95 globally
- Availability
    - 99.0 writes
    - 99.9 reads
    
## Load Estimation

Let's assume that an average image is 1 MB.
Considering that we have 0.5 mln uploads per day, that gives us 500 000 / 24 / 60 / 60 = 5.7 WPS.  
Write bandwidth then would be 1 * 5.7 ~ 6 MB/sec
Assuming expiration time of 1 year, we will need 0.5 mln * 365 = 182 500 000 MB = 182.5 TB of storage  
to store the original versions of the files.

As for the reads, since we have 5 mln views per day, we're looking at 5000000 / 24 / 60 / 60 = 57 RPS.  
Read Bandwidth is 57 MB/sec

## Design

Considering that we want to store a ton of images that should be highly available, we should consider  
distributed BLOB stores like S3. It would cost approximately $4.5k/month to store 182.5 TB of images.
To reduce latency, we can also use Cloudfront as CDN.  

## Image processing
    How long does image resizing take? According to https://github.com/libvips/libvips/wiki/Benchmarks#results-summary, 
    if we provision a machine with Ryzen Threadripper 3955x processor, 4.3	GHz clock and 16 (32ht) cores, we can get   
    it done under 300 ms.  
    Such setup will support ~32 QPS. 

### Offline service
    We could run a lambda function on a chron say, every minute, that would pick up the records inserted since the last  
    time it ran, and run them through the image processing pipeline. The image processing would include resizing the  
    image to the 3 sizes we support. If we go down this path, we will need 4X amount of storage but read latency  
    will be minimized. Considering that the amount of reads per day is only 10 times bigger than writes on average,  
    the extra storage cost is probably not justified. 
### On-demand generation
    We could resize the image only if and when a user requests a particular image size. From here, we could keep it in
    memory in case someone else requests it soon. If we go down this road, we will need at least 2 quite beafy app servers.   
    It would cost us $500 * 2 ~ $1k per month.
