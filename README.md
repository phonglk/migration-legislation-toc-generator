# Migration Legislation TOC Generator

A comprehensive Jupyter notebook-based tool for extracting Table of Contents (TOC) from PDF documents and creating enhanced PDFs with functional bookmarks and navigation.

## 🎯 Purpose

This project processes the "Migration Legislation Annotations.pdf" document to:
- Extract TOC entries from pages 12-13
- Handle complex formatting including multiline entries and mixed numbering (Roman/Arabic)
- Generate a clean, structured TOC
- Create an enhanced PDF with functional bookmarks and navigation

## ✨ Features

### Advanced TOC Processing
- **Multiline Entry Detection**: Handles TOC entries that span multiple lines
- **Mixed Numbering Support**: Processes both Roman numerals (v, vii, xiii) and Arabic numbers (1, 3, 27)
- **Smart Filtering**: Automatically excludes copyright notices and document headers
- **Manual Entry Addition**: Adds missing entries like "Contents" at roman page xi

### Auditable Workflow
- **Step-by-Step Processing**: Each phase is clearly separated and verifiable
- **JSON Output**: Structured data saved for inspection and reuse
- **Intermediate Files**: All processing stages create output files for verification
- **Error Handling**: Graceful fallbacks and clear error messages

### Enhanced PDF Generation
- **Bookmark Creation**: Functional PDF bookmarks for easy navigation
- **TOC Page Insertion**: Adds a formatted TOC page at the beginning
- **Page Offset Handling**: Correctly maps document pages to PDF pages
- **Flat Structure**: Clean, non-hierarchical TOC format

## 📁 Project Structure

```
Gen TOC/
├── Enhance TOC.ipynb          # Main Jupyter notebook with complete workflow
├── requirements.txt           # Python dependencies
├── README.md                 # This file
├── .gitignore               # Git ignore patterns
└── output/                  # Generated files (ignored by git)
    ├── raw_toc_text.txt     # Raw extracted TOC text
    ├── toc_structure.json   # Structured TOC data
    ├── generated_toc.txt    # Formatted TOC for verification
    └── Migration_Legislation_with_TOC.pdf  # Enhanced PDF output
```

## 🚀 Quick Start

### Prerequisites
- Python 3.7+
- Jupyter Notebook or JupyterLab
- **Your own PDF file**: "Migration Legislation Annotations.pdf" (not included due to licensing)

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd "Gen TOC"
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Provide the source PDF:**
   - **Important**: You must provide your own copy of "Migration Legislation Annotations.pdf"
   - Place the PDF file in the project root directory
   - The file is not included in this repository due to potential licensing restrictions
   - Ensure your PDF has the same structure (TOC on pages 12-13, document page 1 at PDF page 43)

4. **Launch Jupyter:**
   ```bash
   jupyter notebook "Enhance TOC.ipynb"
   ```

## 📋 Usage Workflow

The notebook is organized into sequential steps that can be run independently:

### Phase 1: Analysis & Verification
- **Step 1**: PDF Structure Analysis
- **Step 2**: TOC Pages Inspection

### Phase 2: TOC Extraction
- **Step 3**: TOC Entry Processing & JSON Export

### Phase 3: TOC Generation
- **Step 4**: Content Validation (Optional)
- **Step 5a**: TOC Text Generation
- **Step 5b**: Enhanced PDF Creation

### Running the Workflow

1. **Complete Workflow**: Run all cells sequentially from Step 1 to Step 5b
2. **Partial Workflow**: Run Steps 1-3, then jump to Step 5a/5b using the JSON file
3. **Resume from JSON**: Start directly from Step 5a if you have a valid `toc_structure.json`

## 🔧 Configuration

Key parameters in the notebook:

```python
PDF_PATH = "Migration Legislation Annotations.pdf"
OUTPUT_DIR = "output"
TOC_PAGES = [11, 12]  # PDF pages containing TOC
PAGE_OFFSET = 42      # Document page 1 starts at PDF page 43
```

## 📊 Technical Details

### TOC Format Handling
- **Pattern**: `[Title]....[Page number|Roman number]`
- **Multiline Support**: Detects titles spanning multiple lines
- **Copyright Filtering**: Excludes "© THOMSON REUTERS" and similar content
- **Smart Title Combination**: Merges multiline entries intelligently

### Page Number Mapping
- **Roman Numerals**: Direct mapping (roman page v → PDF page 5)
- **Arabic Numbers**: Offset mapping (document page 1 → PDF page 43)
- **Mixed Support**: Handles both numbering systems in one document

### Data Structure
```json
{
  "metadata": {
    "total_entries": 65,
    "source_pages": [11, 12],
    "page_offset": 42
  },
  "entries": [
    {
      "title": "Contents",
      "document_page": 11,
      "pdf_page": 11,
      "level": 0,
      "page_type": "roman"
    }
  ]
}
```

## 📈 Output Files

| File | Description | Usage |
|------|-------------|-------|
| `raw_toc_text.txt` | Raw extracted text from TOC pages | Debugging, verification |
| `toc_structure.json` | Structured TOC data with metadata | Step 5 input, inspection |
| `generated_toc.txt` | Formatted TOC text for verification | Manual review before PDF creation |
| `Migration_Legislation_with_TOC.pdf` | Enhanced PDF with bookmarks | Final output |

## 🛠 Dependencies

- **PyMuPDF (fitz)**: PDF manipulation and text extraction
- **re**: Regular expression pattern matching
- **json**: Data serialization
- **os**: File system operations
- **dataclasses**: Structured data handling
- **typing**: Type hints for better code clarity

## 🔍 Troubleshooting

### Common Issues

1. **"JSON file not found"**
   - Run Step 3 first to generate `toc_structure.json`

2. **"PDF file not found"**
   - Ensure "Migration Legislation Annotations.pdf" is in the project root
   - **Note**: The PDF file is not included in this repository due to licensing restrictions

3. **"Output directory not found"**
   - The `output/` directory is created automatically when you run the notebook
   - All generated files are excluded from Git for privacy and licensing reasons

4. **Bookmark creation failed**
   - Check PyMuPDF version compatibility
   - Verify PDF page numbers are within valid range

5. **Multiline entries not detected**
   - Check the `is_valid_toc_start()` function filters
   - Verify TOC pattern regex in Step 2

### Debug Mode
Enable verbose output by checking intermediate files:
- Review `raw_toc_text.txt` for extraction issues
- Inspect `toc_structure.json` for data problems
- Verify `generated_toc.txt` before PDF creation

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with the sample PDF
5. Submit a pull request

## 📝 License

This project is for processing the Migration Legislation Annotations document. Please respect copyright and licensing terms of the source material.

## 🔄 Version History

- **v1.0**: Initial implementation with basic TOC extraction
- **v1.1**: Added multiline entry support and Roman numeral handling
- **v1.2**: Implemented JSON-based workflow and enhanced filtering
- **v1.3**: Added comprehensive error handling and documentation 