# 14. Responsive Layout and Events

**Status:** Normative.
This section defines how UI definitions adapt to viewport size, orientation, and host platform, and how user-interaction events propagate through the widget tree.

Responsive properties and event propagation are part of the Core Profile. See [`18_Conformance.md`](18_Conformance.md).

---

## 14.1 Breakpoints

A breakpoint is a named minimum-width threshold. The runtime selects the matching value for any responsive property based on the current viewport width.

### 14.1.1 Default Breakpoints

| Label | Min width (dp) | Typical device |
|-------|----------------|----------------|
| `xs` | 0 | Phone, portrait |
| `sm` | 600 | Phone landscape, small tablet |
| `md` | 900 | Tablet |
| `lg` | 1200 | Desktop |
| `xl` | 1536 | Wide desktop |

Each label represents a minimum width. A viewport of 1024 dp matches `md` (≥ 900 and < 1200).

### 14.1.2 Custom Breakpoints

An application MAY override breakpoints via `theme.breakpoints` or an application-level `breakpoints` field:

```json
{
  "type": "application",
  "breakpoints": {
    "xs": 0,
    "sm": 600,
    "md": 900,
    "lg": 1280,
    "xl": 1920
  }
}
```

Custom labels (e.g., `mobile`, `tablet`, `desktop`) MAY be added; they become valid keys in responsive property objects.

### 14.1.3 Current Breakpoint Binding

`{{runtime.breakpoint}}` resolves to the active breakpoint label (`"xs"`, `"sm"`, `"md"`, `"lg"`, or `"xl"`, or a custom label).

---

## 14.2 Responsive Property Values

Any property MAY accept a **responsive object** — a JSON object whose keys are breakpoint labels and whose values are the property's normal type:

```json
{
  "type": "text",
  "text": "Hello",
  "style": {
    "fontSize": { "xs": 14, "sm": 16, "md": 18, "lg": 20, "xl": 24 }
  }
}
```

### 14.2.1 Resolution Rule

1. Find all breakpoint keys in the responsive object whose minimum width is ≤ current viewport width.
2. Pick the value of the largest matching breakpoint.
3. If no breakpoint matches (viewport smaller than the smallest), use the smallest defined breakpoint's value.
4. A `default` key MAY be used as a fallback for any unmatched case.

```json
{ "columns": { "default": 1, "sm": 2, "md": 3, "lg": 4 } }
```

### 14.2.2 Where Responsive Objects Are Accepted

Responsive objects are accepted on any numeric, string, or enum property. Non-scalar properties (children, actions, widget subtrees) are resolved via the `mediaQuery` widget (§14.3), not via responsive objects.

---

## 14.3 MediaQuery Widget

`mediaQuery` chooses between widget subtrees based on viewport characteristics.

```json
{
  "type": "mediaQuery",
  "condition": { "minWidth": 900 },
  "then": {
    "type": "linear",
    "direction": "horizontal",
    "children": [
      { "type": "box", "flex": 1, "child": { "type": "text", "text": "Sidebar" } },
      { "type": "box", "flex": 3, "child": { "type": "text", "text": "Main" } }
    ]
  },
  "else": {
    "type": "linear",
    "direction": "vertical",
    "children": [
      { "type": "text", "text": "Main" },
      { "type": "text", "text": "Sidebar" }
    ]
  }
}
```

### 14.3.1 Condition Properties

| Property | Type | Description |
|----------|------|-------------|
| `minWidth` | number (dp) | Matches when viewport width ≥ value |
| `maxWidth` | number (dp) | Matches when viewport width ≤ value |
| `minHeight` | number (dp) | Matches when viewport height ≥ value |
| `maxHeight` | number (dp) | Matches when viewport height ≤ value |
| `orientation` | `"portrait"` \| `"landscape"` | Matches current device orientation |
| `platform` | platform string | Matches the host platform (see §14.5) |
| `breakpoint` | breakpoint label | Matches when the current breakpoint equals the value |

Multiple conditions combine with AND. Pass `then` and `else` for the branching subtrees.

### 14.3.2 Lifecycle

`mediaQuery` re-evaluates its condition on every viewport change (resize, rotation). The subtree is swapped atomically; local state in the discarded subtree is disposed per state-isolation rules.

---

## 14.4 Orientation

`{{runtime.orientation}}` resolves to `"portrait"` or `"landscape"`.

### 14.4.1 Page-Level Hooks

A page MAY declare an `onOrientationChange` action, fired whenever orientation changes:

```json
{
  "type": "page",
  "onOrientationChange": {
    "type": "state",
    "action": "set",
    "binding": "layoutMode",
    "value": "{{runtime.orientation}}"
  }
}
```

### 14.4.2 Orientation Lock

A page MAY request an orientation lock via `lockOrientation`:

| Value | Meaning |
|-------|---------|
| `portrait` | Lock to portrait |
| `landscape` | Lock to landscape |
| `any` | Allow all orientations (default) |

Runtimes MAY ignore the lock on platforms that do not support programmatic orientation control (desktop, web).

### 14.4.3 Re-Evaluation

On orientation change, all responsive properties and `mediaQuery` conditions that reference orientation re-evaluate and their subtrees re-render.

---

## 14.5 Platform Detection

`{{runtime.platform}}` resolves to one of:

| Value | Host |
|-------|------|
| `macos` | macOS |
| `linux` | Linux |
| `windows` | Windows |
| `ios` | iOS |
| `android` | Android |
| `web` | Browser / web runtime |

Grouped aliases accepted in `mediaQuery.condition.platform`:

| Alias | Expands to |
|-------|------------|
| `mobile` | `ios`, `android` |
| `desktop` | `macos`, `linux`, `windows` |
| `apple` | `macos`, `ios` |

---

## 14.6 Event Propagation Phases

Events propagate through three phases, modeled on the DOM event model:

| Phase | Direction | Purpose |
|-------|-----------|---------|
| `capture` | Root → target | Ancestors observe the event before it reaches the target |
| `target` | At target | The target widget's handler fires |
| `bubble` | Target → root | Ancestors observe the event after the target handles it |

Default behavior: events fire in the `target` phase, then bubble up. Capture handlers fire only if explicitly registered.

### 14.6.1 Stop Propagation

A handler MAY halt further traversal:

```json
{
  "type": "box",
  "onTap": {
    "type": "state",
    "action": "set",
    "binding": "selected",
    "value": "{{item.id}}",
    "propagation": "stop"
  }
}
```

| `propagation` value | Effect |
|---------------------|--------|
| `continue` | Default. Event continues to bubble |
| `stop` | Halts traversal after this handler |
| `stopImmediate` | Halts traversal and prevents other handlers on the same widget from firing |

---

## 14.7 Event Delegation

A parent widget MAY register a delegated handler that fires for descendants matching a selector:

```json
{
  "type": "list",
  "items": "{{items}}",
  "delegate": true,
  "onTap": {
    "type": "state",
    "action": "set",
    "binding": "selectedItem",
    "value": "{{event.target.id}}"
  },
  "itemTemplate": { "type": "listItem", "label": "{{item.name}}" }
}
```

With `delegate: true`, the parent's `onTap` fires whenever any descendant emits a tap event. The original target is available at `{{event.target}}`.

### 14.7.1 Selector Form

Delegation MAY narrow by selector:

```json
{ "onTap": { "delegate": "button[data-action]", "action": { } } }
```

Selectors follow the subset defined by the runtime (at minimum: widget type, `id`, and data-attribute presence).

---

## 14.8 Custom Events

Widgets MAY emit custom events via the `event` action:

```json
{
  "type": "button",
  "label": "Select",
  "onTap": {
    "type": "event",
    "action": "emit",
    "name": "itemSelected",
    "data": "{{item}}",
    "bubble": true
  }
}
```

Ancestors subscribe via the `on` property:

```json
{
  "type": "box",
  "on": {
    "itemSelected": {
      "type": "state",
      "action": "set",
      "binding": "selected",
      "value": "{{event.data}}"
    }
  }
}
```

### 14.8.1 Event Filters

A subscription MAY include a `when` condition. The handler fires only when the condition resolves truthy:

```json
{
  "on": {
    "itemSelected": {
      "when": "{{event.data.category === 'electronics'}}",
      "action": {
        "type": "state",
        "action": "set",
        "binding": "selectedElectronics",
        "value": "{{event.data}}"
      }
    }
  }
}
```

### 14.8.2 Application Event Bus

Emitting with `bubble: true` and no matching ancestor handler propagates to the application event bus. Any subscriber anywhere in the tree receives the event.

---

## 14.9 Event Naming

See [`17_Naming.md`](17_Naming.md) §17.1.4 — event-name strings use camelCase (`change`, `tap`, `longPress`, `itemSelected`); callback properties use `on` + PascalCase (`onChange`, `onTap`, `onLongPress`).

Legacy kebab-case event-name strings (`long-press`, `double-click`, `value-change`) are accepted per [`17_Naming.md`](17_Naming.md) §17.3.3.

---

## 14.10 Event Object Shape

Inside any event handler, `{{event}}` resolves to:

| Field | Type | Description |
|-------|------|-------------|
| `event.type` | string | Event-name string (e.g., `"tap"`, `"change"`) |
| `event.target` | object | The widget that originated the event (id, type, data attributes) |
| `event.currentTarget` | object | The widget whose handler is currently executing |
| `event.phase` | string | `"capture"`, `"target"`, or `"bubble"` |
| `event.data` | any | Handler-specific payload (new value for `onChange`, dragged item for `onDrop`, custom data for emitted events) |
| `event.timestamp` | number | Milliseconds since the runtime started |

---

## 14.11 Conformance

Core Profile runtimes MUST:

- Resolve responsive property values per §14.2.1.
- Render the `mediaQuery` widget with all condition properties listed in §14.3.1.
- Expose `{{runtime.orientation}}`, `{{runtime.platform}}`, and `{{runtime.breakpoint}}` bindings.
- Dispatch events through capture → target → bubble phases and honor `propagation: "stop"` / `"stopImmediate"`.
- Fire delegated handlers per §14.7 when `delegate: true` is set.
- Accept both canonical and legacy event-name spellings per [`17_Naming.md`](17_Naming.md) §17.3.3.

Core Profile runtimes SHOULD:

- Honor `lockOrientation` where the host platform supports orientation control.
- Implement the application event bus (§14.8.2).
- Accept custom breakpoint labels defined in `application.breakpoints` or `theme.breakpoints`.
