# 🎬 Movie Information Extractor

An AI-powered **Movie Information Extractor** that takes a movie description or paragraph as input and converts it into structured movie data using **LangChain, Pydantic, and an LLM**.

The project demonstrates how to use **PydanticOutputParser** to force an LLM to return structured information such as the movie title, release year, genre, director, cast, rating, and summary.

---

## 🚀 Features

* 🎬 Extract movie information from natural-language text
* 🤖 Uses an LLM through LangChain
* 📋 Converts unstructured text into structured JSON
* ✅ Uses Pydantic for data validation
* 🧩 Uses `PydanticOutputParser` for structured output
* 🌐 Streamlit web interface
* 🔐 API keys stored securely using `.env`
* ⚡ Cached model initialization with Streamlit
* ❌ Handles invalid input and parsing errors

---

## 🛠️ Tech Stack

* **Python**
* **Streamlit**
* **LangChain**
* **LangChain Core**
* **Pydantic**
* **python-dotenv**
* **Groq API**

---

## 📁 Project Structure

```text
cinsage/
│
├── uicore.py
├── .env
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 📦 Installation

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

Move into the project directory:

```bash
cd cinsage
```

---

### 2. Create a virtual environment

Windows:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\activate
```

---

### 3. Install dependencies

```powershell
pip install -r requirements.txt
```

If you don't have a `requirements.txt` yet, install the required packages:

```powershell
pip install streamlit python-dotenv langchain langchain-core langchain-mistralai pydantic
```

For the Groq version:

```powershell
pip install streamlit python-dotenv langchain langchain-core langchain-groq pydantic
```

---

# 🔑 API Key Configuration

This project uses an API key to communicate with the AI model.

Create a file named:

```text
.env
```

inside the project directory.


### For Groq

```env
GROQ_API_KEY=your_groq_api_key
```

The Python application loads the environment variables using:

```python
from dotenv import load_dotenv

load_dotenv()
```

---

# 🔒 Important: Never Upload Your API Key

**Do not upload your `.env` file to GitHub.**

Create a `.gitignore` file:

```gitignore
.env
.venv/
__pycache__/
*.pyc
```

This prevents your API key from being uploaded to GitHub.

If you accidentally uploaded an API key, **revoke/regenerate the key immediately** from the relevant API provider.

---

# 🧠 How It Works

The application follows this workflow:

```text
User enters movie description
          ↓
      Streamlit UI
          ↓
     ChatPromptTemplate
          ↓
          LLM
          ↓
 PydanticOutputParser
          ↓
    Pydantic Movie Model
          ↓
      Structured JSON
```

---

# 📋 Data Schema

The application extracts the following information:

```python
class Movie(BaseModel):
    title: str
    release_year: Optional[int]
    genre: List[str]
    director: Optional[str]
    cast: List[str]
    rating: Optional[float]
    summary: str
```

### Example output

Input:

```text
3 Idiots is a 2009 Indian Hindi-language comedy-drama film directed by Rajkumar Hirani. It stars Aamir Khan, R. Madhavan and Sharman Joshi. The movie follows three engineering students and their journey through college life, friendship and pressure.
```

Possible structured output:

```json
{
  "title": "3 Idiots",
  "release_year": 2009,
  "genre": [
    "Comedy",
    "Drama"
  ],
  "director": "Rajkumar Hirani",
  "cast": [
    "Aamir Khan",
    "R. Madhavan",
    "Sharman Joshi"
  ],
  "rating": null,
  "summary": "Three engineering students experience college life, friendship and academic pressure while learning important lessons about life."
}
```

---

# 🌐 Running the Streamlit Application

Start the application using:

```powershell
python -m streamlit run uicore.py
```

Or:

```powershell
streamlit run uicore.py
```

After starting the application, Streamlit will provide a local URL similar to:

```text
http://localhost:8501
```

Open the URL in your browser.

---

# 💻 Streamlit Interface

The application provides:

* Movie description text area
* **Extract Data** button
* Raw model response
* Structured movie information
* Error handling
* Success notification

---

# 🧩 Main Components

## 1. Environment Variables

```python
from dotenv import load_dotenv

load_dotenv()
```

Loads API keys and other environment variables from `.env`.

---

## 2. Prompt Template

```python
prompt = ChatPromptTemplate.from_messages([
    ("system", """
    Extract movie information from the paragraph.
    {format_instructions}
    """),
    ("human", "{paragraph}")
])
```

The prompt tells the model to extract movie information according to the required format.

---

## 3. Pydantic Model

```python
class Movie(BaseModel):
    title: str
    release_year: Optional[int]
    genre: List[str]
    director: Optional[str]
    cast: List[str]
    rating: Optional[float]
    summary: str
```

This defines the expected structure of the extracted movie information.

---

## 4. Pydantic Output Parser

```python
parser = PydanticOutputParser(
    pydantic_object=Movie
)
```

The parser converts the model response into a validated Pydantic object.

---

## 5. Streamlit Model Caching

```python
@st.cache_resource
def get_model():
    return init_chat_model(model="openai/gpt-oss-120b",model_provider="groq",temperature =0.9)
```

Caching prevents Streamlit from unnecessarily creating a new model object on every interaction.

---

# 📄 Requirements

Example `requirements.txt`:

If you are using Groq instead of Mistral:

```txt
streamlit
python-dotenv
langchain
langchain-core
langchain-groq
pydantic
```

---




# 🔐 GitHub Security

Before pushing the project:

```powershell
git status
```

Make sure `.env` is **not** listed as a file that will be committed.

Then:

```powershell
git add .
git commit -m "Initial commit"
git push
```

Your repository should contain:

```text
uicore.py
requirements.txt
.gitignore
README.md
```

but **not**:

```text
.env
```

---

# 🎯 Learning Objectives

This project demonstrates:

* Working with LLMs
* LangChain fundamentals
* Prompt engineering
* Structured LLM output
* Pydantic data validation
* Environment variables
* API key management
* Streamlit application development
* Error handling
* Building an AI-powered application

---

# 🔮 Future Improvements

Possible improvements include:

* 🎥 Movie poster generation
* 🔎 Movie search functionality
* ⭐ IMDb/TMDB integration
* 🎭 Actor information
* 🎬 Trailer links
* 💾 Save extracted movies to a database
* 📊 Movie analytics dashboard
* 🔍 Search and filter extracted movies
* 📥 Export movie information as JSON/CSV
* 🎨 Improve Streamlit UI
* 🌍 Deploy the application online

---

# 👨‍💻 Author

**Manya Rajput**

This project was created as a learning project for exploring **Generative AI, LangChain, Pydantic, and Streamlit**.

---

## ⭐ If You Like This Project

Give the repository a ⭐ on GitHub and feel free to improve the project!
