This code combines HTML, CSS, and JavaScript to create a webpage that interacts with the DeepSeek API, an AI chatbot. Users can type messages and receive responses from DeepSeek. The page also includes settings for the API key, model selection, and token usage display. Additionally, it fetches and displays articles from the NConnect Insights Feed.

**Main Components**

* **HTML (Structure)**
    * `<header>`:  Contains the website header with the logo (NConnect) and main menu (Home, About, Services, Insights, Contact).
    * `<div class="container">`: Holds the main content, divided into:
        * `<div id="settings-container">`:  For settings configuration, including:
            * API Key input field (`<input type="password" id="api-key">`).
            * Save button (`<button onclick="saveSettings()">`).
            * Model selection dropdown (`<select id="model-select">`).
        * `<div id="chat-container">`: For the chat interface, containing:
            * `<div id="messages">`: Displays the chat messages.
            * `<div id="input-container">`:  Includes the message input field (`<input type="text" id="message-input">`) and the Generate button (`<button id="generate-btn" onclick="sendMessage()">`).
    * `<h1 id="insights-title">`:  Title for the NConnect Insights Feed section.
    * `<div id="feed-container">`: Displays articles from the NConnect Insights Feed.

* **CSS (Styling)**
    * Styles the webpage with colors, fonts, spacing, and element positioning.
    * Uses flexbox and grid for layout.
    * Defines styles for user messages (`user-message`), bot messages (`bot-message`), generating messages (`generating`), code sections (`code-section`), copy buttons (`copy-btn`).
    * Styles the article display (`post`), including the title (`post-title`), link (`post-link`), and image (`post-image`).

* **JavaScript (Functionality)**
    * `loadSettings()`: Loads the saved API key and model from localStorage.
    * `saveSettings()`: Saves the API key and model to localStorage.
    * `sendMessage()`: Sends the user's message to the DeepSeek API and handles the response.
        * Checks if the API key is provided.
        * Displays "Generating..." while waiting for the response.
        * Sends a POST request to `https://api.deepseek.com/v1/chat/completions`.
        * Receives the response in JSON format.
        * Displays the response and the number of tokens used.
    * `appendGeneratingMessage()`: Adds the "Generating..." message to the `<div id="messages">`.
    * `processResponse(text)`: Processes the response from DeepSeek.
        * Splits the text into parts based on code blocks (```).
        * Returns an array of objects with `type` (code or text) and `content`.
    * `appendMessage(sender, text, tokensUsed)`:  Adds a message to the `<div id="messages">`.
        * Separates the message by type (code or text) and displays it accordingly.
        * Shows the token count (for bot messages).
        * Includes "Copy All" and "Copy Code" buttons.
    * `formatText(text)`: Formats the text with bold, italics, and code elements.
    * `copyCode(button)`: Copies code from a code block.
    * **Fetching NConnect Insights Feed**:
        * Uses `fetch` to retrieve data from `https://insights.nconnect.asia/wp-json/wp/v2/posts`.
        * Displays each article in a `<div class="post">`.
        * Shows the image (if available), title, and a "Read more" link.

* **Event Listeners**
    * Pressing Enter in the message input field (`#message-input`) triggers `sendMessage()`.
    * Changing the model in the model selection dropdown (`#model-select`) updates the `selectedModel`.


**How to Use**

1. **Enter API Key**:  Input your DeepSeek API key in the "DeepSeek API Key" field and click "Save."
2. **Select Model**: Choose the desired model from the options (DeepSeek Chat, DeepSeek Reasoner, DeepSeek Coder).
3. **Type Message**: Enter your message in the "Type your message..." field.
4. **Generate Response**: Click the "Generate" button or press Enter to send the message.
5. **View Response**: DeepSeek's response will appear in the "Messages" section.
6. **Check Token Usage**: The number of tokens used will be displayed below the bot's response.
