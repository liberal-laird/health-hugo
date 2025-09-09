# Hugo文章多语言翻译工具

这个工具可以将英文的Hugo文章自动翻译成多种语言，支持中文、法语、日语、西班牙语等9种语言。

## 功能特点

- 🌍 支持9种语言：中文、法语、西班牙语、德语、日语、韩语、意大利语、葡萄牙语、俄语
- 📝 保持Markdown格式和frontmatter结构
- 🏥 专业的医学术语翻译
- 🔄 批量处理多个文件
- ⚡ 使用LM Studio本地API，快速高效
- 🎯 支持指定文件或语言进行翻译

## 文件说明

- `translate_multi_languages.py` - 主要的多语言翻译脚本
- `run_multi_translation.sh` - 便于使用的启动脚本
- `example_usage.py` - 使用示例
- `config.py` - 配置文件（已更新支持多语言）

## 使用方法

### 1. 基本使用

```bash
# 翻译所有文件到所有语言（中文、法语、日语、西班牙语）
./run_multi_translation.sh

# 或者直接使用Python脚本
uv run python translate_multi_languages.py
```

### 2. 指定目标语言

```bash
# 只翻译到中文和法语
./run_multi_translation.sh chinese french

# 只翻译到日语
./run_multi_translation.sh japanese
```

### 3. 指定文件

```bash
# 只翻译指定文件到所有语言
./run_multi_translation.sh file1.md file2.md

# 翻译指定文件到指定语言
uv run  translate_multi_languages.py Zinc.md chinese
```

### 4. 支持的语言

- `chinese` - 中文
- `french` - 法语
- `spanish` - 西班牙语
- `german` - 德语
- `japanese` - 日语
- `korean` - 韩语
- `italian` - 意大利语
- `portuguese` - 葡萄牙语
- `russian` - 俄语

## 输出目录结构

翻译后的文件将保存在以下目录中：

```
../content/
├── english/          # 源文件（英文）
├── chinese/          # 中文翻译
├── french/           # 法语翻译
├── japanese/         # 日语翻译
├── spanish/          # 西班牙语翻译
└── ...              # 其他语言
```

## 配置说明

### 语言特定配置

每种语言都有特定的配置参数：

- **块大小**：根据语言特点优化的文本块大小
- **温度参数**：控制翻译的创造性
- **特殊指令**：针对语言特点的翻译要求

### 示例配置

```python
LANGUAGE_CONFIGS = {
    "chinese": {
        "name": "中文",
        "chunk_size": 3000,
        "temperature": 0.2,
        "special_instructions": "使用简体中文，保持医学术语的准确性"
    },
    "french": {
        "name": "法语",
        "chunk_size": 2800,
        "temperature": 0.3,
        "special_instructions": "使用标准法语，注意法语语法和医学术语"
    },
    # ... 其他语言配置
}
```

## 前置要求

1. **LM Studio**：需要运行LM Studio并加载模型
2. **Python环境**：使用uv管理Python环境
3. **依赖包**：requests, pyyaml

## 安装和设置

1. 确保LM Studio正在运行并加载了模型
2. 安装依赖：
   ```bash
   uv pip install -r requirements.txt
   ```
3. 运行脚本：
   ```bash
   ./run_multi_translation.sh
   ```

## 使用示例

### 示例1：翻译所有文件

```python
from translate_multi_languages import MultiLanguageTranslator

# 创建翻译器
translator = MultiLanguageTranslator()

# 开始翻译
translator.translate_all_languages()
```

### 示例2：指定语言

```python
# 只翻译到中文和法语
translator = MultiLanguageTranslator(target_languages=['chinese', 'french'])
translator.translate_all_languages()
```

### 示例3：指定文件

```python
# 只翻译特定文件
translator = MultiLanguageTranslator()
translator.translate_all_languages(specific_files=['example.md', 'another.md'])
```

## 注意事项

1. **LM Studio连接**：确保LM Studio正在运行并监听端口1234
2. **模型推荐**：建议使用`openai/gpt-oss-20b`模型以获得最佳翻译效果
3. **内存要求**：确保有足够的内存运行模型
4. **翻译质量**：医学术语翻译需要专业模型，建议使用专门的医学翻译模型

## 故障排除

### 连接问题
- 检查LM Studio是否正在运行
- 确认端口1234是否可用
- 验证模型是否正确加载

### 翻译质量问题
- 检查模型是否为医学专业模型
- 调整温度参数
- 检查语言特定配置

### 性能问题
- 减少并发请求数
- 调整块大小
- 增加延迟时间

## 更新日志

- **v1.0** - 初始版本，支持基本多语言翻译
- **v1.1** - 添加语言特定配置
- **v1.2** - 优化批量处理性能
