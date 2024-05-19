# Mixture of Expert Model for Code Generation
This paper explores the efficacy of the Mixture-of-Experts (MoE) framework in code generation, showcasing superior performance compared to traditional monolithic model architectures. By applying MoE to code generation tasks across various programming languages, including Python, C++, Java, and Javascript, the study demonstrates enhanced precision and reduced computational overhead.

# Overview
The paper proposes a MoE framework tailored to code generation tasks, where different programming languages are handled by specialized expert models within the Mistral-7B base model. Through this architecture, the system optimally selects expert models based on the input code snippet's language, thereby improving output precision.

# Architecture
- The widely adopted Transformer architecture in natural language processing consists of encoder and decoder blocks, typically implemented with multiple Transformer layers. 
- Mixtral, a variant of Transformer, replaces feed-forward blocks with Mixture-of-Expert layers, enhancing its capabilities for specific tasks. 
- The Mixture-of-Experts layer comprises expert networks and a gating network, which dynamically selects experts based on input data, optimizing computational efficiency. 
- Two gating methods, Softmax Gating and Noisy Top-K Gating, are utilized to manage the expert selection process effectively, facilitating improved model performance

<img width="961" alt="image" src="https://github.com/Santhoshkumar-p/neural-code-generation-moe/assets/24734488/5bb27578-ffc9-494d-b2c2-169ed0258972">

# Dataset
We used the xlcost-text-to-code dataset offered by organization "codeparrot" on Hugging Face

# Evaluation
We leverage a system called CodeBLEU [9] to benchmark our models. CodeBLEU is a novel automatic evaluation metric proposed for code synthesis tasks like text-to-code, code translation,and code refinement.

| Language    | Baseline | Finetuned |
|-------------|----------|-----------|
| Python      | 0.1800   | 0.4000    |
| Java        | 0.1860   | 0.4287    |
| JavaScript  | 0.1909   | 0.4182    |
| C++         | 0.2170   | 0.3340    |

| Language                      | Mistral 7B | Mixture-of-Experts |
|-------------------------------|------------|--------------------|
| Python, Java, JavaScript, C++ | 0.1660     | 0.2500             |

# Key Findings
- Experimentation involves fine-tuning Mistral-7B models for specific programming languages, model merging techniques, and evaluation using the CodeBLEU metric.
- Results indicate significant performance improvements across Python, Java, JavaScript, and C++ code generation tasks, showcasing the efficacy of the  proposed MoE framework.

<img width="938" alt="image" src="https://github.com/Santhoshkumar-p/neural-code-generation-moe/assets/24734488/fa2428c5-3e60-4524-955a-409d162bfff2">

# Conclusion
The study underscores the potential of MoE to revolutionize code generation tasks by improving precision, reducing computational overhead, and democratizing access to advanced machine learning models. By harnessing specialized expert models, MoE offers a scalable and economically viable solution for diverse tech-driven domains.
