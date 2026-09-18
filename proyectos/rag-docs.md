# rag-docs

## Problema
Las empresas quieren un asistente que responda sobre sus propios documentos, pero un LLM suelto inventa respuestas y no dice de dónde las sacó. En un dominio legal eso es inaceptable: hay que citar el artículo exacto y decir "no está en los documentos" cuando no está.

## Qué construí
Un RAG en español sobre dos leyes chilenas (consumidor y datos personales) que responde citando `[Ley N, Art. M]` y se abstiene cuando la evidencia no alcanza. Todo local: embeddings ONNX (`fastembed`) sin GPU ni API keys, PostgreSQL + pgvector en Docker, CLI en ~500 líneas de Python sin frameworks de RAG. Con un set de evaluación fijo publicado: `hit@3 = 0.93` y abstención en preguntas sin respuesta `= 0.93`.

## Stack
Python 3.12 (stdlib + `fastembed`, `psycopg`, `pgvector`) · PostgreSQL 16 + pgvector (Docker) · modelo `jina-embeddings-v2-base-es` · generación enchufable (`claude -p` opcional) · tests `unittest` · gate `pre-commit` + `gitleaks`.

## Decisiones técnicas
- Chunking por **artículo** con metadatos, no por largo fijo: la unidad de cita en una ley es el artículo; los largos se parten por inciso sin cortar oraciones y repiten el encabezado.
- El set de evaluación se commiteó **antes** del buscador y de cualquier ajuste de parámetros; después no se toca para subir números (el gate lo verifica en la historia de git).
- Umbral de abstención elegido por barrido sobre la distribución de scores de preguntas respondibles vs. no respondibles, con el trade-off publicado (16 % de falsa abstención).
- Se midieron dos modelos de embeddings y se publicó el que perdió (MiniLM multilingüe, hit@3 0.77) junto al elegido.
- Sin índice HNSW con 299 filas: scan exacto; la línea del índice queda lista para cuando el corpus crezca.

## Qué aprendí
Que el control de alucinación es una decisión de arquitectura (el modelo solo puede citar lo que recibió) más una medición honesta, no un prompt. Y que la abstención por una sola señal separa bien lo lejano pero es débil con negativos vecinos: la próxima mejora es un re-ranker o clasificador de "¿responde?".

## Estado
Terminado y evaluado. Código público: https://github.com/ISAACRICARDO2043/rag-docs
