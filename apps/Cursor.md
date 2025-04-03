# Cursor Application

## Overview

Cursor is an AI-powered code editor designed to enhance developer productivity with features like autocomplete, inline code suggestions, and AI-assisted debugging. It is built as a wrapper around VS Code, meaning the UI and experience are identical to VS Code.
![[Pasted image 20250403203703.png]]
## Features

- **AI Code Completion**: Context-aware code suggestions for faster development.
    
- **Inline Chat & Editing**: AI can explain, refactor, and improve code directly in the editor.
    
- **Multi-file Context**: Understands and references multiple files for better assistance.
    
- **Command Palette AI**: Natural language commands for quick navigation and actions.
    
- **AI Debugging**: Detects and suggests fixes for errors in real time.
    
- **Customizable AI Behavior**: Fine-tune AI suggestions and responses.
    
- **VS Code Settings Import**: Easily import your existing VS Code settings, extensions, and keybindings.
    

## Installation

### Windows / macOS / Linux

1. Visit [Cursor's website](https://www.cursor.com/) and download the appropriate version.
    
2. Install the application by following on-screen instructions.
    
3. Launch Cursor and configure settings as needed.
    

## Usage

### Getting Started

- Open a project folder to enable multi-file context.
    
- Start coding, and AI suggestions will appear automatically.
    
- Use `Cmd + K` (Mac) or `Ctrl + K` (Windows/Linux) to access the AI command palette.
    

### AI Commands

- `Explain`: Provides an explanation of selected code.
    
- `Refactor`: Suggests improvements and restructuring.
    
- `Generate`: Creates functions or components based on prompts.
    

### Debugging

- Highlight an error and ask the AI for suggestions.
    
- AI suggests potential fixes and explanations.
    

## Special Features

### Privacy Mode

- If enabled, none of your code will be stored.
    
- If disabled, Cursor may save prompts and collect telemetry data.
    

### Cursor Tabs

- A powerful CodePilot replacement that can suggest changes across multiple lines.
    

### Web Search Tools

- Allows AI to pull in external information to enhance its responses.
    

### Play Sound on Finish

- Plays a notification sound when a task is completed.
    

### Docs

- Allows users to paste URL links so that the AI can use and reference them when generating responses.
    

## Model Names

Users can add new models to Cursor, often to configure the latest OpenAI models or OpenRouter models:

- **claude-3-opus**
    
- **claude-3.5-haiku**
    
- **claude-3.5-sonnet**
    
- **claude-3.7-sonnet**
    
- **claude-3.7-sonnet-max**
    
- **cursor-fast**
    
- **cursor-small**
    
- **deepseek-r1**
    
- **deepseek-v3**
    
- **gemini-2.0-flash**
    
- **gemini-2.0-pro-exp**
    
- **gemini-2.5-pro-exp-03-25**
    
- **gemini-2.5-pro-max**
    
- **gpt-3.5-turbo**
    
- **gpt-4**
    
- **gpt-4-turbo-2024-04-09**
    
- **gpt-4.5-preview**
    
- **gpt-40**
    
- **gpt-40-mini**
    
- **grok-2**
    
- **01**
    
- **01-mini**
    
- **01-preview**
    
- **03-mini**
    
- **+ Add model**
    

## Rules

Rules provide more context to AI models to help them follow your personal preferences and operate more efficiently in your codebase.

### User Rules

These preferences get sent to the AI on all chats, composers, and Ctrl-K sessions.

- Example: Keep comments simple, concise, and in lowercase.
    

### Project Rules

- **+ Add new rule**
    
- Project-specific rules help the AI understand your codebase and follow your project's conventions.
    
- They can be automatically included or fetched by an agent.
    
- These rules are synced with your codebase.
    
- **Include .cursorrules file**: If disabled, Cursor will not include the `.cursorrules` file in your requests.
    

## Integration

- Supports GitHub Copilot and OpenAI APIs.
    
- Works with popular languages like Python, JavaScript, TypeScript, Go, Rust, and more.
    
- Integrates with VS Code extensions.
    

## Pricing

Cursor offers a free plan with basic AI features and a pro plan with extended capabilities.

## Resources

- [Official Website](https://www.cursor.com/)
    
- [Documentation](https://docs.cursor.com/)
    
- [Community Discord](https://discord.gg/cursor)
    

---

**Tags:** #Cursor #AI #CodeEditor #DeveloperTools #VSCode