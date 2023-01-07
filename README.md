# trending-youtube-videos-stats

In this project, build a pipeline using AWS services and snowflake, used tableau for visualization.

The data is available in kaggle - https://www.kaggle.com/datasets/datasnaek/youtube-new
We have structured as well as unstructured (json) data.

# Pipeline:

![image](https://user-images.githubusercontent.com/83829614/211152878-495f1d10-227b-441b-8e04-fe9c6ec2952d.png)

The data is stored in aws s3 bucket.

Snowpipes are used for auto-ingeston. Whenever new data is uploaded in the bucket, SQS queue notificaiton triggers the snowpipe for auto-ingestion.

Then the data is loaded into inbound tables. In snowflake we have 3 databses - inbound, canonical, outbound.

![image](https://user-images.githubusercontent.com/83829614/211152888-c180702b-d712-4df0-bf76-74dec416accc.png)

The raw data is loaded in the inbound database. Then using stream and task required transformation are done and the data is populated in canonical database.

The json data in inbound db was stored as a variant. The major transformation was to transform unstructured data to structured data for analytics.

The data is moved to outbound db using stream and task and the data is used for analytics which is done using tableau.

Tableau Dashboard - https://public.tableau.com/app/profile/mukul6401/viz/TrendingYoutubeVideosStats/Dashboard1?publish=yes

![image](https://user-images.githubusercontent.com/83829614/211151748-379f573a-20ac-42be-a318-8556d55f8f34.png)

The dashboard is interative and region can be used as a filter to view region wise data.
