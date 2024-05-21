# Step-by-Step-Guide-for-Installing-Prometheus-and-Grafana-Using-Docker-Compose

## Step-by-Step Guide for Installing Prometheus and Grafana Using Docker Compose

### Step 1: Install Docker and Docker Compose

Before starting, ensure that Docker and Docker Compose are installed on your system. You can follow these steps:

1. **Install Docker**:

###  my docker installation link repo step by step producer guide

```
https://github.com/FokkerYe/docker_installation_bath_script.git
``

3. **Verify Installations**:

    ```bash
    docker --version
    docker-compose --version
    ```

### Step 2: Set Up Project Directory

1. **Create a Directory for Your Project**:

    ```bash
    mkdir prometheus-grafana
    cd prometheus-grafana
    ```

### Step 3: Create Docker Compose File

1. **Create a `docker-compose.yml` File**:

    ```bash
    touch docker-compose.yml
    ```

2. **Edit the `docker-compose.yml` File**:

    Open the file with your preferred text editor and add the following content:

    ```yaml
    version: '3.7'

    services:
      prometheus:
        image: prom/prometheus:latest
        volumes:
          - ./prometheus.yml:/etc/prometheus/prometheus.yml
        ports:
          - "9090:9090"

      grafana:
        image: grafana/grafana:latest
        ports:
          - "3000:3000"
        environment:
          - GF_SECURITY_ADMIN_PASSWORD=admin
        volumes:
          - grafana-storage:/var/lib/grafana

    volumes:
      grafana-storage:
    ```

### Step 4: Configure Prometheus

1. **Create Prometheus Configuration File**:

    ```bash
    touch prometheus.yml
    ```

2. **Edit the `prometheus.yml` File**:

    Open the file with your preferred text editor and add the following content:

    ```yaml
    global:
      scrape_interval: 15s

    scrape_configs:
      - job_name: 'prometheus'
        static_configs:
          - targets: ['localhost:9090']
    ```

### Step 5: Start Services

1. **Start Docker Compose**:

    ```bash
    sudo docker-compose up -d
    ```

2. **Verify Services**:

    - Prometheus should be accessible at `http://localhost:9090`.
    - Grafana should be accessible at `http://localhost:3000` with default credentials (`admin`/`admin`).

### Step 6: Configure Grafana

1. **Access Grafana**:

    Open your browser and go to `http://localhost:3000`.

2. **Log In**:

    Use the default credentials:
    - Username: `admin`
    - Password: `admin`

3. **Add Prometheus as a Data Source**:

    - Go to "Configuration" -> "Data Sources".
    - Click "Add data source".
    - Select "Prometheus".
    - Set the URL to `http://prometheus:9090`.
    - Click "Save & Test".

4. **Create a Dashboard**:

    - Go to "Create" -> "Dashboard".
    - Add new panels and use Prometheus queries to visualize your metrics.
      ```
      Reflink =https://selftuts.in/prometheus-and-grafana-installation-using-docker-compose/
      ```
