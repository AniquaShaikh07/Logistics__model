# Logistics_model
**An end-to-end AI-powered logistics system** that predicts delivery time using Machine Learning, optimizes multi-stop routes using Dijkstra's Algorithm & TSP, and provides intelligent explanations using Google Gemini AI — all wrapped in a beautiful Streamlit UI.

## 📌 Table of Contents
- [Project Overview](#-project-overview)
- [Live Demo Features](#-live-demo-features)
- [Tech Stack & APIs Used](#-tech-stack--apis-used)
- [ML Model Details](#-ml-model-details)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Environment Variables](#-environment-variables)
- [Installation & Setup](#-installation--setup)
- [How to Run](#-how-to-run)
- [Docker Setup](#-docker-setup)

  ## ✨ Live Demo Features
| Feature | Description |
|--------|-------------|
| 🗺️ Route Optimizer | Enter source, destination & stops — get optimal route instantly |
| 🚛 Mode Comparison | Compares Road, Rail, and Sea delivery time side-by-side |
| 🤖 AI Explanation | Gemini AI explains why a specific route/mode is recommended |
| 📊 Analytics Dashboard | Charts for delivery trends, mode distribution, top routes |
| 💬 AI Assistant | Chat interface powered by Google Gemini for logistics queries |
| 🗓️ Delivery Scheduler | Plan shipments with date and time predictions |
| 🔗 Google Maps Link | One-click open-in-maps for the full optimized route |

## 🛠️ Tech Stack & APIs Used
### Machine Learning
| Library | Purpose |
|--------|---------|
| `scikit-learn` | RandomForestRegressor for delivery time prediction |
| `pandas` | Data loading, merging, and feature engineering |
| `numpy` | Numerical computation and synthetic feature generation |
| `joblib` | Saving and loading trained model (`model.pkl`, `features.pkl`) |

### Web UI & Visualization
| Library | Purpose |
|--------|---------|
| `streamlit` | Full web application UI with sidebar navigation |
| `plotly` | Interactive charts — pie, bar, line graphs for analytics |

### AI & APIs
| API | Purpose | Environment Variable |
|-----|---------|---------------------|
| **Google Gemini API** (`google-generativeai`) | AI route explanation & chatbot | `GEMINI_API_KEY` |
| **Google Maps Distance Matrix API** | Real city-to-city distance in km | `GOOGLE_API_KEY` |
| **OpenWeatherMap API** | Live weather data for routing context | `WEATHER_API_KEY` |

### Algorithms (Custom Implementation)
| Algorithm | File | Purpose |
|----------|------|---------|
| **Dijkstra's Algorithm** | `UI.py` | Shortest path between cities using predicted travel times |
| **TSP (Travelling Salesman Problem)** | `UI.py` | Optimal ordering of multi-stop deliveries |
| **Nearest Neighbor Heuristic** | `UI.py` | Fast approximation for TSP with many stops (>10) |

### Infrastructure
| Tool | Purpose |
|-----|---------|
| `Docker` | Containerized deployment |
| `Flask` | Backend API layer |
| `requests` | HTTP calls to external APIs |

---

## 🤖 ML Model Details

**Model:** `RandomForestRegressor`

**Task:** Regression — predict delivery time in days

**Training File:** `train.py`

### Features Used

| Feature | Description |
|--------|-------------|
| `distance` | Absolute distance between seller & customer zip codes |
| `traffic_delay` | `distance × traffic coefficient` per transport mode |
| `traffic_level` | Normalized traffic ratio |
| `weight` | Product weight in kg (converted from grams) |
| `price` | Product price in INR |
| `freight` | Freight value |
| `payment` | Total payment value |
| `departure_hour` | Hour of order purchase (0–23) |
| `priority` | Delivery priority level (1–3) |
| `mode` | Transport mode encoded: Road=1, Rail=2, Sea=3 |

### Hyperparameters

```python
RandomForestRegressor(
    n_estimators=150,
    max_depth=20,
    min_samples_split=10,
    min_samples_leaf=4,
    random_state=42,
    n_jobs=-1
)
```

### Mode Multipliers

| Mode | Traffic Rate | Speed Factor |
|------|-------------|--------------|
| Road | 0.15 | 1.0× |
| Rail | 0.05 | 1.2× (faster) |
| Sea  | 0.02 | 0.8× (slower) |

**Files Used:**

```
olist_orders_dataset.csv
olist_order_items_dataset.csv
olist_products_dataset.csv
olist_sellers_dataset.csv
olist_customers_dataset.csv
olist_order_payments_dataset.csv
```

**Target Variable:** `delivery_time` = `order_delivered_customer_date` − `order_purchase_timestamp` (in days)

### How to Get API Keys

| API | Link |
|-----|------|
| Google Gemini | https://aistudio.google.com/app/apikey |
| Google Maps Distance Matrix | https://console.cloud.google.com/ |
| OpenWeatherMap | https://openweathermap.org/api |

### model 
https://logistics-model-528414856505.us-central1.run.app/

