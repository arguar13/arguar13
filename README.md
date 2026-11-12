<p align="center">
  <img src="assets/banner.svg" alt="Armando Guarnera, Data Scientist and MLOps Engineer" width="100%">
</p>

<p align="center">
  <a href="https://armandoguar.com"><img src="https://img.shields.io/badge/Portfolio-armandoguar.com-0A5361?style=for-the-badge&logo=wordpress&logoColor=white" alt="Portfolio"></a> <a href="https://www.linkedin.com/in/arguar13/"><img src="https://img.shields.io/badge/LinkedIn-arguar13-0A5361?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a> <a href="mailto:contacto@armandoguar.com"><img src="https://img.shields.io/badge/Email-contacto%40armandoguar.com-0A5361?style=for-the-badge" alt="Email"></a> <a href="https://armandoguar.com/#cv"><img src="https://img.shields.io/badge/CV-English%20and%20Spanish-F2A54A?style=for-the-badge&logoColor=black" alt="Curriculum Vitae"></a>
</p>

---

## About

I'm a mathematician (**B.S. in Mathematics**, specialisation in Probability, Statistics and Mathematical Modelling) working as a **data scientist and MLOps engineer**. I build predictive models and the systems around them: versioned data, tracked experiments, promotion gates, containerised APIs on Kubernetes and drift monitoring.

Every project below is evaluated on **held-out data the model never saw** and comes with a written case study that explains each decision, including the shortcuts I chose not to take. Most use real-world data; the salary and grocery projects use public simulated datasets, and their write-ups say so.

**How I work**

| | |
| :--- | :--- |
| **Beat the obvious baseline** | Every model is measured against the simplest thing that could work: the last reading, the majority class, a naive guess. If it does not clearly beat it, it does not ship. |
| **Leakage-free by construction** | Splits by engine, customer or time. Transformations fitted inside the pipeline. Features limited to what exists at prediction time. |
| **Evaluate against the future** | Held-out years, unseen engines, time-based windows. I report the honest score, even when it is the modest one. |
| **Operate, don't just train** | Data and models versioned, promotion gates in a registry, services on Kubernetes and drift checks once the model is live. |

---

## Production ML systems

Three end-to-end MLOps projects that share the same lifecycle:

```mermaid
flowchart LR
    A[Raw data] --> B[Data contract<br/>Pandera, Pydantic]
    B --> C[Versioned data<br/>DVC, S3]
    C --> D[Training + tuning<br/>PyTorch, scikit-learn, Optuna]
    D --> E[MLflow tracking<br/>+ registry]
    E --> F{Promotion gate<br/>beats baseline?}
    F -- yes --> G[FastAPI service<br/>Docker]
    F -- no --> D
    G --> H[Kubernetes on EKS<br/>Kustomize, HPA]
    H --> I[Batch jobs + drift checks<br/>CronJobs]
    I -.-> D
```

| Project | Problem | Result on held-out data | Stack |
| :--- | :--- | :--- | :--- |
| [**Transformer oil temperature**](https://github.com/arguar13/Transformer-Oil-Temperature-MLOps) | 48-hour forecasts for a power transformer, promoted only if they beat the last reading | **1.72 °C** MAE on 3,389 unseen windows, **+5.8%** skill vs persistence | PyTorch: Optuna, DVC, MLflow, FastAPI, Kubernetes, Terraform, AWS, GitLab CI |
| [**Turbofan predictive maintenance**](https://github.com/arguar13/Turbofan-Predictive-Maintenance-MLOps) | Healthy, Alert or Critical from the last 30 flight cycles of NASA turbofan data | **88.4%** of Critical windows caught, **0.831** macro F1 on 142 unseen engines | PyTorch: Pandera, DVC, MLflow, FastAPI, Kubernetes, Terraform, GitLab CI, GitHub Actions |
| [**Hotel market-segment classifier**](https://github.com/arguar13/Hotel-Booking-MLOps) | Segment classifier with a feature contract, two promotion gates and daily drift monitoring | **0.818** macro F1 on test, **0.653** on 2017, a year it never saw | scikit-learn, Optuna, DVC, MLflow, FastAPI, PostgreSQL, Streamlit, Kubernetes, Terraform |

**Infrastructure behind them:** local first, then the cloud. Every change runs against Docker Compose and LocalStack before it reaches AWS, so most errors show up on the laptop instead of in a paid environment. All three were then deployed end to end on a real AWS account with Terraform (S3, ECR, EKS, RDS PostgreSQL, IAM with OIDC for CI, CloudWatch) and torn down afterwards to avoid running costs. CI/CD runs in GitLab CI, with quality checks in pytest, ruff, mypy and pre-commit.

---

## More case studies

<table>
  <tr>
    <th align="left">Area</th><th align="left">Project</th><th align="left">Result</th><th align="left">Tools</th>
  </tr>
  <tr>
    <td>Deep learning</td>
    <td><a href="https://github.com/arguar13/Vehicle-Image-Classification">Seven-class vehicle image classification</a></td>
    <td><b>0.969</b> macro F1 on unseen images</td>
    <td>PyTorch, torchvision, transfer learning</td>
  </tr>
  <tr>
    <td>Deep learning</td>
    <td><a href="https://github.com/arguar13/Turbofan-Predictive-Maintenance">Turbofan engine health from 30 flights</a></td>
    <td><b>0.79</b> macro F1 on unseen engines</td>
    <td>PyTorch, multivariate time series</td>
  </tr>
  <tr>
    <td>Deep learning</td>
    <td><a href="https://github.com/arguar13/Transformer-Oil-Temperature-Forecasting">One-hour transformer oil temperature</a></td>
    <td><b>0.436 °C</b> MAE, five architectures vs the last reading</td>
    <td>PyTorch, Optuna</td>
  </tr>
  <tr>
    <td>Machine learning</td>
    <td><a href="https://github.com/arguar13/AI4I-Predictive-Maintenance">Catching machine failures before they happen</a></td>
    <td><b>46 of 51</b> failures caught on test</td>
    <td>XGBoost, LightGBM, CatBoost, Optuna</td>
  </tr>
  <tr>
    <td>Machine learning</td>
    <td><a href="https://github.com/arguar13/Employee-Salary-Prediction">Salary prediction from 250,000 profiles</a></td>
    <td><b>0.981</b> R² on 50,000 unseen records</td>
    <td>scikit-learn, XGBoost, LightGBM, Optuna</td>
  </tr>
  <tr>
    <td>Machine learning</td>
    <td><a href="https://github.com/arguar13/Hotel-Booking-Segment-Classification">Hotel booking market segments</a></td>
    <td><b>0.77</b> macro F1 across 7 imbalanced classes</td>
    <td>scikit-learn, imbalanced-learn, XGBoost, LightGBM</td>
  </tr>
  <tr>
    <td>Machine learning</td>
    <td><a href="https://github.com/arguar13/Customer-Segmentation-Clustering">Segmenting a real online retailer</a></td>
    <td><b>77.7%</b> of next-quarter revenue from 33.8% of customers</td>
    <td>scikit-learn, clustering, Optuna</td>
  </tr>
  <tr>
    <td>Data engineering</td>
    <td><a href="https://github.com/arguar13/Grocery-Sales-SQL-Analytics">PostgreSQL warehouse for 6.76M sales lines</a></td>
    <td>Star schema, data-quality contracts, RFM and basket analysis</td>
    <td>PostgreSQL, SQL, SQLAlchemy</td>
  </tr>
  <tr>
    <td>Data engineering</td>
    <td><a href="https://github.com/arguar13/Uber-Eats-MongoDB-Analytics">MongoDB analytics for 63,381 restaurants</a></td>
    <td>Indexed rankings that only trust averages backed by evidence</td>
    <td>MongoDB, aggregation pipelines, PyMongo</td>
  </tr>
  <tr>
    <td>Analytics & BI</td>
    <td><a href="https://github.com/arguar13?tab=repositories&q=TABLEAU">Four Tableau dashboards</a></td>
    <td>Retail, telecom, banking and hospitality over 709,530 records</td>
    <td>Tableau, pandas</td>
  </tr>
</table>

---

## Toolkit

**Languages & data**<br>
<img src="https://img.shields.io/badge/Python-0A5361?style=flat-square&logo=python&logoColor=white" alt="Python"> <img src="https://img.shields.io/badge/SQL-0A5361?style=flat-square&logo=postgresql&logoColor=white" alt="SQL"> <img src="https://img.shields.io/badge/pandas-0A5361?style=flat-square&logo=pandas&logoColor=white" alt="pandas"> <img src="https://img.shields.io/badge/NumPy-0A5361?style=flat-square&logo=numpy&logoColor=white" alt="NumPy"> <img src="https://img.shields.io/badge/SciPy-0A5361?style=flat-square&logo=scipy&logoColor=white" alt="SciPy"> <img src="https://img.shields.io/badge/Jupyter-0A5361?style=flat-square&logo=jupyter&logoColor=white" alt="Jupyter">

**Machine learning & deep learning**<br>
<img src="https://img.shields.io/badge/scikit--learn-095F69?style=flat-square&logo=scikitlearn&logoColor=white" alt="scikit-learn"> <img src="https://img.shields.io/badge/XGBoost-095F69?style=flat-square" alt="XGBoost"> <img src="https://img.shields.io/badge/LightGBM-095F69?style=flat-square" alt="LightGBM"> <img src="https://img.shields.io/badge/CatBoost-095F69?style=flat-square" alt="CatBoost"> <img src="https://img.shields.io/badge/imbalanced--learn-095F69?style=flat-square" alt="imbalanced-learn"> <img src="https://img.shields.io/badge/Optuna-095F69?style=flat-square" alt="Optuna"> <img src="https://img.shields.io/badge/PyTorch-095F69?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch">

**MLOps**<br>
<img src="https://img.shields.io/badge/MLflow-0D536D?style=flat-square&logo=mlflow&logoColor=white" alt="MLflow"> <img src="https://img.shields.io/badge/DVC-0D536D?style=flat-square&logo=dvc&logoColor=white" alt="DVC"> <img src="https://img.shields.io/badge/FastAPI-0D536D?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI"> <img src="https://img.shields.io/badge/Pydantic-0D536D?style=flat-square&logo=pydantic&logoColor=white" alt="Pydantic"> <img src="https://img.shields.io/badge/Pandera-0D536D?style=flat-square" alt="Pandera"> <img src="https://img.shields.io/badge/pytest-0D536D?style=flat-square&logo=pytest&logoColor=white" alt="pytest"> <img src="https://img.shields.io/badge/Poetry-0D536D?style=flat-square&logo=poetry&logoColor=white" alt="Poetry"> <img src="https://img.shields.io/badge/pre--commit-0D536D?style=flat-square&logo=precommit&logoColor=white" alt="pre-commit"> <img src="https://img.shields.io/badge/Streamlit-0D536D?style=flat-square&logo=streamlit&logoColor=white" alt="Streamlit">

**Infrastructure & cloud**<br>
<img src="https://img.shields.io/badge/Docker-183F75?style=flat-square&logo=docker&logoColor=white" alt="Docker"> <img src="https://img.shields.io/badge/Kubernetes-183F75?style=flat-square&logo=kubernetes&logoColor=white" alt="Kubernetes"> <img src="https://img.shields.io/badge/Kustomize-183F75?style=flat-square" alt="Kustomize"> <img src="https://img.shields.io/badge/Terraform-183F75?style=flat-square&logo=terraform&logoColor=white" alt="Terraform"> <img src="https://img.shields.io/badge/AWS-S3%2C%20ECR%2C%20EKS%2C%20RDS-183F75?style=flat-square" alt="AWS"> <img src="https://img.shields.io/badge/LocalStack-183F75?style=flat-square" alt="LocalStack"> <img src="https://img.shields.io/badge/GitLab%20CI-183F75?style=flat-square&logo=gitlab&logoColor=white" alt="GitLab CI"> <img src="https://img.shields.io/badge/GitHub%20Actions-183F75?style=flat-square&logo=githubactions&logoColor=white" alt="GitHub Actions">

**Databases, visualisation & BI**<br>
<img src="https://img.shields.io/badge/PostgreSQL-0A5361?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL"> <img src="https://img.shields.io/badge/MongoDB-0A5361?style=flat-square&logo=mongodb&logoColor=white" alt="MongoDB"> <img src="https://img.shields.io/badge/Tableau-0A5361?style=flat-square" alt="Tableau"> <img src="https://img.shields.io/badge/Matplotlib-0A5361?style=flat-square" alt="Matplotlib"> <img src="https://img.shields.io/badge/Seaborn-0A5361?style=flat-square" alt="Seaborn">

**Mathematics & statistics**<br>
<img src="https://img.shields.io/badge/Probability%20%26%20stochastic%20processes-183F75?style=flat-square" alt="Probability & stochastic processes"> <img src="https://img.shields.io/badge/Inferential%20statistics-183F75?style=flat-square" alt="Inferential statistics"> <img src="https://img.shields.io/badge/Hypothesis%20testing%20%26%20ANOVA-183F75?style=flat-square" alt="Hypothesis testing & ANOVA"> <img src="https://img.shields.io/badge/Linear%20models%20%26%20least%20squares-183F75?style=flat-square" alt="Linear models & least squares"> <img src="https://img.shields.io/badge/Matrix%20algebra-183F75?style=flat-square" alt="Matrix algebra"> <img src="https://img.shields.io/badge/Differential%20equations-183F75?style=flat-square" alt="Differential equations"> <img src="https://img.shields.io/badge/Biostatistics-183F75?style=flat-square" alt="Biostatistics">

**Security**<br>
<img src="https://img.shields.io/badge/ISC%C2%B2-Certified%20in%20Cybersecurity-095F69?style=flat-square" alt="ISC2 CC"> <img src="https://img.shields.io/badge/IBM-Cybersecurity%20Analyst-095F69?style=flat-square" alt="IBM Cybersecurity Analyst"> <img src="https://img.shields.io/badge/Linux-bash%20and%20hardening-095F69?style=flat-square&logo=linux&logoColor=white" alt="Linux"> <img src="https://img.shields.io/badge/Secure%20API%20design-095F69?style=flat-square" alt="Secure API design"> <img src="https://img.shields.io/badge/IAM%20with%20OIDC%20for%20CI-095F69?style=flat-square" alt="IAM with OIDC for CI">

---

## Education

**B.S. in Mathematics**, Universidad Nacional de Santiago del Estero<br>
Specialisation in Probability, Statistics and Mathematical Modelling.<br>
**Teaching Assistant, Probability & Statistics**: almost two years explaining inference, distributions and modelling to undergraduates.

<details>
<summary><b>Selected certifications</b></summary>
<br>

| Area | Certifications |
| :--- | :--- |
| Mathematics & modelling | Johns Hopkins University: Advanced Linear Models, Calculus series<br>HKUST: Matrix Algebra, Differential Equations |
| Data science & machine learning | Johns Hopkins University: Mathematical Biostatistics I & II<br>IBM: Data Science Methodology, Machine Learning<br>University of Michigan: Python Data Structures<br>University of London: Machine Learning for All |
| Cybersecurity & infrastructure | ISC²: Certified in Cybersecurity (CC), SSCP coursework<br>IBM: Cybersecurity Analyst<br>Google: Foundations of Cybersecurity<br>Infosec: Python for Reconnaissance & Privilege Escalation<br>LearnQuest: Linux LFCA preparation |

</details>

