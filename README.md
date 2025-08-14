# TU Score Input Helper v3.0

A Chrome extension for efficiently copying scores from CSV files or spreadsheets to web applications for Triam Udom Suksa School, now with **Student ID Matching** for precise data placement and **modular architecture** for enhanced maintainability.

## 🎯 Quick Start

**📋 Need a CSV template?** [Download CSV Template](https://github.com/braskano1/Input-Score-TU/blob/main/csv_template.csv)

## Features

### 🆕 New in Version 3.0
- **🎯 Student ID Matching**: Match CSV data with web page student IDs for precise score placement
- **🗂️ Modular Architecture**: Clean, maintainable code split into specialized modules
- **Smart ID Detection**: Automatically extracts student IDs from web page input fields
- **Flexible Matching**: Works with various student ID input field patterns
- **Dual Paste Modes**: Choose between single column or all columns for ID-based pasting
- **Match Verification**: Preview matched students before pasting data
- **Enhanced Error Handling**: Comprehensive error messages and debugging tools
- **📋 CSV Template**: Easy access to properly formatted CSV template

### 📊 Core Features
- **Multiple Input Methods**: CSV upload, Student ID matching, or manual copy-paste
- **🚀 Multi-Column Processing**: Select and process multiple columns simultaneously
- **Smart Data Processing**: Automatically extracts numeric values and matches by student ID
- **Multiple Paste Destinations**: Support for 13+ different input field types
- **Individual Clear Functions**: Clear specific input fields
- **Data Preview**: Preview processed data and matched students before pasting
- **Sequential Processing**: Auto-paste processes columns one by one for reliability
- **Comprehensive Validation**: CSV structure validation and format checking

## Supported Input Fields

The extension supports pasting data to the following input field types:
- **F1** (formal)
- **SUM ได้** (mark05)
- **SUM แก้ตัว** (mark06)
- **F2** (forma2)
- **คุณลักษณะ 1-10** (sub_qua1 through sub_qua10)
- **ปลายภาค** (mfin)

## Installation

1. Download all the extension files:
   ```
   ├── manifest.json
   ├── popup.html
   ├── content-universal.js
   ├── icon16.png, icon48.png, icon128.png
   └── js/
       ├── popup.js (main entry point)
       ├── utils.js
       ├── csv-handler.js
       ├── ui-controller.js
       ├── id-matcher.js
       ├── storage-manager.js
       └── chrome-api.js
   ```

2. Open Chrome and go to `chrome://extensions/`

3. Enable "Developer mode" (toggle in top right)

4. Click "Load unpacked" and select the folder containing the extension files

5. The extension icon will appear in your Chrome toolbar

## Architecture Overview

### 🗂️ Modular Design

The extension is built with a clean, modular architecture for better maintainability:

#### **js/popup.js** - Main Entry Point
- Coordinates all modules using PopupController class
- Handles initialization and event routing
- Manages application state

#### **js/utils.js** - Utility Functions
- Common helper functions and constants
- Input field mappings and configurations
- Data validation utilities

#### **js/csv-handler.js** - CSV Processing
- CSV parsing and validation with CSVHandler class
- Data extraction from columns
- File format detection and delimiter handling

#### **js/ui-controller.js** - UI Management
- DOM manipulation and control
- Status messages and previews
- Tab switching and user interface state management

#### **js/id-matcher.js** - Student ID Matching
- Student ID extraction from web pages
- CSV-to-webpage matching logic with IDMatcher class
- Match validation and reporting

#### **js/storage-manager.js** - Data Persistence
- Chrome storage operations
- Settings management and data backup
- Temporary data handling with expiration

#### **js/chrome-api.js** - Extension APIs
- Chrome extension API interactions
- Content script communication
- Tab management and batch processing

## Usage

### Method 1: Student ID Matching (🆕 Recommended for Precision)

This method ensures scores are pasted to the correct student by matching student IDs between your CSV file and the web page.

#### Prerequisites
- Your CSV file must contain a column with student IDs
- The web page must have student ID input fields that the extension can detect

#### Steps
1. **Click the extension icon** in your Chrome toolbar
2. **Select "🎯 ID Match" tab**
3. **Upload your CSV file**:
   - Click "📁 Click to select CSV file" or drag and drop
   - Your CSV must contain both student IDs and score columns
   - [Use this CSV template](https://github.com/braskano1/Input-Score-TU/blob/main/csv_template.csv) for proper formatting
4. **Preview your data**: The extension shows a preview of your CSV
5. **Select Student ID column**: Choose which column contains the student IDs (auto-selected if named appropriately)
6. **Navigate to your web application** (the score input page)
7. **Extract Student IDs**: Click "🎯 Extract Student IDs from Page"
   - The extension will scan the web page for student ID input fields
   - It will show how many students were matched between CSV and web page
8. **Select score columns**: Check the columns you want to process
9. **Click "🚀 Process Selected Columns by ID"**
10. **Save your changes** in the web application

### Method 2: CSV File Upload (Multi-Column Processing)

#### Steps
1. **Click the extension icon** in your Chrome toolbar
2. **Select "📄 CSV File" tab**
3. **Upload your CSV file**:
   - Click "📁 Click to select CSV file" or drag and drop
   - [Download CSV template](https://github.com/braskano1/Input-Score-TU/blob/main/csv_template.csv) for proper format
4. **Preview your data**: The extension will show a preview of your CSV
5. **Select columns**: Check the columns you want to process
6. **Choose processing method**:
   - **"🚀 Process Selected Columns"** (smart mapping)
   - **"🚀 Process All Columns & Auto-Paste"** (template format)
7. **Navigate to your web application**
8. **Save your changes** in the web application

### Method 3: Manual Copy-Paste

1. **Click the extension icon** in your Chrome toolbar
2. **Select "✏️ Manual" tab**
3. **Copy data from your spreadsheet** (Ctrl+C)
4. **Paste into the text box** (Ctrl+V)
5. **Click "📊 Process Manual Data"**
6. **Navigate to your web application**
7. **Click the appropriate paste button** for your target input fields
8. **Save your changes** in the web application

## Student ID Matching Details

### How Student ID Detection Works
The extension automatically looks for student ID input fields using these patterns:
- Input names containing: `student_id`, `studentid`, `std_id`, `stdid`
- Input IDs containing: `student_id`, `studentid`, `std_id`, `stdid`
- Input placeholders containing: "รหัสนักเรียน", "Student ID"
- Input values that look like student IDs (5-8 digit numbers)
- Input field names with bracket notation: `formal[65932]`, `mark05[65936]`

### Supported Student ID Formats
- 5-8 digit numbers (e.g., 12345, 1234567, 12345678)
- The extension is flexible and can adapt to different ID lengths

### CSV Requirements for ID Matching
- Must contain a column with student IDs that match those on the web page
- Student IDs should be in the same format as the web page
- Score columns should contain numeric values
- For auto-paste all columns, use template format column names

### Template Format for Auto-Paste
When using "🚀 All Columns" mode, your CSV should have columns named:
- `F1_Score` → F1 input fields
- `Mark05_Score` → SUM ได้ input fields
- `Mark06_Score` → SUM แก้ตัว input fields
- `F2_Score` → F2 input fields
- `Sub_Qua1` through `Sub_Qua10` → คุณลักษณะ 1-10 input fields
- `Final_Score` → ปลายภาค input fields

**📋 [Download the CSV template](https://github.com/braskano1/Input-Score-TU/blob/main/csv_template.csv)** with proper column names and formatting.

## File Structure

```
TU-Score-Input-Helper/
├── manifest.json              # Extension configuration
├── popup.html                # Extension popup interface  
├── content-universal.js       # Content script for web page interaction
├── README.md                 # This documentation
├── csv_template.csv          # Template CSV file for users
├── icons/                    # Extension icons
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
└── js/                       # Modular JavaScript files
    ├── popup.js              # Main entry point (PopupController class)
    ├── utils.js              # Utility functions and constants
    ├── csv-handler.js        # CSV parsing (CSVHandler class)
    ├── ui-controller.js      # UI management (UIController class)
    ├── id-matcher.js         # Student ID matching (IDMatcher class)
    ├── storage-manager.js    # Chrome storage (StorageManager class)
    └── chrome-api.js         # Chrome APIs (ChromeAPI class)
```

## Technical Details

### Modular Architecture Benefits
- **Maintainability**: Each module has a single responsibility
- **Testability**: Individual modules can be tested in isolation
- **Scalability**: Easy to add new features without affecting existing code
- **Debugging**: Issues are isolated to specific modules
- **Collaboration**: Multiple developers can work on different modules

### Student ID Matching Algorithm
1. **Extraction**: Scans web page for input fields that likely contain student IDs
2. **Pattern Recognition**: Uses multiple CSS selectors and content analysis
3. **Validation**: Filters for valid student ID formats (5-8 digits)
4. **Matching**: Cross-references extracted IDs with CSV data using IDMatcher class
5. **Targeting**: Finds specific input fields for each student and score type
6. **Pasting**: Places scores in the correct input field for each student

### CSV Processing
- **Supported formats**: .csv and .txt files
- **Delimiter detection**: Automatically detects comma, semicolon, or tab delimiters
- **Quote handling**: Properly handles quoted fields in CSV
- **Data validation**: Only extracts valid numeric values (integers and decimals)
- **Memory efficient**: Previews only first 100 rows for large files
- **Student ID extraction**: Builds mapping between student IDs and their data

### Global Module Exposure
All modules are exposed to the global scope for cross-module communication:
```javascript
// Each module exposes itself globally
window.UIController = UIController;
window.CSVHandler = CSVHandler;
window.IDMatcher = IDMatcher;
// etc.
```

### Data Flow
```
CSV Upload → Parsing → Validation → UI Display → 
User Selection → Data Processing → Chrome API → 
Content Script → Web Page Interaction → Results
```

## Browser Compatibility

- **Chrome**: Fully supported (Manifest V3)
- **Edge**: Compatible (Chromium-based)
- **Other browsers**: Not tested

## Development

### Setting Up Development Environment

1. Clone the repository
2. Load the extension in Chrome (Developer mode)
3. Make changes to the modular files in `js/` directory
4. Reload the extension to test changes

### Module Dependencies

```
popup.js (PopupController class)
├── utils.js (utilities and constants)
├── ui-controller.js (UIController class)
├── csv-handler.js (CSVHandler class)
├── id-matcher.js (IDMatcher class)
├── storage-manager.js (StorageManager class)
└── chrome-api.js (ChromeAPI class)
```

### Adding New Features

1. Identify the appropriate module for your feature
2. Add new functions to the relevant module class
3. Expose new functions globally if needed
4. Update the main PopupController if needed
5. Test thoroughly with different CSV formats
6. Update documentation

## Troubleshooting

### Common Issues

1. **"Missing required modules" error**:
   - Check that all JS files are in the correct location
   - Ensure global module exposure is working
   - Verify all `window.ModuleName = ModuleName;` lines are present

2. **"Could not find input fields" error**:
   - Make sure you're on the correct web page
   - Check that the page has loaded completely
   - Try refreshing the page

3. **"No students matched" error**:
   - Verify student IDs in CSV match those on web page exactly
   - Check student ID column selection in CSV
   - Ensure web page has student ID input fields
   - Try refreshing the web page and extracting IDs again

4. **CSV not loading**:
   - Ensure file is a valid .csv or .txt file
   - Check that the file is not empty
   - Verify the file uses standard CSV formatting
   - Use the provided CSV template for proper format

5. **Extension not working**:
   - Try refreshing the web page
   - Check Chrome's developer console for errors
   - Ensure the extension is enabled in Chrome's extension settings
   - Verify all required permissions are granted

### Debug Information

The extension logs detailed information to the browser console. To view debug logs:
1. Right-click on the web page and select "Inspect"
2. Go to the "Console" tab
3. Look for messages starting with "TU Score Input Helper"

### Performance Optimization

- CSV files are processed in chunks to prevent browser freezing
- Large datasets are previewed partially (first 100 rows)
- Sequential processing prevents overwhelming the target web page
- Automatic delays between operations ensure reliability
- Modular architecture improves loading and execution speed

## Best Practices

### For Student ID Matching
1. **Verify student IDs**: Always check that student IDs in your CSV exactly match those on the web page
2. **Use consistent formats**: Ensure student IDs don't have leading zeros in one place but not another
3. **Test with small batches**: Try with a few students first to verify the matching works correctly
4. **Check match results**: Always review the "Matched Students" section before pasting
5. **Save frequently**: Save your work in the web application after each successful paste

### For CSV Files
1. **Use the template**: Download and use the provided CSV template for best results
2. **Clean data**: Ensure score columns contain only numeric values
3. **Consistent formatting**: Use the same number format throughout (e.g., all decimals or all integers)
4. **Template format**: For auto-paste, use the exact column names specified
5. **Backup data**: Keep a backup of your original CSV file

### For Development
1. **Module isolation**: Keep modules focused on single responsibilities
2. **Global exposure**: Remember to expose new modules/functions globally
3. **Error handling**: Add comprehensive error handling in each module
4. **Logging**: Use consistent logging for debugging
5. **Testing**: Test each module independently when possible

## Resources

- **📋 [CSV Template](https://github.com/braskano1/Input-Score-TU/blob/main/csv_template.csv)**: Download the properly formatted CSV template
- **📖 [Full Documentation](https://github.com/braskano1/Input-Score-TU/blob/main/README.md)**: Complete documentation and usage guide
- **🐛 [Report Issues](https://github.com/braskano1/Input-Score-TU/issues)**: Report bugs or request features

## Version History

### v3.0 (Current)
- **New**: Student ID matching functionality with precise data placement
- **New**: Modular architecture with class-based design
- **New**: Multi-column selection and processing
- **New**: CSV template download integration
- **Enhanced**: Error handling and user feedback
- **Enhanced**: CSV validation and format detection
- **Enhanced**: Global module exposure system
- **Improved**: Code organization and documentation
- **Added**: Extension icon integration

### v2.0
- Added CSV file upload functionality
- Implemented tabbed interface
- Enhanced data processing and validation
- Added drag & drop support
- Improved error handling and user feedback

### v1.0
- Basic manual copy-paste functionality
- Support for multiple input field types
- Individual clear functions
- Chrome extension framework

## Contributing

1. Fork the repository
2. Create a feature branch
3. Follow the modular architecture patterns
4. Add appropriate error handling and logging
5. Ensure global module exposure for new modules
6. Test thoroughly with various CSV formats
7. Update documentation
8. Submit a pull request with detailed description

## License

This extension is created for educational purposes for Triam Udom Suksa School.

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Review the browser console for error messages
3. Ensure you're using the latest version
4. Use the provided CSV template for best results
5. Contact the developer with specific error details
