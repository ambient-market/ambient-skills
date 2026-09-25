# Ambient skills

Official agent skills for [Ambient](https://ambient.market), programmable infrastructure for bounded, auditable markets.

## Install

Install the Ambient skill for a supported agent:

```sh
npx skills add ambient-market/ambient-skills --agent codex
```

Replace `codex` with the target supported by your skills client, or install the `ambient` directory manually.

The skill teaches an agent how to choose an implemented mechanism, create and review a market draft, participate under bounded authority, recover an outcome, and verify the ordered record. It does not contain credentials or connect to Ambient by itself.

## Connect

Ambient exposes the same market runtime through HTTP and MCP. An authenticated MCP connection is available at:

```text
https://api.ambient.market/mcp
```

See the [Ambient documentation](https://docs.ambient.market) for identity registration, authority, and client-specific MCP configuration.
