## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:
Develop an LCEL-based application to process expressions with dynamic parameters, leveraging a prompt template for structured interaction, a language model to process the input, and an output parser for extracting meaningful results.
### DESIGN STEPS:

#### STEP 1:
Create a prompt template with placeholders for at least two parameters.
#### STEP 2:
Use LangChain's language model to process the prompt and generate a response.
#### STEP 3:
Implement an output parser to extract structured results from the model's response.
### PROGRAM:
````
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain.output_parsers import StructuredOutputParser, ResponseSchema

# Step 1: Define Parameters and Prompt Template
prompt_template = PromptTemplate(
    input_variables=["topic", "length"],
    template=(
        "You are a helpful assistant. Please provide the following in valid JSON format:\n"
        "- A concise summary of {topic}.\n"
        "- The word count of the summary.\n\n"
        "Response should look like this:\n"
        "{{\n"
        '  "summary": "Your concise summary here.",\n'
        '  "word_count": 123\n'
        "}}\n\n"
        "Write a {length}-word summary about {topic}. Be concise and factual."
    )
)

# Step 2: Define the Output Parser
response_schemas = [
    ResponseSchema(name="summary", description="A concise summary of the topic."),
    ResponseSchema(name="word_count", description="The number of words in the summary."),
]
output_parser = StructuredOutputParser.from_response_schemas(response_schemas)

# Step 3: Create the LangChain LLM Chain with Gemini Model
API_KEY = "**************************"
llm = ChatGoogleGenerativeAI(model="gemini-pro", temperature=0.3, google_api_key=API_KEY)

chain = LLMChain(prompt=prompt_template, llm=llm, output_parser=output_parser)

# Step 4: Execute the Chain with Examples
examples = [
    {"topic": "Climate Change", "length": "50"},
    {"topic": "Artificial Intelligence", "length": "30"},
]

for example in examples:
    try:
        result = chain.run(example)
        print(f"Input: {example}")
        print(f"Output: {result}\n")
    except Exception as e:
        print(f"Error for input {example}: {e}\n")
````
### OUTPUT:
![image](https://github.com/user-attachments/assets/3aa96ce0-3c45-49f3-adb0-0202c6df8deb)

### RESULT:
Hence,the program to design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios is written and successfully executed.
