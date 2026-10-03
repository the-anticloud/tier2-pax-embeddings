# PAX Embeddings — Vector Embedding Generation

**Status:** Production | **Version:** 1.0.0 | **Author:** PAX Reasoning Team  
**Domain:** 0-1.gg/pax/embeddings

---

## What Is PAX Embeddings?

PAX Embeddings generates vector representations for text, code, and images, powering semantic search, RAG (Retrieval-Augmented Generation), and similarity matching across PAX system.

**Specifications:**
- Model: text-embedding-ada-002 compatible
- Dimension: 1536 (configurable)
- Throughput: 10K embeddings/sec
- Latency: <50ms P95 per embedding
- Formats: Text, code, multimodal (with vision)

---

## Architecture

- **Layer 1:** Input normalization (text/code/image)
- **Layer 2:** Tokenization (10K token limit)
- **Layer 3:** Embedding model (transformer-based)
- **Layer 4:** Output caching (Redis)

---

## Quick Start

```python
from pax_embeddings import EmbeddingClient

client = EmbeddingClient(base_url="http://localhost:8001")

# Text embedding
embedding = client.embed(
    text="What is machine learning?",
    model="text-embedding-ada-002"
)
print(len(embedding))  # 1536 dimensions
```

---

## Integration

- **PAX_RETRIEVAL:** Uses embeddings for dense retrieval
- **PAX_KNOWLEDGE_GRAPH:** Embeddings for semantic search
- **PAX_CACHE:** Cache embeddings for repeated texts
- **api-oss-gateway:** Embedding endpoint

---

**Next:** See APPENDIX/
