# AI-Customer-Care-Agent-LangGraph-RAG-SQL
An intelligent AI Customer Care Agent built using LangGraph, LangChain, RAG, SQL Server, FAISS, and Streamlit. The application can answer general customer-care questions from company policy documents and manage customer-specific order requests using database tools.
Features
💬 Natural-language customer support
📚 RAG-based policy question answering
🔎 Semantic search using FAISS
🧠 HuggingFace sentence-transformer embeddings
🛠️ LangChain tool calling
🔄 LangGraph-based agent workflow
📦 Order status lookup using SQL Server
❌ Order cancellation with status validation
🗄️ SQL Server integration using SQLAlchemy
🧾 PDF-based customer-care knowledge base
💾 Conversation memory using MemorySaver
🖥️ Interactive Streamlit interface
🔐 Environment-variable based OpenAI API configuration
🏗️ Architecture
                    ┌─────────────────────┐
                    │     Streamlit UI    │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   LangGraph Agent   │
                    │      (GPT-4o)       │
                    └──────────┬──────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐       ┌─────────────────┐
        │    rag_help     │       │  order_manage   │
        │                 │       │                 │
        │ PDF → Chunks    │       │   SQL Server    │
        │ → Embeddings    │       │ Order Status    │
        │ → FAISS Search  │       │ Cancellation    │
        └─────────────────┘       └─────────────────┘
🔧 Tools
1. rag_help

Handles general customer-care questions such as:

Return policy
Refund policy
Cancellation policy
Shipping policy
Delivery information
Payment methods
Warranty
Exchange policy
General customer-support guidelines

The tool loads the company knowledge-base PDF, splits the content into chunks, generates embeddings, stores them in FAISS, and retrieves the most relevant information for the customer's question.

2. order_manage

Handles order-specific operations using SQL Server.

Supported operations include:

Check order status
Check order details
Check delivery/dispatch information
Cancel an order when cancellation is allowed

The agent extracts the order ID from the customer's natural-language request and passes it to the order-management tool.

Example:

Customer:
"What is the status of order 123?"

Agent:
→ Extract order_id = 123
→ Call order_manage(123, "status")
→ Query SQL Server
→ Return order information

For cancellation:

Customer:
"Cancel order 123"

Agent:
→ Extract order_id = 123
→ Check current order status
→ Cancel only when the order is eligible
→ Update SQL Server
→ Return confirmation
🧠 LangGraph Workflow

The project uses a LangGraph workflow containing:

START
  ↓
Chatbot
  ↓
Tool Decision
  ├── rag_help
  │      ↓
  │    Chatbot
  │
  └── order_manage
         ↓
       Chatbot
         ↓
        END

MemorySaver is used as the checkpointer so that conversation state can be maintained using a thread_id.

🛠️ Tech Stack
Technology	Purpose
Python	Core programming language
Streamlit	User interface
LangChain	LLM and tool integration
LangGraph	Agent workflow orchestration
GPT-4o	Natural-language reasoning
FAISS	Vector similarity search
HuggingFace Embeddings	Document embeddings
PyPDFLoader	PDF document loading
SQLAlchemy	Database connectivity
SQL Server	Order database
pyodbc	SQL Server driver
python-dotenv	Environment configuration
📁 Knowledge Base

The application uses a customer-care PDF containing company policies and guidelines.

The RAG pipeline is:

PDF
 ↓
PyPDFLoader
 ↓
Document Chunking
 ↓
HuggingFace Embeddings
 ↓
FAISS Vector Store
 ↓
Similarity Search
 ↓
Relevant Context
 ↓
GPT-4o
 ↓
Customer Answer
💬 Example Queries
General Policy
What is your return policy?

→ Uses rag_help

Can I get a refund for a cancelled order?

→ Uses the customer-care policy knowledge base.

Order Management
What is the status of order 1?

→ Uses order_manage

Where is my order 25?

→ Uses order_manage

Cancel order 10

→ Checks the order before attempting cancellation.

🎯 Project Objective

The goal of this project is to demonstrate how LLMs can be integrated with enterprise data and business tools to build a practical customer-support system.

Instead of allowing the LLM to directly invent order information, the agent uses tools to retrieve real order data from SQL Server and uses RAG to answer policy-related questions from trusted company documentation.

🔮 Future Improvements
JWT-based customer authentication
User-specific order access
Return/refund workflow
Delivery tracking integration
Ticket creation system
Email notifications
Human-agent escalation
PostgreSQL/SQL Server production database
Persistent vector database
LangSmith observability
FastAPI backend
Docker deployment
Role-based access control
Production-grade logging and monitoring
👨‍💻 Learning Outcomes

This project demonstrates practical implementation of:

LLM tool calling
RAG architecture
Vector databases
LangGraph StateGraph
Conditional tool routing
Agent memory/checkpointing
SQL database integration
Natural-language order management
Streamlit application development
Enterprise AI customer-support architecture
