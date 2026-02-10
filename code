import streamlit as st
import os
from dotenv import load_dotenv
from google import genai
from datetime import datetime

# 1. PAGE SETUP
st.set_page_config(page_title="Insightify AI", page_icon="📈", layout="wide")

# 2. CSS: HEADER-IN-BOX & PRODUCTION UI
st.markdown("""
    <style>
    .stApp {
        background: linear-gradient(135deg, #16133a 0%, #1c194b 100%);
        color: white;
    }
    [data-testid="stSidebar"] { background-color: #f8f9fc !important; border-right: 1px solid #e3e6f0; }
    [data-testid="stSidebar"] .stMarkdown h2, [data-testid="stSidebar"] .stMarkdown p { color: #4e4e4e !important; }
    .main-title { color: #4ed8ff !important; font-size: 52px !important; font-weight: 800 !important; margin-bottom: 0px; }
    .sub-headline { color: #4ed8ff !important; font-size: 20px !important; font-style: italic; margin-bottom: 25px !important; }

    /* UI FIX: Heading inside the white box */
    div[data-testid="stWidgetLabel"] p {
        background-color: #ffffff !important;
        color: #16133a !important;
        font-weight: 800 !important;
        font-size: 18px !important;
        padding: 10px 20px !important;
        border-radius: 15px 15px 0px 0px !important;
        margin-bottom: -15px !important;
        border: 2px solid #4ed8ff;
        border-bottom: none;
    }
    
    .stTextArea textarea {
        background-color: #ffffff !important;
        color: #1c194b !important;
        font-weight: 500 !important;
        border: 2px solid #4ed8ff !important;
        border-top: 1px solid #eee !important;
        border-radius: 0px 0px 15px 15px !important;
        padding: 15px !important;
    }

    .stButton>button {
        background: linear-gradient(90deg, #6648d7 0%, #4766f9 100%) !important;
        color: white !important;
        border-radius: 12px !important;
        font-weight: bold !important;
        padding: 15px !important;
        width: 100%;
        margin-top: 15px;
        border: none !important;
    }

    .report-box { 
        padding: 25px; background: rgba(255, 255, 255, 0.08); 
        border-radius: 15px; border-left: 6px solid #4ed8ff; margin-top: 30px;
        color: white !important;
    }
    </style>
    """, unsafe_allow_html=True)

# 3. INITIALIZATION
# In production, we get the key from st.secrets instead of .env
api_key = st.secrets.get("GOOGLE_API_KEY") or os.getenv("GOOGLE_API_KEY")
client = genai.Client(api_key=api_key)

if 'history' not in st.session_state: st.session_state.history = []
if 'active_report' not in st.session_state: st.session_state.active_report = ""

# 4. SIDEBAR
with st.sidebar:
    st.markdown("## 🚀 System Status")
    st.success("Core: Gemini 3 Flash")
    st.info("SDK: Google-GenAI 2026")
    st.write("---")
    st.markdown("## 📜 Archive / History")
    if not st.session_state.history:
        st.caption("No records found.")
    else:
        for i, item in enumerate(reversed(st.session_state.history)):
            if st.button(f"📄 Log: {item['time']}", key=f"hist_{i}"):
                st.session_state.active_report = item['content']
    
    if st.button("🗑️ Clear Archive"):
        st.session_state.history = []
        st.session_state.active_report = ""
        st.rerun()

# 5. MAIN UI
st.markdown('<h1 class="main-title">📈 Insightify</h1>', unsafe_allow_html=True)
st.markdown('<p class="sub-headline">Enterprise Sentiment & Strategic Intelligence</p>', unsafe_allow_html=True)

col1, col2 = st.columns([2, 1])

with col1:
    user_input = st.text_area("📄 DATA INGESTION STREAM:", placeholder="Paste feedback logs here...", height=300)
    
    if st.button("🚀 EXECUTE STRATEGIC ANALYSIS"):
        if user_input:
            with st.spinner("🧠 Analyzing..."):
                try:
                    #
                    response = client.models.generate_content(
                        model="gemini-3-flash-preview", 
                        contents=f"Analyze this data and provide 1. Summary, 2. Pain Points, 3. Roadmap: {user_input}"
                    )
                    st.session_state.active_report = response.text
                    st.session_state.history.append({"time": datetime.now().strftime("%H:%M:%S"), "content": response.text})
                except Exception as e:
                    st.error(f"Error: {e}")
        else:
            st.warning("Please enter some data.")

with col2:
    st.markdown("## 💡 Instructions")
    st.write("1. Ingest raw feedback data.")
    st.write("2. Generate AI Strategy.")
    st.write("3. View Archive in Sidebar.")
    st.write("4. Download for stakeholders.")

# 6. RESULTS
if st.session_state.active_report:
    st.markdown('<div class="report-box">', unsafe_allow_html=True)
    st.markdown("### 📊 STRATEGIC INTELLIGENCE REPORT")
    st.markdown(st.session_state.active_report)
    st.markdown('</div>', unsafe_allow_html=True)
    
    st.download_button("📥 DOWNLOAD REPORT", st.session_state.active_report, "Insightify_Report.txt")

st.write("---")
st.caption("Mansi • Feb 2026 • Gemini 3 Flash Deployment")
