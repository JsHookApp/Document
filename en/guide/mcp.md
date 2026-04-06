# MCP Tools Usage Guide

JsHook has a built-in MCP (Model Context Protocol) server that allows AI tools like VS Code Copilot to interact directly with target applications.

## Prerequisites

1. Phone is rooted with JsHook installed
2. JsHook is activated and running
3. VS Code with GitHub Copilot extension installed on your computer
4. Phone and computer on the same LAN

## Enable MCP Service

1. Open JsHook app
2. Go to **Settings** → **MCP Service**
3. Enable the MCP service toggle
4. Note the displayed IP address and port number (default port `28050`)

## Connection Configuration

Make sure the phone and computer are on the same LAN. Add MCP server configuration in `.vscode/mcp.json` or VS Code user settings:

```json
{
  "servers": {
    "jshook": {
      "type": "http",
      "url": "http://PHONE_IP:28050/mcp",
      "headers": {
        "X-Api-Key": "YOUR_API_KEY"
      }
    }
  }
}
```

Replace `PHONE_IP` with your phone's actual LAN IP address, e.g. `192.168.1.100`.

### API Key Authentication

When the MCP service starts, an API Key is automatically generated to verify client authenticity. All requests must include the `X-Api-Key` header to pass validation.

**Getting your API Key:**
- Tap the MCP service connection info button — the dialog shows the API Key and the complete VS Code configuration (with the key already included)
- Simply copy the configuration to use it

> ⚠️ The API Key is generated on first launch and persisted. Keep it safe and do not share it with untrusted parties.

## Available Tools

### Device Info
| Tool | Description |
|------|-------------|
| `device_info` | Get device info (model, OS version, screen resolution) |

### Process Management
| Tool | Description |
|------|-------------|
| `process_list` | List all running processes |
| `process_find` | Find process by name |
| `process_info` | Get detailed process information |
| `set_target` | Set target process (subsequent operations default to this process) |

### Modules & Memory Maps
| Tool | Description |
|------|-------------|
| `module_list` | List all loaded modules in target process |
| `module_base` | Get base address of a specific module |
| `maps_list` | List process memory maps |
| `maps_find` | Search memory maps by name |

### Memory Read/Write
| Tool | Description |
|------|-------------|
| `mem_read_int32` | Read 32-bit integer |
| `mem_read_int64` | Read 64-bit integer |
| `mem_read_float` | Read single-precision float |
| `mem_read_double` | Read double-precision float |
| `mem_read_bytes` | Read specified number of bytes |
| `mem_read_string` | Read string |
| `mem_read_pointer_chain` | Read via pointer chain (multi-level offsets) |
| `mem_write_int32` | Write 32-bit integer |
| `mem_write_int64` | Write 64-bit integer |
| `mem_write_float` | Write single-precision float |
| `mem_write_double` | Write double-precision float |
| `mem_write_bytes` | Write byte array |

### Search & Dump
| Tool | Description |
|------|-------------|
| `scan_pattern` | Memory pattern scan |
| `memory_dump` | Dump specified memory region |
| `mem_scan` | General memory value search (like Cheat Engine first scan) |
| `mem_scan_filter` | Filter scan results (like Cheat Engine Next Scan) |
| `mem_scan_reset` | Reset/clear scan session |
| `mem_scan_list` | List all active scan sessions |

### Memory Freeze
| Tool | Description |
|------|-------------|
| `mem_freeze` | Freeze memory value (background thread keeps writing) |
| `mem_freeze_list` | List all currently frozen memory addresses |
| `mem_unfreeze` | Unfreeze memory value |

### ImGui Drawing
| Tool | Description |
|------|-------------|
| `imgui_draw_text` | Draw text on screen |
| `imgui_draw_line` | Draw a line |
| `imgui_draw_rect` | Draw a rectangle |
| `imgui_draw_circle` | Draw a circle |
| `imgui_clear` | Clear all drawings |
| `imgui_status` | Query ImGui rendering status |

### Kernel Driver
| Tool | Description |
|------|-------------|
| `kernel_status` | Query kernel driver status |
| `kernel_get_module_base` | Get module base address via kernel |
| `kernel_read_int32` / `int64` / `float` / `double` / `bytes` | Kernel-level memory read |
| `kernel_write_int32` / `int64` / `float` / `double` / `bytes` | Kernel-level memory write |

### Frida MCP Mode (Remote Script Execution)

> Requires enabling **MCP Mode** in the app injection configuration, with FridaMod as the injection framework.

| Tool | Description |
|------|-------------|
| `frida_list_targets` | List target apps with FridaMod injected and MCP mode enabled |
| `frida_execute` | Execute Frida JS script in the target app |
| `frida_unload` | Unload the running script in the target app |
| `frida_read_log` | Read target app runtime logs (console.log output) |
| `frida_save_script` | Save script to JsHook's script directory |

### Other
| Tool | Description |
|------|-------------|
| `shell_exec` | Execute shell commands on the device |

## Usage Examples

In VS Code Copilot Chat, describe your needs in natural language:

```
List all running processes on the phone
```

```
Set target process to com.example.game, read libil2cpp.so base address
```

```
Read a float value at base address + 0x1234
```

```
Draw red text "Health: 100" at screen coordinates (500, 300)
```

### MCP Mode Examples

#### Auto-Discover Target Apps

With MCP Mode enabled, you don't need to manually specify the target process. AI can automatically discover target apps that have FridaMod injected with MCP mode enabled via the `frida_list_targets` tool:

```
Which target app is currently injected?
```

AI will automatically call `frida_list_targets` to query the list of injected apps, then you can choose the target app for further operations. This approach is more convenient than manually using `set_target` to set the target process, since FridaMod is already injected into the target app and AI can directly execute Frida scripts on it.

```
Check which apps are currently injected, then run a simple test script on the first one
```

#### Manually Specify Target App

If you need to operate on a specific app, you can also directly specify the package name:

```
Execute in com.example.game: Java.perform(function(){ var Activity = Java.use('android.app.Activity'); console.log('Activity loaded'); })
```

```
Read the recent runtime logs for com.example.game
```

```
Save this script as hook_activity.js to com.example.game's script directory
```

## MCP Mode

MCP Mode is an advanced JsHook feature that allows AI to remotely execute Frida scripts via MCP tools.

### Enabling MCP Mode

1. Select the target app in JsHook
2. Open the app injection configuration
3. Ensure the injection framework is set to **FridaMod**
4. Enable the **MCP Mode** toggle
5. Launch the target app

When MCP Mode is enabled, JsHook will not inject user scripts. Instead, it waits for AI to send scripts via MCP tools.

### How It Works

```
AI (VS Code Copilot)
    ↓ MCP HTTP Request
JsHook Daemon (MCP Server, port 28050)
    ↓ Unix Domain Socket
FridaMod (injected in target app)
    ↓ GumScript eval
Frida JS Execution → Return Result
```

1. AI calls the `frida_execute` tool, sending JS code
2. Daemon connects to FridaMod in the target app via Unix domain socket
3. FridaMod executes the code in Frida GumScript
4. Results are returned back to AI through the same path

### Typical Workflow

1. **Write & Execute** → `frida_execute` to run Frida scripts
2. **Check Logs** → `frida_read_log` to view console.log output
3. **Iterate & Debug** → Adjust scripts based on logs, re-execute
4. **Save Script** → `frida_save_script` to save completed scripts to the device

## Notes

- MCP tools require the JsHook service to be running
- Kernel tools require the kernel driver to be loaded (see [Kernel Driver Mode](en/guide/kernel))
- Memory read/write operations should be used carefully — wrong addresses may crash the target app
- ImGui drawing requires the target app to use OpenGL/Vulkan rendering
- MCP Mode requires the FridaMod framework, with a 30-second timeout for script execution
- Code executed via `frida_execute` runs in Frida global scope with access to Java.perform, Interceptor, and all Frida APIs
