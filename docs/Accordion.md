### Accordion

Accordion component built on top of `@radix-ui/react-accordion`. It exposes the Radix Root and subcomponents with themeable styles and small conveniences (e.g., `asChild` default on Trigger).

See Radix docs: https://www.radix-ui.com/primitives/docs/components/accordion

#### Import and basic usage

```tsx
import React from "react";
import {Accordion, AccordionItem, AccordionHeader, AccordionTrigger, AccordionContent} from "addon-ui";

export function Example() {
    return (
        <div style={{display: "grid", gap: 12}}>
            {/* Single (one panel open at a time) */}
            <Accordion type="single" collapsible defaultValue="item-1">
                <AccordionItem value="item-1">
                    <AccordionHeader>
                        <AccordionTrigger>General</AccordionTrigger>
                    </AccordionHeader>
                    <AccordionContent>
                        <div style={{padding: 12}}>General content</div>
                    </AccordionContent>
                </AccordionItem>

                <AccordionItem value="item-2">
                    <AccordionHeader>
                        <AccordionTrigger>Advanced</AccordionTrigger>
                    </AccordionHeader>
                    <AccordionContent>
                        <div style={{padding: 12}}>Advanced content</div>
                    </AccordionContent>
                </AccordionItem>
            </Accordion>

            {/* Multiple (several panels can be open) */}
            <Accordion type="multiple" defaultValue={["a"]}>
                <AccordionItem value="a">
                    <AccordionHeader>
                        <AccordionTrigger>Section A</AccordionTrigger>
                    </AccordionHeader>
                    <AccordionContent>
                        <div style={{padding: 12}}>A content</div>
                    </AccordionContent>
                </AccordionItem>
                <AccordionItem value="b">
                    <AccordionHeader>
                        <AccordionTrigger>Section B</AccordionTrigger>
                    </AccordionHeader>
                    <AccordionContent>
                        <div style={{padding: 12}}>B content</div>
                    </AccordionContent>
                </AccordionItem>
            </Accordion>
        </div>
    );
}
```

---

#### Props: Accordion (root)

Only the prop name, type, and default are listed below.

| Prop             | Type                                             | Default |
| ---------------- | ------------------------------------------------ | ------- |
| Radix Root props | `AccordionSingleProps \| AccordionMultipleProps` | —       |

Notes:

- The root component is a thin wrapper around Radix `Root` and accepts all Radix props for single or multiple mode.

#### Props: AccordionItem

| Prop             | Type                 | Default |
| ---------------- | -------------------- | ------- |
| Radix Item props | `AccordionItemProps` | —       |

#### Props: AccordionHeader

| Prop               | Type                   | Default |
| ------------------ | ---------------------- | ------- |
| Radix Header props | `AccordionHeaderProps` | —       |

#### Props: AccordionTrigger

| Prop                | Type                    | Default |
| ------------------- | ----------------------- | ------- |
| `asChild`           | `boolean`               | `true`  |
| Radix Trigger props | `AccordionTriggerProps` | —       |

#### Props: AccordionContent

| Prop                | Type                    | Default |
| ------------------- | ----------------------- | ------- |
| Radix Content props | `AccordionContentProps` | —       |

---

### CSS variables for Accordion

Only variables actually referenced in `src/components/Accordion/accordion.module.scss` are listed, with their exact fallback chains. Variables provided by Radix are noted separately.

| Variable                             | Fallback chain                                                           |
| ------------------------------------ | ------------------------------------------------------------------------ |
| `--accordion-header-pading`          | `var(--accordion-header-pading)` (none)                                  |
| `--accordion-header-bg-color`        | `var(--accordion-header-bg-color, var(--bg-primary-color))`              |
| `--accordion-header-hover-bg-color`  | `var(--accordion-header-hover-bg-color)` (none)                          |
| `--accordion-content-bg-color`       | `var(--accordion-content-bg-color)` (none)                               |
| `--accordion-speed-bg`               | `var(--accordion-speed-bg, var(--speed-color))`                          |
| `--accordion-speed-animation`        | `var(--accordion-speed-animation, var(--speed-sm))`                      |
| `--radix-collapsible-content-height` | `var(--radix-collapsible-content-height)` (provided by Radix at runtime) |

Notes:

- The variable name `--accordion-header-pading` is intentionally spelled exactly as in the stylesheet.
- Transitions and animations use component-scoped speed variables (`--accordion-speed-*`) with fallbacks to global tokens like `--speed-sm` and `--speed-color`.

---

### Accessibility (A11y)

- Built on Radix Accordion, inheriting correct roles, aria attributes, and keyboard interaction (Arrow Up/Down to move focus, Enter/Space to toggle).
- Use `type="single"` with `collapsible` to allow closing the currently open item; without `collapsible`, one item stays open at all times.

Radix reference: https://www.radix-ui.com/primitives/docs/components/accordion

---

### Usage notes

- Header background/hover styles are controlled with `--accordion-header-bg-color` and `--accordion-header-hover-bg-color`.
- Content open/close uses CSS keyframe animations that rely on Radix’s `--radix-collapsible-content-height` variable.
- You can wrap your own element as the trigger thanks to `asChild` defaulting to `true` on `AccordionTrigger`.
