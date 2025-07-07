---
date: '2025-07-04T23:00:00-05:00'
draft: false
title: 'Trying Tauric Research TradingAgents'
description: 'My experience setting up and running Tauric Research TradingAgents'
tags: ["AI", "trading", "llm", "multi-agent", "TauricResearch", "TradingAgents", "python", "finance", "machine-learning", "college-tech"]
categories: ["AI & Machine Learning", "Finance", "Student Projects"]
keywords: ["Tauric Research", "TradingAgents", "multi-agent trading", "LLM trading", "SPY", "GPT-4o", "o1", "intraday trading", "python", "finance"]
---
This week I decided to try out [Tauric Research's TradingAgents](https://github.com/TauricResearch/TradingAgents) after reading their [arXiv paper](https://arxiv.org/pdf/2412.20138). As someone interested in both AI and trading, the idea of a multi-agent LLM-powered trading framework was too cool to pass up.

![Screenshot of TradingAgents CLI running SPY test](https://github.com/TauricResearch/TradingAgents/blob/main/assets/schema.png?raw=true)

The architecture of Tauric Research's TradingAgents framework is designed to facilitate multi-agent trading using large language models (LLMs). Here's a breakdown of the key components:

- **Data Ingestion**: The framework starts by ingesting market data, which is crucial for making informed trading decisions. This data is processed and fed into the system in real-time.

- **Agent Coordination**: Multiple agents work in tandem, each specializing in different aspects of trading. These agents communicate and coordinate to optimize trading strategies.

- **Model Selection**: The framework allows for flexible model selection, enabling users to choose from various LLMs like GPT-4o and o1. This flexibility is key to adapting to different market conditions and trading goals.

- **Decision Making**: The agents use the insights from the LLMs to make trading decisions. This involves analyzing market trends, predicting future movements, and executing trades.

- **Feedback Loop**: After executing trades, the system evaluates the outcomes and adjusts strategies accordingly. This feedback loop is essential for continuous improvement and adaptation to changing market dynamics.

This architecture not only supports complex trading strategies but also allows for experimentation and integration with custom models, as I plan to do with my own intraday trading system.


## Setup Experience

It took me a bit to get everything set up in my CLI (mostly just Python environment stuff and getting the right API keys), but once I hooked it up with my OpenAI API, it was actually really easy to use. The docs are pretty clear, and the CLI lets you pick tickers, models, and other options interactively.

```bash
# Clone the repo
git clone https://github.com/TauricResearch/TradingAgents.git
cd TradingAgents

# (Recommended) Create a virtual environment
conda create -n tradingagents python=3.13
conda activate tradingagents

# Install dependencies
pip install -r requirements.txt

# Set your API keys
export FINNHUB_API_KEY=your_finnhub_key
export OPENAI_API_KEY=your_openai_key

# Run the CLI
python -m cli.main
```

## My First Test: SPY with GPT-4o and o1

For my first test, I used SPY as the ticker. I set GPT-4o for the basic models and o1 for the final model. The whole run only cost me about **5 cents** in API usage, which is honestly super reasonable for a full multi-agent LLM pipeline.

![Screenshot of TradingAgents CLI running SPY test](https://github.com/TauricResearch/TradingAgents/blob/main/assets/cli/cli_news.png?raw=true)

## Understanding the TradingAgents Architecture

## Thoughts and Next Steps

What I want to do next is pair TradingAgents with my own intraday trading model and custom indicators. My idea is to use TradingAgents as a separate signal—if it says "buy" or "sell" for the day, I would only take trades in that direction with my own system. I think this could be a really interesting way to combine LLM-based reasoning with my more traditional quant models.

**Pros:**
- Easy to set up after initial environment config
- Super flexible with model selection
- Cheap to run even with GPT-4o and o1
- Open source and well-documented

**Cons:**
- Still early days for LLM trading agents (lots to experiment with)
- Needs good API keys and some Python comfort

## Links
- [Tauric Research TradingAgents GitHub](https://github.com/TauricResearch/TradingAgents)
- [arXiv Paper: TradingAgents: Multi-Agents LLM Financial Trading Framework](https://arxiv.org/pdf/2412.20138)