# 🩺 Medical Chatbot using Uri AI & Flask

An interactive AI-powered medical chatbot built with **Flask** and **Uri AI Foundation Models**. The application provides preliminary healthcare information through a user-friendly web interface while encouraging users to seek advice from qualified medical professionals.

---

## 🚀 Features

- ✅ AI-powered medical assistant using Uri AI SDK
- ✅ Flask-based backend API
- ✅ Interactive web chat interface
- ✅ Prompt guardrails for responsible medical responses
- ✅ JSON REST API endpoint
- ✅ HTTP error handling and validation
- ✅ Environment variable support with `.env`
- ✅ Clean and responsive UI

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| Python 3.11 | Programming Language |
| Flask | Backend Framework |
| Uri AI SDK | AI Model Integration |
| python-dotenv | Environment Variable Management |
| HTML5 | Frontend Structure |
| CSS3 | Styling |
| JavaScript | Client-side Interaction |

---

## 📂 Project Structure

```text
medical-chatbot-uri-ai/
│
├── app.py
├── requirements.txt
├── .env
│
├── templates/
│   └── index.html
│
└── static/
    └── style.css
```

---

## 🏗️ Architecture

```text
User
 │
 ▼
Frontend (HTML + CSS + JavaScript)
 │
 ▼
Flask Backend (/chat)
 │
 ▼
Prompt Engineering & Guardrails
 │
 ▼
Uri AI SDK Client
 │
 ▼
Uri AI Foundation Model
 │
 ▼
Response Parsing
 │
 ▼
JSON Response
 │
 ▼
Chat UI
```

---

## ⚙️ Installation

### 1. Clone Repository

```bash
git clone https://github.com/your-username/medical-chatbot-uri-ai.git
cd medical-chatbot-uri-ai
```

### 2. Create Virtual Environment

Using Conda:

```bash
conda create -n LLM_app python=3.11 -y
conda activate LLM_app
```

Or using venv:

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

### 3. Install Dependencies

Create a `requirements.txt` file:

```text
Flask
python-dotenv
uri-ai
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 🔑 Environment Variables

Create a `.env` file in the root directory:

```env
UDEAI_API_KEY=your_api_key_here
```

Get your API key from the Uri AI Developer Portal.

---

## ▶️ Running the Application

Start the Flask server:

```bash
python app.py
```

Application will be available at:

```text
http://localhost:8080
```

---

## 💻 Sample Backend Code

```python
import os
from flask import Flask, render_template, request, jsonify
from uri_ai import UriClient
from dotenv import load_dotenv

load_dotenv()

api_key = os.getenv("UDEAI_API_KEY")

client = UriClient(
    api_key=api_key,
    model="gpt-4.1-nano"
)

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("index.html")

@app.route('/chat', methods=['POST'])
def chat():
    try:
        user_message = request.json.get("message")

        if not user_message:
            return jsonify({
                "error": "message is required"
            }), 400

        prompt = f"""
        You are a helpful medical assistant.
        Provide general medical information and
        always encourage consultation with a doctor.

        User Question:
        {user_message}
        """

        response = client.generate_completion(
            prompt=prompt,
            temperature=0.7,
            max_tokens=300
        )

        reply = response["choices"][0]["message"]["content"]

        return jsonify({
            "response": reply
        })

    except Exception as e:
        return jsonify({
            "error": str(e)
        }), 500

if __name__ == "__main__":
    app.run(
        host="0.0.0.0",
        port=8080,
        debug=True
    )
```

---

## 📡 API Documentation

### Endpoint

```http
POST /chat
```

### Request Headers

```http
Content-Type: application/json
```

### Request Body

```json
{
  "message": "I have a fever since yesterday."
}
```

### Success Response

**HTTP 200**

```json
{
  "response": "Fever can occur due to several reasons. Please stay hydrated and consult a healthcare professional for proper diagnosis."
}
```

### Validation Error

**HTTP 400**

```json
{
  "error": "message is required"
}
```

### Server Error

**HTTP 500**

```json
{
  "error": "Detailed exception message"
}
```

---

## 🔒 Medical Disclaimer

> This chatbot is intended for educational and informational purposes only.
> It does not provide medical diagnoses, treatment plans, or professional healthcare advice.
> Always consult a qualified healthcare provider for medical concerns.

---

## 🔮 Future Enhancements

### 1. Retrieval-Augmented Generation (RAG)

- Integrate Pinecone, FAISS, or Qdrant
- Retrieve information from verified medical literature
- Ground responses using trusted clinical sources

### 2. Conversational Memory

- Redis-based chat history
- Multi-turn context awareness
- Session management

### 3. Real-Time Streaming

- Server-Sent Events (SSE)
- WebSockets
- Token-by-token response generation

### 4. Authentication & Security

- User login and registration
- API rate limiting
- Request validation
- Secure session handling

### 5. Deployment

- Docker support
- AWS / Azure deployment
- CI/CD pipeline with GitHub Actions

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a new feature branch
3. Commit your changes
4. Push to your branch
5. Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

Developed with ❤️ using Flask and Uri AI.
