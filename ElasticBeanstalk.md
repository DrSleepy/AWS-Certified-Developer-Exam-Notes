# Elastic Beanstalk

You basically pass it a zip file of your code and it will create an environment for you based on the configuration in your code

- Elastic Beanstalk is a service for deploying and scaling web applications
- Applications can be developer in any language and even Docker
- Applications can are run on servers like Apache Tomcat, Nginx, Passenger etc
- Similar to CloudFormation
  - The config files must end with .config
  - .config files can be written in JSON or YAML
  - All .config files must be saved under a folder named .ebextensions (lives at top level)
- Elastic Beanstalk will handle many things for you

  - Deployment
  - Capacity provisioning
  - Load balancing
  - Auto-scaling
  - Application health

- You still retain full control of the underlying AWS resources powering your applicaiton
- Integrated with CloudWatch and X-Ray

## Updates

Elastic Beanstalk supports multiple options for processing deployments:

- All at once
- Rolling
- Rolling with additonal batch
- Immutable

**All at once:**

Best to do this only dev environment, not production

- Deploys the new version to all instance simultaneously
- All of your instances are out of service while deployment takes place
- If the update fails, you will need to roll back the changes by re-deploying the original version to all your instances

**Rolling:**

Not ideal for performance sensitive systems

- Deploys the new version in batches
- Each batch of instances are taken out of service while the deployment takes place
- Your environment capacity will be reduced by the number of instances in the batch while the deployment takes place
- If the update fails, you will need to roll back the changes by re-deploying the original version to all your instances

**Rolling with additonal batch:**

Best options for performance sensitive systems

- Launches an additonal batch of instances
- Deploys the new version in batches
- Maintains full capacity during the deployment process
- If the update fails, you will need to roll back the changes by re-deploying the original version to all your instances

**Immutable:**

Best option for Mission Critical Production systems

- Deploys the new version to a fresh group of instance in theirn own new auto-scaling group
- When the new instances pass their helath checks, they are moved to your existing auto-scaling group before terminating the old instances
- Maintains full capacity during the deployment process
- The impact of a failed update is far less
- To rollback, you only need to delete the new instance and auto-scaling groups created

## RDS & Elastic Beanstalk

- You can launch an RDS instance from within the Elastic Beanstalk console
  - This means the RDS instance is created within your Elastic Beanstalk environment (good options for Dev/Testing deployments)
- Launching an RDS instance within your Elastic Beanstalk may not be ideal for Production environments because it means the lifecylce of your database is tied to the lifecyle of the environment
  - Terminating (by an Immutable update, for example) the environment means the database instance will also be terminated
- For Production environments, the preferred option is to decouple the RDS instance from your Elastic Beanstalk environment
  - This is done by launching the RDS instance outside of Elastic Beanstalk, directly from the RDS console
  - This option gives you more flexibility:
    - Allows you to connect multiple environments to the same database
    - Provides a wider choice of database types
    - Allows you to tear down your environment without affecting the database instance

**Access RDS from Elastic Beanstalk:**

To allow EC2 instances in your Elastic Beanstlak environment to connect to an outside database,
there are two additional configuration steps required:

- An additional Security Group must be added to your environment's auto-scaling group
- You must provide the RDS endpoint and password using Elastic Beanstalk environment properties
