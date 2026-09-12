# 🤖 Local AI Chatbot — Ollama + Streamlit

A professional **local AI chatbot** built with **Python, Streamlit, and Ollama**. The application provides a ChatGPT-style conversational interface while running the language model locally on your own machine.

The project is designed as a beginner-friendly **Generative AI project** for understanding how local LLM applications work, including conversation memory, streaming responses, temperature control, system prompts, and communication with a locally hosted Ollama model.

---

## 🚀 Features

* 🤖 **Local LLM inference** using Ollama
* 💬 **ChatGPT-style conversational UI**
* 🧠 **Conversation memory** within the current session
* ⚡ **Streaming responses** for a real-time chat experience
* 🎛️ **Temperature control** to adjust response creativity
* 📝 **Custom system prompts**
* 🔄 **Multiple Ollama model selection**
* 🩺 **Ollama health check** before starting the chat
* 🧹 **Clear conversation** functionality
* 🌐 **No OpenAI API key required**
* 🔒 **Local-first architecture** — prompts and responses are sent to your local Ollama server
* 🌍 Supports multilingual interaction, including prompts such as Telugu questions

---

## 🧠 Hallucination-Aware Responses

One of the goals of this project is to demonstrate how a local LLM can behave responsibly when it does not have reliable information.

For example, when asked:

> **Who won the IPL match in 2030?**

The chatbot responds that it cannot provide the result because the event is in the future and the outcome is not known.

Instead of inventing a team or pretending to have access to future sports data, it clearly explains the limitation.

### Example

```text
User:
Who won the IPL match in 2030?

Assistant:
I don't have real-time data or the ability to predict future events,
including sports matches. The Indian Premier League matches in 2030
have not yet been played, and the outcome of such matches is not known.
```

This demonstrates an important Generative AI principle:

> **When reliable information is unavailable, the model should acknowledge the limitation instead of confidently fabricating an answer.**

### ⚠️ Important Note

This project is **hallucination-aware**, but it does not mathematically guarantee zero hallucinations.

LLMs can still generate incorrect information. The application's behavior depends on the selected model, system prompt, temperature, and conversation context.

For knowledge-grounded applications, this chatbot can later be extended into a **RAG (Retrieval-Augmented Generation)** system so that responses are based on retrieved documents.

---

## 🏗️ Architecture

```text
                ┌──────────────────────┐
                │      User            │
                │   Chat Interface     │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │      Streamlit       │
                │       app.py         │
                └──────────┬───────────┘
                           │
                  HTTP POST /api/chat
                           │
                           ▼
                ┌──────────────────────┐
                │       Ollama         │
                │   Local LLM Server   │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │   Selected LLM       │
                │ llama / Mistral /    │
                │ Gemma / Qwen / etc.  │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │ Streaming Response   │
                └──────────┬───────────┘
                           │
                           ▼
                ┌──────────────────────┐
                │   Streamlit Chat UI  │
                └──────────────────────┘
```

---

## 🔄 How It Works

The application follows this basic workflow:

```text
User enters a message
        ↓
Message added to session history
        ↓
System prompt + conversation history
        ↓
Sent to Ollama API
        ↓
Local LLM generates response
        ↓
Response streamed token-by-token
        ↓
Response displayed in Streamlit
        ↓
Assistant response stored in conversation memory
```

---

## 🧩 Technologies Used

| Technology | Purpose                       |
| ---------- | ----------------------------- |
| Python     | Application logic             |
| Streamlit  | Web-based chat interface      |
| Ollama     | Local LLM runtime             |
| Requests   | Communication with Ollama API |
| HTML/CSS   | UI customization              |

---

## 📁 Project Structure

```text
AI-CHATBOT/
│
├── app.py
├── requirements.txt
│
└── screenshot/
    └── Screenshot.png
```

### `app.py`

Main Streamlit application containing:

* UI configuration
* Ollama connection
* model selection
* temperature control
* system prompt
* conversation memory
* streaming response handling
* error handling

### `requirements.txt`

Contains the Python dependencies required to run the application.

---

## ⚙️ Requirements

### Hardware

A dedicated GPU is helpful but not mandatory.

For example, this application can run locally on a laptop with:

* **16 GB RAM**
* **NVIDIA RTX 2050 4 GB VRAM**
* **Intel Core i5-12450H**

Smaller quantized models are recommended for hardware with limited VRAM.

> The exact performance depends on the selected Ollama model, quantization, context size, and available RAM/VRAM.

---

# 🛠️ Installation

## 1. Clone the Repository

```bash
git clone https://github.com/your-username/AI-CHATBOT.git
```

Navigate into the project:

```bash
cd AI-CHATBOT
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv .venv
```

Activate it:

```bash
.venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🦙 Install Ollama

Download and install Ollama for your operating system.

After installation, verify it:

```bash
ollama --version
```

Start the Ollama service if necessary:

```bash
ollama serve
```

---

# 📥 Download an LLM

For a lightweight starting model:

```bash
ollama pull llama3.2
```

You can verify installed models using:

```bash
ollama list
```

You can also test the model directly:

```bash
ollama run llama3.2
```

---

# ▶️ Run the Chatbot

Start the Streamlit application:

```bash
streamlit run app.py
```

Streamlit will provide a local address similar to:

```text
http://localhost:8501
```

Open that address in your browser.

---

# ⚙️ Available Settings

The sidebar provides several controls.

## Model Selection

The application allows you to select different Ollama models, including models such as:

```text
llama3.2
llama3.1
llama3
mistral
gemma2
qwen2.5
qwen2.5:3b
```

Make sure the model you select has been downloaded using:

```bash
ollama pull <model-name>
```

For example:

```bash
ollama pull qwen2.5:3b
```

---

## 🌡️ Temperature

Temperature controls the randomness of the model's responses.

```text
0.0 ─────────────────────── 1.0
Focused                       Creative
```

### Lower temperature

Useful for:

* factual questions
* technical explanations
* deterministic responses
* structured outputs

### Higher temperature

Useful for:

* brainstorming
* creative writing
* generating ideas
* conversational responses

A lower temperature can help reduce unnecessary variation, but **temperature alone cannot eliminate hallucinations**.

---

# 📝 System Prompt

The application allows you to define a custom system prompt.

Default behavior:

```text
You are a helpful AI assistant.
Explain concepts clearly and simply.
When useful, respond with examples.
```

The system prompt establishes the assistant's general behavior and response style.

For example, you can create a more cautious assistant:

```text
You are a helpful AI assistant.

Do not invent facts.
If you do not know something, clearly say that you do not know.
Do not claim access to real-time or future information.
Explain your reasoning clearly and concisely.
```

---

# 🧠 Conversation Memory

The application maintains conversation history using Streamlit's:

```python
st.session_state
```

Messages are stored in:

```python
st.session_state.messages
```

The conversation history is then sent to Ollama along with the system prompt.

Conceptually:

```text
System Prompt
      +
User Message 1
      +
Assistant Response 1
      +
User Message 2
      +
Assistant Response 2
      ↓
     Ollama
```

This allows the model to understand previous messages in the current conversation.

### Important

The LLM itself is fundamentally stateless between API calls.

The application creates conversational memory by sending previous messages back to the model.

---

# ⚡ Streaming Responses

Instead of waiting for the entire response, the application uses Ollama's streaming API.

```text
Ollama
   │
   ├── Response chunk 1
   ├── Response chunk 2
   ├── Response chunk 3
   ├── Response chunk 4
   │
   ▼
Streamlit UI
```

This makes the application feel much more responsive and similar to modern AI chat applications.

---

# 🔒 Privacy

One of the major advantages of this project is its local architecture.

```text
User
 ↓
Streamlit
 ↓
localhost
 ↓
Ollama
 ↓
Local LLM
```

The application communicates with the local Ollama endpoint:

```text
http://localhost:11434/api/chat
```

No OpenAI API key is required.

However, privacy ultimately depends on the model/runtime and any additional services you connect to the application.

---

# 🩺 Ollama Health Check

Before allowing the user to chat, the application checks whether Ollama is running.

If Ollama is unavailable, the application displays an error and provides instructions such as:

```bash
ollama serve
```

This prevents confusing API connection errors when the Ollama service has not been started.

---

# 🧪 Example Conversations

### General Question

```text
User:
What is Generative AI?

Assistant:
Generative AI refers to artificial intelligence systems that can
create new content such as text, images, audio, video, or code...
```

### Technical Question

```text
User:
What is the difference between AI and ML?

Assistant:
AI is the broader concept of machines performing tasks that normally
require human intelligence, while machine learning is a subset of AI...
```

### Future Information

```text
User:
Who won the IPL match in 2030?

Assistant:
I don't have access to future results, and matches in 2030 have not
yet been played. Therefore, I cannot provide a factual winner.
```

The third example is particularly useful for demonstrating **responsible uncertainty** rather than fabricated information.

---

# 🚧 Limitations

This project intentionally remains simple so that the underlying architecture is easy to understand.

Current limitations include:

* No RAG/document retrieval
* No persistent database
* Conversation memory is session-based
* No authentication
* No user accounts
* No document upload
* No web search
* No guaranteed factual accuracy
* Model performance depends on local hardware
* Larger models may require significant RAM/VRAM

---

# 🚀 Future Improvements

This project provides a strong foundation for building more advanced local AI applications.

Possible improvements include:

### 🔹 RAG Integration

Add document retrieval:

```text
Documents
    ↓
Chunking
    ↓
Embeddings
    ↓
Vector Database
    ↓
Relevant Context
    ↓
Ollama
    ↓
Answer
```

This would allow the chatbot to answer questions based on your own documents.

### 🔹 Persistent Chat History

Store conversations using:

* SQLite
* PostgreSQL
* MongoDB

### 🔹 Document Upload

Allow users to upload:

* PDF
* TXT
* DOCX
* CSV

and ask questions about them.

### 🔹 Multiple Chat Sessions

Create separate conversations such as:

```text
Chat 1 — Python
Chat 2 — Machine Learning
Chat 3 — RAG
Chat 4 — Unity
```

### 🔹 Source Citations

A future RAG implementation could display:

```text
Answer:
...

Sources:
📄 document.pdf — Page 4
📄 notes.txt — Section 2
```

This would make the system more transparent and significantly more useful for knowledge-grounded applications.

---

# 📚 Learning Outcomes

By building this project, you can understand:

* What local LLMs are
* How Ollama works
* How to communicate with an LLM through an API
* How chat applications maintain conversation history
* How system prompts influence model behavior
* What temperature does
* How streaming responses work
* How Streamlit can be used to build AI applications
* Why LLMs can hallucinate
* Why uncertainty handling is important
* How a local chatbot can become the foundation for a RAG application

---

# 🎯 Why This Project?

This project is intentionally designed as a bridge between a basic Python application and more advanced Generative AI systems.

```text
Python
   ↓
Streamlit
   ↓
Ollama
   ↓
Local LLM
   ↓
Chatbot
   ↓
Conversation Memory
   ↓
RAG
   ↓
Advanced AI Application
```

It provides a practical starting point for learning how modern LLM applications are constructed without depending on paid cloud APIs.

---

# 📸 Project Preview

Add your application screenshot here:

```markdown
![Local AI Chatbot](screenshot/Screenshot.png)
```

---

# 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

If you find a bug or have an idea for improving the chatbot:

1. Fork the repository
2. Create a new branch
3. Make your changes
4. Commit your changes
5. Open a Pull Request

---

# 📄 License

This project is available for educational and personal use.

Add an appropriate open-source license if you plan to distribute the project publicly.

---

## ⭐ If You Found This Project Useful

If this project helped you learn about **Ollama, local LLMs, Streamlit, or Generative AI**, consider giving the repository a ⭐ on GitHub.

---

### 👨‍💻 Project

**Local AI Chatbot**

Built with:

`Python` • `Streamlit` • `Ollama` • `Local LLMs`

A beginner-friendly step toward building **private, local, and knowledge-grounded AI applications**.
