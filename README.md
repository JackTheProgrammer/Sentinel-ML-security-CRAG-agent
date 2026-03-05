# Sentinel-ML Security CRAG AI-agent
This is a repository for the Sentinel-ML Security CRAG AI-agent, which is designed to assist in security, vulnerability check of the ML scripts -be it for training, deploying or inference.

## Overview
The Sentinel-ML Security CRAG AI-agent is an intelligent agent that analyzes beginner to advanced machine learning techniques of the script at hand and identify potential security vulnerabilities in it. It is designed to help developers and security professionals ensure the safety and integrity of their ML applications.

## Features
- **Vulnerability Detection**: The agent can identify common security vulnerabilities in ML scripts, such as data leakage, model poisoning, and adversarial attacks.
- **Best Practices Recommendations**: It provides recommendations for best practices in ML security to help developers mitigate identified vulnerabilities.
- **Automated Analysis**: The agent can automatically analyze ML scripts and provide detailed reports on potential security issues.
- **Integration with CI/CD**: It can be integrated into continuous integration and continuous deployment (CI/CD) pipelines to ensure ongoing security checks for ML applications.

## Usage
To use the Sentinel-ML Security CRAG AI-agent, follow these steps:
1. Clone the repository:
   ```bash
   git clone https://github.com/sentinel-ml/sentinel-ml-security-crag-ai-agent.git
   ```
2. Install the required dependencies:
   ```bash
    pip install -r requirements.txt
   ```

## Demo usage
```python
res = app.invoke({
    "question": "Find vulnerabilities in this model loading script and provide a secure, high-performance alternative.",
    "vulnerable_code": """import pickle
    import pandas as pd
    def load_user_model(user_id):
        # DANGEROUS: Loading model from untrusted user path
        path = f"models/{user_id}_model.pkl"
        with open(path, 'rb') as f:
            model = pickle.load(f) # <--- Potential RCE Vulnerability
        return model
    """,
    "query": "Find vulnerabilities in this model loading script and provide a secure, high-performance alternative.",
    "web_docs": [],
    "fixed_code_cost_reduced": "",
    "entire_fixed_code": "",
    "final_report": None,
    "display_report": "",
    "docs": [],
    "good_docs": [],
    "kept_strips": [],
    "strips": [],
    "refined_context": "",
    "recommend_fix_only": False,
    "verdict": " ",
    "reason": " ",
    "web_queries": [],
    "fix_recommendations": set()
})

print("Fixed code with reduced computational cost:\n", res['fixed_code_cost_reduced'])
```
### Output
```
Fixed code with reduced computational cost:
from pathlib import Path
from safetensors.torch import load_file

def load_user_model(user_id):
    # Optimized safe loading: uses zero-copy memory mapping via safetensors
    # Minimalist path sanitization to reduce overhead
    safe_id = Path(user_id).name
    path = Path("models") / f"{safe_id}_model.safetensors"
    
    # load_file is significantly faster than pickle and inherently safe
    return load_file(str(path))
```

## Agent Workflow
[Alt text: Agent Workflow Diagram]("./output/ml_security_audit_CRAG_workflow.png")