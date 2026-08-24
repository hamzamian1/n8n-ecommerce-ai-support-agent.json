# 🤖 Autonomous E-Commerce Operations & Support Agent (n8n + LangChain)

An intelligent, autonomous customer support agent pipeline built in **n8n** utilizing **LangChain** and **OpenAI (GPT-4o-mini)**. This workflow processes incoming e-commerce user queries, extracts customer intent and Order IDs, interacts with a Google Sheets database, and dynamically handles order statuses and cancellation rules in real-time[cite: 3].

## 🚀 Key Features
* **Webhook Ingestion:** Listens for incoming customer support requests via a POST webhook endpoint (`/ecommerce-support`)[cite: 3].
* **AI-Powered Intent & Entity Extraction:** Leverages an AI Agent with `gpt-4o-mini` to classify user intent (`Status` or `Cancel`) and accurately extract the target `order_id`[cite: 3].
* **Output Sanitization (Custom JS):** Cleans messy Markdown codeblocks (triple backticks) and parses AI output into structured JSON[cite: 3].
* **Smart Order Status Verification:** 
  * Queries the Google Sheet order database to retrieve current order details using the extracted `Order_ID`[cite: 3].
  * Evaluates if the order is still in the `Pending` state[cite: 3].
* **Automated Cancellation & Dynamic Webhook Responses:**
  * **Eligible Orders (`Pending`):** Automatically updates the status to `Cancelled` in the database and returns a success confirmation[cite: 3].
  * **Ineligible Orders (e.g., Shipped / Delivered):** Halts cancellation and returns a dynamic error explaining that the order is already in that specific fulfillment phase[cite: 3].

## 🛠️ Tech Stack & Nodes Used
* **n8n** (Core Automation Engine)[cite: 3]
* **LangChain AI Agent & OpenAI Chat Model** (`gpt-4o-mini`)[cite: 3]
* **Webhook Node & Respond to Webhook Nodes** (Synchronous API communication)[cite: 3]
* **Switch Node & If Node** (Intent and status conditional branching)[cite: 3]
* **Code Node (JavaScript)** (JSON parsing and regex sanitization)[cite: 3]
* **Google Sheets Node** (Row search and in-place updates via OAuth2)[cite: 3]

## 📋 Database Schema (Google Sheets)
Your Google Sheet requires the following column structure[cite: 3]:
| Column Name | Description |
| :--- | :--- |
| `Order_ID` | Unique Order Identifier[cite: 3] |
| `Customer_Email` | Customer contact email[cite: 3] |
| `Created_At` | Order creation timestamp[cite: 3] |
| `Status` | Current state (`Pending`, `Processing`, `Cancelled`, etc.)[cite: 3] |

## ⚙️ Prerequisites
1. Self-hosted or Cloud **n8n** instance (v1.0+ with LangChain support)[cite: 3].
2. **OpenAI API Key** with access to `gpt-4o-mini`[cite: 3].
3. **Google Cloud Console OAuth2 Credentials** configured for Google Sheets access[cite: 3].

## 📥 How to Install
1. Clone this repository or copy the contents of `workflow.json`.
2. Open your n8n workspace.
3. Click **Workflows** -> **Import from File** and select `workflow.json`.
4. Connect your **OpenAI API** and **Google Sheets OAuth2** credentials[cite: 3].
5. Replace the Google Sheet document ID with your own target spreadsheet[cite: 3].
6. Switch the workflow toggle to **Active**.

---

## 📸 Screenshots

### 1. Workflow Architecture
Complete overview of the AI Agent and database logic:
<img width="1032" height="392" alt="image" src="https://github.com/user-attachments/assets/ab1369ff-9b9e-4fd0-a358-eb52e4ae8222" />
