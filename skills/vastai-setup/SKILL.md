---
name: vastai-setup
description: "Set up Vast.ai CLI — configure API key, verify installation, set up SSH keys, and check account. Use when the user needs to get started with Vast.ai or is having authentication issues."
disable-model-invocation: true
allowed-tools: Bash
---

# Vast.ai CLI Setup

Help the user set up and verify their Vast.ai CLI.

## Step 1: Check Installation

```bash
vastai --version
```

If not installed:
```bash
pip install vastai
```

## Step 2: Configure API Key

Get an API key from https://cloud.vast.ai/account/

```bash
vastai set api-key <API_KEY>
```

Or set via environment variable:
```bash
export VAST_API_KEY=<API_KEY>
```

## Step 3: Verify Authentication

```bash
vastai show user
```
Should return account details (username, email, balance).

## Step 4: Check SSH Keys

```bash
vastai show ssh-keys
```

If no keys exist, create/upload one:
```bash
vastai create ssh-key                   # Auto-generates and uploads
# OR upload existing:
vastai create ssh-key "$(cat ~/.ssh/id_rsa.pub)"
```

## Step 5: Check Account Balance

```bash
vastai show user --raw | jq '.credit'
```

## Step 6: Test Search

```bash
vastai search offers 'gpu_name=RTX_4090 num_gpus=1 reliability>0.9' -o 'dph_total'
```

If this returns results, setup is complete.

## Step 7: Environment Variables (Optional)

Store commonly used values:
```bash
vastai create env-var HF_TOKEN <token>
vastai create env-var WANDB_API_KEY <key>
vastai show env-vars
```

These are available in all instances.

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Auth errors | Re-set API key from https://cloud.vast.ai/account/ |
| No search results | Broaden query or check credits |
| SSH connection refused | Wait 30s after instance starts, check `vastai ssh-url <ID>` |
| Instance won't start | Check offer is still available, try another offer |
| `vastai: command not found` | `pip install vastai` or check PATH |
