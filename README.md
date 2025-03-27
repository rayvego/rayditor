# Rayditor

A lightweight, terminal-based text editor written in Rust. Rayditor provides a simple yet powerful editing experience with syntax highlighting and basic text editing features.

## Features

- Terminal-based UI with clean interface
- Syntax highlighting for Rust files
- File opening, editing, and saving
- Text search functionality with forward and backward search
- Unicode support via grapheme clusters
- Full keyboard navigation
- Status bar with file information and edit status
- Confirmation when quitting with unsaved changes

## Implementation Details

Rayditor is built with a modular architecture that separates concerns and provides a clean codebase:

### Core Components

- **Editor (`editor.rs`)**: The main component that handles user interaction, keypress processing, and coordinates all other modules.
- **Document (`document.rs`)**: Manages file operations, text insertion/deletion, and coordinates row rendering.
- **Row (`row.rs`)**: Handles text operations at the row level, including insertion, deletion, and rendering.
- **Terminal (`terminal.rs`)**: Provides an abstraction over terminal operations using the Termion library.
- **FileType (`filetype.rs`)**: Determines file type based on extension and provides appropriate highlighting options.
- **Highlighting (`highlighting.rs`)**: Defines highlighting types and color schemes for syntax highlighting.

### Key Implementation Features

#### Text Handling

Rayditor uses Unicode grapheme clusters (via `unicode-segmentation` crate) to properly handle multi-byte characters and ensure correct cursor positioning and text manipulation.

#### Syntax Highlighting

The editor implements syntax highlighting for Rust code with support for:
- Keywords (primary and secondary)
- Strings and characters
- Numbers
- Comments (single-line and multi-line)
- Search match highlighting

#### Terminal Interface

The terminal interface is implemented using the Termion library, providing:
- Raw mode terminal handling
- Color support
- Keyboard input processing
- Terminal size detection

#### Search Functionality

Text search supports:
- Forward and backward searching
- Highlighted search results
- Navigation between search results using arrow keys

## Usage

### Running the Editor

```bash
cargo run [filename]
```

### Keyboard Shortcuts

- `Ctrl-Q`: Quit (prompts for confirmation if there are unsaved changes)
- `Ctrl-S`: Save file
- `Ctrl-F`: Find text
- Arrow keys: Navigate through text
- During search:
  - `ESC`: Cancel search
  - Arrow keys: Navigate between matches

## Building from Source

### Prerequisites

- Rust (2021 edition or newer)
- Cargo package manager

### Build and Run

```bash
# Clone the repository
git clone [repository-url]
cd rayditor

# Build the project
cargo build --release

# Run the editor
cargo run [optional-filename]
```

## Dependencies

- `termion`: Terminal handling library
- `unicode-segmentation`: Unicode text segmentation according to UAX #29 rules

## Project Structure

```
rayditor/
├── Cargo.toml           # Project configuration and dependencies
├── Cargo.lock           # Locked dependencies
└── src/                 # Source code
    ├── main.rs          # Entry point
    ├── editor.rs        # Main editor component
    ├── document.rs      # Document handling
    ├── row.rs           # Row-level text operations
    ├── terminal.rs      # Terminal interface
    ├── filetype.rs      # File type detection and highlighting options
    └── highlighting.rs  # Syntax highlighting definitions
```

## Implementation Notes

- The editor uses a row-based text representation for efficient editing
- File operations are handled using Rust's standard library
- The status bar shows file name, type, and number of lines
- Error handling is implemented for file operations
- The editor tracks "dirty" state for unsaved changes
- Syntax highlighting is applied incrementally for performance

## Future Improvements

Potential areas for enhancement:

- Support for multiple file types and syntax highlighting
- Line numbers
- Tab completion
- Configurable key bindings
- Undo/redo functionality
- Clipboard support

## Inspiration

This project was inspired by [Build Your Own Text Editor in Rust](https://www.flenker.blog/hecto/)