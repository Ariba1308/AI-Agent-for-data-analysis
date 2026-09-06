# AI Agent for Data Analysis

## Overview

This project leverages multi-agent collaboration to automate SQL query execution, data analysis, reporting, and visualization. It uses a **locally hosted Qwen3 LLM through Ollama** with the CrewAI framework to facilitate seamless interaction between SQL developers, data analysts, report writers, and data visualization agents.

The application is designed to support **local and offline AI inference**, eliminating the need for an OpenAI API key.

## Features

* **SQL Query Execution:** Automatically generate and run SQL queries on an SQLite database.
* **Data Analysis:** Extract meaningful insights from queried data.
* **Report Generation:** Summarize analysis results into an executive-level report.
* **Data Visualization:** Create Plotly visualizations based on user queries.
* **Multi-Agent Collaboration:** Uses specialized CrewAI agents for SQL development, analysis, reporting, and visualization.
* **Local LLM:** Uses **Qwen3 4B through Ollama** for local AI inference.
* **Offline AI Processing:** AI inference runs locally without requiring a cloud-based LLM API.
* **Streamlit UI:** Interactive interface for users to upload datasets and request analysis or visualizations.

---

## Setup Instructions

### Prerequisites

Ensure you have the following installed:

* Python 3.10+
* `pip`
* `virtualenv`
* **Ollama**

### Step 1: Clone the Repository

```sh
git clone <repository-url>
cd <repository-folder>
```

### Step 2: Set Up Virtual Environment

```sh
python -m venv venv
```

#### On macOS/Linux:

```sh
source venv/bin/activate
```

#### On Windows:

```sh
venv\Scripts\activate
```

### Step 3: Install Dependencies

```sh
pip install -r requirements.txt
```

If required, install the Ollama integration:

```sh
pip install langchain-ollama
pip install "crewai[litellm]"
```

### Step 4: Set Up Ollama and Qwen3

Make sure Ollama is installed and running.

Pull the Qwen3 4B model:

```sh
ollama pull qwen3:4b
```

Verify that the model has been installed:

```sh
ollama list
```

You can also test the model manually:

```sh
ollama run qwen3:4b
```

The application connects to the local Ollama server at:

```text
http://localhost:11434
```

No OpenAI API key or `.env` file is required.

### Step 5: Run the Streamlit Application

```sh
streamlit run streamlit_app.py
```

---

## Project Structure

```text
├── agents.py          # Defines AI agents for SQL execution, analysis, reporting, and visualization
├── tasks.py           # Defines tasks assigned to agents
├── custom_tools.py    # Custom tools for SQL execution and validation
├── crew.py             # Orchestrates agents and tasks into a CrewAI workflow
├── streamlit_app.py   # Streamlit-based user interface
├── requirements.txt   # Required Python dependencies
├── README.md          # Project documentation
```

### **agents.py**

Defines different AI agents:

* **SQL Developer:** Generates and executes SQL queries using the available database tools.
* **Data Analyst:** Analyzes retrieved data and extracts meaningful insights.
* **Report Writer:** Summarizes the analysis into an executive-level report.
* **Visualization Agent:** Generates Python code using Plotly to create visualizations.

All agents use the **Qwen3 4B model running locally through Ollama**.

### **tasks.py**

Defines the structured tasks performed by each agent, including:

* Data extraction
* Data analysis
* Report generation
* Visualization generation

### **custom_tools.py**

Implements tools for SQL database operations:

* List tables
* Retrieve table schema and sample data
* Execute SQL queries
* Validate SQL queries

### **crew.py**

Manages the coordination and sequential execution of the different agents and tasks using CrewAI.

### **streamlit_app.py**

Provides a web interface for:

* Uploading CSV datasets
* Querying the AI assistant
* Viewing generated analysis reports
* Generating and displaying Plotly visualizations

---

## Local LLM

The project uses:

**Qwen3 4B + Ollama**

The CrewAI agents connect to the locally running model using:

```text
ollama/qwen3:4b
```

Ollama runs locally at:

```text
http://localhost:11434
```

This allows the application to perform AI inference locally without depending on OpenAI's API.

---

## Usage

1. **Start Ollama** and ensure the Qwen3 model is available.
2. **Run the Streamlit application**.
3. **Upload a CSV file** through the Streamlit interface.
4. **Enter a natural-language query**, for example:

   ```text
   Show the average salary by department.
   ```
5. **Generate an analysis report** to obtain insights from the dataset.
6. **Request a visualization** by describing the desired chart, for example:

   ```text
   Create a bar chart for sales over time.
   ```

The application processes the request through the appropriate CrewAI agents and returns the analysis, report, or visualization.

---
