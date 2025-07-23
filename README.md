
# AI G-Mail Generator

This is a web-based application designed to generate professional emails using Google’s Gemini AI model. It supports different scenarios such as personalized invitations, quick communications, and workflow emails. The app provides a simple interface for users to input key details and receive an AI-crafted email in response.

## Project Structure

```
Final Code Files/
│
├── backend/
│   ├── app.py               # Flask backend logic
│                    
│   └── requirements.txt     # Python dependencies
│
├── frontend/
│   ├── index.html           # Web interface
│   ├── style.css            # Styling for the interface
│   └── script.js            # Frontend logic and API communication
```

## How to Run the Project Locally

### Requirements

- Python 3.8 or later
- A valid Google Gemini API key

### Setup Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/ai-gmail-generator.git
   cd ai-gmail-generator
   ```

2. **Install Backend Dependencies**
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

3. **Add Your Gemini API Key**
   Create a `.env` file in the `backend` directory and add:
   ```env
   GEMINI_API_KEY=your_gemini_api_key_here
   ```

4. **Run the Backend Server Locally**
   ```bash
   python app.py
   ```

   This will start the Flask server at:  
   `http://127.0.0.1:5000`

5. **Open the Frontend**
   - Open `frontend/index.html` directly in your browser, OR
   - Serve it using Python:
     ```bash
     cd frontend
     python -m http.server
     ```
     Then go to `http://localhost:8000`

## Deploying the Backend to Render

To make the project work online, deploy the backend API using Render.

### Steps:

1. Go to [https://render.com](https://render.com) and sign in.

2. Click **"New Web Service"** and connect your GitHub repo.

3. Set the environment:
   - **Runtime**: Python 3.8+
   - **Start Command**: `python app.py`
   - **Build Command**: *(leave blank)*
   - **Environment Variables**: Add your `GEMINI_API_KEY`

4. Deploy the backend. It will be available at a URL like:
   https://your-render-service.onrender.com

### Update Frontend Code

In `script.js`, change the fetch URL to match your Render backend:

```javascript
fetch("https://your-render-service.onrender.com/generate-email", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ prompt })
})
```

Now your frontend will communicate with your deployed backend.

## Troubleshooting

- `GEMINI_API_KEY not found in .env`: Ensure the key is set correctly in both `.env` (locally) and Render's environment variables.
- No email generated: Check for issues in browser console or backend logs on Render.

## Code Overview

### Frontend

- `index.html`: Form and layout for input
- `script.js`: Builds prompt and sends it to Flask backend

### Backend

- `app.py`: Receives prompt, calls Gemini, returns generated email

Example route:
```python
@app.route("/generate-email", methods=["POST"])
def generate_email():
    prompt = request.json.get("prompt")
    response = model.generate_content(prompt)
    return jsonify({"email": response.text})
```

## Prompt Design Examples

### Personalized Email Prompt

```
Write a professional email.

Subject: Birthday Party  
To: AbhiRam  
Special Instructions: Please attend the event on 2025-10-07T03:38 at Vizag.  
Email:
```

### Efficient Communication Prompt

```
Write a Thank You email.

To: Sai Kiran  
Subject: Project Completed  
Key Detail: Thanks for your Help Sir  
Email:
```

## Final Notes

This project demonstrates how to build and connect a frontend with a Gemini-powered Flask backend, and how to deploy the backend using Render.

You can continue expanding this app by adding export options, storing history, user login, or even integrating Gmail API to send emails directly.
