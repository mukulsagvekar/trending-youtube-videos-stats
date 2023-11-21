# trending-youtube-videos-stats

Objective: To build a data pipeline to load and transform data using AWS and Snowflake and used visualize the data using Tableau.

The data is available on kaggle - https://www.kaggle.com/datasets/datasnaek/youtube-new
It consists of structured as well as semi-structured (json) data.

# Pipeline:

![image](https://user-images.githubusercontent.com/83829614/211152878-495f1d10-227b-441b-8e04-fe9c6ec2952d.png)

The data is stored in aws s3 bucket.

Snowpipes are used for auto-ingeston. Whenever new files are uploaded in the bucket, SQS queue triggers the snowpipe for auto-ingestion.

Snowpipe loads the data in inbound db. In snowflake we have three databases - inbound, canonical, outbound.

![image](https://user-images.githubusercontent.com/83829614/211152888-c180702b-d712-4df0-bf76-74dec416accc.png)

The raw data is loaded in the inbound database. Then using stream and task, the data is transformed and loaded populated in canonical database.

The json data in inbound db is stored in a variant data type column. This semi-structured data is transformed to structured data for analytics.

Raw json data in inbound:
![image](https://user-images.githubusercontent.com/83829614/221406622-654c5164-78d8-40f1-8f5c-77d03ea406a0.png)

Transformed json data: 
![image](https://user-images.githubusercontent.com/83829614/221406699-1e1b6736-629c-48fc-8287-6ee0b32252a0.png)


The data is moved to outbound db using stream and task and the data is used for analysis and visualization.

Tableau Dashboard - https://public.tableau.com/app/profile/mukul6401/viz/TrendingYoutubeVideosStats/Dashboard1?publish=yes

![image](https://user-images.githubusercontent.com/83829614/211151748-379f573a-20ac-42be-a318-8556d55f8f34.png)

The dashboard is interative and region can be used as a filter to view region wise data.
