# CloudFront

CloudFront is a bunch of servers around the world that host your cached content making latency times as low as possible for people around the world.

2. Cached content has a time-to-live (set by you) before the cache is cleared
3. Cache can be cleared manually but you will pay a fee

## CloudFront - Edge Locations

The bunch of servers around the world are referred to as Edge Locations.
CloudFront utilizes these edge locations to cache your content.

**Edge Locations are NOT limit to AWS Regions. There are many more edge locations than AWS Regions**

Once the FIRST request (of the day/week/month etc) is made to an edge location,
the edge location will download the content from the origin server where the content is hosted and cache it into the edge location.

**Example**
Specifications:

- Origin server location: London
- User location: Australia
- Closest edge location to user: India

Flow of Edge Location:

1. User makes FIRST (ever) request to the edge location
2. Edge location checks if it has a cache of the content
   1. If false: make request to origin server, then cache content on edge location, then deliver content to user
   2. If true: check if cached content is out of date
      1. If false: respond to request of user with content
      2. If true: make request to origin server, then update cached content, then deliver content to user

## CloudFront - Transfer Acceleration

1. CloudFront is focused primarily on allowing faster reads/downloads to deliver its content at insane speed
2. CloudFront can also be used to accelerate file uploads into S3 by uploading the files into the closest edge location - this is called Transfer acceleration

## CloudFront - Distributions

Distribution is the name given to the CDN which consists of a collection of edge locations.

Types of distributions:

1. Web Distribution -
   1. Used for websites
2. RTMP (Real-time Messaging Protocol) -
   1. Used for media streaming

## CloudFront - Works with

1. S3
2. EC2
3. ELB
4. Route53
5. Any server outside AWS (could be manually hosted by you)
