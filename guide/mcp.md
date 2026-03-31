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

### Frida MCP 模式（远程脚本执行）

> 需要在应用注入配置中开启 **MCP 模式**，且注入框架必须是 FridaMod。

| 工具名 | 功能 |
|--------|------|
| `frida_execute` | 在目标应用中执行 Frida JS 脚本 |
| `frida_unload` | 卸载目标应用中正在执行的脚本 |
| `frida_read_log` | 读取目标应用的运行日志 (console.log 输出) |
| `frida_save_script` | 将脚本保存到 JsHook 的脚本目录 |
| `frida_api_info` | 获取 JsHook Frida 扩展 API 文档 |

### ESP 分析与渲染
| 工具名 | 功能 |
|--------|------|
| `scan_vp_matrix` | 扫描 VP 矩阵候选地址 |
| `scan_entity_array` | 扫描实体数组候选地址 |
| `validate_matrix` | 验证矩阵数据有效性 |
| `world_to_screen` | 世界坐标转屏幕坐标 |
| `mem_read_float_array` | 批量读取浮点数组 |
| `mem_diff_region` | 内存区域变化对比 |
| `esp_start` | 启动 ESP 渲染 |
| `esp_stop` | 停止 ESP 渲染 |
| `esp_status` | 查询 ESP 运行状态 |
| `esp_update` | 更新 ESP 渲染配置 |

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

### MCP 模式示例

```
查看 frida 扩展 API 文档
```

```
在 com.example.game 中执行: Java.perform(function(){ var Activity = Java.use('android.app.Activity'); console.log('Activity loaded'); })
```

```
读取 com.example.game 最近的运行日志
```

```
将这个脚本保存为 hook_activity.js 到 com.example.game 的脚本目录
```

## MCP 模式

MCP 模式是 JsHook 的高级功能，允许 AI 通过 MCP 工具远程执行 Frida 脚本。

### 开启 MCP 模式

1. 在 JsHook 中选择目标应用
2. 进入应用注入配置
3. 确保注入框架选择 **FridaMod**
4. 开启 **MCP 模式** 开关
5. 启动目标应用

开启 MCP 模式后，JsHook 不会注入用户脚本，而是等待 AI 通过 MCP 工具下发脚本执行。

### 工作原理

```
AI (VS Code Copilot)
    ↓ MCP HTTP 请求
JsHook Daemon (MCP Server, 端口 28050)
    ↓ Unix Domain Socket
FridaMod (注入在目标应用中)
    ↓ GumScript eval
Frida JS 执行 → 返回结果
```

1. AI 调用 `frida_execute` 工具，发送 JS 代码
2. Daemon 通过 Unix 域 socket 连接到注入在目标应用中的 FridaMod
3. FridaMod 在 Frida GumScript 中执行代码
4. 执行结果原路返回给 AI

### 典型工作流

1. **查看 API** → `frida_api_info` 了解可用的扩展 API
2. **编写执行** → `frida_execute` 执行 Frida 脚本
3. **查看日志** → `frida_read_log` 查看 console.log 输出
4. **迭代调试** → 根据日志调整脚本，重复执行
5. **保存脚本** → `frida_save_script` 将完成的脚本保存到设备

## 注意事项

- MCP 工具需要 JsHook 服务持续运行
- 内核相关工具需要加载内核驱动（参见 [内核驱动模式](guide/kernel)）
- 内存读写操作应谨慎，错误的地址可能导致目标应用崩溃
- ImGui 绘制需要目标应用使用 OpenGL/Vulkan 渲染
- MCP 模式需要 FridaMod 框架，且脚本执行有 30 秒超时限制
- `frida_execute` 执行的代码在 Frida 全局作用域，可使用 Java.perform、Interceptor 等所有 Frida API
- ESP 分析工具需要设置目标进程后使用
