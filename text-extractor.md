# 📸 Text Extractor API

**Extract text from images using advanced OCR (Optical Character Recognition) technology**

## ✨ Features

- 🔍 **High-accuracy OCR** using Tesseract.js engine
- 📸 **Multi-image processing** - Extract text from up to 10 images in one request
- 🌍 **Multi-language support** (English, French, Spanish, German, and more)
- 📁 **Multiple image formats** (JPEG, PNG, GIF, BMP, TIFF)
- 📏 **Large file support** up to 10MB per file
- ⚡ **Fast processing** with real-time progress
- 🛡️ **Robust error handling** with detailed feedback for each file
- 📊 **Confidence scoring** for extracted text quality
- 📋 **Ordered results** - Results returned in same order as uploaded files

## 🚀 Quick Start

### API Endpoint
```
POST /text-extractor
```

## 📋 Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `images` | File[] | ✅ | Array of image files to extract text from (max 10 files) |
| `language` | String | ❌ | Language code for OCR (default: "eng") |

### Request Examples

```bash
# Single image
curl -X POST http://localhost:3000/text-extractor \
  -F "images=@/path/to/your/image.jpg" \
  -F "language=eng"

# Multiple images
curl -X POST http://localhost:3000/text-extractor \
  -F "images=@/path/to/image1.jpg" \
  -F "images=@/path/to/image2.png" \
  -F "images=@/path/to/image3.jpg" \
  -F "language=eng"
```

### Response
```json
{
  "success": true,
  "total_files": 3,
  "results": [
    {
      "filename": "image1.jpg",
      "text": "Hello World! This is extracted text from the first image.",
      "language": "eng",
      "confidence": 1,
      "success": true
    },
    {
      "filename": "image2.png",
      "text": "Text from the second image.",
      "language": "eng",
      "confidence": 1,
      "success": true
    },
    {
      "filename": "image3.jpg",
      "text": "Text from the third image.",
      "language": "eng",
      "confidence": 1,
      "success": true
    }
  ]
}
```

## 📋 Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `success` | Boolean | Whether the overall request was successful |
| `total_files` | Number | Total number of files processed |
| `results` | Array | Array of extraction results for each file |

### Individual Result Fields

| Field | Type | Description |
|-------|------|-------------|
| `filename` | String | Original filename of the processed image |
| `text` | String | Extracted text from the image |
| `language` | String | Language used for OCR |
| `confidence` | Number | Confidence score (0-1) |
| `success` | Boolean | Whether extraction was successful for this file |
| `error` | String | Error message (if extraction failed) |

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
| JPEG | .jpg, .jpeg | 10MB per file |
| PNG | .png | 10MB per file |
| GIF | .gif | 10MB per file |
| BMP | .bmp | 10MB per file |
| TIFF | .tiff, .tif | 10MB per file |

**Note**: Maximum 10 files per request, 10MB per file

## 🔧 Error Responses

### No Images Provided
```json
{
  "error": "No image files provided",
  "success": false
}
```

### Invalid File Type
```json
{
  "error": "Only image files are allowed",
  "success": false
}
```

### File Too Large
```json
{
  "error": "File too large",
  "success": false
}
```

### Mixed Success/Failure Response
```json
{
  "success": true,
  "total_files": 3,
  "results": [
    {
      "filename": "image1.jpg",
      "text": "Successfully extracted text",
      "language": "eng",
      "confidence": 1,
      "success": true
    },
    {
      "filename": "image2.png",
      "text": "",
      "language": "eng",
      "confidence": 0,
      "success": false,
      "error": "Text extraction failed: No text found in image"
    },
    {
      "filename": "image3.jpg",
      "text": "Another successful extraction",
      "language": "eng",
      "confidence": 1,
      "success": true
    }
  ]
}
```

## 💡 Usage Examples

### JavaScript (Node.js)
```javascript
const FormData = require('form-data');
const fs = require('fs');
const axios = require('axios');

async function extractTextFromMultipleImages(imagePaths, language = 'eng') {
  const formData = new FormData();
  
  // Add multiple images
  imagePaths.forEach(imagePath => {
    formData.append('images', fs.createReadStream(imagePath));
  });
  
  formData.append('language', language);

  try {
    const response = await axios.post('http://localhost:3000/text-extractor', formData, {
      headers: {
        ...formData.getHeaders(),
      },
    });
    
    console.log(`Processed ${response.data.total_files} files:`);
    response.data.results.forEach(result => {
      console.log(`${result.filename}: ${result.success ? 'Success' : 'Failed'}`);
      if (result.success) {
        console.log(`  Text: ${result.text}`);
      } else {
        console.log(`  Error: ${result.error}`);
      }
    });
    
    return response.data.results;
  } catch (error) {
    console.error('Error:', error.response?.data || error.message);
  }
}

// Usage
const images = ['document1.jpg', 'document2.png', 'document3.jpg'];
extractTextFromMultipleImages(images, 'eng');
```

### Python
```python
import requests

def extract_text_from_multiple_images(image_paths, language='eng'):
    url = 'http://localhost:3000/text-extractor'
    
    files = []
    for image_path in image_paths:
        files.append(('images', open(image_path, 'rb')))
    
    data = {'language': language}
    
    try:
        response = requests.post(url, files=files, data=data)
        
        if response.status_code == 200:
            result = response.json()
            print(f"Processed {result['total_files']} files:")
            
            for file_result in result['results']:
                print(f"{file_result['filename']}: {'Success' if file_result['success'] else 'Failed'}")
                if file_result['success']:
                    print(f"  Text: {file_result['text']}")
                else:
                    print(f"  Error: {file_result['error']}")
            
            return result['results']
        else:
            print(f"Error: {response.json()['error']}")
    except Exception as e:
        print(f"Error: {e}")

# Usage
images = ['document1.jpg', 'document2.png', 'document3.jpg']
results = extract_text_from_multiple_images(images, 'eng')
```

### cURL
```bash
# Single image
curl -X POST http://localhost:3000/text-extractor \
  -F "images=@document.jpg"

# Multiple images
curl -X POST http://localhost:3000/text-extractor \
  -F "images=@document1.jpg" \
  -F "images=@document2.png" \
  -F "images=@document3.jpg" \
  -F "language=eng"
```