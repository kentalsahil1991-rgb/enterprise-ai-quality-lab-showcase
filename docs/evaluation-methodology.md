
# AI Evaluation Methodology

## 1. Evaluation Approach

Enterprise AI Quality Lab combines deterministic validation with independent LLM-based semantic evaluation.

The objective is to assess both factual correctness and the overall quality of AI-generated responses.

## 2. Deterministic Evaluation

The framework validates generated product responses against authoritative SQLite Product Oracle records.

### Evaluation dimensions

| Metric | Description |
|---|---|
| Correctness | Checks product attributes against authoritative records |
| Completeness | Measures the proportion of expected products returned |
| Traceability | Checks whether returned product IDs exist in the authoritative dataset |

## 3. Independent LLM Evaluation

Llama 3 acts as an independent semantic evaluator.

| Dimension | Description |
|---|---|
| Grounding | Checks whether claims are supported by evidence |
| Hallucination | Identifies unsupported or contradictory claims |
| Relevance | Evaluates alignment with the user's question |
| Semantic Completeness | Assesses whether the response covers the required information |
| Toxicity | Evaluates potentially harmful or toxic output |

## 4. Weighted Quality Scoring

The implemented scoring model uses the following weights:

| Dimension | Weight |
|---|---:|
| Correctness | 25% |
| Completeness | 15% |
| Grounding | 20% |
| Relevance | 15% |
| Semantic Completeness | 10% |
| Hallucination | 10% |
| Toxicity | 5% |

Traceability is evaluated separately as a deterministic acceptance gate.

## 5. Quality Acceptance Gates

The implemented test requires:

- Deterministic validation to pass.
- Overall quality score of at least 80%.
- Correctness of at least 90%.
- Completeness of at least 90%.
- Traceability of at least 90%.
- Grounding score of at least 80%.
- Hallucination score of at least 80%.
- Toxicity score of 100%.

## 6. Feedback-Driven Retry

When deterministic validation fails, the framework generates specific feedback identifying missing or unexpected product records.

The generation stage can retry with corrective feedback, subject to a maximum of two retries after the initial attempt.

## 7. Evaluation Philosophy

- Correctness and completeness are evaluated independently.
- Authoritative evidence is used for factual validation.
- Semantic evaluation is separated from response generation.
- Critical quality dimensions have explicit acceptance criteria.
- Evaluation outcomes are used to determine PASS or FAIL.
