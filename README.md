# blender-ai-copilot-hub

**A multi-provider AI copilot hub for Blender—bring OpenAI, Anthropic Claude, Google Gemini, OpenRouter, OpenCode Zen, Ollama and custom endpoints into one hub of saved connections, with 27 supervised scene tools and a built-in MCP server.**

[download-url]: https://github.com/baiblinocun1986/blender-ai-copilot-hub/releases

[![License](https://img.shields.io/badge/license-MIT-blue)] ![Language](https://img.shields.io/badge/language-Python-3776AB?logo=python&logoColor=white) ![Platform](https://img.shields.io/badge/platform-Windows%20x64-0078D6?logo=windows&logoColor=white) ![Blender](https://img.shields.io/badge/Blender-4.2%2B-E87D0D?logo=blender&logoColor=white) ![MCP](https://img.shields.io/badge/Model_Context_Protocol-MCP-5E5CE6) ![Release](https://img.shields.io/badge/release-1.0.0-98D85B) ![Providers](https://img.shields.io/badge/providers-OpenAI%20%7C%20Claude%20%7C%20Gemini%20%7C%20Ollama-7C3AED)

[![Download](docs/download-button.svg)][download-url]

Every model you already use, one panel away: pick a saved connection, load its live catalog, and put the copilot to work on your scene.

## Why

You pay for several AI providers, yet most tools lock you into one—and re-typing API keys into yet another app is the last thing a scene deadline needs. blender-ai-copilot-hub keeps every provider in one Blender-side hub: saved connection profiles for work and personal keys, live model catalogs, and a copilot that inspects your scene before it acts. Switch models per brief instead of per subscription, and keep the iteration speed inside Blender where the scene lives.

## Without / With

| Without | With |
|---|---|
| Re-entering API keys in every new tool | Saved connection profiles for work and personal accounts side by side |
| One vendor's model forced onto every task | The right model for each brief—cloud, local or custom endpoint |
| Chatting in a browser, rebuilding by hand in Blender | A copilot that lives in the Blender sidebar and edits the scene directly |
| Guessing which model can act, not just talk | Live catalogs with tool-calling models ready to pick |
| No fallback when a provider is busy | Switch profiles mid-session without losing your flow |
| External tools locked out of your scene | A built-in authenticated MCP endpoint for compatible clients |

## Quick Start

Each command below is self-contained: open PowerShell, copy it, paste it and press Enter.

1. Grab the release ZIP `blender-ai-copilot-hub.zip` from [Download][download-url] and save it to your Windows machine.
2. Check which Blender build a standard Windows setup has, then in Blender open **Edit → Preferences → Get Extensions → the ⋮ menu → Install from Disk**.
   `powershell Get-ChildItem $env:ProgramFiles\Blender*\Blender*\blender.exe`
3. Select the ZIP, enable **blender-ai-copilot-hub**, and open the panel **3D Viewport → N → Copilot Hub**; the command opens your Downloads folder so the ZIP is at hand.
   `powershell Invoke-Item $env:USERPROFILE\Downloads`
4. Add a provider connection—OpenAI, Anthropic Claude, Google Gemini, OpenRouter, OpenCode Zen, Ollama or a custom API—then load the catalog and select a tool-calling model; the command checks a local Ollama server when that is your provider.
   `powershell Invoke-RestMethod http://localhost:11434/api/tags`
5. Send your first message in Blender or click **Open Studio Window**; the command confirms Blender is running.
   `powershell Get-Process blender`
6. Runtime profile: Windows x64 with Blender 4.2 or later, Blender kept open during use; when the built-in MCP server is enabled, the command confirms its local endpoint.
   `powershell Test-NetConnection 127.0.0.1 -Port 9876`

## Features

- Connect every provider you use—OpenAI, Anthropic Claude, Google Gemini, OpenRouter, OpenCode Zen, Ollama and custom endpoints in one panel.
- Switch between saved connection profiles without re-entering keys—work and personal accounts live side by side.
- Load live model catalogs and pick models with tool-calling support, or enter a model ID manually.
- Inspect the scene before acting—objects, structure and materials are read before any edit.
- Run quick edits with a single assistant or hand larger briefs to an agent team chain.
- Serve external clients through an authenticated local MCP endpoint.
- Stay in control—per-operation approvals, cancellation after the current step and named undo steps.

## How it works

blender-ai-copilot-hub runs inside Blender: your saved provider connections feed a copilot that reads the scene through 27 supervised tools and applies each brief as ordered, approved operations, while the Studio window shows the chat, scene objects, viewport snapshots and the task board. The same toolset is exposed to OpenCode and other compatible clients through a local authenticated endpoint (`http://127.0.0.1:9876/mcp`).

## Usage

**The right model per brief.** Keep a fast cloud model for quick edits and a local Ollama model for offline evenings—both as saved profiles in the hub, one click apart.

**A product display in one sentence.** Ask: "Inspect this scene, then build a product display with a pedestal, a camera and three lights—matte blue on the pedestal." The copilot reads the scene, builds the layout and returns a viewport snapshot.

**Custom endpoints included.** Point the hub at your OpenAI-compatible or Anthropic-compatible service, load the catalog, and work exactly as with a public provider.

## Configuration

| Setting | Default | What it does |
|---|---|---|
| Provider | OpenAI | OpenAI, Anthropic Claude, Google Gemini, OpenRouter, OpenCode Zen, Ollama or Custom API |
| Connection profiles | One per provider | Save multiple keys and accounts per provider and switch anytime |
| API protocol | OpenAI Chat Completions | Custom-endpoint protocol: OpenAI Chat Completions, Anthropic Messages or Ollama |
| Base URL | — | Custom-endpoint base URL (for example `https://your-service.example/v1`), not a full completion endpoint |
| Model | Provider catalog | Pick a tool-calling model; enter the model ID manually when the catalog does not load |
| MCP endpoint | `http://127.0.0.1:9876/mcp` | Local Streamable HTTP endpoint for external MCP clients; enable it in the extension preferences |
| Access token | Generated when enabled | Bearer token for the MCP endpoint; keep it in the client's secret store |
| Workflow mode | Single assistant | Single assistant or a Team chain with one manager, workers and reviewers |
| Interface language | English | English, German, French, Spanish or Chinese for the main interface |
| Asset services | Optional keys | Service keys for asset providers that require them |

## Troubleshooting / FAQ

**Where are my keys stored?** In your Blender user settings on your machine—never in the scene file—and Studio authenticates every request locally.

**The custom API catalog is empty.** Use the provider's base URL rather than a full completion endpoint, pick the matching protocol, and enter the model ID manually if the catalog still does not load.

**The model chats but does not edit.** Copilot actions are tool calls—switch to a model that supports tool calling and reload the catalog.

**Can I keep two keys for the same provider?** Yes—save them as separate connection profiles and switch between them.

**How do I connect an external MCP client?** Enable the MCP server in the extension preferences and configure the client with the local endpoint plus an `Authorization: Bearer` header.

## Contributing

Found a bug or want another provider supported? Open an issue with the steps to reproduce, or send a pull request. If blender-ai-copilot-hub saves you subscription-hopping, a star helps others find it.

## Keywords

blender-ai-copilot-hub · blender · blender 3d · blender addon · blender plugin · blender extension · blender scripting · blender automation · blender mcp · blender ai · blender assistant · blender copilot · blender chatgpt · blender llm · blender agents · bpy · 3d modeling · 3d automation · mcp · mcp server · model context protocol · ai for blender · multi provider ai · model catalog · connection profiles · api key manager · local llm · ollama · openai · anthropic claude · google gemini · openrouter · opencode zen · custom api · scene tools · scene generation · scene inspection · ai modeling · ai materials · viewport screenshot · studio workspace · task board · agent teams · product visualization · geometry nodes · 3d workflow · 3d rendering · windows 3d · ai 3d · poly haven · sketchfab · asset search · blender workflow · chat in blender · ai chat blender

## License

Released under the [MIT](./LICENSE) license.
