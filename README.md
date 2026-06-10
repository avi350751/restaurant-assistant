# Ghoroya Restaurant Assistant - RAG System

## 📋 Project Overview

This is a **Retrieval Augmented Generation (RAG)** system built for **Ghoroya Restaurant**, a Bengali fine dining establishment. The system powers an AI chatbot assistant called **Amontron** that helps restaurant staff and customers access information about the restaurant operations, menu, inventory, loyalty programs, and more.

The project uses **n8n** workflow automation, **OpenAI GPT-4o** for language understanding, and **Pinecone Vector Store** for semantic search and retrieval of restaurant data.

---

## 📁 Project Structure

### Core Configuration Files

#### 1. **Amontron_Assistant.json**
- **Purpose**: N8n workflow configuration for the chatbot assistant
- **Key Features**:
  - Chat trigger webhook for receiving user messages
  - GPT-4o LLM integration for intelligent responses
  - Pinecone Vector Store integration for retrieving restaurant data
  - Memory buffer for maintaining conversation context
  - Custom CSS styling with Ghoroya restaurant branding (orange/brown colors)
  - System prompt defining Amontron's role and behavior
- **Functionality**: Acts as the main orchestration layer that receives user queries, retrieves relevant information from the vector store, and generates contextual responses

#### 2. **Chat_Amontron_Agent.txt**
- **Purpose**: Example conversation log and test cases
- **Content**: Sample interactions demonstrating the chatbot's capabilities
- **Example Queries Handled**:
  - Order history (Uber Eats orders)
  - Branch information and locations
  - Loyalty program member details and points
  - Menu pricing (Weekend Bengali Buffet)
  - Menu items and ingredients
  - Promotional campaigns
  - Inventory checks (stock availability)

#### 3. **Ghoroya_Restaurant_Data_Insert.json**
- **Purpose**: N8n workflow for data ingestion and vectorization
- **Key Components**:
  - Google Drive integration to fetch restaurant documents
  - Batch processing of documents
  - Content extraction from document files
  - Pinecone vector store insertion for semantic search
- **Workflow**: Downloads documents from Google Drive → Processes in batches → Converts to embeddings → Stores in Pinecone

---

## 📚 Knowledge Base - Ghoroya_KB

The `Ghoroya_KB/` folder contains 11 essential operational documents for the restaurant:

| # | Document | Purpose |
|---|----------|---------|
| **1** | 1_Customer_Reviews.docx | Customer feedback and ratings for service quality and menu items |
| **2** | 2_Employee_Schedule.docx | Staff scheduling and shift assignments |
| **3** | 3_Social_Media_Presence.docx | Social media account information and engagement data |
| **4** | 4_Hours_of_Operation.docx | Restaurant operating hours (regular and special hours) |
| **5** | 5_Inventory.docx | Current stock levels and ingredient availability |
| **6** | 6_Loyalty_Program.docx | Member tiers, points, rewards, and campaigns (e.g., Welcome Home Bonus, Dessert Tuesday, Gold Table Priority, Birthday Mishti) |
| **7** | 7_Menu.docx | Complete menu items, prices, ingredients, and dietary information |
| **8** | 8_Orders.docx | Order history including delivery platforms (Uber Eats, DoorDash, etc.) |
| **9** | 9_Promotions.docx | Current and upcoming promotional campaigns and discounts |
| **10** | 10_Reservation_Policy.docx | Reservation guidelines, availability, and special event policies |
| **11** | 11_Branches_and_Addresses.docx | All restaurant locations with addresses (e.g., Ghoroya Astoria Express) |

---

## 🤖 Amontron Assistant - Key Features

### System Capabilities
- **Menu Information**: Provides details on dishes, prices, ingredients, and dietary options
- **Employee Management**: Access to schedules and shift information
- **Inventory Tracking**: Real-time stock checks and ingredient availability
- **Order Management**: Retrieves order history from multiple delivery platforms
- **Promotional Support**: Information on current campaigns and discounts
- **Customer Service**: Access to reviews and customer feedback
- **Loyalty Program**: Member information, tier status, and point balances
- **Operational Details**: Hours of operation, branch locations, reservation policies
- **Social Media**: Updates on social media presence and engagement

### Communication Style
- Warm, friendly, and professional tone
- Concise and informative responses
- Empathetic and clear communication
- When information is unavailable: Directs users to contact support (1234567899)

### Intelligence Architecture
- **LLM**: OpenAI GPT-4o via OpenRouter API
- **Vector Search**: Pinecone semantic search for retrieving relevant context
- **Memory**: Conversation context buffer (10-message window)
- **Retrieval**: Retrieved data is used as primary source of truth before generating responses

---

## 🔧 Technical Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Workflow Automation** | n8n | Orchestrates data ingestion and chatbot interactions |
| **Language Model** | OpenAI GPT-4o | Generates intelligent, contextual responses |
| **Vector Database** | Pinecone | Semantic search and document retrieval |
| **Cloud Storage** | Google Drive | Source storage for restaurant documents |
| **API Gateway** | OpenRouter | LLM API access and routing |

---

## 🚀 How It Works

### Data Flow: Ingestion Pipeline
```
Google Drive Documents 
    ↓
n8n Workflow (Ghoroya_Restaurant_Data_Insert.json)
    ↓
Extract & Process Content
    ↓
Generate Embeddings
    ↓
Pinecone Vector Store
```

### Query Flow: Chat Pipeline
```
User Message
    ↓
Chat Webhook Trigger
    ↓
GPT-4o LLM + Amontron Agent
    ↓
Query Pinecone Vector Store
    ↓
Retrieve Relevant Context
    ↓
Generate Response
    ↓
Return to User
```

---

## 📊 Use Cases

### For Restaurant Staff
- Quickly access menu items and pricing
- Check inventory levels and stock availability
- View employee schedules
- Retrieve order information from multiple platforms
- Access loyalty program member details

### For Customers
- Browse menu options and pricing
- Check reservation availability
- Get loyalty program information
- View restaurant hours and locations
- Learn about current promotions

### For Management
- Monitor customer reviews and feedback
- Analyze order patterns
- Track inventory levels
- Review promotional campaign performance
- Access operational data quickly

---

## ⚙️ Configuration Details

### Amontron Agent Settings
- **Model**: GPT-4o (via OpenRouter)
- **Credentials**: OpenRouter API key stored in n8n
- **Max Iterations**: 10 (for agent loop complexity)
- **Pinecone Index**: "ghoroya"
- **Pinecone Namespace**: "Ghoroya"
- **Reranker**: Enabled for improved relevance

### Chat UI Customization
- **Title**: "Ghoroya - Your search of Bengal ends here!"
- **Color Scheme**: Orange (#d9480f) and brown (#7c2d12) - brand colors
- **Window Size**: 430px × 680px
- **Initial Message**: "My name is Amontron. How can I assist you today?"

---

## 📞 Support & Fallback

When the assistant cannot find information:
- **Response**: "I am not aware of this information. For immediate assistance, kindly contact: 1234567899."
- **Purpose**: Ensures users have a path to human support when needed
- **No Hallucination**: System is designed not to make assumptions or fabricate information

---

## 🔐 Data Management

- **Source**: All restaurant data originates from Google Drive documents
- **Storage**: Processed data is stored in Pinecone vector database with "Ghoroya" namespace
- **Access**: Via n8n workflows with proper API credentials
- **Security**: Uses OAuth2 for Google Drive and API keys for external services

---

## 📝 Notes

- The system uses a **retrieval-augmented generation** approach to ensure all responses are grounded in actual restaurant data
- **Conversation memory** maintains context across 10 messages for better user experience
- The assistant is specifically designed for **staff support** with the capability to serve **customers**
- Documents are regularly updated through the data insertion pipeline

---

## 🌟 Restaurant Information

**Restaurant Name**: Ghoroya Restaurant  
**Cuisine**: Bengali Fine Dining  
**Branches**: Multiple (including Ghoroya Astoria Express in Astoria, NY)  
**Support Contact**: 1234567899  
**Assistant Name**: Amontron

---

*Last Updated: June 2026*
*Project Type: RAG (Retrieval Augmented Generation) System*
