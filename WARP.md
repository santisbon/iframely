# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview
Iframely is a self-hosted API service that provides oEmbed/2 gateway endpoint functionality. It takes URLs and returns metadata and rich media embeds for supported domains. The service includes domain-specific parsers for popular publishers and supports generic publishing protocols like oEmbed, Open Graph, and Twitter Cards.

## Setup and Configuration
1. Copy `config.local.js.SAMPLE` to `config.local.js` and configure the options
2. Key config options:
   - `port`: Default 8061 (can be overridden by PORT env var)
   - `CACHE_ENGINE`: Options are 'no-cache', 'node-cache', 'redis', 'memcached'
   - `baseAppUrl`: For embeds requiring render, default "http://localhost:8061"
   - Configure provider-specific keys in `providerOptions` (e.g. Google Maps, Twitter)

## Development Commands
```bash
# Install dependencies
pnpm install

# Run tests
pnpm test              # Run all tests
pnpm test:core-plugins # Run core plugin tests only
pnpm test-e2e         # Run e2e tests (runs on port 8080)

# Start server
node server.js
```

## Code Architecture
- `lib/`: Core functionality modules
  - `core.js`: Main API functionality
  - `cache.js`: Caching implementation
  - `fetch.js`: URL fetching and processing
  - `whitelist.js`: Domain whitelisting logic
- `plugins/domains/`: Domain-specific parsers for supported publishers
- `test/`: Test suites including core plugins, e2e, and custom plugins tests

## Debugging
- Visual debug tool available at `{your.server}/debug`
- API endpoints:
  - Iframely format: `{your.server}/iframely?url=...`
  - oEmbed format: `{your.server}/oembed?url=...`