### **Personalized Diet Plan Generator**

**Description:**

This Python application, built with Streamlit, is designed to provide personalized diet plans for diabetic patients. It leverages the **Groq API** for data generation and the **TinyLlama API** for optimization.

**Installation:**

1. **Create a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
2. **Install requirements:**
   ```bash
   pip install -r requirements.txt
   ```

**Usage:**

1. **Set API keys:** Replace the placeholders in the code with your actual Groq and Hugging Face API keys.
2. **Run the application:**
   ```bash
   streamlit run app.py
   ```
3. **Provide user inputs:** Enter the patient's information, including age, dietary preferences, cultural foods, allergies, diabetes condition, and blood pressure.
4. **Generate diet plan:** Click the "Generate Diet Plan" button to obtain a personalized diet plan.

**Features:**

- **Personalized diet plans:** Generates diet plans tailored to individual needs and preferences.
- **Educational information:** Provides relevant tips and information for managing diabetes.
- **User-friendly interface:** Streamlit-based interface for easy interaction.

**Limitations:**

- **Disclaimer:** The generated diet plans are for informational purposes only and should not replace professional medical advice.
- **Data privacy:** Ensure proper handling of sensitive user information.
------------------------------------------------

**Explanation of Code:**

**Import Necessary Libraries:**

```python
import streamlit as st
import pandas as pd
import requests
```

- `streamlit`: Used to create interactive web applications.
- `pandas`: For data manipulation and analysis.
- `requests`: For making HTTP requests to the TinyLlama API.

**Define Functions:**

1. **`get_synthetic_data(prompt)`:**
   - Uses the Groq API to generate synthetic data based on a given prompt.
   - Creates a Groq client object.
   - Sends a completion request to the Groq API with the prompt.
   - Returns the generated text from the completion.

2. **`optimize_data(data)`:**
   - Optimizes the given data using the TinyLlama API.
   - Sends a POST request to the TinyLlama API with the data.
   - Returns the optimized text from the API response.

**Create Streamlit App:**

```python
st.title("Personalized Diet Plan for Diabetic Patients")
```

- Sets the title of the web application.

**Get User Inputs:**

```python
st.header("Patient Information")
dietary_preferences = st.text_input("Dietary Preferences")
cultural_foods = st.text_input("Cultural Foods")
allergies = st.text_input("Allergies")
diabetes_condition = st.selectbox("Diabetes Condition", ["Type 1", "Type 2", "Gestational"])
blood_pressure = st.selectbox("Blood Pressure Condition", ["Normal", "High", "Low"])
```

- Creates a section for user inputs.
- Gets user information for dietary preferences, cultural foods, allergies, diabetes condition, and blood pressure.

**Generate Diet Plan:**

```python
if st.button("Generate Diet Plan"):
    prompt = f"Dietary Preferences: {dietary_preferences}, Cultural Foods: {cultural_foods}, Allergies: {allergies}, Diabetes Condition: {diabetes_condition}, Blood Pressure: {blood_pressure}"
    synthetic_data = get_synthetic_data(prompt)
    optimized_data = optimize_data(synthetic_data)
    st.subheader("Personalized Diet Plan")
    st.write(optimized_data)
```

- Creates a button to trigger the generation of the diet plan.
- If the button is clicked:
    - Constructs a prompt using the user inputs.
    - Calls the `get_synthetic_data` function to generate synthetic data.
    - Calls the `optimize_data` function to optimize the synthetic data.
    - Displays the optimized data as the personalized diet plan.

**Educational Section:**

```python
st.header("Educational Information")
st.write("Here are some tips and information for managing diabetes based on your provided information:")
# Add educational content here
```

- Creates a section for educational information.
- Provides tips and information related to diabetes management.

**Explanation of Code (Step-by-Step):**

1. Import necessary libraries.
2. Define functions for data generation and optimization.
3. Create a Streamlit app with a title.
4. Get user inputs for dietary preferences, cultural foods, allergies, diabetes condition, and blood pressure.
5. Create a button to trigger the diet plan generation.
6. If the button is clicked:
   - Construct a prompt using the user inputs.
   - Generate synthetic data using the Groq API.
   - Optimize the synthetic data using the TinyLlama API.
   - Display the optimized data as the personalized diet plan.
7. Provide educational information related to diabetes management.

**Note:** Replace the placeholder for the Hugging Face API key with your actual API key before running the code.


# CODE
```python
import streamlit as st
import pandas as pd
import requests

# Function to get synthetic data from Meta's Llama-3.1-8B-Instant
def get_synthetic_data(prompt):
    from groq import Groq
    client = Groq()
    completion = client.chat.completions.create(
        model="llama-3.1-8b-instant",
        messages=[{"role": "user", "content": prompt}],
        temperature=1,
        max_tokens=1024,
        top_p=1,
        stream=True,
        stop=None,
    )
    return completion['choices'][0]['message']['content']

# Function to optimize data using TinyLlama
def optimize_data(data):
    response = requests.post(
        "https://api-inference.huggingface.co/models/TinyLlama/TinyLlama-1.1B-Chat-v0.6",
        headers={"Authorization": f"Bearer YOUR_HUGGING_FACE_API_KEY"},
        json={"inputs": data},
    )
    return response.json()['generated_text']

# Streamlit app
st.title("Personalized Diet Plan for Diabetic Patients")

# User inputs
st.header("Patient Information")
dietary_preferences = st.text_input("Dietary Preferences")
cultural_foods = st.text_input("Cultural Foods")
allergies = st.text_input("Allergies")
diabetes_condition = st.selectbox("Diabetes Condition", ["Type 1", "Type 2", "Gestational"])
blood_pressure = st.selectbox("Blood Pressure Condition", ["Normal", "High", "Low"])

# Generate diet plan
if st.button("Generate Diet Plan"):
    prompt = f"Dietary Preferences: {dietary_preferences}, Cultural Foods: {cultural_foods}, Allergies: {allergies}, Diabetes Condition: {diabetes_condition}, Blood Pressure: {blood_pressure}"
    synthetic_data = get_synthetic_data(prompt)
    optimized_data = optimize_data(synthetic_data)
    st.subheader("Personalized Diet Plan")
    st.write(optimized_data)

# Educational section
st.header("Educational Information")
st.write("Here are some tips and information for managing diabetes based on your provided information:")
# Add educational content here
```




# Generating Synthetic Data base on Prompt

The code is a Python function that utilizes the Groq API to generate synthetic data based on a given prompt. 

Here's a breakdown of the code's key components:

**Import necessary libraries:**

- `import laport`
- `import pandas`
- `import requests`
- `import os`
- `from dotenv import load_dotenv`

These libraries are used for various tasks, including loading environment variables, making API requests, and data manipulation.

**Load environment variables:**

- `load_dotenv()`

This line loads environment variables from a `.env` file, which is typically used to store sensitive information like API keys.

**Define the `get_synthetic_data` function:**

- `def get_synthetic_data(prompt):`

This function takes a `prompt` as input and returns synthetic data generated by the Groq API.

**Import Groq and initialize the client:**

- `from groq import Groq`
- `api_key = os.getenv("GROQ_API_KEY")`
- `client = Groq(api_key=api_key)`

This code imports the Groq library, retrieves the API key from the environment variables, and creates a Groq client object.

**Create a completion request:**

- `completion = client.chat.completions.create(
    model="lamsa-3.1-8b-instant",
    messages=[("role": "user", "content": prompt)],
    temperature=1,
    max_tokens=1024,
    top_p=1,
    stream=True,
    stop=None
)`

This line sends a request to the Groq API to generate a completion based on the provided `prompt`. The request includes various parameters to control the generation process, such as the model to use, the temperature, the maximum number of tokens, and whether to stream the response.

**Collect the streamed content:**

- `content = ""`
- `for message in completion:
    if hasattr(message, 'choices') and len(message.choices) > 0:
        content += message.choices[0].delta.get('content', '')`

This code iterates over the streamed response from the Groq API and collects the generated content.

**Return the content:**

- `return content`

Finally, the function returns the collected synthetic data.

The error message you mentioned ("'ChoiceDelta' object has no attribute 'get'") indicates that there might be an issue with the Groq API response format or the way the content is being extracted. 

It would be helpful to inspect the actual response from the Groq API to determine the root cause of the error.
