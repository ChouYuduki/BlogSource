+++
date = '2026-10-17'
title = '【Agent】What is RAG'
draft = false
author = 'Saka'
categories = [
    "Agent"
]

+++

# RAG とは

RAG(Retrieval-Augmented Generation, 検索拡張生成) は、LLMに外部の情報を組み合わせることで、LLMモデルの出力の質を向上させる手法です。  　　
外部の情報としては、主に次のようなものが使われます。　　

1. 独自に用意した資料（例：自動車の整備マニュアル、製品の取扱説明書、カスタマーサポートのFAQ、社内文書など）
2. Web検索で取得した情報

RAGでは、外部のデータソースから関連する情報を検索し、ユーザーの質問と一緒にLLMへ入力します。これにより、出力の正確性と信頼性が向上します。

# RAGのメリット

* Reduce Hallucinations (ハルシネーション)
* Provide current or domain-specific information 
* Being efficient and cost-effective (fine-tuning is costive)

# the steps of RAG 

Knowledge Base -> Split into Text chunks -> change into Vectors by embedding model -> storage into Vector Database -> retrieve 

Un-structured Data (image, video, etc.) convert to Vector, then can be storaged into Vector Database, for managing and storaging

* embedding model e.g.: text-embedding-3-large by OpenAI

# Traditional Database VS Vector Database

| Traditional Database | Vector Database |
|------|------|
| For Un-structured Data | For structured Data | 

