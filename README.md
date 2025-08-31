# Ad Click Prediction

A machine learning project for predicting advertisement click-through rates using LightGBM and deployed as a FastAPI microservice with monitoring capabilities.

## 🎯 Project Overview

This project builds a binary classification model to predict whether users will click on advertisements based on various features like region, content tags, pricing, and positioning information. The solution includes:

- **Data Analysis & Modeling**: Comprehensive EDA and model training in Jupyter notebooks
- **Production API**: FastAPI microservice for real-time predictions
- **Monitoring**: Prometheus metrics and Grafana dashboards
- **Containerization**: Docker-based deployment

## 📊 Key Results

- **Best Model**: LightGBM Classifier
- **ROC-AUC Score**: 0.803
- **F1 Score**: 0.710
- **Features**: 11 input features including region, content tags, and ad positioning

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- Docker & Docker Compose (for API deployment)
- Git

### 1. Clone and Setup
```bash
git clone <your-repo-url>
cd ad_click_prediction
pip install -r requirements.txt
```

### 2. Run Data Analysis
```bash
chmod +x run_jupyter.sh
./run_jupyter.sh
```

### 3. Deploy API Service
```bash
cd services
docker compose up --build
```

## 📁 Project Structure

```
ad_click_prediction/
├── ad_click_prediction.ipynb    # Main analysis notebook
├── research_functions.py        # Helper functions for analysis
├── requirements.txt            # Python dependencies
├── run_jupyter.sh             # Script to start Jupyter Lab
├── run_mlflow_server.sh       # MLflow tracking server
├── assets/                    # Generated plots and visualizations
│   ├── Dataset feature correlation.png
│   ├── LGBM Receiver Operating Characteristic.png
│   └── ...
└── services/                  # Production API
    ├── app/
    │   ├── app.py            # FastAPI application
    │   ├── app_fastapi_handler.py  # Request handler
    │   └── constants.py      # Model configuration
    ├── models/               # Model files (excluded from git)
    ├── prometheus/           # Monitoring configuration
    ├── docker-compose.yaml   # Multi-service deployment
    ├── Dockerfile           # Container definition
    └── requirements.txt     # API dependencies
```

## 🔬 Data Science Workflow

1. **Data Exploration**: Understanding the advertisement dataset structure and quality
2. **Feature Engineering**: Creating additional features from existing data
3. **Model Training**: Training multiple models (Logistic Regression, Random Forest, LightGBM)
4. **Model Evaluation**: Comparing models using ROC-AUC and F1 scores
5. **Feature Importance**: Analyzing which features contribute most to predictions

### Key Features
- `rv_perc`: Advertisement visibility percentage
- `ctr_sort`: Click-through rate value
- `rate`: Advertisement bid rate in rubles
- `rubrica`: Advertisement category
- `tags_bhv`: Behavioral targeting value

## 🛠️ API Usage

### Start the Service
```bash
cd services
docker compose up --build
```

### API Endpoints
- **Swagger UI**: http://127.0.0.1:8081/docs
- **Prediction**: `POST /api/app/`
- **Metrics**: http://localhost:8081/metrics

### Example Request
```python
import requests

data = {
    "region_id": 38.0,
    "city_id": 590.0,
    "tags_cont": 0.0,
    "tags_bhv": 0.5,
    "rubrica": 1.812,
    "rate": 1.7,
    "ctr_sort": 1.3072,
    "rv_perc": 66.41,
    "slider": 0
}

response = requests.post(
    "http://127.0.0.1:8081/api/app/",
    params={"ad_id": "test_ad_123"},
    json=data
)
print(response.json())
```

## 📈 Monitoring & Observability

### Prometheus Metrics
- Custom prediction counters
- Request latency histograms
- Model prediction distributions

### Grafana Dashboard
Access at http://localhost:3000
- Real-time prediction monitoring
- Performance metrics visualization
- System health indicators

### URLs
- **Prometheus**: http://localhost:9090
- **Grafana**: http://localhost:3000
- **API Docs**: http://127.0.0.1:8081/docs

## 🔧 Development

### Environment Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt
```

### Model Training
1. Run the Jupyter notebook `ad_click_prediction.ipynb`
2. Models will be automatically saved to `services/models/`
3. Use MLflow for experiment tracking

### Testing the API
```bash
cd services
python app/app.py
```

## 📋 Model Performance

| Model | F1 Score | ROC-AUC |
|-------|----------|---------|
| Baseline (Logistic Regression) | 0.652 | 0.734 |
| Random Forest | 0.652 | 0.748 |
| Random Forest + Features | 0.668 | 0.750 |
| **LightGBM** | **0.710** | **0.803** |

## 🏗️ Technical Stack

- **ML/Data**: Python, pandas, scikit-learn, LightGBM, MLflow
- **API**: FastAPI, Pydantic, uvicorn
- **Monitoring**: Prometheus, Grafana
- **Deployment**: Docker, Docker Compose
- **Visualization**: matplotlib, seaborn

## 📝 License

This project is available under the MIT License.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## ⚠️ Notes

- Model files are excluded from git due to size (use Git LFS if needed)
- Ensure proper environment variables are set for database connections
- The monitoring stack requires Docker Compose for full functionality
<br>На предикт ML модели выдается выборка объявлений доступных в текущий момент к показу, модель выдает по ним вероятность клика.

## Цель проекта
Построение модели для прогнозирования кликов по рекламному объявлению
	
## Ход исследования
- Знакомство с данными
- Исследовательский анализ данных
- Предобработка данных (при необходимости)
- Разработка дополнительных признаков (при необходимости)
- Построение baseline
- Обучение нескольких моделей
- Выбор лучшей модели
- Проверка важности признаков
- Проверка лучшей модели на отложенной выборке
- Заключение о проделанном исследовании

## Используемые инструменты
- python: pandas, seaborn, matplotlib, phik, category_encoders, LightGBM;
- mlflow;
- postgresql;
- bash;
- fastapi, grafana, prometheus

## Заключение:

Итоги проделанного исследования.

**Выбор целевых метрик**

- `ROC-AUC` (Receiver Operating Characteristic - Area Under the Curve) является метрикой,
  <br>которая оценивает качество бинарной классификации, учитывая полноту (True Positive Rate) и
  <br>специфичность (True Negative Rate) модели.
  <br>ROC-AUC измеряет способность модели различать между классами и представляет площадь под кривой ROC.
  <br>ROC-AUC особенно полезна, когда важно контролировать баланс между ложно-положительными и ложно-отрицательными предсказаниями.
  <br>Она также устойчива к несбалансированным классам.
- `F1-мера` является метрикой, которая оценивает точность и полноту модели для бинарной классификации.
  <br>F1-мера является гармоническим средним между точностью (precision) и полнотой (recall).
  <br>Она особенно полезна, когда важно достичь баланса между точностью и полнотой.
  <br>F1-мера хорошо работает, когда классы сбалансированы или когда важно минимизировать как ложно-положительные, так и ложно-отрицательные предсказания.

**Загрузка и ознакомление с данными**

- шаг выполнен полностью, трудностей не возникло;
- данные загружены;
- изучены типы данных;
- приняты решения о дальнейшей предобработке;

**Исследовательский анализ данных**

- шаг выполнен полностью, трудностей не возникло;
- исследованы зависимости и корреляции признаков;
- приняты решения об удалении неинформативных признаков;

**Построение базовой модели**

- в качестве базовой модели выбрана модель логистической регрессии;
- обусловлено это тем, что данная модель имеет небольшое количество гиперпараметров
  <br>и короткое время обучения;

**Генерация дополнительных признаков**

- шаг выполнен полностью, трудностей не возникло;
- разработаны несколько дополнительных признаков на основании уже существующих;

**Обучение моделей**

- шаг выполнен полностью, трудностей не возникло;
- обучены несколько различных моделей:
  - логистическая регрессия;
  - случайный лес;
  - градиентный бустинг;
  - градиентный бустинг с подбором гиперпараметров;
- наиболее высокое качество предсказания по выбранным метрикам показала модель градиентного бустинга.

**Итоговая оценка качества предсказания лучшей модели и анализ важности её признаков**

- шаг выполнен полностью, трудностей не возникло;
- на тестовой выборке модель показала неплохой результат ROC AUC = 0.82;
- модель верно предсказала 39092 отрицательных примеров и 34393 положительных примера;
- модель ошибочно предсказала 12124 отрицательных примеров как положительные и 13430 положительных примеров как отрицательные;
- наиболее важными для модели признаками определены:
  - процент видимости объявления;
  - значение ctr объявления;
  - ставка в рублях объявления;
  - тематика объявления;
  - значение таргетинга по поведению.

**Рекомендации**

- для получения более высокого качества предсказаний требуются дополнительные данные:
  - данные о пользователях;
  - временная последовательность;
  - возможно, ещё какая-то информация, которой обладает заказчик.

**Общий итог**

**Для решения поставленной задачи оптимальным образом подходит модель градиентного бустинга LightGBM**
