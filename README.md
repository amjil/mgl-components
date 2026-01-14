# MGL Components

A ClojureDart component library for Flutter applications with Mongolian language support. This library provides a collection of reusable, theme-aware UI components designed for building modern Flutter apps using ClojureDart.

## Features

- 🎨 **Theme-aware components** - All components automatically adapt to Flutter's Material Design theme
- 🇲🇳 **Mongolian language support** - Built-in support for vertical Mongolian text rendering
- 🎯 **Type-safe** - Built with ClojureDart for type safety and functional programming
- 🎛️ **Highly configurable** - Extensive customization options for each component
- 📱 **Modern UI** - Material Design 3 compliant components

## Components

- **Bottom Sheet** - Modal bottom sheet with customizable height and styling
- **Chip** - Filter chips with selection state management and haptic feedback
- **Expansion Tile** - Expandable/collapsible content sections
- **Input Dialog** - Text input dialogs with validation
- **Layout** - Row-first layout container for side-by-side content arrangement
- **Search Bar** - Search input with clear functionality
- **Select** - Dropdown selection menus with grouping support
- **Tab Layout** - Tab navigation component
- **Text** - Vertical Mongolian text display with focus highlighting and tap support
- **Text Field** - Text input field with vertical Mongolian text support and placeholder hints
- **Toast** - Toast notifications with multiple types (success, error, warning, info) and animations
- **Tooltip** - Contextual tooltips
- **Design Tokens** - Spacing, typography, and color tokens for consistent design

## Installation

Add this library to your `deps.edn`:

```clojure
{:deps {amjil/mgl-components
        {:git/url "https://github.com/amjil/mgl-components.git"
         :sha "YOUR_SHA"}}}
```

## Dependencies

This library requires:
- [ClojureDart](https://github.com/tensegritics/ClojureDart)
- [mongol](https://pub.dev/packages/mongol) - For Mongolian text rendering
- [mongol-virtual-keyboard](https://github.com/amjil/mongol-virtual-keyboard) - For virtual keyboard support

## Usage

### Basic Example

```clojure
(ns my-app.main
  (:require
   ["package:flutter/material.dart" :as m]
   [components.bottom-sheet :as bottom-sheet]
   [components.chip :as chip]))

(defn my-widget []
  (f/widget
   (m/Scaffold
    .body (m/Center
           .child (m/ElevatedButton
                   .onPressed (fn []
                               (bottom-sheet/bottom-sheet
                                context
                                [{:type :item
                                  :title "Option 1"
                                  :on-tap #(print "Selected 1")}]))
                   .child (m/Text "Show Bottom Sheet"))))))
```

### Using Design Tokens

```clojure
(ns my-app.main
  (:require
   [components.tokens :as tokens]))

(defn styled-widget []
  (m/Container
   .padding (m/EdgeInsets.all (tokens/space :m))
   .child (m/Text
           "Hello"
           .style (m/TextStyle
                   .fontSize (tokens/font-size :l)
                   .color (tokens/color :text-main)))))
```

## Example App

See the `example/` directory for a complete demonstration of all components. To run the example:

```bash
cd example
clj -M:cljd build
flutter run
```

## Component Documentation

### Bottom Sheet

A modal bottom sheet component with customizable height, border radius, and item rendering.

```clojure
(bottom-sheet/bottom-sheet
 context
 [{:type :item :title "Item 1" :on-tap #(print "tapped")}
  {:type :header :title "Section"}
  {:type :item :title "Item 2" :on-tap #(print "tapped 2")}]
 :height-factor 0.4
 :min-height 250.0
 :border-radius 28.0
 :show-handle? true)
```

### Chip

Filter chips with state management and haptic feedback support.

```clojure
(def state (atom {}))

(chip/filter-chip
 :chip-id "my-chip"
 "Label"
 state
 :haptic? true
 :max-select 3)
```

### Select

Dropdown selection component with grouping and theming support.

```clojure
(select/select
 context
 {:items [{:value "1" :label (m/Text "Option 1")}
          {:value "2" :label (m/Text "Option 2") :group "Group A"}]
  :value "1"
  :on-changed #(print "Selected:" %)})
```

### Text Field

Text input field component with vertical Mongolian text support, placeholder hints, and cursor positioning.

```clojure
(def controller (m/TextEditingController))

(text-field/text-field
 {:controller controller
  :hint "Enter text"
  :on-changed #(print "Text changed:" %)
  :max-lines 1
  :autofocus true})
```

### Toast

Toast notification component with multiple types and animation support.

```clojure
;; Success toast
(toast/success context "Operation successful!")

;; Error toast (manual close)
(toast/error context "An error occurred")

;; Warning toast
(toast/warn context "Please note")

;; Info toast
(toast/info context "Information")

;; Custom toast
(toast/show context "Custom message"
            :type :success
            :pos st/StyledToastPosition.bottom
            :anim :slide-right
            :dur 5
            :manual-close? false)
```

### Text

Vertical Mongolian text display component with focus highlighting and tap support.

```clojure
(text/text-block
 {:text "Mongolian text"
  :is-focused true
  :on-tap #(print "Text tapped")
  :style (m/TextStyle .fontSize 18 .color m/Colors.black)})
```

### Layout

Row-first layout container for arranging side-by-side content.

```clojure
(layout/row-layout
 {:main-row (m/Container .child (m/Text "Main content"))
  :side-row (m/Container .child (m/Text "Sidebar"))
  :side-row-position :left})
```

## Design Tokens

The library includes a comprehensive set of design tokens:

- **Spacing**: `:xs`, `:s`, `:m`, `:l`, `:xl`
- **Font Sizes**: `:xl`, `:l`, `:m`, `:s`
- **Colors**: `:bg`, `:bg-focus`, `:text-main`, `:text-weak`, `:accent`

Access tokens using helper functions:
- `(tokens/space key)` - Get spacing value
- `(tokens/font-size key)` - Get font size
- `(tokens/color key)` - Get color value
- `(tokens/line-height font-size)` - Calculate line height

## Development

### Building

```bash
clj -M:cljd build
```

### Running Tests

```bash
cd example
flutter test
```

## License

MIT License

Copyright (c) 2024 amjil

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- Built with [ClojureDart](https://github.com/tensegritics/ClojureDart)
- Mongolian text support via [mongol](https://pub.dev/packages/mongol) package
