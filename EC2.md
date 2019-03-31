# EC2 - Elastic Computer Cloud

A "virtual" server (or instance) that provides resizeable compute capacity

## EC2 - Abilities

1. Allows you to change the instance type - there are 11 different instance types. All are referred to be a letter
   How to remember: Fight Dr Mc PX (Fight Club vs Donal Duck)
   F - FPGA
   I - IOPS
   G - Graphics
   H - High Disk Throughput
   T - cheap general purpose (think T2 Micro - or Titanfall 2)

   D - Density
   R - RAMk

   M - Main choice for general purpose apps
   C - Compute

   P - Graphics (think Pics)
   X - Xtreme Memory

2. Can use multiple instances at once

## EC2 - Pricing

1. On Demand -
   1. Pay a cheap fixed rate with no commitment. Windows instances are by the hour whereas linux instances are by the minute
2. Reserved -
   1. Book an instances for 1 or 3 years and provides you with a great hourly discount
   2. Can be scheduled (such as running for 5 minutes every week on a Monday)
3. Spot -
   1. Bid on an instance whenever the price is below X and sell whenever it is about X
   2. Good option when your applications have flexbile start/end times
   3. When the price of an instance exceeds your range of pay, it will automatically be terminated by AWS. If it is terminated by AWS within the hour, you will not pay anything for that hour. If it is terminated by you, you will pay for the whole hour.
4. Dedicated Hosts -
   1. Physical servers dedicated for your use. Helps reduce cost by allowing you to use your existing server-bound software licenses
   2. Good for hospitals that don't allow data to be stored in the cloud due to security risk
