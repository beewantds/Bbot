# Bbot - Selective Web Indexing & Ranking System

A lightweight, cost-aware pipeline that distills the **10 M-page Common Crawl** corpus into a clean, high-quality search index you can query with LLMs.

## ✨ Key Features
- **Selective crawling** – rank URLs before fetching heavy content  
- **LLM‐based relevance scoring** (Llama-3 / Qwen)  
- **Robots-aware fetcher** with adaptive revisit scheduling  
- **Compact JSON index** → `{url, title, snippet, score, last_seen}`  
- **AWS-first storage** (S3 + Athena/OpenSearch/Weaviate)

## 🚀 Quick Start
```bash
# 1. Clone and set up Python env
git clone https://github.com/your-org/selective-indexer.git
cd selective-indexer
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# 2. Download latest Common Crawl URL list
make fetch-cc-seeds   # outputs data/raw/cc_urls/

# 3. Run the seed scorer (CPU/GPU or Groq)
make score-seeds

# 4. Crawl top-scoring domains (respects robots.txt)
make crawl-batch

# 5. Build/update parquet index shards
make build-index
```
## 🗂 Repo Layout

```bash
.
├─ configs/          # thresholds, weights, crawl rules
├─ data/             # URL lists, metadata, index shards
├─ src/
│  ├─ scorer/        # LLM relevance classifier
│  ├─ crawler/       # polite, throttled HTTP fetcher
│  ├─ extractor/     # title/snippet & metadata
│  └─ ranker/        # final quality score + scheduler
└─ scripts/          # one-off utilities & notebooks
```

## 📅 Roadmap

1. Seed scoring prototype 🔄 loading ...

2. Async crawler v1 

3. Adaptive sitemap discovery

4. Public search API + Integration with Beewant
