# gdbmcp

GDB MCP server.

## Overview
`gdbmcp` exposes GDB operations over the MCP (Model Context Protocol) using `FastMCP`. It manages GDB sessions over a socket connection (via `gdbrpc`) and provides MCP tools to connect, list, terminate sessions, and run GDB commands.

## Features
- Start and manage multiple GDB sessions
- Execute arbitrary GDB commands through MCP
- Run as MCP stdio server or HTTP server

## Requirements
- Python >= 3.10
- `gdbrpc`
- `mcp`
- **HTTP mode only**: `uvicorn` (required to run the HTTP server)

## Installation
From repo root:

```bash
pip install .
```

For development:

```bash
pip install -e .
```

## Usage

### Run MCP server (stdio)
```bash
gdbmcp --stdio
```

### Run MCP server (HTTP)
```bash
gdbmcp --port 20819
```

You can also run via module:

```bash
python -m gdbmcp --stdio
```

## MCP Tools

### `gdb_connect(host: Optional[str] = None, port: Optional[int] = None) -> str`
Establish a GDB session and returns a session ID.

### `gdb_terminate(session_id: str) -> str`
Terminate an existing session and clean up resources.

### `gdb_list_sessions() -> str`
List all active sessions and their host/port.

### `gdb_command(session_id: str, command: str) -> str`
Execute a GDB command in the session and return output.

## Configuration
CLI flags:
- `--stdio` : Run in stdio transport mode
- `--port` : HTTP server port (default: `20819`)
