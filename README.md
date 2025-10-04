# Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

#### Date - 04/10/2025
#### Register No. - 212222100020

## Aim: 

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools.

## AI Tools Required:

- Python 3.x (PyCharm IDE)

- OpenAI API

- Hugging Face Inference API

- Python Libraries: requests, json, openai

## Explanation:

- The experiment demonstrates the persona pattern of a programmer requesting AI-generated outputs.

- Two AI tools—OpenAI GPT and Hugging Face GPT-2—are used to generate responses to the same prompt.

- Outputs are compared based on length and common keywords to generate actionable insights.

- This shows how multiple AI tools can be integrated, compared, and analyzed to determine which provides the most detailed or relevant response.

## Python Code Implementation:

```py
import requests
import json
import openai

# -------------------------
# Set your API keys
openai.api_key = "YOUR_OPENAI_API_KEY"
HF_API_KEY = "YOUR_HUGGINGFACE_API_KEY"
# -------------------------

# Function to query OpenAI GPT
def query_openai(prompt):
    response = openai.Completion.create(
        model="text-davinci-003",
        prompt=prompt,
        max_tokens=150
    )
    return response.choices[0].text.strip()

# Function to query Hugging Face Inference API
def query_huggingface(prompt):
    url = "https://api-inference.huggingface.co/models/gpt2"
    headers = {"Authorization": f"Bearer {HF_API_KEY}"}
    payload = {"inputs": prompt}
    response = requests.post(url, headers=headers, json=payload)
    output = response.json()
    return output[0]['generated_text'].strip() if isinstance(output, list) else str(output)

# Function to compare outputs and provide actionable insight
def compare_outputs(out1, out2):
    print("\n--- OpenAI GPT Output ---\n", out1)
    print("\n--- Hugging Face Output ---\n", out2)

    # Compare by length
    if len(out1) > len(out2):
        insight = "OpenAI provided a more detailed response."
    elif len(out2) > len(out1):
        insight = "Hugging Face provided a more detailed response."
    else:
        insight = "Both responses are of similar length."

    # Keyword analysis (common words)
    words1 = set(out1.lower().split())
    words2 = set(out2.lower().split())
    common_words = words1.intersection(words2)
    insight += f" Common keywords: {', '.join(list(common_words)[:5])}."
    
    return insight

# Main execution
if __name__ == "__main__":
    user_prompt = "Explain the importance of cloud computing in simple terms."
    openai_output = query_openai(user_prompt)
    hf_output = query_huggingface(user_prompt)
    result = compare_outputs(openai_output, hf_output)
    print("\n--- Actionable Insight ---\n", result)

```

## Output:

<img width="823" height="220" alt="image" src="https://github.com/user-attachments/assets/026f5b89-8a42-480a-afec-bd5ae322632c" />

## Conclusion:

- The experiment successfully demonstrated integration of multiple AI tools using Python.

- Outputs from OpenAI and Hugging Face were collected, compared, and analyzed.

- Actionable insights were derived based on response length and common keywords.

- The code executed successfully, fulfilling the aim of automating multi-AI output generation and analysis.

## Result: 

The corresponding prompt was executed successfully.
