# Privacy Policy

**Last updated:** 2026-03-02

## Overview

job-assistant is a Claude plugin that runs entirely within your local Claude environment (Claude Code or Claude Desktop). This plugin does not collect, store, or transmit any user data to external servers.

## Data Processing

### What the plugin processes

- Job posting text or URLs you provide
- Resume text or files you provide
- Supplementary career information you provide

### How data is processed

- All processing happens within your Claude session
- Your data is sent to Anthropic's Claude API as part of normal Claude conversation
- The plugin itself does not make any external API calls or network requests
- No data is stored between sessions

### Personal Information Masking

- The plugin uses masking tokens (`[Masked:Name]`, `[Masked:Phone]`, etc.) to protect personal information during analysis
- Personal information is only restored during local PDF generation
- Masking is applied throughout all analysis and review stages

## Optional MCP Server

If you choose to use the optional MCP server (premium feature):

- Resume and job posting text is sent to Anthropic's Claude API for AI analysis
- This follows the same data handling as standard Claude API usage
- Your Anthropic API key is required and stored locally
- No data is stored on any third-party server

## Data Storage

- The plugin does not maintain any database or persistent storage
- All generated files (optimized resumes, analysis reports) are saved locally on your machine
- You have full control over all output files

## Third-Party Services

- **Anthropic Claude API**: Used for AI analysis (standard Claude usage)
- No other third-party services are used

## Your Rights

- You can delete all generated files at any time
- You can uninstall the plugin at any time with no residual data
- The plugin is open source (MIT License) — you can inspect all code

## Contact

For privacy concerns or questions, please open an issue at:
https://github.com/imfelixkim/job_assistant/issues
