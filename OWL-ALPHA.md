# Bonus: OpenRouter OWL Alpha Setup 🦉

Add **OWL Alpha** (free, 1M context) to the same OpenClaw instance via OpenRouter.

## Step 0: Get an OpenRouter Key

Generate at [openrouter.ai/keys](https://openrouter.ai/keys) — starts with `sk-or-v1-...`

## Step 1: Add Provider

In `~/.openclaw/openclaw.json` under `models.providers`:

```json
"openrouter": {
  "baseUrl": "https://openrouter.ai/api/v1",
  "apiKey": "sk-or-v1-YOUR_KEY_HERE",
  "api": "openai-completions",
  "models": [
    {
      "id": "openrouter/owl-alpha",
      "name": "OWL Alpha",
      "api": "openai-completions",
      "reasoning": true,
      "input": ["text"],
      "contextWindow": 1000000,
      "maxTokens": 32000,
      "cost": { "input": 0, "output": 0, "cacheRead": 0, "cacheWrite": 0 }
    }
  ]
}
```

## Step 2: Agent Models List

Same as the Fable guide — mirror the provider block in `~/.openclaw/agents/main/agent/models.json`, otherwise the model won't be in the allowed list.

## Step 3: Switch

```
/reload-config
/model openrouter/owl-alpha
```

Verify with `/status` — no `🔑 unknown`, no fallback line = working. ✅

## Gotcha: Config Overwrites

If you restore/rebuild your OpenClaw instance, custom providers can get wiped from `openclaw.json`. Keep a backup of your provider blocks (like this guide 😉) so you can re-add them quickly.

---

*Part of the [Claude Fable 5 setup guide](README.md) · by Glasswing 🦋*
