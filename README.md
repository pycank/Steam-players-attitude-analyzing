# Steam-Data-Engineering-Project

## The Pipeline Trio 
Three pipelines, three different cadences—daily, weekly, and monthly. This setup ensures a separation of concerns and a steady flow of fresh data. 

### Daily Rhythms 
- Source:
    - [Most Played Games](https://store.steampowered.com/charts/mostplayed)
- Purpose: Collect daily data on the most played games.

Every day, the curtain rises on the gaming stage. Behold the Most Played Games list from Steam. With the finesse of web scraping and the power of Kafka, the Daily Kafka Producer takes the spotlight, bringing the latest player counts, game ranks, and more to the forefront. 

### Weekly Data 
- Sources:
    - [Top Sellers in the US](https://store.steampowered.com/charts/topsellers/US)
    - [Steam News](http://api.steampowered.com/ISteamNews/GetNewsForApp/v0002/?appid=)
    - [App Reviews](https://store.steampowered.com/appreviews/)
- Purpose: Gathers weekly insights by aggregating data from top sellers, game news, and user reviews.    

Our Weekly Data unfold from the WEEKLY TOP SELLERS, showcasing the top 100 games in revenue. Armed with App IDs, it delves into game news for updates and bug fixes straight from the developers. Simultaneously, I also tap into the community's heartbeat—user reviews from the app page, offering a valuable pulse on user sentiments.

### Monthly Data
- Source: 
    - [Monthly Visits](https://data.similarweb.com/api/v1/data?domain=store.steampowered.com)
- Purpose: Collects monthly data related to network traffic, page visits, and engagement metrics, enriching our understanding of Steam's audience.

## Local Setup
- Setup Kafka
- Install PySpark `pip install pyspark`
- Setup Airflow

### Setting Up Docker 
Check the [DOCKER-README.md](https://github.com/SartajBhuvaji/Steam-Big-Data-Pipeline/blob/main/DOCKER-README.md) file  

### AWS
#### EC2 Instance Configuration
- Launched an EC2 instance optimized for Kafka and Spark usage.
- Configured security groups to manage inbound/outbound traffic, ensuring Kafka and Spark functionality.
- Established an IAM role granting S3 access to the EC2 instance.
#### Kafka Deployment on EC2
- Installed and set up Kafka on the EC2 instance.
- Configured producer-consumer schemas enabling smooth data flow within Kafka.
#### S3 Bucket Creation
- Created dedicated S3 buckets: `steam-project-raw`, `steam-project-processed-data`, `steam-project-raw-backup` and `steam-project-processed-data-backup`
- Implemented stringent bucket policies to ensure secure data storage.
#### Kafka Data Streaming to S3
- Developed scripts facilitating seamless data streaming from various Steam sources into Kafka topics.
- Integrated scripts to efficiently store data into the designated `steam-project-raw-storage` S3 bucket.
#### Apache Spark Configuration
- Installed and configured Apache Spark on the EC2 instance.
- Crafted Spark scripts adept at transforming and processing data according to daily, weekly, and monthly pipelines.
- Successfully loaded processed data into the steam-clean-storage S3 bucket.
#### S3 Triggers and QuickSight Integration
- Configured S3 event triggers to promptly detect and respond to new data arrivals.
- Integrated QuickSight with S3, enabling direct visualization of data stored in the steam-clean-storage bucket for real-time insights.

