# AWS-Cloud-Cost-Optimization
### The "Why" of Cloud Migration and the Need for Cost
### **Primary Reasons for Cloud Adoption:** Organizations primarily move to the cloud for two reasons:
1. To reduce the overhead of the infrastructure (e.g., setting up and maintaining data centers, purchasing servers, managing IT teams).
2. To optimize their Cloud cost.
- **On-Premises Challenges:** For startups and mid-scale organizations, establishing and maintaining an on-premises data center involves significant upfront costs (servers, infrastructure) and ongoing operational expenses (team salaries, monitoring). This makes cloud platforms like AWS an "easy gold go to solution."
- **Cloud Efficiency is Key to Cost Reduction:** Simply migrating to the cloud does not automatically guarantee cost savings. "the cloud cost will go down only if you are doing this efficiently." Inefficient use can lead to higher-than-expected cloud costs.

## Identifying Stale EBS Snapshots
In this project, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

## Description:
The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

## Setup Formation
- Take a general instance with t2.micro, a volume which comes by default with it.
- Creating a snapshot
- Creating a Lambda function
    - Creating test event
    - edit the timeout to 10s
    - Setting permissions by creating policies for the function Role which has been created
      - Choosing Ec2 service and allowing
        - DescribeSnapshots
        - DeleteSnapshot
        - DescribeVolumes
        - DescribeInstances
      - attaching policy to the Function role
- Executing the lambda function
![](https://github.com/deepakbehera11/AWS-Cloud-Cost-Optimization/blob/ad6d8c8110b4b26ac9414096dd69d1d217011645/Assets/Screenshot-function.png)
- but the snapshot is not deleted because our function checks if it's not attached to any volume or the volume is not attached to a running instance
- So here, deleting the instance, eventually the volume also gets deleted
- Now Executing the code
- And Now snapshots get deleted .
