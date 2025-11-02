# Groq Setup Guide

This project has been configured to use Groq's ultra-fast LLM inference API instead of OpenAI.

## Why Groq?

- **Blazing Fast**: Groq's LPU (Language Processing Unit) delivers incredibly fast inference
- **OpenAI Compatible**: Drop-in replacement for OpenAI's API
- **Cost Effective**: Competitive pricing with generous free tier
- **Quality Models**: Access to Llama 3.3, Mixtral, Gemma 2, and more

## Setup Instructions

### 1. Get Your Groq API Key

1. Visit [console.groq.com](https://console.groq.com)
2. Sign up or log in
3. Navigate to [API Keys](https://console.groq.com/keys)
4. Create a new API key

### 2. Configure Environment Variables

Edit the `.dev.vars` file in the project root:

```env
OPENAI_API_KEY=gsk_your_groq_api_key_here
OPENAI_BASE_URL=https://api.groq.com/openai/v1
OPENAI_MODEL=llama-3.3-70b-versatile
```

### 3. Available Models

Choose from these recommended Groq models:

| Model | Description | Best For |
|-------|-------------|----------|
| `llama-3.3-70b-versatile` | Meta's Llama 3.3 70B | General purpose, recommended |
| `llama-3.1-70b-versatile` | Meta's Llama 3.1 70B | High quality responses |
| `llama-3.1-8b-instant` | Meta's Llama 3.1 8B | Ultra-fast responses |
| `mixtral-8x7b-32768` | Mistral's Mixtral | Long context (32k tokens) |
| `gemma2-9b-it` | Google's Gemma 2 | Efficient and capable |

See the full list at [console.groq.com/docs/models](https://console.groq.com/docs/models)

### 4. Run Locally

```bash
npm start
```

The app will now use Groq for AI inference!

### 5. Deploy to Production

For production deployment to Cloudflare Workers:

1. Set the API key as a secret:
   ```bash
   echo "OPENAI_API_KEY=gsk_your_groq_api_key_here" > .dev.vars
   wrangler secret bulk .dev.vars
   ```

2. Deploy:
   ```bash
   npm run deploy
   ```

The `OPENAI_BASE_URL` and `OPENAI_MODEL` are already configured in `wrangler.jsonc` and will be used in production.

## Switching Between Providers

You can easily switch between different OpenAI-compatible providers by changing the environment variables:

### Use OpenAI
```env
OPENAI_API_KEY=sk-...
# OPENAI_BASE_URL=  # Leave empty or comment out
OPENAI_MODEL=gpt-4o-2024-11-20
```

### Use Groq (Current Setup)
```env
OPENAI_API_KEY=gsk_...
OPENAI_BASE_URL=https://api.groq.com/openai/v1
OPENAI_MODEL=llama-3.3-70b-versatile
```

### Use Together AI
```env
OPENAI_API_KEY=...
OPENAI_BASE_URL=https://api.together.xyz/v1
OPENAI_MODEL=meta-llama/Meta-Llama-3.1-70B-Instruct-Turbo
```

### Use Local LLM (Ollama)
```env
OPENAI_API_KEY=ollama  # Any value works
OPENAI_BASE_URL=http://localhost:11434/v1
OPENAI_MODEL=llama3.3
```

## Troubleshooting

### API Key Not Working
- Ensure your API key starts with `gsk_` for Groq
- Check that the key is active in the Groq console
- Verify no extra spaces in `.dev.vars`

### Model Not Found
- Check the model name matches exactly (case-sensitive)
- Visit [console.groq.com/docs/models](https://console.groq.com/docs/models) for the current list

### Rate Limits
- Groq has generous rate limits on the free tier
- For production use, consider upgrading your plan
- See [console.groq.com/settings/limits](https://console.groq.com/settings/limits)

## Resources

- [Groq Documentation](https://console.groq.com/docs)
- [Groq API Reference](https://console.groq.com/docs/api-reference)
- [Rate Limits & Pricing](https://console.groq.com/settings/limits)
- [Model Playground](https://console.groq.com/playground)
