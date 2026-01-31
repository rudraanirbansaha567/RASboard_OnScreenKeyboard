# 🎹 RASboard: Custom Virtual Keyboard

RASboard is a sleek, cross-platform on-screen keyboard built with Python. Designed for Linux and Windows, it features a modern "Midnight Neon" theme, functional keys (F1-F12), and an intuitive drag-and-drop interface.

![RASboard Icon](https://via.placeholder.com/100x100.png?text=RAS) ## ✨ Features
- **Modern UI:** Deep charcoal and neon blue aesthetic with a "borderless" flat design.
- **Full Functionality:** Includes Function keys (F1-F12), Caps Lock, Shift, and Arrow keys.
- **Smart State Management:** Real-time UI updates for Shift and Caps Lock states.
- **Portable:** Can be compiled into a single `.exe` (Windows) with pyinstaller or run as a standalone script (Linux).
- **Draggable:** Custom drag handle (`::`) to position the keyboard anywhere on your screen.

## 🚀 Installation & Usage

### 1. Run from Source
If you have Python installed, you can run the keyboard directly:

**Requirements:**
- Python 3.x
- `pynput` library

```bash
# Install dependency
pip install pynput

# Run the app
python main.py
