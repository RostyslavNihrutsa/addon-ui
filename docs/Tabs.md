# Tabs

Documentation for the Tabs component and its subcomponents: Tabs, TabsList, TabsTrigger, TabsContent. The implementation is built on top of @radix-ui/react-tabs and adds visual features (active tab indicator, rounded edges, badges, etc.).

See the official Radix documentation: https://www.radix-ui.com/primitives/docs/components/tabs

## Import

```ts
import {Tabs, TabsList, TabsTrigger, TabsContent} from "addon-ui";
```

## Quick example

```tsx
<Tabs defaultValue="general">
  <TabsList indicator roundedEdges>
    <TabsTrigger value="general" before={2}>General</TabsTrigger>
    <TabsTrigger value="advanced" after={"!"}>Advanced</TabsTrigger>
    <TabsTrigger value="about" disabled>About</TabsTrigger>
  </TabsList>

  <TabsContent value="general">General content</TabsContent>
  <TabsContent value="advanced">Advanced content</TabsContent>
  <TabsContent value="about">About content</TabsContent>
</Tabs>
```

---

## Components and API

### Tabs (root container)

A wrapper over Radix Tabs Root.

- Inherits all Radix `TabsProps` except `orientation`.
- Additional props:
  - `reverse?: boolean` — when true, changes the order: content on top, tab list on the bottom.

Supports contextual props via the UI provider: `useComponentProps("tabs")`.

Example:

```tsx
<Tabs defaultValue="tab1" reverse>
  ...
</Tabs>
```

### TabsList

A wrapper over Radix Tabs List. Renders the top/bottom tab switcher panel and the active tab indicator.

Props:

- All Radix `TabsListProps`.
- Additionally:
  - `separator?: boolean` (default `true`) — draws a separator line (at the bottom or at the top when `reverse`).
  - `indicator?: boolean` (default `true`) — toggles the active tab indicator.
  - `roundedEdges?: boolean` — rounds the left/right edge of the indicator.
  - `indicatorClassname?: string` — additional class name for the indicator element.

TabsList automatically measures the active trigger and smoothly moves the indicator using ResizeObserver and MutationObserver.

Supports contextual props: `useComponentProps("tabsList")`.

Examples:

```tsx
// Without the indicator
<TabsList indicator={false}>
  ...
</TabsList>

// Rounded indicator edges
<TabsList indicator roundedEdges />
```

### TabsTrigger

A wrapper over Radix Tabs Trigger. By default renders via `asChild` to keep your markup.

Props:

- All Radix `TabsTriggerProps`.
- Additionally:
  - `before?: number | string` — badge/label to the left of the text.
  - `after?: number | string` — badge/label to the right of the text.
  - `beforeClassname?: string` — extra class for the left badge.
  - `afterClassname?: string` — extra class for the right badge.
  - `asChild?: boolean` — defaults to `true`.

Supports contextual props: `useComponentProps("tabsTrigger")`.

Examples:

```tsx
<TabsTrigger value="inbox" before={12}>Inbox</TabsTrigger>
<TabsTrigger value="updates" after={"•"}>Updates</TabsTrigger>
```

### TabsContent

A wrapper over Radix Tabs Content. It doesn’t add extra props.

- Props type: `TabsContentProps` from `@radix-ui/react-tabs`.
- Supports contextual props: `useComponentProps("tabsContent")`.

Example:

```tsx
<TabsContent value="inbox">...</TabsContent>
```

---

## Styles and CSS variables

Below are the CSS variables used in the component styles (`src/components/Tabs/tabs.module.scss`). Values in parentheses are defaults.

- Tab list (`.tabs__list`):
  - `--tabs-list-border-width` (1px)
  - `--tabs-list-border-color` (var(--separator-color))

- Trigger (`.tabs__trigger`):
  - `--tabs-trigger-padding` (10px)
  - `--tabs-trigger-height` (40px)
  - `--tabs-trigger-font-size` (14px)
  - `--tabs-trigger-font-family` (var(--font-family))
  - `--tabs-trigger-font-weight` (400)
  - `--tabs-trigger-font-weight-active` (600)
  - `--tabs-trigger-color` (var(--text-primary-color))
  - `--tabs-trigger-dissabled-opacity` (0.6)
  - Badges on the trigger (`before`/`after`):
    - `--tabs-trigger-badge-min-width` (18px)
    - `--tabs-trigger-badge-font-size` (12px)
    - `--tabs-trigger-badge-font-weight` (700)
    - `--tabs-trigger-badge-padding` (2px 4px)
    - `--tabs-trigger-badge-radius` (4px)
    - `--tabs-trigger-badge-color` (var(--text-secondary-color))
    - `--tabs-trigger-badge-bg-color` (var(--bg-secondary-color))
    - `--tabs-trigger-badge-active-color` (white)
    - `--tabs-trigger-badge-active-bg-color` (var(--primary-color))
  - `--tabs-trigger-gap` (4px)

- Indicator (`.tabs__indicator`):
  - `--tabs-indicator-size` (4px)
  - `--tabs-indicator-color` (var(--primary-color))
  - `--tabs-indicator-radius` (10px)

- Misc:
  - Uses `--transition-speed-sm` for animations.

---

## Accessibility

Components inherit behavior and ARIA attributes from Radix Tabs: keyboard navigation, correct roles, and states. Avoid removing focus styles or disabling the indicator if it harms the visibility of the active tab.

Useful: https://www.radix-ui.com/primitives/docs/components/tabs

---

## Usage notes

- If you want the tab list at the bottom, use the `reverse` prop on `Tabs`.
- `TabsList` measures the active `TabsTrigger` and updates the indicator on window/container resize.
- Use `before`/`after` on `TabsTrigger` for counts/status badges.
