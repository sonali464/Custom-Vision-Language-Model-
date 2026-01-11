# Task 3: Custom Vision-Language Model (VLM) for Industrial Quality Inspection
Problem Statement
A semiconductor manufacturer requires an offline AI system for PCB inspection where:
•	50,000 PCB images are available
•	Bounding box annotations exist
•	No QA pairs are provided
•	Generic VLMs hallucinate and give unreliable answers
•	Inference must be fast (<2s) and accurate

 ### Proposed Solution
We propose a custom lightweight VLM architecture inspired by  LLaVA , modified specifically for industrial defect inspection

## (A) Model Selection
Chosen Architecture:  
Custom  LLaVA-style Vision-Language Model

### Reasons:
•	Supports image–text fusion
•	Flexible for fine-tuning
•	Suitable for offline deployment
•	Allows precise localization control
•	Open-source friendly design

### Key Considerations:
•	Model size (edge deployment)
•	Inference speed
•	Fine-tuning flexibility
•	Licensing constraints
•	Hallucination control

### (B) Architecture Design
 High-Level Pipeline
 PCB Image
↓
Custom CNN Vision Encoder
↓
Spatial Feature Tokens
↓
Cross-Modal Fusion
↓
Lightweight Language Decoder
↓
Structured Output (JSON)


### Components:
Vision Encoder Custom CNN trained on PCB defect images
Language Decoder Lightweight distilled transformer
Fusion Cross-attention between visual and text tokens
Output Structured responses instead of free-form text



## (C) Optimization Strategy 
To meet real-time industrial constraints, the following optimizations are applied:
•	INT8 Quantization
•	Model Pruning
•	Knowledge Distillation
•	LoRA-based fine-tuning
•	Batch size = 1 (real-time inference)

## (D) Hallucination Mitigation
•	Generic pretraining on internet data
•	Lack of domain grounding
### Mitigation Techniques:
•	Enforced structured output format
•	Mandatory bounding box grounding
•	Vision-conditioned decoding only
•	Consistency loss during training
•	Confidence-score thresholding
## (E) Training Strategy
# Stage 1: Vision Encoder Training
•	Train CNN on PCB images + bounding boxes
•	Objective: Accurate localization
# Stage 2: QA Pair Generation
•	Auto-generate QA pairs from annotations
# Stage 3: VLM Fine-Tuning
•	Input: Image + Question
•	Output: Structured JSON response
### Data Augmentation:
•	Rotation
•	Noise injection
•	Contrast variation
•	Occlusion simulation
## (F) Validation & Evaluation
### Metrics:
•	Counting Accuracy
•	Localization IoU
•	Hallucination Rate
•	Inference Latency
### Validation Approach:
•	Compare predicted boxes with ground truth
•	Measure false positive responses
•	Stress-test on unseen PCB layouts

