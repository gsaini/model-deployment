# Containerization

## Challenges with Model Deployment

### Environment Inconsistencies

- **Dependency Conflicts**: Different library versions across development, testing, and production environments
- **"It Works on My Machine" Problem**: Models fail when moved from data scientist's laptop to production servers
- **OS Differences**: Code behaves differently on Windows, macOS, and Linux systems

### Scalability Issues

- **Manual Setup**: Time-consuming configuration for each new deployment instance
- **Resource Management**: Difficulty in efficiently allocating compute resources
- **Load Handling**: Challenges in scaling up/down based on demand

### Deployment Complexity

- **System Dependencies**: Missing libraries or incompatible system packages
- **Configuration Management**: Tracking and maintaining environment variables and settings
- **Version Control**: Managing multiple model versions simultaneously

## Virtualization and Containerization

### Virtualization

**Definition**: Technology that creates virtual versions of physical hardware, allowing multiple operating systems to run on a single physical machine.

**Characteristics**:

- Each VM includes a full OS copy
- Managed by a hypervisor
- Heavy resource consumption (GBs)
- Slower startup times (minutes)
- Strong isolation at hardware level

### Containerization

**Definition**: Lightweight virtualization that packages applications with their dependencies, sharing the host OS kernel.

**Characteristics**:

- Shares host OS kernel
- Minimal resource overhead (MBs)
- Fast startup times (seconds)
- Process-level isolation
- Highly portable across environments

### Key Differences

| Aspect | Virtualization | Containerization |
|--------|---------------|------------------|
| **Size** | GBs | MBs |
| **Boot Time** | Minutes | Seconds |
| **Resource Usage** | High | Low |
| **Isolation** | Hardware-level | Process-level |
| **Portability** | Limited | High |
| **Use Case** | Running different OS | Running applications |

## Images in Containerization

### What is a Container Image?

A **container image** is a lightweight, standalone, executable package that includes everything needed to run an application:

- Application code
- Runtime environment
- System libraries
- Dependencies
- Configuration files

### Image Layers

Images are built in layers:

1. **Base Layer**: Operating system (e.g., Ubuntu, Alpine)
2. **Runtime Layer**: Programming language runtime (e.g., Python 3.9)
3. **Dependency Layer**: Required libraries and packages
4. **Application Layer**: Your code and models

### Image vs Container

- **Image**: Read-only template (blueprint)
- **Container**: Running instance of an image (actual application)

**Analogy**: Image is like a class, Container is like an object instance.

### Image Registries

**Purpose**: Store and distribute container images

**Popular Registries**:

- **Docker Hub**: Public registry with millions of images
- **AWS ECR**: Amazon Elastic Container Registry
- **Google Container Registry**: GCR
- **Azure Container Registry**: ACR
- **Hugging Face Spaces**: For ML model deployment

## Introduction to Dockerfile

### What is a Dockerfile?

A **Dockerfile** is a text file containing instructions to build a Docker image. It defines:

- Base image to use
- Dependencies to install
- Files to copy
- Commands to run
- Application entry point

### Basic Dockerfile Structure

```dockerfile
# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements
COPY requirements.txt .

# Install dependencies
RUN pip install -r requirements.txt

# Copy application code
COPY . .

# Expose port
EXPOSE 5000

# Run application
CMD ["python", "app.py"]
```

### Common Dockerfile Instructions

| Instruction | Purpose | Example |
|------------|---------|----------|
| `FROM` | Specify base image | `FROM python:3.9-slim` |
| `WORKDIR` | Set working directory | `WORKDIR /app` |
| `COPY` | Copy files to container | `COPY app.py .` |
| `RUN` | Execute commands during build | `RUN pip install flask` |
| `EXPOSE` | Document port usage | `EXPOSE 5000` |
| `ENV` | Set environment variables | `ENV PORT=5000` |
| `CMD` | Default command to run | `CMD ["python", "app.py"]` |

### Best Practices

- Use specific base image versions (e.g., `python:3.9-slim` not `python:latest`)
- Copy requirements file first for better caching
- Minimize number of layers
- Use `.dockerignore` to exclude unnecessary files
- Don't run containers as root user

## Containerization Platforms and Docker

### What is Docker?

**Docker** is the most popular containerization platform that enables developers to package applications into containers.

**Key Components**:

- **Docker Engine**: Core runtime that builds and runs containers
- **Docker CLI**: Command-line interface for interacting with Docker
- **Docker Desktop**: GUI application for Windows and macOS
- **Docker Hub**: Cloud-based registry for sharing images

### Docker Architecture

```
Docker Client (CLI)
        ↓
   Docker Daemon
        ↓
   ┌────┴────┐
Images    Containers
```

### Essential Docker Commands

```bash
# Build image
docker build -t my-app:v1 .

# Run container
docker run -p 5000:5000 my-app:v1

# List containers
docker ps

# View logs
docker logs container-name

# Stop container
docker stop container-name
```

### Alternative Platforms

- **Podman**: Daemonless container engine
- **containerd**: Industry-standard container runtime
- **LXC/LXD**: Linux container technology
- **Kubernetes**: Container orchestration platform

## Introduction to REST API

### What is REST API?

**REST** (Representational State Transfer) is an architectural style for building web services that allow systems to communicate over HTTP.

### Key Principles

1. **Stateless**: Each request contains all necessary information
2. **Client-Server**: Separation of concerns
3. **Uniform Interface**: Consistent way to interact with resources
4. **Resource-Based**: Everything is a resource with a unique URI

### HTTP Methods

| Method | Purpose | Example |
|--------|---------|----------|
| `GET` | Retrieve data | Get customer info |
| `POST` | Create new resource | Submit prediction request |
| `PUT` | Update resource | Update model parameters |
| `DELETE` | Remove resource | Delete old model |

### REST API for ML Models

**Purpose**: Expose ML models as web services that can be accessed by any application.

**Example Endpoints**:

```
GET  /health              - Check API status
POST /v1/predict          - Single prediction
POST /v1/predict/batch    - Batch predictions
GET  /v1/model/info       - Model metadata
```

### Benefits for ML Deployment

- **Language Agnostic**: Any application can consume the API
- **Scalable**: Handle multiple requests simultaneously
- **Decoupled**: Model updates don't affect client applications
- **Accessible**: Easy integration with web/mobile apps

## Architecture of Containerized Model Deployment

### Complete Architecture

```
┌─────────────────────────────────────────────┐
│         Client Applications                 │
│    (Web, Mobile, Dashboard, CRM)            │
└──────────────────┬──────────────────────────┘
                   │ HTTP/HTTPS
                   ▼
┌─────────────────────────────────────────────┐
│         Load Balancer / API Gateway         │
└──────────────────┬──────────────────────────┘
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
┌──────────────┐    ┌──────────────┐
│  Container 1 │    │  Container 2 │
│              │    │              │
│  Flask API   │    │  Flask API   │
│  ML Model    │    │  ML Model    │
└──────────────┘    └──────────────┘
         │                   │
         └─────────┬─────────┘
                   ▼
┌─────────────────────────────────────────────┐
│         Shared Storage / Database           │
│         (Model Files, Logs, Cache)          │
└─────────────────────────────────────────────┘
```

### Component Breakdown

#### 1. Client Layer

- Web applications
- Mobile apps
- Data pipelines
- Business intelligence tools

#### 2. API Layer (Containerized)

- **Flask/FastAPI**: Web framework serving predictions
- **Model Loading**: Deserialize trained model (pickle/joblib)
- **Request Handling**: Process input data and return predictions
- **Validation**: Ensure input data meets requirements

#### 3. Container Layer

- **Docker Container**: Isolated environment with all dependencies
- **Horizontal Scaling**: Multiple container instances for load distribution
- **Health Checks**: Monitor container status

#### 4. Storage Layer

- **Model Storage**: Serialized model files
- **Logging**: Request/response logs for monitoring
- **Caching**: Redis/Memcached for faster responses

### Deployment Workflow

```
1. Train Model → 2. Serialize Model → 3. Create Dockerfile
                                              ↓
6. Monitor ← 5. Deploy Container ← 4. Build Image
```

### Benefits of This Architecture

✅ **Portability**: Run anywhere (local, cloud, edge)
✅ **Scalability**: Add more containers as demand increases
✅ **Reliability**: Container failures don't affect others
✅ **Consistency**: Same environment everywhere
✅ **Maintainability**: Easy updates and rollbacks
✅ **Isolation**: Multiple models with different dependencies

### Real-World Example: Churn Prediction API

```dockerfile
# Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY app.py model.pkl .
EXPOSE 5000
CMD ["python", "app.py"]
```

```python
# app.py
from flask import Flask, request, jsonify
import joblib

app = Flask(__name__)
model = joblib.load('model.pkl')

@app.post('/predict')
def predict():
    data = request.get_json()
    prediction = model.predict([data['features']])
    return jsonify({'prediction': int(prediction[0])})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

**Deployment**:

```bash
docker build -t churn-api .
docker run -d -p 5000:5000 churn-api
```

**Usage**:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"features": [0, 1, 12, 70.5, 844.2]}'
```

## Reference Materials

- [This is an official tutorial provided by Docker, covering the fundamentals of containers](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)

- [This tutorial covers everything from the basics of REST to advanced API design](https://www.restapitutorial.com/)
