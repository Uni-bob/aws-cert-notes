## Introduction
- Amazon Web Services (AWS) is a cloud provider; meaning they provide servers and services one can use on demand and scale easily.
- Apparently AWS is a big deal and it powers some of the biggest websites in the world. For Ex: Netflix allegedly doesn't own a single server they rent it all from AWS. Others are Dropbox and NASA.

## Cloud History
- In 2023, AWS had 90 billion in annual revenue.
- AWS accounts for 31% of the market in Q1 2024 with Microsoft in 2nd at 25%.
- Pioneer and leader of the AWS Cloud Market for 13 years in a row
- Over 1,000,000 active users

## AWS Cloud Use Cases
- Enables one to build sophisticated, scalable applications
- Applicable to a diverse set of industries, every company can benefit from using the cloud. Ex... McDonalds, Activision, 21st Century FOX
- Use cases include: Enterprise IT, backup and storage, Big data analytics, Website Hosting, Mobile and Social Apps, Gaming.

## AWS Global Infrastructure
AWS is global, you have:
- AWS Regions
- AWS Availability Zones
- AWS Data Centers
- AWS Edge Locations/Points of Presence
- Reference infrastructure.aws/ to get a clearer picture.

## AWS Regions
- They're all around the world and they are named in us-east-1 or eu-west-3 type format.
- A region is a cluster of data centers.
- Most AWS services are linked and scoped to a specific region. Meaning if we use a service in one region and we try to use in another it will be like a new time using the service.

# Question that may come up in the exam:
Q - How do you choose an AWS Region  
A - It depends on certain factors such as;
   - Compliance w/ (local) data governance and legal requirements: Sometimes governments want the data to be local to the country you're deploying the app in.
   - Proximity to customers: you want to reduce the chance for latency issues.
     - For Ex: you deploy your app in America but your users are in Australia, they are very likely to experience latency.
   - Available Services: not every region has the same services and features available. Make sure that the region you are planning to deploy into has the services that you need.
   - Pricing: pricing varies region to region and is transparent in the service pricing page.
