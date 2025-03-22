# Getting Started with Promptfoo for Gardening Guides

This guide will walk you through setting up and using promptfoo to test your gardening guide prompts for Paraguayan crops.

## Prerequisites

- **Node.js**: v20.19.0 works well
- **Ollama**: For local LLM testing
- **Your prompt template**: Located in `1-page-gardening-guide-prompt.txt`

## Step 1: Check Your Node.js Version

```bash
node -v
```

If you're using Node.js v22+ and encounter compatibility issues, downgrade to v20:
1. Download Node.js v20 from [nodejs.org/download/release](https://nodejs.org/download/release/)
2. Uninstall your current Node.js version
3. Install the downloaded v20 version

## Step 2: Create Your Prompt Template 

Create a file, example: `1-page-gardening-guide-prompt.txt` with your prompt template.(https://www.promptfoo.dev/docs/configuration/parameters/) Use `[BOTANICAL NAME]` as a placeholder for different plant species.

Example structure:
```
Create a 1-page gardening guide for "{{BOTANICAL NAME}}" in Paraguay. Include:

1. Local name (Spanish/Guaraní)
2. Growing conditions (soil, climate)
3. Planting instructions
4. Care requirements
5. Harvesting tips
6. Common pests and diseases
7. Cultural significance in Paraguay
```

## Step 3: Create Your Promptfoo Configuration

Create a file named `promptfooconfig-gardening.yaml` with the following content:

```yaml
description: "Paraguayan Crops Gardening Guide Test"

# Prompt configuration
prompts:
  - file://1-page-gardening-guide-prompt.txt

# Provider configuration
providers:
  - id: ollama:hf.co/MaziyarPanahi/ZYH-LLM-Qwen2.5-14B-V3-GGUF:Q5_K_M
    config:
      temperature: 0

# Test cases
tests:
  # Test case 1: Chayote squash
  - vars:
      BOTANICAL NAME: "Sechium edule"
    description: "Chayote squash gardening guide"
  
  # Test case 2: Cassava
  - vars:
      BOTANICAL NAME: "Manihot esculenta"
    description: "Cassava gardening guide"
  
  # Test case 3: Sweet potato
  - vars:
      BOTANICAL NAME: "Ipomoea batatas"
    description: "Sweet potato gardening guide"
  
  # Test case 4: Common bean
  - vars:
      BOTANICAL NAME: "Phaseolus vulgaris"
    description: "Common bean gardening guide"

# Output configuration
outputPath: "./results/gardening-guides-results.json"
```

## Step 4: Run the Evaluation
(https://github.com/promptfoo/promptfoo/tree/main/examples/simple-cli)

Run the following command to test your prompt with different botanical names:

```bash
npx promptfoo@latest eval -c promptfooconfig-gardening.yaml
```

## Step 5: View the Results

After the evaluation completes, you can view the results:

```bash
npx promptfoo@latest view
```

This will open a web interface where you can compare the outputs for different botanical names.

## Troubleshooting

### Node.js Version Issues

If you see errors like:
```
Error: The module '...\better_sqlite3.node' was compiled against a different Node.js version
```

This means your Node.js version is too new. Downgrade to Node.js v20.x as described in Step 1.

### Configuration Syntax Errors

If you see template rendering errors, check your configuration syntax:

1. Make sure you're using `file://` to include prompt files
2. Verify that your YAML indentation is correct


## Additional Resources

- [Promptfoo Documentation](https://www.promptfoo.dev/docs/)
- [Promptfoo Configuration Guide](https://www.promptfoo.dev/docs/configuration/guide/)
- [Promptfoo Parameters Reference](https://www.promptfoo.dev/docs/configuration/parameters/)

Happy prompt testing!
