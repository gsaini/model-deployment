# REST API and Containerization - Telecom Customer Churn Prediction

## 📋 Problem Statement

### Business Context

In the highly competitive telecommunications industry, customer retention is critical to sustaining growth and profitability. Customer churn remains a persistent challenge, making it essential to understand customer behavior and the underlying factors that drive their decision to leave.

The Customer Analytics & Retention Department has developed a predictive model to identify patterns associated with churn risk. However, several challenges hinder effectiveness:

1. **Data Overload** — Vast volume and complexity of customer data make it difficult to extract timely insights
2. **Delayed Responses** — Existing analysis lacks speed needed to respond to emerging trends
3. **Limited Accessibility** — Model must be easily accessible to all customer-facing teams

### Objective

Develop a **standardized, portable solution** that packages the model, dependencies, configurations, and runtime environment into a self-contained unit. This approach aims to:

- Eliminate compatibility issues across different systems
- Reduce errors during deployment
- Simplify setup and configuration
- Enable reliable, low-latency access to the churn prediction model
- Support timely and proactive customer retention efforts

## 🏗️ Solution Architecture

The solution implements a **Flask-based REST API** containerized with **Docker** for consistent deployment across distributed teams and systems.

```
┌─────────────────────────────────────────┐
│     Trained Churn Prediction Model      │
│      (Serialized with Joblib)           │
└──────────────────┬──────────────────────┘
                   │
         ┌─────────▼─────────┐
         │    Flask API      │
         │  (Backend Server) │
         └─────────┬─────────┘
                   │
         ┌─────────▼─────────┐
         │  Docker Container │
         │  (Portable Unit)  │
         └───────────────────┘
```

## 🔧 Technology Stack

| Component | Technology |
|-----------|-----------|
| **Web Framework** | Flask |
| **Model Serialization** | Joblib |
| **Containerization** | Docker |
| **Programming Language** | Python |
| **Data Processing** | Pandas |
| **Deployment Platform** | Hugging Face Spaces |

## 🚀 API Endpoints

### 1. Home Endpoint

- **URL**: `/`
- **Method**: `GET`
- **Description**: Welcome message and API status check

### 2. Single Customer Prediction

- **URL**: `/v1/customer`
- **Method**: `POST`
- **Content-Type**: `application/json`
- **Description**: Predicts churn for a single customer

**Request Body**:

```json
{
  "SeniorCitizen": 0,
  "Partner": "Yes",
  "Dependents": "No",
  "tenure": 12,
  "PhoneService": "Yes",
  "InternetService": "Fiber optic",
  "Contract": "Month-to-month",
  "PaymentMethod": "Electronic check",
  "MonthlyCharges": 70.35,
  "TotalCharges": 844.20
}
```

**Response**:

```json
{
  "Prediction": "churn"
}
```

### 3. Batch Customer Prediction

- **URL**: `/v1/customerbatch`
- **Method**: `POST`
- **Content-Type**: `multipart/form-data`
- **Description**: Predicts churn for multiple customers via CSV upload

## 📦 Model Features

The churn prediction model uses the following customer attributes:

- `SeniorCitizen` — Whether the customer is a senior citizen (0/1)
- `Partner` — Whether the customer has a partner (Yes/No)
- `Dependents` — Whether the customer has dependents (Yes/No)
- `tenure` — Number of months the customer has stayed
- `PhoneService` — Whether the customer has phone service (Yes/No)
- `InternetService` — Type of internet service (DSL/Fiber optic/No)
- `Contract` — Contract term (Month-to-month/One year/Two year)
- `PaymentMethod` — Payment method used
- `MonthlyCharges` — Monthly charges amount
- `TotalCharges` — Total charges to date

## 🐳 Containerization Benefits

Docker containerization provides:

- **Portability** — Run anywhere without environment conflicts
- **Consistency** — Same behavior across development, testing, and production
- **Isolation** — Dependencies packaged within the container
- **Scalability** — Easy to replicate and scale horizontally
- **Version Control** — Track and manage different model versions

## 📁 Project Structure

```
backend_files/
├── app.py                              # Flask API application
├── churn_prediction_model_v1_0.joblib  # Serialized ML model
├── Dockerfile                          # Container configuration
└── requirements.txt                    # Python dependencies
```

## 🎯 Key Learning Outcomes

- Building production-ready **REST APIs** with Flask
- **Containerizing** ML models for consistent deployment
- Handling both **single and batch predictions**
- Implementing **API versioning** (v1 endpoints)
- Deploying to **cloud platforms** (Hugging Face Spaces)
- Managing **model serialization** with Joblib
- Creating **portable, self-contained** ML solutions

## ⚠️ Important Notes

- When creating Hugging Face Spaces, use hyphens (`-`) instead of underscores (`_`) in space names to avoid API URL exceptions
- Space SDK should be set to **Docker**
- Docker template should be **Blank** for custom configuration

## 🔗 Deployment Platform

The backend is deployed on **Hugging Face Spaces** with Docker SDK, providing:

- Free hosting for ML applications
- Automatic HTTPS endpoints
- Built-in version control
- Easy sharing and collaboration

## 💡 Use Cases

This containerized API enables:

- **Customer Retention Teams** — Identify at-risk customers proactively
- **CRM Systems** — Integrate churn predictions into existing workflows
- **Analytics Dashboards** — Display real-time churn insights
- **Mobile Applications** — Provide field teams with instant predictions
- **Batch Processing** — Analyze large customer segments periodically

## 📈 Business Impact

- **Faster Decision-Making** — Real-time predictions enable immediate action
- **Improved Accessibility** — All teams can access the model via simple API calls
- **Reduced Churn** — Proactive interventions based on predictive insights
- **Scalable Solution** — Handles growing data volumes and user base
- **Cost Efficiency** — Containerization reduces deployment and maintenance overhead

---

This project demonstrates the practical application of **model deployment**, **API development**, and **containerization** to solve real-world business challenges in the telecommunications industry.
