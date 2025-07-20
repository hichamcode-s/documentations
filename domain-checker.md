# 🌐 Domain Availability Checker API

**Check domain availability across multiple TLDs with a single API call**

## ✨ Features

- 🔍 **Real-time availability checking** using WHOIS data
- 🌍 **Multi-TLD support** (.com, .net, .io, .org, and more)
- 📦 **Bulk domain checking** in one request
- ✅ **Automatic validation** of domain formats
- ⚡ **Fast responses** (1-3 seconds)
- 🛡️ **Error handling** with clear messages

## 🚀 Quick Start

### API Endpoint
```
POST /api/domain-availability
```

### Request
```json
{
  "domains": ["mywebsite", "testdomain"],
  "tlds": ["com", "net", "io"]
}
```

### Response
```json
{
  "mywebsite": {
    "com": "available",
    "net": "taken",
    "io": "available"
  },
  "testdomain": {
    "com": "taken",
    "net": "available",
    "io": "taken"
  }
}
```

## 📋 Response Status
-------------------------------------------------
| Status      | Description                      |
|-------------|--------------------------------- |
| `available` | ✅ Domain is free to register    |
| `taken`     | ❌ Domain is already registered  |
| `invalid`   | ⚠️ Domain format is invalid      |
| `error`     | 🔧 Lookup failed                 |
-------------------------------------------------