# ELK Stack Log Monitoring

This project uses **Elasticsearch**, **Logstash**, **Kibana**, and **Filebeat** to monitor and analyze logs.

## Prerequisites

- Docker and Docker Compose installed
- Minimum 4GB RAM allocated to Docker
- Ports 5601 (Kibana), 9200 (Elasticsearch), and 5044 (Logstash) available

## Setup Instructions

### 1. Start the Docker Compose Stack

Run the following command to start all services (Elasticsearch, Logstash, Kibana, and Filebeat):

```bash
docker-compose up -d
```

### 2. Provide Log Data

You have two options:

#### Option A: Use Existing Logs

If you already have log files in the directories specified in `filebeat.yml`, Filebeat will automatically read and forward them to Logstash.

#### Option B: Generate Logs (Simulate Ingestion)

Run the log generator script in the background:

```bash
chmod +x generate_logs.sh
./generate_logs.sh
```

This will continuously generate sample logs to simulate real-time data ingestion.

### 3. Access Kibana

Open your web browser and navigate to:

```
http://localhost:5601
```

Login credentials are configured in your `.env` file (automatic login should work if properly set up).

### 4. Import Dashboards and Views

To import predefined Kibana views and dashboards:

1. Navigate to **Stack Management** in the left sidebar menu
2. Go to **Kibana** → **Saved Objects**
3. Click **Import** and select the `kibanaviews.ndjson` file

## Services Overview

| Service | Port | Purpose |
|---------|------|---------|
| Elasticsearch | 9200 | Log storage and indexing |
| Logstash | 5044 | Log processing pipeline |
| Kibana | 5601 | Visualization and dashboarding |
| Filebeat | - | Log shipping agent |

## Project Structure

```
├── docker-compose.yml
├── filebeat.yml
├── generate_logs.sh
├── kibanaviews.ndjson
├── .env
└── logs/               # Directory for log files
```

## Troubleshooting

- **Elasticsearch won't start**: Ensure `vm.max_map_count` is set properly:  
  `sudo sysctl -w vm.max_map_count=262144`
- **No data in Kibana**: Verify Filebeat is running and logs exist in the specified paths
- **Connection refused**: Ensure all containers are running: `docker-compose ps`
```
