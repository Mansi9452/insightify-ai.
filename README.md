# 📈 Insightify AI: Enterprise Strategic Intelligence

**Insightify AI** is a next-generation sentiment analysis and strategic planning terminal designed for the 2026 enterprise landscape. By leveraging the high-speed reasoning of the **Gemini 3 Flash** model, it transforms unstructured feedback streams—from CEO rants to technical logs—into actionable 30-day roadmaps.

## 🚀 Key Features

* **Gemini 3 Flash Engine**: Powered by the latest Flash variant for near-instantaneous processing of complex datasets.
* **Strategic Roadmapping**: Automatically generates 30-day action plans and identifies critical pain points from raw text.
* **System Persistence**: Features a dynamic Sidebar Archive to track and review previous intelligence logs during a session.
* **Stakeholder Ready**: One-click report generation with professional text exports for immediate distribution.
* **Adaptive UI**: A bespoke, high-contrast dark-mode interface built for executive focus.

## 🛠️ Technical Stack

* **Core Model**: Gemini 3 Flash (v1beta).
* **SDK**: Google-GenAI 2026.
* **Frontend**: Streamlit 1.28.0 (Custom CSS Overhaul).
* **Deployment**: Streamlit Community Cloud.

## 💻 Installation & Setup

1. **Clone the Repository**:
```bash
git clone https://github.com/your-username/insightify-ai.git
cd insightify-ai

```


2. **Install Dependencies**:
```bash
pip install -r requirements.txt

```


3. **Environment Configuration**:
Create a `.env` file in the root directory and add your API key:
```text
GOOGLE_API_KEY=your_actual_api_key_here

```


4. **Run Locally**:
```bash
streamlit run app.py

```



## 📊 Deployment

This project is optimized for **Streamlit Community Cloud**. To deploy:

1. Push this code to a public GitHub repo.
2. Connect the repo to Streamlit Cloud.
3. Add `GOOGLE_API_KEY` to the **Secrets** manager in the Streamlit dashboard.

