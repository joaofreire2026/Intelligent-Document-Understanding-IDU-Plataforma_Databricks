# =============================================================================
# PROJETO: Intelligent Document Understanding (IDU)
# PLATAFORMA: Databricks (Apache Spark + Delta Lake)
# CIENTISTA DE DADOS: MSc. João Freire Abramowicz
# INSTITUIÇÃO: Banco Bradesco S.A.
# LINGUAGEM: Python 3.x + PySpark
# DATA: 2025
# VERSÃO: 2.0 (Refatorado e Comentado — AI-GEN Review)
# =============================================================================
#
# OBJETIVO:
#   Desenvolver uma pipeline de Inteligência Artificial capaz de:
#     1. Ler documentos PDF nativos e digitalizados (OCR)
#     2. Extrair e pré-processar texto
#     3. Classificar documentos por tipo (RG, CNH, Contrato, etc.)
#     4. Extrair entidades nomeadas (NER): pessoas, CPFs, endereços, datas
#     5. Gerar embeddings semânticos vetoriais
#     6. Indexar embeddings no banco vetorial FAISS
#     7. Realizar busca semântica via LLM (RAG pipeline)
#     8. Monitorar experimentos com MLflow
#     9. Gerar dados sintéticos para testes e validação
#
# ARQUITETURA (Medallion Architecture):
#   Bronze  → Documentos brutos (PDFs, imagens)
#   Silver  → Texto extraído e limpo, entidades identificadas
#   Gold    → Embeddings, classificações, índice FAISS, resultados LLM
#
# ESTRUTURA DE NOTEBOOKS:
#   01_Instalacao         → Dependências e bibliotecas
#   02_Importacoes        → Imports organizados por categoria
#   03_Configuracao       → Sessão Spark, caminhos, parâmetros globais
#   04_Leitura_Documentos → Leitura de PDFs do Data Lake
#   05_Preprocessamento   → Limpeza e normalização de texto
#   06_Extracao_Entidades → NER com SpaCy
#   07_Classificacao      → Classificação baseada em palavras-chave
#   08_Embeddings         → Vetorização semântica (SentenceTransformer)
#   09_FAISS              → Indexação e busca vetorial
#   10_LangChain          → Chunking para RAG
#   11_MLFlow             → Rastreamento de experimentos
#   12_Testes             → Validação e smoke tests
# =============================================================================


# =============================================================================
# BLOCO 01 — INSTALAÇÃO DAS DEPENDÊNCIAS
# =============================================================================
# NOTA: Em Databricks, use %pip install no início do notebook (cell mágica).
#       Aqui estão documentadas como referência para reprodutibilidade.
#
# Dependências de produção (fixar versões em requirements.txt):
#   reportlab==4.2.x    → Geração de PDFs sintéticos
#   faker==26.x         → Dados falsos realistas em pt_BR
#   pandas==2.x         → Manipulação de DataFrames
#   pyspark==3.5.x      → Processamento distribuído (já presente no Databricks)
#   numpy==1.26.x       → Operações numéricas e vetoriais
#   nltk==3.9.x         → Tokenização e stopwords
#   spacy==3.7.x        → NER (Reconhecimento de Entidades Nomeadas)
#   sentence-transformers → Embeddings multilíngues
#   faiss-cpu==1.8.x    → Banco vetorial para busca semântica
#   langchain==0.2.x    → Orquestração LLM e text splitting
#   mlflow==2.x         → Rastreamento de experimentos ML
#   transformers==4.x   → Modelos HuggingFace (LLMs, tokenizers)
#



