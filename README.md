# 🤖 RAG Chatbot Template

**Production-ready RAG chatbot you can customize in 5 minutes**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

> 💡 **This is a template!** Clone it, add your content, customize the branding, and deploy your own AI chatbot.

---

## ✨ Features

- 🚀 **5-Minute Setup** - Clone → Configure → Deploy
- 🎨 **Easy Branding** - Customize name, colors, messages via `.env`
- 📝 **Just Add Content** - Drop `.md` files in `blogs/` folder
- 🤖 **Production RAG** - FAISS vector search + OpenAI embeddings
- 💬 **Dual Interface** - Streamlit web UI + CLI chatbot
- 🔒 **Security Built-In** - API key sanitization, input validation
- 📊 **Observability** - Structured logging, metrics tracking
- ✅ **127 Tests Included** - Production-ready code quality
- 📱 **Deploy Anywhere** - Streamlit Cloud (free), Docker, Vercel

---

## 🚀 Quick Start

### Prerequisites

- Python 3.11 or higher
- OpenAI API key ([Get one here](https://platform.openai.com/api-keys))
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/rag-chatbot-template
   cd rag-chatbot-template
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env and add your OPENAI_API_KEY
   # Also customize: APP_NAME, WELCOME_MESSAGE, EXAMPLE_QUESTIONS
   ```

5. **Verify setup**
   ```bash
   python scripts/setup.py
   ```

### Running the Application

#### Option 1: Web Interface (Streamlit) ⭐ Recommended

The easiest way to use the chatbot is through the web interface:

```bash
# Run the Streamlit web app
streamlit run streamlit_app.py

# Or use the launcher script
./run_web.sh
```

Then open your browser to `http://localhost:8501`

**Features:**
- 💬 Beautiful chat interface
- 📊 Real-time statistics dashboard
- 📚 Source citations with expandable details
- 🎨 Markdown rendering
- 🔄 Conversation management

#### Option 2: Command Line Interface (CLI)

For terminal lovers, use the CLI chatbot:

```bash
# Start the CLI chatbot
python chat.py

# Available commands:
# /help     - Show help
# /stats    - View statistics
# /history  - Show conversation
# /clear    - Clear history
# /exit     - Exit chatbot
```

#### Option 3: Test Scripts

Run individual test scripts to explore functionality:

```bash
# Test blog loading
python scripts/test_blog_loading.py

# Generate embeddings from blog posts
python scripts/test_embeddings.py

# Test the complete RAG pipeline
python scripts/test_rag.py
```

---

## 📖 Customization

See **[CUSTOMIZATION.md](CUSTOMIZATION.md)** for detailed branding and customization guide.

Quick customization via `.env`:

```bash
APP_NAME="Your Bot Name"
APP_TAGLINE="Your Tagline Here"
WELCOME_TITLE="Welcome to YourBot"
WELCOME_MESSAGE="Your custom welcome message..."

# Customize example questions:
EXAMPLE_QUESTION_1="Your question 1?"
EXAMPLE_QUESTION_2="Your question 2?"
```

### Adding Your Content

```bash
# Delete example blogs
rm blogs/example-*.md

# Add your own .md files
cp your-blog-post.md blogs/
```

See **[docs/BLOG_FORMAT.md](docs/BLOG_FORMAT.md)** for blog post formatting guidelines.

---

## 🏗️ Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Blog Posts │────▶│   Embedding  │────▶│   Vector    │
│  (Markdown) │     │   Generator  │     │  Database   │
└─────────────┘     └──────────────┘     │   (FAISS)   │
                                          └──────┬──────┘
                                                 │
                    ┌────────────────────────────┘
                    │
                    ▼
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│    User     │────▶│  RAG Engine  │────▶│   OpenAI    │
│   Query     │     │              │     │   API       │
└─────────────┘     └──────┬───────┘     └─────────────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Response   │
                    │ with Sources │
                    └──────────────┘
```

### System Design

The chatbot follows a layered architecture:

1. **Data Layer** (`src/blog_loader.py`)
   - Loads markdown blog posts from `blogs/` directory
   - Parses YAML frontmatter for metadata
   - Validates blog structure

2. **Embeddings Layer** (`src/embeddings_manager.py`)
   - Chunks blog content into 500-token pieces
   - Generates embeddings using OpenAI's `text-embedding-3-small`
   - Manages FAISS vector index for similarity search
   - Handles save/load of index to disk

3. **RAG Engine** (`src/rag_engine.py`)
   - Core query processing pipeline
   - Retrieves top-5 relevant chunks via vector search
   - Constructs prompts with retrieved context
   - Calls OpenAI API (GPT-4o-mini by default)
   - Returns answers with source citations

4. **User Interfaces**
   - **Streamlit UI** (`streamlit_app.py`): Modern web interface
   - **CLI** (`src/cli_chatbot.py`): Terminal-based chatbot

5. **Infrastructure**
   - **Config** (`src/config.py`): Environment-specific configuration
   - **Logger** (`src/logger.py`): Structured JSON logging with correlation IDs

---

## 🛠️ Technology Stack

### Core Technologies
- **Language:** Python 3.11+
- **LLM Provider:** OpenAI (GPT-4o-mini / GPT-4o)
- **Vector Database:** FAISS (local) → Pinecone (scale)
- **UI:** Streamlit
- **CLI:** Rich

### Testing & Quality
- **Testing:** pytest, pytest-cov
- **Linting:** black, pylint, mypy
- **Security:** bandit

---

## 📊 Project Status

**Current Phase:** ✅ v1.0.0 - Production Template Release

| Phase | Status | Description |
|-------|--------|-------------|
| **Phase 0** | ✅ Complete | Project structure, configuration, logging |
| **Phase 1** | ✅ Complete | Blog data handling and vector embeddings |
| **Phase 2** | ✅ Complete | RAG query engine |
| **Phase 3** | ✅ Complete | CLI chatbot |
| **Phase 4** | ✅ Complete | Testing & quality assurance (127 tests) |
| **Phase 6** | ✅ Complete | Streamlit UI (production-ready) |
| Phase 5 | ⏸️ Deferred | FastAPI backend (will build if needed) |
| Phase 7+ | 📅 Planned | Advanced features (see ROADMAP.md) |

**Test Results:** 120/127 tests passing, ~75% code coverage

See **[docs/ROADMAP.md](docs/ROADMAP.md)** for detailed timeline and **[docs/TEST_SUMMARY.md](docs/TEST_SUMMARY.md)** for test details.

---

## 💡 Use Cases

- **Personal Knowledge Base** - Query your blog posts and notes through an AI interface
- **Learning Platform** - Understand how production RAG systems work
- **Documentation Assistant** - Build a chatbot for your documentation
- **Content Discovery** - Help readers find relevant content from your blog
- **Portfolio Project** - Demonstrate AI engineering skills

---

## 📚 Documentation

- **[CUSTOMIZATION.md](CUSTOMIZATION.md)** - How to brand and customize
- **[BLOG_FORMAT.md](BLOG_FORMAT.md)** - How to write blog posts
- **[docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)** - Deploy to Streamlit Cloud (free!)
- **[docs/ROADMAP.md](docs/ROADMAP.md)** - Project roadmap and future plans
- **[CLAUDE.md](CLAUDE.md)** - Development guide for contributors
- **[agent.md](agent.md)** - Development standards and best practices

---

## 🤝 Contributing

We welcome contributions! This project is designed for learning, so feel free to:

- 🐛 Report bugs
- 💡 Suggest features
- 📝 Improve documentation
- 🔧 Submit pull requests

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Built with [LangChain](https://www.langchain.com/)
- Powered by [OpenAI](https://openai.com/)
- Vector search with [FAISS](https://github.com/facebookresearch/faiss)
- Inspired by the open-source AI community

---

## 📞 Support & Questions

- 🐛 **Issues:** [GitHub Issues](https://github.com/yourusername/rag-chatbot-template/issues)
- 💬 **Discussions:** [GitHub Discussions](https://github.com/yourusername/rag-chatbot-template/discussions)

---

## ⭐ Star History

If you find this project useful, please consider giving it a star! It helps others discover the project.

---

**Built with ❤️ for the AI Engineering community**
