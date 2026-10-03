# Developer Cookbook — PAX_EMBEDDINGS
**Stack:** Python 3.11, sentence-transformers, FAISS, numpy, AIOSS_FORMAT

## Basic Usage
```python
from pax_embeddings import Embeddings
module = Embeddings(pax_model="./pax-27b-q4.gguf",
                               aioss_chain="./pax_embeddings.aioss")
result = module.process(input_data)
print(result.output, result.chain_hash)
```

## Batch Processing
```python
results = module.process_batch(inputs, batch_size=4)
for r in results:
    print(r.chain_hash)
```

## AIOSS Append
```python
import hashlib, time
def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

chain_hash = aioss_append("./pax_embeddings.aioss", result.to_bytes(), "PAX_EMBEDDINGS")
```

## Integration with Anticloud TIER_2
```python
# Chain with PAX_INFERENCE_CORE
from pax_inference_core import PAXInferenceCore
from pax_embeddings import Embeddings

core = PAXInferenceCore(model="./pax-27b-q4.gguf")
module = Embeddings(inference_core=core)
```

## Domain: Sovereign embedding generation for RAG and semantic search
This module specializes in: sovereign embedding generation for rag and semantic search.
AIOSS entry type: embedding batch (input hash + embedding tensor hash + model version).

## Performance
Use module.benchmark() to measure throughput on your hardware.
Pre-warm: module.warmup() before serving production requests.
