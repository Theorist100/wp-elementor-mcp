# Changelog

All notable changes to the WordPress Elementor MCP Server will be documented in this file.

## [1.6.2] - 2025-12-24 (Fork: Theorist100)

### ✨ Added

- **New Tool**: `reorder_top_level_sections` - Reorder main page sections/containers by providing an array of section IDs in desired order. Useful for reorganizing page layout without manually moving each section.

### 🛠️ Fixed

#### Container Support for Widget Operations
Modern Elementor uses `container` type instead of legacy `section`/`column`. Three functions were not handling containers properly:

- **`insert_widget_at_position`**: Added `inside` position support to properly nest widgets inside containers. Previously, `inside` was treated same as `after`, inserting widget as sibling instead of child.

- **`move_widget`**: Added `container` type detection. Previously only looked for `section` and `column` types, causing "Target container not found" errors with modern Elementor pages.

- **`add_widget_to_section`**: Added `container` type detection. Same issue as `move_widget`.

#### JSON Parsing Error in Elementor Data Consumer Methods
- The `getElementorData` method returns formatted text with debug info followed by JSON after "--- Elementor Data ---" separator
- Multiple methods were parsing entire response as JSON, causing "Unexpected token 'F'" errors when text started with "Found as page..."
- Added `extractElementorJsonFromText()` helper to properly extract JSON portion
- Updated 14 affected methods to use the new helper

**Affected methods:**
- getElementorElements
- getElementorDataChunked
- getPageStructure
- createElementorSection
- addColumnToSection
- duplicateSection
- addWidgetToSection
- insertWidgetAtPosition
- cloneWidget
- moveWidget
- deleteElementorElement
- reorderElements
- copyElementSettings
- findElementsByType

---

## [1.6.1] - 2024-01-XX

### ✨ Added
- **New Tool**: `list_all_content` - Content discovery with Elementor status indicators (✅/⚠️/❌)
- **Enhanced Error Handling**: Much more informative 404 and connection error messages
- **Debugging Infrastructure**: Console logging and detailed request information
- **Connection Diagnostics**: Automatic timeout handling (30s) and enhanced error reporting
- **Test Suite**: Comprehensive credential testing with real WordPress connections
- **Documentation**: Added `TROUBLESHOOTING.md` and `CREDENTIAL-TESTING.md` guides

### 🔧 Improved
- **WordPress Integration**: Enhanced data retrieval with `context: 'edit'` for full meta access
- **Error Messages**: Much more informative debugging information for connection issues
- **Data Discovery**: Better handling of posts/pages that may not have Elementor data
- **Connection Setup**: Enhanced axios configuration with timeout and debug logging

### 🛠️ Fixed
- **404 Errors**: Better handling and diagnosis of "Request failed with status code 404"
- **Missing Elementor Data**: Improved detection and reporting of "No Elementor data found"
- **Post/Page Discovery**: Enhanced search and filtering capabilities
- **Connection Issues**: Better error messages for authentication and network problems

### 📚 Documentation
- Added comprehensive troubleshooting guide
- Created credential testing documentation
- Enhanced error message examples
- Added debugging tips and common solutions

### 🧪 Testing
- Added `test:enhanced` script for enhanced features
- Added `test:credentials` script for credential testing
- Updated tool count validation for new `list_all_content` tool
- Enhanced test coverage for error scenarios

## [1.6.0] - Previous Release

### Features
- Modular configuration system (Essential → Standard → Advanced → Full)
- Complete Elementor page building capabilities
- Performance optimizations and caching
- Comprehensive WordPress operations
- Advanced element management tools

### Tools
- 34 total tools across different modes
- WordPress CRUD operations
- Elementor section/container creation
- Widget management and manipulation
- Performance and caching tools

## Previous Versions

See Git history for detailed information about earlier versions.

---

### Legend
- ✨ Added: New features
- 🔧 Improved: Enhanced existing features  
- 🛠️ Fixed: Bug fixes
- 📚 Documentation: Documentation changes
- 🧪 Testing: Test-related changes
- ⚠️ Breaking: Breaking changes (when applicable) 