# Mixture of Expert Model for Code Generation
This paper explores the efficacy of the Mixture-of-Experts (MoE) framework in code generation, showcasing superior performance compared to traditional monolithic model architectures. By applying MoE to code generation tasks across various programming languages, including Python, C++, Java, and Javascript, the study demonstrates enhanced precision and reduced computational overhead.  

**Walkthrough Video** ->  https://youtu.be/FjxlqdsM-KI 

# Overview
The paper proposes a MoE framework tailored to code generation tasks, where different programming languages are handled by specialized expert models within the Mistral-7B base model. Through this architecture, the system optimally selects expert models based on the input code snippet's language, thereby improving output precision.

# Architecture
<img width="961" alt="image" src="https://github.com/Santhoshkumar-p/neural-code-generation-moe/assets/24734488/5bb27578-ffc9-494d-b2c2-169ed0258972">

<img width="1096" alt="image" src="https://github.com/Santhoshkumar-p/neural-code-generation-moe/assets/24734488/be903e28-d20a-459a-90b6-bb85337129b9">

- We are opting for the Transformer architecture, a fundamental element in natural language processing, entails encoder and decoder blocks, each layered with Transformer units.
- The architectural approach integrates Mixtral, a variation that substitutes feed-forward blocks with Mixture-of-Expert layers to support a fully dense context length of 32k tokens.
- The Mixture-of-Experts (MoE) layer, composed of expert networks and a gating network, facilitates computational efficiency through sparsity.
- Within the gating network, methods like Softmax Gating and Noisy Top-K Gating are investigated to improve computation and balance the load

# Dataset
We used the xlcost-text-to-code dataset offered by organization "codeparrot" on Hugging Face

# Training
- We adopted traditional fine-tuning techniques, specifically parameter-efficient fine-tuning (PEFT) with quantization using adapters (QLoRA) to cater to our resource-optimized requirements.
- To create the MoE model, we use the mergekit library. This script combines parameters from a "base" model with those from various "expert" models.
- Experts in the MoE gating can be selected based on prompts, enabling model specialization.
- Training optimizes the gating network to route inputs through the most suitable experts, enhancing performance

## Example Dataset
**Text:** Sum of sum | Function to find the sum ; Driver code
**Program:**
```python
def sumOfSumSeries ( n ) :
NEW_LINE INDENT return ( n * ( n + 1 ) * ( n + 2 ) ) // 6
NEW_LINE DEDENT N = 5 NEW_LINE print ( sumOfSumSeries ( N ) )
```

# Training the Gating Network: 
We train the gating network by simple back-propagation, along with the rest of the model. If we choose k > 1, the gate values for the top k experts have nonzero derivatives with respect to the weights of the gating network. Gradients also back-propagate through the gating network to its inputs.

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
