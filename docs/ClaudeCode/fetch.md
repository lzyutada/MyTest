# Fetch

## 问题与解决办法(方案)

### **Unable to verify if domain**

fetch时提示错误：
```
Fetch(https://huggingface.co/microsoft/VibeVoice-Realtime-0.5B)
  ⎿  Error: Unable to verify if domain huggingface.co is safe to fetch. This may be due to network restrictions or enterprise security policies blocking claude.ai.
```

- ** 解决办法 **
需改配置文件：`.claude/settings.json`
```
{
    "env": {
        "ANTHROPIC_AUTH_TOKEN": "your-token",
        "ANTHROPIC_BASE_URL": "https://coding.dashscope.aliyuncs.com/apps/anthropic",
        "ANTHROPIC_MODEL": "qwen3.5-plus",
        "ANTHROPIC_SMALL_FAST_MODEL": "glm-4.7"
    },
    "skipWebFetchPreflight": true
}
```

- 参考：`https://zhuanlan.zhihu.com/p/2012819798686454483`