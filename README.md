backend
from flask import Flask, render_template, request

app = Flask(__name__)

# Function to process user input and generate responses
def process_query(query):
    if 'hello' in query:
        return "Hello! How can I assist you today?"
    elif 'time' in query:
        # You can use a library like datetime to get the current time
        # For simplicity, this example uses a hardcoded response
        return "The current time is 12:00 PM."
    elif 'weather' in query:
        # You might integrate with a weather API for accurate information
        return "The weather is sunny today."
    else:
        return "I'm sorry, I don't understand that command."

# Route for the home page
@app.route('/')
def index():
    return render_template('index.html')

# Route to handle user queries
@app.route('/process_query', methods=['POST'])
def execute_query():
    user_query = request.form['query']
    response = process_query(user_query)
    return render_template('index.html', query=user_query, response=response)

if __name__ == '__main__':
    app.run(debug=True)
