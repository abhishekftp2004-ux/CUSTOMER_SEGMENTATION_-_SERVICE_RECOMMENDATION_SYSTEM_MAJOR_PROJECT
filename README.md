# Customer Segmentation & Service Recommendation System

## Project overview
This project builds a customer analytics workflow that groups customers by behavioral and engagement patterns, profiles the resulting groups, and suggests suitable services or learning programs. It is designed for a Veda Technology-style services/learning business scenario.

**Important:** `data/customer_data.csv` is synthetic demonstration data created for this project. It is not real customer information. Replace it with approved, consented data before making business decisions.

## Objectives
- Clean missing values and prepare numerical features.
- Standardize features so high-value numeric columns do not dominate distance calculations.
- Compare candidate cluster counts using inertia (elbow method) and silhouette score.
- Use K-Means to group customers.
- Use PCA to project high-dimensional customer behavior into two dimensions for visualization.
- Create cluster profiles, interpretable customer segment labels, and rule-based service recommendations.
- Explore results through a Streamlit dashboard and export filtered customer records.

## Technology stack
Python, Pandas, NumPy, scikit-learn, Matplotlib, Seaborn, Streamlit, Joblib, Jupyter Notebook.

## Dataset fields
- `customer_id`: unique synthetic customer identifier
- `age`: customer age
- `website_visits_30d`: visits in the last 30 days
- `monthly_spend_inr`: monthly spend in INR
- `service_inquiries_90d`: service inquiries over 90 days
- `engagement_score`: engagement score from 0 to 100
- `tenure_months`: months since becoming a customer
- `satisfaction_score`: satisfaction rating from 1 to 5
- `courses_enrolled`: number of enrolled learning courses
- `preferred_channel`: preferred communication channel
- `region`: broad region

## Run locally
1. Install Python 3.10+.
2. Open a terminal in this project folder.
3. Create and activate a virtual environment (recommended).
4. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
5. Run the analytics pipeline:
   ```bash
   python run_pipeline.py
   ```
6. Launch the dashboard:
   ```bash
   streamlit run app.py
   ```
7. Optional: open `Customer_Segmentation_Analysis.ipynb` in Jupyter Notebook and run cells in order.

## Output files
The pipeline creates:
- `outputs/cluster_metrics.csv` — inertia and silhouette scores for k=2..8
- `outputs/segmented_customers.csv` — customer rows, cluster IDs, PCA coordinates, segment names and recommendations
- `outputs/cluster_profiles.csv` — cluster-level averages
- `outputs/elbow_method.png` — elbow chart
- `outputs/silhouette_scores.png` — silhouette chart
- `outputs/customer_clusters.png` — PCA scatter plot
- `outputs/run_summary.json` — run summary
- `outputs/clustering_model.joblib` — saved clustering model and feature metadata

## Methodology
1. **Data quality:** inspect types and missingness; impute numeric values with the median and categorical values with the most frequent category.
2. **Feature scaling:** StandardScaler puts numerical features on a comparable scale before K-Means.
3. **Model selection:** compare k=2 through k=8 with inertia and silhouette score. The elbow chart shows diminishing inertia returns; silhouette measures separation/cohesion.
4. **Clustering:** K-Means assigns each customer to one of four clusters as a practical initial configuration. Review the metric results and business context before finalizing k.
5. **Interpretation:** cluster IDs are arbitrary. Segment labels and recommendations are generated using transparent rules; they are not the same thing as the unsupervised cluster labels.
6. **Visualization:** PCA compresses the scaled feature space to two dimensions for a visual overview. Distances in this plot are approximate.
7. **Recommendation logic:** readable rules map behavior to a potential service or learning program. Test these rules with business stakeholders and customer feedback.

## Limitations and responsible use
- Synthetic data cannot establish real customer behavior or business impact.
- K-Means favors roughly spherical clusters and can be sensitive to outliers and feature scaling.
- Rule-based recommendations are starting suggestions, not validated predictions.
- Avoid using sensitive personal attributes; comply with applicable privacy, consent, retention and access requirements.
- Monitor segment stability, recommendation acceptance, satisfaction, conversion, and fairness after a real deployment.

## Suggested business KPIs
- Segment size and share
- Average spend and engagement by segment
- Repeat visit rate
- Recommendation click/acceptance rate
- Course/service conversion rate
- Customer satisfaction after recommendation
- Retention and churn rate by segment

## Future enhancements
- Add a time-based holdout to evaluate changes in behavior.
- Tune feature weights and cluster count with stakeholder input.
- Compare K-Means with hierarchical clustering or DBSCAN.
- Add recommendation feedback collection and A/B testing.
- Deploy with authentication, data governance, logging and monitoring.
