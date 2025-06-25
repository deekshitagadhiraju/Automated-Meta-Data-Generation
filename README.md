# Automated Metadata Generator

A powerful Flask-based web application that automatically extracts and generates comprehensive metadata from various document types including PDFs, Word documents, images, and text files.

## Features

- **Multi-format Support**: PDF, DOCX, TXT, PNG, JPG, JPEG
- **Intelligent Text Extraction**: Multiple fallback methods for reliable text extraction
- **OCR Capabilities**: Handles scanned documents and images
- **Smart Content Classification**: Automatically categorizes documents
- **Keyword Extraction**: Identifies key terms from document content
- **Auto-summarization**: Generates document summaries
- **Comprehensive Metadata**: File size, creation dates, word count, and more
- **Web Interface**: Clean, responsive Bootstrap UI


## Installation

### Prerequisites

- Python 3.7+
- Tesseract OCR
- Poppler (for PDF processing)

### System Dependencies

#### Windows
1. **Tesseract OCR**: Download from [GitHub](https://github.com/UB-Mannheim/tesseract/wiki)
2. **Poppler**: Download from [GitHub](https://github.com/oschwartz10612/poppler-windows/releases/) and add to PATH

#### Linux (Ubuntu/Debian)
```bash
sudo apt-get update
sudo apt-get install tesseract-ocr poppler-utils
```

#### macOS
```bash
brew install tesseract poppler
```

### Python Setup

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/automated-metadata-generator.git
cd automated-metadata-generator
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install Python dependencies**
```bash
pip install -r requirements.txt
```
if the above doesn't work then you have to install the following
```bash
pip install Flask==2.3.3
pip install PyPDF2==3.0.1
pip install PyMuPDF==1.23.8
pip install python-docx==0.8.11
pip install pytesseract==0.3.10
pip install Pillow==10.0.1
pip install nltk==3.8.1
pip install Werkzeung==2.3.7
pip install pdf2image==1.16.3
pip install PyMuPDF
```

4. **Configure Tesseract path** (if needed)
Edit `metadata_generator.py` and update the Tesseract path:
```python
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'  # Windows
# or
pytesseract.pytesseract.tesseract_cmd = '/usr/bin/tesseract'  # Linux/macOS
```

## Usage

### Running the Application

```bash
python app.py
```

Visit `http://localhost:5000` in your web browser.

### API Usage

You can also use the metadata generation function directly:

```python
from metadata_generator import generate_metadata

# Generate metadata for a file
metadata = generate_metadata('path/to/your/document.pdf')
print(metadata)
```

## Supported File Types

| File Type | Extensions | Extraction Method |
|-----------|------------|-------------------|
| PDF | `.pdf` | PyMuPDF → PyPDF2 → OCR |
| Word Document | `.docx` | python-docx |
| Text File | `.txt` | Native Python |
| Images | `.png`, `.jpg`, `.jpeg` | Tesseract OCR |

## Metadata Fields

The application generates the following metadata:

- **File Information**: Name, type, size, creation/modification dates
- **Content Analysis**: Word count, character count, line count
- **Text Processing**: Keywords, summary, content classification
- **Extraction Details**: Status, method used, processing log
- **Preview**: First 500 characters of extracted text

## Project Structure

```
automated-metadata-generator/
│
├── app.py                    # Flask application
├── metadata_generator.py     # Core metadata extraction logic
├── requirements.txt          # Python dependencies
├── README.md                # This file
│
├── templates/
│   ├── index.html           # Upload page
│   └── results.html         # Results display page
│
├── uploads/                 # Temporary file storage
└── static/                  # CSS/JS assets (if any)
```

## Configuration

### Environment Variables

You can set the following environment variables:

```bash
export UPLOAD_FOLDER=/path/to/uploads
export MAX_CONTENT_LENGTH=16777216  # 16MB max file size
export TESSERACT_CMD=/usr/bin/tesseract
```


## Error Handling

The application includes comprehensive error handling:

- **File Upload Errors**: Invalid file types, size limits
- **Processing Errors**: Corrupted files, extraction failures
- **OCR Errors**: Missing Tesseract, image processing issues
- **Memory Errors**: Large file handling

## Performance Considerations

- **File Size**: Recommended maximum 50MB per file
- **OCR Processing**: Can be slow for large images/scanned PDFs
- **Memory Usage**: Large files are processed in chunks
- **Concurrent Users**: Consider using production WSGI server

## Troubleshooting

### Common Issues

1. **"Tesseract not found"**
   - Ensure Tesseract is installed and in PATH
   - Update `tesseract_cmd` path in the code

2. **"Poppler not found"**
   - Install poppler-utils
   - Ensure binaries are in system PATH

3. **PDF extraction fails**
   - Check if PDF is password-protected
   - Try with different PDF files
   - Check extraction logs in results

4. **Memory errors with large files**
   - Reduce image DPI in OCR settings
   - Process files in smaller chunks

### Debug Mode

Run with debug mode for detailed error information:

```bash
export FLASK_DEBUG=1
python app.py
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [PyMuPDF](https://pymupdf.readthedocs.io/) for PDF processing
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) for optical character recognition
- [NLTK](https://www.nltk.org/) for natural language processing
- [Flask](https://flask.palletsprojects.com/) for the web framework

## Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/yourusername/automated-metadata-generator/issues) section
2. Create a new issue with detailed information
3. Include error logs and file types you're testing with

---
