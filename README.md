# Web Chatbot with n8n and Google Gemini

This repository contains a simple yet powerful example of how to build and embed an AI chatbot into a standard webpage. The chatbot's backend is powered by an [n8n](https://n8n.io/) workflow, using the [Google Gemini](https://deepmind.google/technologies/gemini/) model for natural language processing and conversation.

The project demonstrates a complete end-to-end setup, from the frontend chat interface to the backend AI agent.

## Workflow Diagram

The n8n workflow orchestrates the entire backend logic for the chatbot.



## How It Works

The system is composed of two main parts: a simple HTML frontend and an n8n workflow backend.

### 1. Frontend (`sample_web_page.html`)

*   A basic HTML page that serves as the host for the chat interface.
*   It uses the official `@n8n/chat` package, loaded via a CDN, to render a beautiful and ready-to-use chat widget.
*   The widget is configured with a specific `webhookUrl` that points to our n8n workflow, creating the link between the user's messages and the backend logic.

### 2. Backend (`web_chats.json`)

This is an n8n workflow that acts as the "brain" of the chatbot.

*   **When chat message received (Trigger):** This is a Chat Trigger node. It exposes a public webhook URL and listens for new messages sent from the chat widget on our webpage.
*   **AI Agent:** This node orchestrates the conversation. It receives the user's input from the trigger.
*   **Google Gemini Chat Model:** The AI Agent uses this powerful language model to understand the user's query and generate a human-like response.
*   **Simple Memory:** This node gives the agent conversational memory. It allows the chatbot to remember previous parts of the conversation, enabling context-aware follow-up questions and a more natural dialogue flow.

## Getting Started

Follow these steps to get your own version of this chatbot running.

### Prerequisites

*   A running **n8n instance** (either on [n8n.cloud](https://n8n.cloud/) or self-hosted).
*   **Google Gemini (or PaLM) API credentials**. You can get these from the Google AI Studio.

### Setup Instructions

1.  **Download the Workflow**:
    *   Download the `web_chats.json` file from this repository.

2.  **Import the Workflow into n8n**:
    *   In your n8n canvas, select **Import from file** and upload `web_chats.json`.

3.  **Configure Credentials**:
    *   Click on the **Google Gemini Chat Model** node.
    *   In the "Credentials" section, select your existing Google Gemini API credentials or create a new set by providing your API key.

4.  **Activate the Workflow**:
    *   Click the **Activate** toggle in the top-right corner of the n8n editor. This will make the webhook live and ready to receive messages.

## Embed the Chatbot in Your Website

1.  **Copy the Webhook URL**:
    *   Open the **When chat message received** node.
    *   Copy the **Webhook URL** provided in the node's parameters panel. It will look something like `https://your-n8n-instance.com/webhook/451f5f08-ac45-432d-a854-a1471f9a170d/chat`.

2.  **Add the Snippet to Your HTML**:
    *   Open your `sample_web_page.html` file (or any other HTML file).
    *   Paste the following `<script>` tag just before the closing `</body>` tag.
    *   **Important:** Replace `'YOUR_WEBHOOK_URL_HERE'` with the URL you copied from n8n.

    ```html
    <!-- n8n Chat Widget -->
    <script type="module">
        import { createChat } from 'https://cdn.jsdelivr.net/npm/@n8n/chat/dist/chat.bundle.es.js';

        createChat({
            webhookUrl: 'YOUR_WEBHOOK_URL_HERE'
        });
    </script>
    ```

## Usage

1.  Save your HTML file.
2.  Open the HTML file in a web browser.
3.  You should see a chat icon in the bottom-right corner of the page.
4.  Click the icon to open the chat widget and start a conversation with your new AI-powered chatbot!

## License

This project is licensed under the MIT License. See the [LICENSE.md](LICENSE.md) file for details.
