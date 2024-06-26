# Inference script

We are using a multi-model enpoint hosted on Sagemaker and provide a inference script to process requests and send responses back.

The inference script is currently hardcoded with the supported models (lib/rag-engines/sagemaker-rag-models/model/inference.py)

```py
embeddings_models = [
    "intfloat/multilingual-e5-large",
    "sentence-transformers/all-MiniLM-L6-v2",
]
cross_encoder_models = ["cross-encoder/ms-marco-MiniLM-L-12-v2"]
```

The API is JSON body based:

```json
{
  "type": "embeddings",
  "model": "intfloat/multilingual-e5-large",
  "input": "I love Berlin"
}
```

```json
{
  "type": "cross-encoder",
  "model": "cross-encoder/ms-marco-MiniLM-L-12-v2",
  "input": "I love Berlin",
  "passages": ["I love Paris", "I love London"]
}
```

## Cohere Rerank 3

To use the Cohere Rerank 3 model, get an API key from Cohere, and include the following in the JSON request body:

```json
{
  "type": "cross-encoder",
  "model": "rerank-english-v3.0",
  "input": "What is the capital of the United States?",
  "passages": [
    "Carson City is the capital city of the American state of Nevada.",
    "Washington, D.C. is the capital of the United States.",
    ...
  ]
}