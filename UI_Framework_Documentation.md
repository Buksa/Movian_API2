
# UI Framework Documentation

## Overview

The UI Framework is a lightweight, flexible system for building graphical user interfaces, designed for embedded systems, media applications, or custom platforms. It provides a widget-based architecture for creating dynamic, responsive layouts with support for horizontal, vertical, and z-stacked arrangements. The framework handles layout constraints, rendering, and event handling, making it suitable for applications requiring smooth animations and interactive elements.

The framework is implemented in C for performance and portability, with a high-level scripting interface for defining UI structures declaratively. It supports features like dynamic sizing, weighted layouts, aspect ratio constraints, fade animations, and table-based layouts.

## Architecture

The framework is built around the following core concepts:

-   **Widgets**: The basic building blocks of the UI, each representing a visual or interactive element (e.g., containers, labels, buttons).
-   **Containers**: Special widgets that manage the layout of their child widgets (e.g., `container_x`, `container_y`, `container_z`).
-   **Constraints**: Rules that define a widget's size and position, including fixed sizes, weights, and aspect ratios.
-   **Render Context**: A structure (`glw_rctx_t`) that holds rendering parameters like width, height, alpha, and transformations.
-   **Signals**: Events that trigger updates (e.g., child creation, destruction, constraint changes).

### Key Components

-   **Widget Class (`glw_class_t`)**: Defines the behavior of a widget type, including layout, rendering, and signal handling.
-   **Widget Instance (`glw_t`)**: The base structure for all widgets, containing properties like flags, constraints, and parent/child relationships.
-   **Container (`glw_container_t`)**: A specialized widget for arranging children, with properties for padding, spacing, and layout mode.
-   **Table (`glw_table_t`)**: A widget for grid-like layouts, managing rows as containers.
-   **Render Context (`glw_rctx_t`)**: Manages rendering state, including dimensions, alpha, sharpness, and z-index.

## Widget Types

The framework provides several widget types, with the following being central to the provided code:

### 1. Horizontal Container (`container_x` / `hbox`)

-   **Purpose**: Arranges child widgets horizontally (left-to-right).
-   **Class Name**: `container_x` (alias: `hbox`).
-   **Key Features**:
    -   Supports fixed-width, weighted, and aspect ratio-based child sizing.
    -   Homogeneous mode (`GLW2_HOMOGENOUS`) ensures all children have the same width.
    -   Table mode (`tableMode`) integrates with `table` widgets for grid layouts.
    -   Adjustable padding and spacing.
-   **Usage in Script**:
    
    ```plaintext
    widget(container_x, {
      padding: [2em, 0];
      spacing: $view.width / 30;
      cloner(propWindow($self.nodes, 0, 3), loader, {
        width: $view.width / 6;
        source: "skin://items/rect/" + $self.type + ".view";
      });
    });
    
    ```
    
-   **C Implementation**:
    -   `glw_container_x_constraints`: Calculates total width and maximum height.
    -   `glw_container_x_layout`: Positions children horizontally, handling scaling and alignment.
    -   `glw_container_x_render`: Renders children with horizontal translations and scaling.

### 2. Vertical Container (`container_y` / `vbox`)

-   **Purpose**: Arranges child widgets vertically (top-to-bottom).
-   **Class Name**: `container_y` (alias: `vbox`).
-   **Key Features**:
    -   Supports fixed-height, weighted, and aspect ratio-based child sizing.
    -   Fade animations (`GLW2_AUTOFADE`) for smooth child visibility transitions.
    -   Adjustable padding and spacing.
-   **Usage in Script**:
    
    ```plaintext
    widget(list_y, {
      id: "scrollable";
      clipOffsetTop: 3em;
      scrollThresholdTop: 5em;
      spacing: 1em;
      cloner($self.model.nodes, container_y, {
        widget(label, {
          padding: [1em, 0];
          caption: fmt('%s <font size="2" color="#aaaaaa">- %s', ...);
        });
      });
    });
    
    ```
    
-   **C Implementation**:
    -   `glw_container_y_constraints`: Calculates total height and maximum width.
    -   `glw_container_y_layout`: Positions children vertically, supporting fade animations.
    -   `glw_container_y_render`: Renders children with vertical translations and fade effects.

### 3. Z-Stacked Container (`container_z` / `zbox`)

-   **Purpose**: Stacks child widgets along the z-axis (overlapping layers).
-   **Class Name**: `container_z` (alias: `zbox`).
-   **Key Features**:
    -   Copies constraints from the first non-hidden child with constraints.
    -   Renders children in order of z-index.
-   **Usage in Script**:
    
    ```plaintext
    widget(container_z, {
      widget(list_y, { ... });
      widget(container_y, {
        align: top;
        PageHeader($self.model.metadata.title);
      });
    });
    
    ```
    
-   **C Implementation**:
    -   `glw_container_z_constraints`: Copies constraints from a child.
    -   `glw_container_z_layout`: Lays out children in the same position.
    -   `glw_container_z_render`: Renders children with increasing z-index.

### 4. Table (`table`)

-   **Purpose**: Manages a grid layout where rows are containers.
-   **Class Name**: `table`.
-   **Key Features**:
    -   Dynamically calculates column widths based on row containers.
    -   Integrates with `container_x` in `tableMode`.
-   **Usage in Script**: Not directly used in the provided script, but referenced via `tableMode`.
-   **C Implementation**:
    -   `table_recompute`: Calculates column widths and total width.
    -   `glw_table_callback`: Handles constraint changes from rows.

## Core Functionality

### Constraints System

Widgets specify their size requirements using constraints:

-   **Fixed Size** (`GLW_CONSTRAINT_X`, `GLW_CONSTRAINT_Y`): Explicit width or height (e.g., `glw_req_width`, `glw_req_height`).
-   **Weight** (`GLW_CONSTRAINT_W` with `glw_req_weight > 0`): Proportional allocation of remaining space.
-   **Aspect Ratio** (`GLW_CONSTRAINT_W` with `glw_req_weight < 0`): Width or height based on the other dimension (e.g., `width = height * -weight`).

Containers compute their size by aggregating child constraints, accounting for padding and spacing.

### Layout

Each container type has a layout function that positions its children:

-   **Horizontal**: Distributes width among children, respecting fixed sizes, weights, and aspect ratios.
-   **Vertical**: Distributes height, with optional fade animations for visibility changes.
-   **Z-Stacked**: Overlaps children, using z-index to determine rendering order.

### Rendering

Rendering applies transformations (position, scale, alpha) to each child:

-   **Alpha**: Combines widget and render context alpha (`rc_alpha * w->glw_alpha`).
-   **Sharpness**: Affects visual clarity (`rc_sharpness * w->glw_sharpness`).
-   **Transformations**: Uses `glw_Translatef` and `glw_Scalef` for positioning and scaling.

### Event Handling

The framework uses a signal-based system to handle events:

-   **Child Events**: `GLW_SIGNAL_CHILD_CONSTRAINTS_CHANGED`, `GLW_SIGNAL_CHILD_CREATED`, `GLW_SIGNAL_CHILD_DESTROYED`, etc., trigger constraint recalculation.
-   **Navigation**: `glw_navigate_horizontal` and `glw_navigate_vertical` handle focus movement.
-   **Destruction**: Cleans up resources (e.g., freeing column widths).

## Scripting Interface

The framework includes a high-level scripting language for defining UI layouts declaratively. The script uses a syntax similar to JSON or a domain-specific language, with the following features:

-   **Widget Declaration**: `widget(type, { properties })` creates a widget of the specified type.
-   **Properties**: Key-value pairs for configuring widgets (e.g., `padding`, `spacing`, `caption`).
-   **Cloners**: `cloner(data, container, { ... })` generates multiple widgets from a data source.
-   **Event Handlers**: `onEvent(event, action)` binds actions to events (e.g., `onEvent(activate, navOpen($self.url))`).

### Example Script

```plaintext
widget(container_z, {
  widget(list_y, {
    id: "scrollable";
    clipOffsetTop: 3em;
    scrollThresholdTop: 5em;
    spacing: 1em;
    cloner($self.model.nodes, container_y, {
      widget(label, {
        padding: [1em, 0];
        caption: fmt('%s <font size="2" color="#aaaaaa">- %s', ...);
      });
      widget(container_x, {
        padding: [2em, 0];
        spacing: $view.width / 30;
        cloner(propWindow($self.nodes, 0, 3), loader, {
          width: $view.width / 6;
          source: "skin://items/rect/" + $self.type + ".view";
        });
      });
    });
  });
  widget(container_y, {
    align: top;
    PageHeader($self.model.metadata.title);
  });
});

```

This script creates a scrollable list with a header, where each list item contains a label and a horizontal grid of up to three items.

## Usage Guide

### Creating a Widget

1.  **Define the Widget Type**: Use a registered class (e.g., `container_x`, `container_y`).
2.  **Set Properties**:
    -   `padding: [left, top, right, bottom]` (e.g., `[1em, 0, 1em, 0]`).
    -   `spacing: value` (e.g., `1em` for space between children).
    -   `align: position` (e.g., `top`, `center`, `bottom` for `container_y`).
3.  **Add Children**: Nest `widget` calls or use `cloner` for dynamic lists.
4.  **Handle Events**: Use `focusable: true` and `onEvent` for interactivity.

### Configuring Layout

-   **Fixed Sizes**: Set explicit widths or heights in child widgets.
-   **Weighted Layout**: Use `weight` to distribute remaining space (e.g., `glw_req_weight = 1.0`).
-   **Aspect Ratios**: Set negative weights for aspect-constrained children (e.g., `glw_req_weight = -2.0` for width = 2 * height).
-   **Homogeneous Mode**: Enable `GLW2_HOMOGENOUS` for uniform child sizes in `container_x`.

### Rendering and Animations

-   **Fade Animations**: Enable `GLW2_AUTOFADE` in `container_y` for smooth child visibility transitions.
-   **Clipping**: Use properties like `clipOffsetTop`, `clipAlpha`, and `clipBlur` (handled by higher-level framework code).
-   **Custom Styles**: Apply styles like `GridItemBevel()` or `GridItemHighlight()` for visual effects.

### Table Layouts

-   Enable `tableMode: true` in a `container_x` to integrate with a `table` widget.
-   Define rows as containers, with each container specifying column widths.

## API Reference

### Core Structures

-   **`glw_t`**:
    -   `glw_flags`: Visibility and state flags (e.g., `GLW_HIDDEN`, `GLW_RETIRED`).
    -   `glw_flags2`: Additional flags (e.g., `GLW2_DEBUG`, `GLW2_HOMOGENOUS`, `GLW2_AUTOFADE`).
    -   `glw_alpha`: Widget opacity.
    -   `glw_sharpness`: Visual clarity factor.
    -   `glw_childs`: Queue of child widgets.
-   **`glw_container_t`**:
    -   `co_padding[4]`: Padding for left, top, right, bottom.
    -   `co_spacing`: Spacing between children.
    -   `co_num_columns`: Number of columns (in table mode).
    -   `co_table`: Parent table (if in table mode).
-   **`glw_table_t`**:
    -   `gt_columns`: Array of column widths.
    -   `gt_num_columns`: Number of columns.
    -   `gt_rows`: Linked list of row containers.

### Key Functions

-   **`glw_set_constraints(w, width, height, weight, flags)`**: Sets widget constraints.
-   **`glw_layout0(w, rc)`**: Lays out a widget in the given render context.
-   **`glw_render0(w, rc)`**: Renders a widget.
-   **`glw_need_refresh(root, 0)`**: Marks the UI for refresh.
-   **`glw_signal0(w, signal, extra)`**: Sends a signal to a widget.

### Signals

-   `GLW_SIGNAL_CHILD_CONSTRAINTS_CHANGED`: Child constraints changed.
-   `GLW_SIGNAL_CHILD_CREATED`: New child added.
-   `GLW_SIGNAL_CHILD_DESTROYED`: Child removed.
-   `GLW_SIGNAL_CHILD_HIDDEN` / `GLW_SIGNAL_CHILD_UNHIDDEN`: Child visibility changed.
-   `GLW_SIGNAL_DESTROY`: Widget destroyed.

## Best Practices

-   **Optimize Constraints**: Minimize fixed-size children to allow flexible layouts.
-   **Use Cloners for Lists**: Leverage `cloner` for dynamic content to reduce script complexity.
-   **Enable Animations Sparingly**: Use `GLW2_AUTOFADE` only when needed to avoid performance overhead.
-   **Debugging**: Enable `GLW2_DEBUG` for layout diagnostics, but disable in production.
-   **Modularize Scripts**: Break complex UIs into reusable widget definitions.

## Limitations

-   **No Built-in Clipping**: Clipping properties (e.g., `clipAlpha`) require additional framework code.
-   **Limited Z-Stack Constraints**: `container_z` relies on child constraints, which may limit flexibility.
-   **Table Mode Complexity**: Requires careful management of row and column constraints.

## Example Application

To create a media gallery UI:

1.  Use a `container_z` as the root.
2.  Add a `list_y` for a scrollable list of categories.
3.  For each category, use a `container_y` with a `label` (title) and a `container_x` (grid of items).
4.  Use `cloner` to populate the grid with items from a data source.
5.  Add a `focusable` "Show more" button to navigate to additional content.

This structure is demonstrated in the provided widget code, which creates a scrollable list with grid rows and interactive elements.

## Conclusion

The UI Framework provides a robust foundation for building dynamic, interactive user interfaces. Its widget-based architecture, constraint system, and scripting interface enable developers to create responsive layouts with minimal code. By leveraging containers, tables, and animations, developers can build complex UIs for a variety of applications.

For further details, refer to the source code or contact the framework maintainers at [andreas@lonelycoder.com](mailto:andreas@lonelycoder.com).
