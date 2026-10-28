
stripe Blog 
- Idempotent, which means that they can be called any number of times while guaranteeing that side effects only occur once.
- we sometimes need to drop low-priority requests to make sure that more critical requests get through. This is called load shedding.
- 4 different types of limiters : 
    - Request rate limiter : This rate limiter restricts each user to N requests per second ()
    - Concurrent requests Limitter : this rate limiter says “You can only have 20 API requests in progress at the same time”. 
    - Fleet usage load shedder : Using this type of load shedder ensures that a certain percentage of your fleet will always be available for your most important API requests.
    - Worker utilization load shedder : 

DOS - Denial of Service  (only from one IP)
DDOs - Distributed Denial of Service (fro different kind of IPs )




