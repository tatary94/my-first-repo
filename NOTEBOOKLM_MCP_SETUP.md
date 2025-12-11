# NotebookLM MCP Server Setup Guide

This repository now includes the **NotebookLM MCP Server** - a powerful integration that lets Claude Code chat directly with NotebookLM for zero-hallucination answers based on your own notebooks.

## 🎉 What's Been Set Up

The NotebookLM MCP server has been successfully installed and configured in this repository:

- ✅ Repository cloned to: `/home/user/my-first-repo/notebooklm-mcp/`
- ✅ Dependencies installed and built
- ✅ Claude Code configured to use the MCP server
- ✅ Server tested and running successfully

## 📁 Repository Structure

```
my-first-repo/
├── notebooklm-mcp/          # MCP server repository
│   ├── dist/                 # Built TypeScript files
│   ├── src/                  # Source code
│   ├── docs/                 # Documentation
│   └── package.json
├── scripts/                  # Claude Code Skill scripts
├── SKILL.md                  # Skill instructions
└── NOTEBOOKLM_MCP_SETUP.md  # This file
```

## 🚀 Quick Start

### 1. First-Time Authentication

You need to authenticate with Google once to use NotebookLM:

```
"Log me in to NotebookLM"
```

A Chrome window will open for you to log in with your Google account. This is a one-time setup - your authentication will persist across sessions.

### 2. Create a NotebookLM Notebook

1. Go to [notebooklm.google.com](https://notebooklm.google.com)
2. Create a new notebook
3. Upload your documentation:
   - 📄 PDFs, Google Docs, markdown files
   - 🔗 Websites, GitHub repos
   - 🎥 YouTube videos
   - 📚 Multiple sources per notebook (up to 50)
4. Share your notebook:
   - Click **⚙️ Share**
   - Select **Anyone with link**
   - Copy the URL

### 3. Add Notebook to Your Library

Tell Claude:

```
"Add this NotebookLM to my library: [your-notebook-url]"
```

Claude will ask you for:
- A descriptive name
- Topics/tags
- What the notebook contains

### 4. Start Researching

Now you can ask Claude to query your notebooks:

```
"What does my React docs say about hooks?"
"Ask my API documentation about authentication"
"Research this in NotebookLM before coding"
```

Claude will automatically:
- Select the relevant notebook from your library
- Ask NotebookLM for information
- Build understanding through follow-up questions
- Use that knowledge to write accurate code

## 🛠️ Available MCP Tools

The server provides 16 tools (full profile):

### Core Tools
- **ask_question** - Query NotebookLM with context-aware follow-ups
- **setup_auth** - One-time Google authentication
- **get_health** - Check server status and authentication

### Library Management
- **add_notebook** - Add notebooks to your library with metadata
- **list_notebooks** - View all saved notebooks
- **get_notebook** - Get detailed notebook information
- **select_notebook** - Set default notebook
- **update_notebook** - Modify notebook metadata
- **remove_notebook** - Remove notebook from library
- **search_notebooks** - Find notebooks by topic/name
- **get_library_stats** - View library statistics

### Session Management
- **list_sessions** - View active research sessions
- **close_session** - End a specific session
- **reset_session** - Clear session history

### Maintenance
- **re_auth** - Switch Google accounts
- **cleanup_data** - Deep clean all MCP data

## 💡 Common Commands

| What to say | What happens |
|------------|--------------|
| *"Log me in to NotebookLM"* | Opens Chrome for authentication |
| *"Add [url] to my library"* | Saves notebook with metadata |
| *"Show my NotebookLM notebooks"* | Lists all saved notebooks |
| *"Research this in my docs"* | Multi-question session with NotebookLM |
| *"Use the [name] notebook"* | Sets active notebook |
| *"Show me the browser"* | Watch live NotebookLM chat |
| *"Re-authenticate with different account"* | Switch Google accounts |
| *"Clean up NotebookLM data"* | Fresh start (can preserve library) |

## 🎯 Why Use NotebookLM MCP?

### vs. Feeding Docs to Claude Directly
- **Problem**: Massive token consumption, variable retrieval quality
- **NotebookLM**: Pre-indexed by Gemini, minimal tokens

### vs. Web Search
- **Problem**: Outdated info, unreliable sources
- **NotebookLM**: Only your trusted docs, always current

### vs. Local RAG
- **Problem**: Hours of setup, tuning embeddings, still hallucinates
- **NotebookLM**: Upload docs → done. Zero hallucinations.

## 📊 Benefits

1. **Zero Hallucinations** - NotebookLM refuses to answer if info isn't in your docs
2. **Autonomous Research** - Claude asks follow-ups automatically
3. **Smart Library** - Save multiple notebooks with tags
4. **Deep Understanding** - Iterative Q&A builds complete knowledge
5. **Cross-Tool Sharing** - Works with Claude Code, Codex, Cursor

## 🔧 Configuration

### Server Configuration

The MCP server is configured in `/root/.claude.json`:

```json
{
  "mcpServers": {
    "notebooklm": {
      "command": "node",
      "args": ["/home/user/my-first-repo/notebooklm-mcp/dist/index.js"]
    }
  }
}
```

### Data Storage

All data is stored in: `/root/.local/share/notebooklm-mcp/`

- `library.json` - Your notebook library
- `chrome_profile/` - Browser authentication state
- Session data and chat history

### Environment Variables (Optional)

You can configure the server with environment variables:

```bash
# Tool profile (minimal, standard, full)
export NOTEBOOKLM_PROFILE=full

# Disable specific tools
export NOTEBOOKLM_DISABLED_TOOLS="cleanup_data,re_auth"

# Browser settings
export HEADLESS=true
export SHOW_BROWSER=false
```

## 🔍 Troubleshooting

### "Not authenticated" error
Run: `"Log me in to NotebookLM"`

### Browser crashes
Run: `"Clean up NotebookLM data"` and re-authenticate

### Rate limits (50 queries/day on free tier)
- Wait for reset
- Switch to different Google account with `"Re-authenticate"`

### Connection issues
Check server health: `"Check NotebookLM server health"`

## 📚 Additional Resources

- [NotebookLM MCP Documentation](./notebooklm-mcp/docs/)
- [Usage Guide](./notebooklm-mcp/docs/usage-guide.md)
- [Tool Reference](./notebooklm-mcp/docs/tools.md)
- [Troubleshooting](./notebooklm-mcp/docs/troubleshooting.md)
- [GitHub Repository](https://github.com/PleasePrompto/notebooklm-mcp)

## 🎓 Example Workflow

1. **Upload your docs** to NotebookLM (API docs, framework guides, etc.)
2. **Add to library**: `"Add [url] to my library tagged 'api, backend'"`
3. **Start building**: `"Build a user authentication system"`
4. **Claude automatically**:
   - Queries your API docs
   - Asks follow-up questions
   - Builds understanding
   - Writes accurate code
5. **No debugging** hallucinated APIs!

## 🔐 Security Notes

- Chrome runs locally - credentials never leave your machine
- Consider using a dedicated Google account for automation
- Authentication persists across sessions
- Data stored locally in `/root/.local/share/notebooklm-mcp/`

## 🎉 You're Ready!

The NotebookLM MCP server is now fully integrated with Claude Code. Start by:

1. Authenticating with Google
2. Creating a NotebookLM notebook with your docs
3. Adding it to your library
4. Asking Claude to research before coding

**Happy coding with zero hallucinations!** 🚀
