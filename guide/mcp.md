# MCP 工具使用指南

JsHook 内置了 MCP（Model Context Protocol）服务器，可以通过 VS Code Copilot 等 AI 工具直接与目标应用进行交互。

## 前置条件

1. 手机已 root 并安装 JsHook
2. JsHook 已激活并运行
3. 电脑已安装 VS Code 和 GitHub Copilot 扩展
4. 手机与电脑处于同一局域网

## 启用 MCP 服务

1. 打开 JsHook 应用
2. 进入 **设置** → **MCP 服务**
3. 开启 MCP 服务开关
4. 记录显示的 IP 地址和端口号（默认端口 `28050`）

## 连接配置

确保手机和电脑在同一局域网内，在 VS Code 的 `.vscode/mcp.json` 或用户设置中添加 MCP 服务器配置：

```json
{
  "servers": {
    "jshook": {
      "type": "http",
      "url": "http://手机IP:28050/mcp"
    }
  }
}
```

将 `手机IP` 替换为手机在局域网中的实际 IP 地址，例如 `192.168.1.100`。

## 可用工具列表

### 设备信息
| 工具名 | 功能 |
|--------|------|
| `device_info` | 获取设备基本信息（型号、系统版本、屏幕分辨率） |

### 进程管理
| 工具名 | 功能 |
|--------|------|
| `process_list` | 列出所有运行进程 |
| `process_find` | 按名称查找进程 |
| `process_info` | 获取指定进程详细信息 |
| `set_target` | 设置目标进程（后续操作默认对该进程执行） |

### 模块与内存映射
| 工具名 | 功能 |
|--------|------|
| `module_list` | 列出目标进程加载的所有模块 |
| `module_base` | 获取指定模块基地址 |
| `maps_list` | 列出进程内存映射 |
| `maps_find` | 按名称搜索内存映射 |

### 内存读写
| 工具名 | 功能 |
|--------|------|
| `mem_read_int32` | 读取 32 位整数 |
| `mem_read_int64` | 读取 64 位整数 |
| `mem_read_float` | 读取单精度浮点数 |
| `mem_read_double` | 读取双精度浮点数 |
| `mem_read_bytes` | 读取指定长度字节 |
| `mem_read_string` | 读取字符串 |
| `mem_read_pointer_chain` | 按指针链读取（支持多级偏移） |
| `mem_write_int32` | 写入 32 位整数 |
| `mem_write_int64` | 写入 64 位整数 |
| `mem_write_float` | 写入单精度浮点数 |
| `mem_write_double` | 写入双精度浮点数 |
| `mem_write_bytes` | 写入字节数组 |

### 搜索与转储
| 工具名 | 功能 |
|--------|------|
| `scan_pattern` | 内存特征码搜索 |
| `memory_dump` | 转储指定内存区域 |

### ImGui 绘制
| 工具名 | 功能 |
|--------|------|
| `imgui_draw_text` | 在屏幕上绘制文字 |
| `imgui_draw_line` | 绘制线条 |
| `imgui_draw_rect` | 绘制矩形 |
| `imgui_draw_circle` | 绘制圆形 |
| `imgui_clear` | 清除所有绘制内容 |
| `imgui_status` | 查询 ImGui 渲染状态 |

### 内核驱动
| 工具名 | 功能 |
|--------|------|
| `kernel_status` | 查询内核驱动加载状态 |
| `kernel_get_module_base` | 通过内核获取模块基地址 |
| `kernel_read_int32` / `int64` / `float` / `double` / `bytes` | 内核级内存读取 |
| `kernel_write_int32` / `int64` / `float` / `double` / `bytes` | 内核级内存写入 |

### 其他
| 工具名 | 功能 |
|--------|------|
| `shell_exec` | 在设备上执行 shell 命令 |

## 使用示例

在 VS Code Copilot Chat 中，直接用自然语言描述需求即可：

```
请列出当前手机上运行的所有进程
```

```
设置目标进程为 com.example.game，读取 libil2cpp.so 基地址
```

```
在基地址 + 0x1234 处读取一个 float 值
```

```
在屏幕坐标 (500, 300) 处绘制红色文字 "Health: 100"
```

## 注意事项

- MCP 工具需要 JsHook 服务持续运行
- 内核相关工具需要加载内核驱动（参见 [内核驱动模式](guide/kernel)）
- 内存读写操作应谨慎，错误的地址可能导致目标应用崩溃
- ImGui 绘制需要目标应用使用 OpenGL/Vulkan 渲染
