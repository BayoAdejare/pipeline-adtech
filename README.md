# AdTech Data Pipeline

Welcome to the AdTech Data Pipeline project! This cutting-edge system processes and analyzes vast amounts of advertising data to provide real-time insights and optimize ad performance.

## Table of Contents
- [Project Overview](#project-overview)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Google Ads and Analytics Integration](#google-ads-and-analytics-integration)
- [CI/CD with GitHub Actions](#cicd-with-github-actions)
- [License](#license)

## Project Overview

Our AdTech Data Pipeline is designed to handle large-scale data processing for digital advertising. It includes real-time data ingestion, processing, analysis, and visualization components to provide actionable insights for ad campaign optimization.

Key features:
- Real-time data ingestion from multiple sources
- Scalable data processing using Apache Spark
- Machine learning models for ad performance prediction
- Real-time dashboards for campaign monitoring
- Automated alerting system for anomaly detection
- Integration with Google Ads and Google Analytics

## Project Structure

```
adtech-data-pipeline/
│
├── src/
│   ├── ingestion/
│   │   ├── kafka_consumer.py
│   │   └── api_ingestion.py
│   ├── processing/
│   │   ├── spark_jobs/
│   │   │   ├── clickstream_processing.py
│   │   │   └── conversion_attribution.py
│   │   └── ml_models/
│   │       ├── ctr_prediction.py
│   │       └── audience_segmentation.py
│   ├── analysis/
│   │   ├── performance_metrics.py
│   │   └── ab_testing.py
│   ├── visualization/
│   │   ├── dashboard.py
│   │   └── report_generator.py
│   └── integrations/
│       ├── google_ads_client.py
│       └── google_analytics_client.py
│
├── tests/
│   ├── unit/
│   └── integration/
│
├── config/
│   ├── kafka_config.yml
│   ├── spark_config.yml
│   ├── ml_config.yml
│   └── google_api_config.yml
│
├── scripts/
│   ├── setup.sh
│   └── run_pipeline.sh
│
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── cd.yml
│
├── requirements.txt
├── Dockerfile
├── .gitignore
└── README.md
```

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/your-org/adtech-data-pipeline.git
   cd adtech-data-pipeline
   ```

2. Set up a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

4. Set up configuration files in the `config/` directory.

## Usage

1. Start the data ingestion process:
   ```
   python src/ingestion/kafka_consumer.py
   ```

2. Run Spark processing jobs:
   ```
   spark-submit src/processing/spark_jobs/clickstream_processing.py
   ```

3. Generate visualizations and reports:
   ```
   python src/visualization/dashboard.py
   ```

For more detailed instructions, refer to the documentation in each module.

## Google Ads and Analytics Integration

Our pipeline integrates with Google Ads and Google Analytics to provide comprehensive insights into ad performance and user behavior.

### Example: Fetching Google Ads Campaign Data

```python
from src.integrations.google_ads_client import GoogleAdsClient

# Initialize the client
ads_client = GoogleAdsClient('path/to/google_api_config.yml')

# Fetch campaign performance data
campaign_data = ads_client.get_campaign_performance(
    customer_id='1234567890',
    date_range='LAST_30_DAYS',
    metrics=['impressions', 'clicks', 'cost_micros', 'conversions']
)

# Process and analyze the data
for campaign in campaign_data:
    print(f"Campaign: {campaign['campaign_name']}")
    print(f"Impressions: {campaign['impressions']}")
    print(f"Clicks: {campaign['clicks']}")
    print(f"Cost: ${campaign['cost_micros'] / 1000000:.2f}")
    print(f"Conversions: {campaign['conversions']}")
    print("---")
```

### Example: Analyzing Google Analytics Data

```python
from src.integrations.google_analytics_client import GoogleAnalyticsClient

# Initialize the client
analytics_client = GoogleAnalyticsClient('path/to/google_api_config.yml')

# Fetch website traffic data
traffic_data = analytics_client.get_website_traffic(
    view_id='ga:12345678',
    start_date='7daysAgo',
    end_date='today',
    metrics=['ga:sessions', 'ga:pageviews', 'ga:avgTimeOnPage'],
    dimensions=['ga:date']
)

# Process and visualize the data
import matplotlib.pyplot as plt

dates = [row['ga:date'] for row in traffic_data]
sessions = [int(row['ga:sessions']) for row in traffic_data]

plt.figure(figsize=(10, 5))
plt.plot(dates, sessions)
plt.title('Website Traffic Over the Last 7 Days')
plt.xlabel('Date')
plt.ylabel('Sessions')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

These examples demonstrate how to fetch and analyze data from Google Ads and Google Analytics using our integrated clients. You can extend these examples to create more complex analyses and visualizations based on your specific needs.

## CI/CD with GitHub Actions

We use GitHub Actions for continuous integration and deployment. Our workflow includes:

1. **Continuous Integration (CI)**
   - Triggered on every push and pull request to the `main` branch
   - Runs unit and integration tests
   - Performs code linting and style checks
   - Builds Docker images

2. **Continuous Deployment (CD)**
   - Triggered on successful merges to the `main` branch
   - Deploys the application to staging environment
   - Runs smoke tests
   - If successful, promotes to production

To view and modify these workflows, check the `.github/workflows/` directory.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
