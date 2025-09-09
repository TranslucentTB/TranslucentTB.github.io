# TranslucentTB Configuration Documentation

TranslucentTB uses a JSON configuration file to customize the appearance and behavior of the Windows taskbar. This document explains all available configuration options and their usage.

## Table of Contents

- [Overview](#overview)
- [Configuration Structure](#configuration-structure)
- [Appearance Settings](#appearance-settings)
- [Appearance Modes](#appearance-modes)
- [Window Rules](#window-rules)
- [Global Settings](#global-settings)
- [Example Configurations](#example-configurations)
- [Tips and Best Practices](#tips-and-best-practices)
- [Troubleshooting](#troubleshooting)

## Overview

### Configuration File Location

The configuration file should be saved as `settings.json` in the TranslucentTB application directory or user data folder.

### Schema Reference

The configuration follows the JSON schema available at: `https://TranslucentTB.github.io/settings.schema.json`

## Configuration Structure

```json
{
  "$schema": "https://TranslucentTB.github.io/settings.schema.json",
  "desktop_appearance": { ... },
  "visible_window_appearance": { ... },
  "maximized_window_appearance": { ... },
  "start_opened_appearance": { ... },
  "search_opened_appearance": { ... },
  "task_view_opened_appearance": { ... },
  "battery_saver_appearance": { ... },
  "ignored_windows": { ... },
  "hide_tray": false,
  "disable_saving": false,
  "verbosity": "warn",
  "language": "en-US",
  "use_xaml_context_menu": false
}
```

## Appearance Settings

All appearance configurations support the following properties:

### Basic Properties

#### `accent` (string)
The accent/transparency effect to apply:
- `"normal"`: Windows default appearance
- `"opaque"`: Solid, non-transparent taskbar
- `"clear"`: Fully transparent taskbar
- `"blur"`: Blurred transparency effect
- `"acrylic"`: Windows 10/11 acrylic material effect

#### `color` (string)
Custom color in hexadecimal format:
- Format: `#RRGGBB` or `#RRGGBBAA` (with alpha channel)
- Example: `"#00000000"` (fully transparent black)

#### `show_peek` (boolean)
Enable/disable desktop peek functionality:
- `true`: Show desktop peek
- `false`: Disable desktop peek

#### `show_line` (boolean)
Show/hide the taskbar accent line:
- `true`: Display accent line
- `false`: Hide accent line

#### `blur_radius` (number)
Blur effect intensity (when using blur accent):
- Range: Typically 0.0 to 50.0
- Example: `9.0`

## Appearance Modes

### 1. Desktop Appearance

Applied when no windows are open or focused.

```json
"desktop_appearance": {
  "accent": "clear",
  "color": "#00000000",
  "show_peek": false,
  "show_line": false,
  "blur_radius": 9.0
}
```

### 2. Visible Window Appearance

Applied when windows are visible but not maximized.

```json
"visible_window_appearance": {
  "enabled": false,
  "accent": "clear",
  "color": "#00000000",
  "show_peek": true,
  "show_line": false,
  "blur_radius": 9.0,
  "rules": {
    "window_class": {},
    "window_title": {},
    "process_name": {}
  }
}
```

### 3. Maximized Window Appearance

Applied when a window is maximized.

```json
"maximized_window_appearance": {
  "enabled": true,
  "accent": "clear",
  "color": "#00000000",
  "show_peek": true,
  "show_line": false,
  "blur_radius": 9.0,
  "rules": {
    "window_class": {},
    "window_title": {},
    "process_name": {}
  }
}
```

### 4. Start Menu Opened Appearance

Applied when the Start menu is open.

```json
"start_opened_appearance": {
  "enabled": false,
  "accent": "normal",
  "color": "#00000000",
  "show_peek": true,
  "show_line": true,
  "blur_radius": 9.0
}
```

### 5. Search Opened Appearance

Applied when Windows Search is open.

```json
"search_opened_appearance": {
  "enabled": true,
  "accent": "normal",
  "color": "#00000000",
  "show_peek": true,
  "show_line": true,
  "blur_radius": 9.0
}
```

### 6. Task View Opened Appearance

Applied when Task View (Alt+Tab) is open.

```json
"task_view_opened_appearance": {
  "enabled": true,
  "accent": "normal",
  "color": "#00000000",
  "show_peek": false,
  "show_line": true,
  "blur_radius": 9.0
}
```

### 7. Battery Saver Appearance

Applied when Windows Battery Saver mode is active.

```json
"battery_saver_appearance": {
  "enabled": true,
  "accent": "clear",
  "color": "#00000000",
  "show_peek": true,
  "show_line": false,
  "blur_radius": 9.0
}
```

## Window Rules

For `visible_window_appearance` and `maximized_window_appearance`, you can define specific rules based on:

### Rule Types

- **`window_class`**: Target specific window classes
- **`window_title`**: Target windows by title
- **`process_name`**: Target specific applications by process name

### Rule Structure

```json
"rules": {
  "process_name": {
    "notepad.exe": {
      "accent": "blur",
      "color": "#FF000080",
      "show_peek": false,
      "show_line": true,
      "blur_radius": 15.0,
      "inactive": {
        "accent": "clear",
        "color": "#00000000",
        "show_peek": true,
        "show_line": false
      }
    }
  }
}
```

The `inactive` property defines the appearance when the targeted window is not focused.

### Ignored Windows

Configure windows that should be ignored by TranslucentTB:

```json
"ignored_windows": {
  "window_class": ["ClassName1", "ClassName2"],
  "window_title": ["Window Title 1", "Window Title 2"],
  "process_name": ["process1.exe", "process2.exe"]
}
```

## Global Settings

### System Integration

#### `hide_tray` (boolean)
Hide the system tray area:
- `true`: Hide tray
- `false`: Show tray (default)

#### `disable_saving` (boolean)
Prevent saving configuration changes:
- `true`: Disable automatic saving
- `false`: Enable automatic saving (default)

### Localization

#### `language` (string)
Set application language:
- Format: `"en-US"`, `"de-DE"`, etc.
- Must follow ISO 639-1 language code format

### Interface Options

#### `use_xaml_context_menu` (boolean)
Use modern context menu style:
- `true`: Use XAML-based context menu
- `false`: Use classic context menu

### Logging

#### `verbosity` (string)
Set logging level:
- `"trace"`: Most verbose logging
- `"debug"`: Debug information
- `"info"`: General information
- `"warn"`: Warnings only (default)
- `"err"`: Errors only
- `"critical"`: Critical errors only
- `"off"`: No logging

## Example Configurations

### Fully Transparent Desktop

```json
{
  "$schema": "https://TranslucentTB.github.io/settings.schema.json",
  "desktop_appearance": {
    "accent": "clear",
    "color": "#00000000",
    "show_peek": false,
    "show_line": false
  }
}
```

### Blur Effect with Custom Color

```json
{
  "$schema": "https://TranslucentTB.github.io/settings.schema.json",
  "desktop_appearance": {
    "accent": "blur",
    "color": "#1E1E1E80",
    "show_peek": true,
    "show_line": true,
    "blur_radius": 15.0
  }
}
```

### Application-Specific Rules

```json
{
  "$schema": "https://TranslucentTB.github.io/settings.schema.json",
  "maximized_window_appearance": {
    "enabled": true,
    "accent": "normal",
    "rules": {
      "process_name": {
        "chrome.exe": {
          "accent": "acrylic",
          "color": "#000000AA",
          "show_line": true
        },
        "notepad.exe": {
          "accent": "clear",
          "show_peek": false
        }
      }
    }
  }
}
```

### Complete Configuration Example

```json
{
  "$schema": "https://TranslucentTB.github.io/settings.schema.json",
  "desktop_appearance": {
    "accent": "clear",
    "color": "#00000000",
    "show_peek": false,
    "show_line": false,
    "blur_radius": 9.0
  },
  "visible_window_appearance": {
    "enabled": false,
    "accent": "clear",
    "color": "#00000000",
    "show_peek": true,
    "show_line": false,
    "blur_radius": 9.0,
    "rules": {
      "window_class": {},
      "window_title": {},
      "process_name": {}
    }
  },
  "maximized_window_appearance": {
    "enabled": true,
    "accent": "clear",
    "color": "#00000000",
    "show_peek": true,
    "show_line": false,
    "blur_radius": 9.0,
    "rules": {
      "window_class": {},
      "window_title": {},
      "process_name": {}
    }
  },
  "start_opened_appearance": {
    "enabled": false,
    "accent": "normal",
    "color": "#00000000",
    "show_peek": true,
    "show_line": true,
    "blur_radius": 9.0
  },
  "search_opened_appearance": {
    "enabled": true,
    "accent": "normal",
    "color": "#00000000",
    "show_peek": true,
    "show_line": true,
    "blur_radius": 9.0
  },
  "task_view_opened_appearance": {
    "enabled": true,
    "accent": "normal",
    "color": "#00000000",
    "show_peek": false,
    "show_line": true,
    "blur_radius": 9.0
  },
  "battery_saver_appearance": {
    "enabled": true,
    "accent": "clear",
    "color": "#00000000",
    "show_peek": true,
    "show_line": false,
    "blur_radius": 9.0
  },
  "ignored_windows": {
    "window_class": [],
    "window_title": [],
    "process_name": []
  },
  "disable_saving": false,
  "verbosity": "warn"
}
```

## Tips and Best Practices

1. **Start Simple**: Begin with basic appearance settings before adding complex rules
2. **Test Changes**: Use different applications to test your configuration
3. **Backup Configuration**: Keep a backup of working configurations
4. **Performance**: Complex rules with many blur effects may impact system performance
5. **Color Format**: Always use proper hexadecimal color format with alpha channel for transparency
6. **JSON Validation**: Use a JSON validator or editor with syntax checking to avoid errors
7. **Schema Validation**: Include the `$schema` property to enable validation and autocomplete in editors

## Troubleshooting

### Common Issues

- **Configuration not loading**: Check JSON syntax and schema validation
- **Rules not working**: Verify process names and window classes using tools like Spy++
- **Performance issues**: Reduce `blur_radius` values or disable complex effects
- **Color not applying**: Ensure proper hex color format with alpha channel
- **Settings not saving**: Check if `disable_saving` is set to `false`

### Debugging Tips (Advanced)

1. **Check the logs**: Set `verbosity` to `"debug"` to see detailed information
2. **Validate JSON**: Use online JSON validators or VS Code with the schema
3. **Test incrementally**: Add one setting at a time to isolate issues
4. **Use process monitor**: Tools like Process Monitor can help identify file access issues
5. **Check permissions**: Ensure TranslucentTB has write access to the config directory

### Getting Help

If you encounter issues not covered in this documentation:

1. Check the [TranslucentTB Issues](https://github.com/TranslucentTB/TranslucentTB/issues) page
2. Search for similar problems in existing issues
3. Create a new issue with your configuration file and detailed description
4. Include system information and TranslucentTB version
