# Lending Intelligence Assistant - SLM Fine-Tuning

## 1. Overview
This repository contains a parameter-efficient fine-tuned Small Language Model (Qwen2.5-1.5B-Instruct) designed to act as a domain-aware Lending Intelligence Assistant. It assists credit officers with loan summaries, credit risk classification, and loan approval recommendations.

## 2. Technical Decisions & Model Selection
* **Base Model:** Qwen2.5-1.5B-Instruct was chosen because it fits the <3 billion parameter constraint and possesses strong foundational instruction-following capabilities.
* **Fine-Tuning Strategy:** I utilized QLoRA (4-bit quantization via bitsandbytes) and the PEFT library to freeze base weights and train low-rank adapters. This allowed the training to easily run on a consumer GPU (8-16 GB VRAM) within the 1-hour time limit.

## 3. Data Preparation & Feature Engineering
To improve the model's domain awareness, the following features were engineered from the raw dataset:
* **FOIR (Fixed Obligation to Income Ratio):** Capped at 1.0 to prevent outlier skew.
* **Credit Utilization:** Calculated as Outstanding Balance / Sanctioned Amount.
* **Delinquency Flag:** Binary indicator derived from Current DPD.

The dataset was then transformed into prompt-completion pairs using a strict ChatML conversational format.

## 4. Evaluation & Business Impact
* **Evaluation Methodology:** The model was tested against 10 diverse, unseen borrower profiles ranging from 'Ideal' to 'High-Risk'. 
* **Demonstrated Improvement:** [Insert a brief sentence here about how the model correctly rejected high-risk profiles and approved ideal ones without hallucinating].
* **Business Value:** The fine-tuned model understands critical lending concepts like DPD and FOIR, minimizing the risk of inconsistent underwriting and providing clear, actionable recommendations for loan officers.

## 5. Reproducibility
To run this pipeline:
1. Install dependencies via `pip install -r requirements.txt`.
2. Run the `SLM_Fine_Tuning_Pipeline.ipynb` notebook from top to bottom.