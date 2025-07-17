[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/hannesrudolph-sqlite-explorer-fastmcp-mcp-server-badge.png)](https://mseep.ai/app/hannesrudolph-sqlite-explorer-fastmcp-mcp-server)

# SQLite Explorer MCP Server

An MCP server that provides safe, read-only access to SQLite databases through Model Context Protocol (MCP). This server is built with the FastMCP framework, which enables LLMs to explore and query SQLite databases with built-in safety features and query validation.

## 📋 System Requirements

- Python 3.6+
- SQLite database file (path specified via environment variable)

## 📦 Dependencies

Install all required dependencies:

```bash
# Using pip
pip install -r requirements.txt
```

### Required Packages
- **fastmcp**: Framework for building Model Context Protocol servers

All dependencies are specified in `requirements.txt` for easy installation.

## 📑 Table of Contents
- [System Requirements](#-system-requirements)
- [Dependencies](#-dependencies)
- [MCP Tools](#%EF%B8%8F-mcp-tools)
- [Getting Started](#-getting-started)
- [Installation Options](#-installation-options)
  - [Claude Desktop](#option-1-install-for-claude-desktop)
  - [Cline VSCode Plugin](#option-2-install-for-cline-vscode-plugin)
- [Safety Features](#-safety-features)
- [Development Documentation](#-development-documentation)
- [Environment Variables](#%EF%B8%8F-environment-variables)

## 🛠️ MCP Tools

The server exposes the following tools to LLMs:

### read_query
Execute a SELECT query on the database with built-in safety validations. Features:
- Query validation and sanitization
- Parameter binding support
- Row limit enforcement
- Results formatted as dictionaries

### list_tables 
List all available tables in the database with their names.

### describe_table
Get detailed schema information for a specific table, including:
- Column names and types
- NULL constraints
- Default values
- Primary key information

## 🚀 Getting Started

Clone the repository:

```bash
git clone https://github.com/hannesrudolph/sqlite-explorer-fastmcp-mcp-server.git
cd sqlite-explorer-fastmcp-mcp-server
```

## 📦 Installation Options

You can install this MCP server in either Claude Desktop or the Cline VSCode plugin. Choose the option that best suits your needs.

### Option 1: Install for Claude Desktop

Install using FastMCP:

```bash
fastmcp install sqlite_explorer.py --name "SQLite Explorer" -e SQLITE_DB_PATH=/path/to/db
```

Replace `/path/to/db` with the path to your SQLite database file.

### Option 2: Install for Cline VSCode Plugin

To use this server with the [Cline VSCode plugin](http://cline.bot):

1. In VSCode, click the server icon (☰) in the Cline plugin sidebar
2. Click the "Edit MCP Settings" button (✎)
3. Add the following configuration to the settings file:

```json
{
  "sqlite-explorer": {
    "command": "uv",
    "args": [
      "run",
      "--with",
      "fastmcp",
      "--with",
      "uvicorn",
      "fastmcp",
      "run",
      "/path/to/repo/sqlite_explorer.py"
    ],
    "env": {
      "SQLITE_DB_PATH": "/path/to/your/database.db"
    }
  }
}
```

Replace:
- `/path/to/repo` with the full path to where you cloned this repository (e.g., `/Users/username/Projects/sqlite-explorer-fastmcp-mcp-server`)
- `/path/to/your/database.db` with the full path to your SQLite database file

## 🔒 Safety Features

- Read-only access to SQLite databases
- Query validation and sanitization
- Parameter binding for safe query execution
- Row limit enforcement
- Progress output suppression for clean JSON responses

## 📚 Development Documentation

The repository includes documentation files for development:

- `mcp-documentation.txt`: Contains comprehensive documentation about the MCP server implementation and FastMCP framework usage.

This documentation serves as context when developing features and can be used with LLMs to assist in development.

## ⚙️ Environment Variables

The following environment variables must be set:

- `SQLITE_DB_PATH`: Full path to the SQLite database file you want to explore
