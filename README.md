# LLM Red-Team Harness (Promptfoo + GitHub Actions)

Automated adversarial tests for an LLM app: prompt injection, jailbreaks,
system-prompt leakage and PII leakage. Runs in GitHub Actions and **fails the
build** if the model misbehaves — an AI release gate.

Maps to: OWASP LLM01 (Prompt Injection), LLM02 (Sensitive Info Disclosure),
LLM07 (System Prompt Leakage); MITRE ATLAS AML.T0051.

## Run locally
```bash
npm install -g promptfoo
export OPENAI_API_KEY=sk-...        # or any provider Promptfoo supports
promptfoo eval -c promptfooconfig.yaml
promptfoo view                      # opens a results dashboard
```

## How the gate works
`.github/workflows/redteam.yml` runs the eval on every pull request. Any failed
assertion = failed check = PR can't merge (turn on branch protection).

## Files
| File | Purpose |
|---|---|
| `promptfooconfig.yaml` | Target model, system prompt, test cases |
| `tests/attacks.yaml` | Attack prompts with expected safe behaviour |
| `.github/workflows/redteam.yml` | CI release gate |
