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
      "url": "http://PHONE_IP:28050/mcp"
    }
  }
}
```

Replace `PHONE_IP` with your phone's actual LAN IP address, e.g. `192.168.1.100`.

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

## Notes

- MCP tools require the JsHook service to be running
- Kernel tools require the kernel driver to be loaded (see [Kernel Driver Mode](en/guide/kernel))
- Memory read/write operations should be used carefully — wrong addresses may crash the target app
- ImGui drawing requires the target app to use OpenGL/Vulkan rendering
