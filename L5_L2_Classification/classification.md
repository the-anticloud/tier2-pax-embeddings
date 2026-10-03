# L5 Narrow / L2 General Classification — PAX_EMBEDDINGS
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign embedding generation for RAG and semantic search

## L5 Narrow
PAX_EMBEDDINGS operates at L5 Narrow within its specialized scope: sovereign embedding generation for rag and semantic search.
It does not generalize outside this function. PAX 27B inference is scoped to this module's
specific input/output contract. All outputs are deterministically validated before AIOSS append.

## L2 General
PAX_EMBEDDINGS is available to all 9 Anticloud deployment tiers. Any tier project that needs
sovereign embedding generation for rag and semantic search capability calls PAX_EMBEDDINGS without reconfiguration. Same API across all domains.

## PAX Integration
PAX 27B interfaces with PAX_EMBEDDINGS as a specialized inference module. Inputs are preprocessed
to PAX_EMBEDDINGS's schema, PAX generates outputs within that schema, and results are AIOSS-chained
before being returned to the calling module.

## AIOSS Audit Relevance
Every embedding batch (input hash + embedding tensor hash + model version) is appended to the AIOSS chain.
H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n)
Full reproducible audit trail, verifiable offline without cloud.

## Regulatory
GDPR Art. 25 (privacy by design — embeddings never leave device)
