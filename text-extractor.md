# 📸 Text Extractor API

**Extract text from images using advanced OCR (Optical Character Recognition) technology**

## ✨ Features

- 🔍 **High-accuracy OCR** using Tesseract.js engine
- 🌍 **Multi-language support** (English, French, Spanish, German, and more)
- 📁 **Multiple image formats** (JPEG, PNG, GIF, BMP, TIFF)
- 📏 **Large file support** up to 10MB
- ⚡ **Fast processing** with real-time progress
- 🛡️ **Robust error handling** with detailed feedback
- 📊 **Confidence scoring** for extracted text quality

## 🚀 Quick Start

### API Endpoint
```
POST /text-extractor
```

## 📋 Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image` | File | ✅ | Image file to extract text from |
| `language` | String | ❌ | Language code for OCR (default: "eng") |


### Response
```json
{
  "success": true,
  "text": "Hello World! This is extracted text from the image.",
  "language": "eng",
  "confidence": 1
}
```


## 📋 Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `success` | Boolean | Whether the extraction was successful |
| `text` | String | Extracted text from the image |
| `language` | String | Language used for OCR |
| `confidence` | Number | Confidence score (0-1) |

## 🌍 Supported Languages

| Language Code | Language | Example |
|---------------|----------|---------|
| `eng` | English | "Hello World" |
| `fra` | French | "Bonjour le monde" |
| `spa` | Spanish | "Hola mundo" |
| `deu` | German | "Hallo Welt" |
| `ita` | Italian | "Ciao mondo" |
| `por` | Portuguese | "Olá mundo" |
| `rus` | Russian | "Привет мир" |
| `chi_sim` | Simplified Chinese | "你好世界" |
| `jpn` | Japanese | "こんにちは世界" |
| `kor` | Korean | "안녕하세요 세계" |

## 📁 Supported Image Formats

| Format | Extensions | Max Size |
|--------|------------|----------|
| JPEG | .jpg, .jpeg | 10MB |
| PNG | .png | 10MB |
| GIF | .gif | 10MB |
| BMP | .bmp | 10MB |
| TIFF | .tiff, .tif | 10MB |
