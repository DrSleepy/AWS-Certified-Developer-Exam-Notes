# ELB - Elastic Load Balancer

Helps divide network traffic to multiple EC2 instances in order not to overload any instances

## ELB Types

1. Application Load Balancer -
   1. Operates at OSI layer 7 (Application layer)
   2. Makes clever decisions all the way down to layer 7 (application layer) to better divide the network traffic through routing
   3. Best suitable for HTTP(S) traffic
2. Network Load Balancer -
   1. Operates at OSI layer 4 (Transport layer)
   2. Provides super fast performance
   3. Most expensive load balancer (but used in production for its low latency)
   4. Best suited for TCP traffic
3. Classic Load Balancer -
   1. No longer recommended by AWS. Only exists for legacy purposes
   2. Balances HTTP(S) and uses layer 7 (Applicaiton layer) specific features such as X-Forwaded amd sticky sessions
   3. Also has the ability to use layer 4 (Transport layer) TCP Protocol

## ELB Errors

1.  Classic Load Balancer -
    1. 504 Error (gateway timeout) - This is NOT an issue with the ELB. It is thrown by the ELB is your application stops responding.
       Error could be originating from the web server layer or the database layer. Scale the layer causing the error up or out to resolve.
2.  X-Forwaded-For Header -

    1. Example Flow:

    - User makes a request using their IP address >
    - The ELB recieves users IP address but uses its own private IP address to call an EC2 instance >
    - The EC2 instance now holds the private IP address of the ELB but not the public IP(v4) address of the user making the request

    Issue: the EC2 instance does not know where in the world the user is making the request from as it does not have the users IP(v4) address but rather the private IP address of the ELB calling the EC2 instance

    Solution: Look for the users public IP(v4) address in the header of the request under X-Forwarded-For
