# Step 1: Simple Retrieval Flow

This is the foundational "Brain" of your AI agent. This n8n workflow listens for a chat message, sends it to the Guided Mind RAG engine, and returns a context-aware answer.

## 📂 Contents
* `workflow.json`: The n8n workflow file.

## ⚡️ Quick Start

### 1. Import the Workflow
1. Download `workflow.json` from this folder.
2. Open your n8n dashboard.
3. Click **Add Workflow** -> **Import from File**.
4. Select the JSON file.

### 2. Configure Credentials
The workflow uses a standard **HTTP Request** node. You must update it with your specific credentials:

1. Double-click the **HTTP Request** node.
2. Under **Headers** -> **Authorization**, replace `YOUR_API_KEY` with your actual key (format: `Bearer sk_...`).
3. Under **Body Parameters** -> **project_id**, replace `YOUR_PROJECT_ID` with the ID from your Guided Mind dashboard.

### 3. Test
1. Click **Execute Workflow**.
2. Click the **Chat** button (bottom right of the n8n canvas) or open the "Test URL" provided by the Chat Trigger node.
3. Ask a question relevant to the documents you uploaded to Guided Mind.

## 🧩 Node Breakdown

| Node | Type | Purpose |
| :--- | :--- | :--- |
| **When chat message received** | Trigger | Captures user input via the n8n hosted chat interface. |
| **HTTP Request** | Action | POSTs the user query to `api.guidedmind.ai/v1/chat`. |
| **Edit Fields** | Helper | Cleans the JSON response to output only the text answer. |

## ⚠️ Troubleshooting
* **401 Unauthorized:** Check that you kept the word `Bearer ` before your API key in the Header.
* **404 Not Found:** Ensure your `project_id` is correct and the Project exists in Guided Mind.
* **Empty Response:** Verify that your Guided Mind project has finished indexing your documents.