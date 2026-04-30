# MCP UI DSL — Changelog

## [1.3.1]

### Templates ([`09_Templates.md`](1.3/09_Templates.md))

- Rename template body field `body` → `content` for consistency with page-level `content`.
- Remove legacy inline-`name` definition form. Templates declare exclusively in the **map-key form** (`templates: { name: { ... } }`).
- Remove legacy invocation aliases. The `use` widget is the sole canonical invocation type; `template` / `useTemplate` are no longer accepted. `params` is the sole canonical field name; `arguments` / `overrides` are no longer accepted.

### Theme ([`05_Theme.md`](1.3/05_Theme.md) §5.3.6)

- Define mode-specific fallback policy for sparse `theme` blocks. A bundle that omits the `theme` block entirely MUST resolve to the M3 default **dark** scheme under dark host brightness (rather than re-tagging the light scheme). Common-only `theme.color` (no `light`/`dark` variant) MUST apply to both modes unchanged.

### Schema / generated artifacts

- `schema/widgets.schema.json`, `generated/widgets.md`, `generated/llm_prompt_card.md` regenerated from the updated `widgets/utility/use.yaml` (aliases removed).

---

## [1.3] — Modern Theme System

Adopts a modern design-system standard (Material 3 + DTCG + shadcn-style + HCT seed) as canonical. No legacy aliases.

### Theme spec rewrite ([`05_Theme.md`](1.3/05_Theme.md))

- **Color (28 + 6 semantic)** — Material 3 28 roles (primary / primaryContainer / onPrimaryContainer / secondary / secondaryContainer / tertiary / tertiaryContainer / error / errorContainer / surface / surfaceVariant / surfaceTint / background / outline / outlineVariant / inverseSurface / inverseOnSurface / inversePrimary / scrim / shadow plus each on*) plus 6 semantic (success / warning / info plus on*) plus state-layer opacity plus HCT seed auto-derivation.
- **Typography (15 roles)** — Material 3 naming (display / headline / title / body / label × Large/Medium/Small). Earlier names `headline1-6`, `subtitle1/2`, `body1/2`, `caption`, `button`, `overline` are removed.
- **Spacing (9 slots)** — `xxs / xs / sm / md / lg / xl / 2xl / 3xl / 4xl` (8pt grid) plus 4 layout primitives (screenPadding / cardPadding / sectionGap / inlineGap). Earlier `small / medium / large` naming removed.
- **Shape (M3 7 family)** — `none / extraSmall / small / medium / large / extraLarge / full` plus per-corner override (topStart / topEnd / bottomStart / bottomEnd, RTL-aware). `borderRadius` naming removed.
- **Elevation (M3 6 levels)** — `level0`–`level5` (0 / 1 / 3 / 6 / 8 / 12) plus tonal surface (shadow / tint separated). Earlier `small / medium / large` naming removed.
- **New domains** — Motion (M3 13 durations + 4 easings), Density (3-step), Breakpoints (5-class), Border (5 width aliases), Opacity (M3 11-step), FocusRing, Z-index (9 layers), Component tokens (button / input / card / dialog / menu / list).
- **DTCG W3C JSON interchange** — export/import compatible with Tokens Studio, Style Dictionary, and Claude Design ([`05b_DTCG_Interchange.md`](1.3/05b_DTCG_Interchange.md)).
- **3-tier token model** — reference / alias / component ([`05a_Tokens_Reference.md`](1.3/05a_Tokens_Reference.md)).

### Conformance ([`18_Conformance.md`](1.3/18_Conformance.md) §18.2.7)

- MUST — light/dark/system mode, M3 28 color roles, M3 15 typography, 9 spacing, 7 shape, 6 elevation, `theme.*` binding plus page override (deep merge), DTCG JSON import (9 categories).
- SHOULD — HCT seed auto-derivation, state layer, DTCG export, Motion, Density, Breakpoints, Border, Opacity, FocusRing, Z-index, 6 standard components.
- MAY — additional spacing slots, custom components / semantic roles.

### Schema

- New [`schema/theme.schema.json`](1.3/schema/theme.schema.json) — JSON Schema 2020-12, all 14 token domains covered.

### Migration

- All earlier-draft names (h1-h6, headline1-6, subtitle1/2, button, overline, textOnPrimary, divider, borderRadius, spacing.small, etc.) are removed in 1.3. No legacy reader is provided.
- Mapping table: see [`05_Theme.md`](1.3/05_Theme.md) §5.17.

### Other 1.3 additions

- Stateful templates (`stateDefaults` on template definitions).
- Template lifecycle hooks (`onMount`, `onUnmount`).
- Remote template libraries (`templateLibraries` with `bundle://` or `https://` URIs).
- Dashboard rendering mode (`dashboard` field on ApplicationDefinition).
- Canvas widget (drawing commands: `rect`, `circle`, `arc`, `line`, `path`, `text`, `image`).
- Opacity widget (with implicit animation).
- Transform widget (scale / rotate / translate with implicit animation).
- `openApp` navigation action (dashboard → full app transition).
- `exitApp` navigation action (host-inserted close button on root route).

---

## [1.2]

- ApplicationDefinition metadata fields: `id`, `description`, `icon`, `splash`, `category`, `publisher`, `timestamps`, `screenshots`.
- `TimestampInfo` structured type for creation / update timestamps.
- Well-known resource `ui://app/info` for lightweight metadata retrieval.
- `bundle://` URI scheme for referencing bundle-internal assets.
- Bundle serving: read / write adapters implementing the UI port.
- Online serving path (MCP server transparent to client) and local serving path (direct bundle load).
- `PublisherInfo`, `SplashConfig` types.

---

## [1.1]

- Client-side resources: `client.selectFile`, `client.readFile`, `client.writeFile`, `client.saveFile`, `client.listFiles`.
- Client network: `client.httpRequest`.
- Client system: `client.getSystemInfo`, `client.clipboard`, `client.exec`.
- Client notifications: `client.notification`.
- Permission system: file / network / system permissions with trust levels.
- Client data bindings: `client.workingDirectory`, `client.userName`, `client.platform`, `client.locale`, `client.theme.*`, `client.env.*`, `client.file.*`, `client.system.*`.
- Bidirectional channels: `client.watchFile`, `client.watchDirectory`, `client.systemMonitor`, `client.poll` with lifecycle management.
- Enhanced image widget with `client://` path and fallback URL.
- Parallel / sequence / cancel actions.
- `permission.revoke` action.
- `resources.*` binding prefix.
- Template system (static): parameters, slots, scoped styles.
- Responsive layout: breakpoints, MediaQuery, platform detection.
- Event propagation: capture / target / bubble phases, stopPropagation, delegation.
- Plugin system with lifecycle hooks.
- Offline queue and sync with conflict resolution strategies.
- Animation extensions: page transitions, shared element transitions, physics-based.
- Validation system: required, minLength / maxLength, pattern, email, match, async.

---

## [1.0]

Initial public release.

- Application / Page definition structure.
- Multi-page routing with parameterized routes (`route.params.*`).
- 40+ widget types across 8 categories.
- Unified `linear` layout replacing row / column.
- Data binding with expression language (variables, operators, conditionals, functions).
- 16 built-in expression functions.
- Type coercion rules.
- List iteration context (`item`, `index`, `isFirst`, `isLast`, `isEven`, `isOdd`).
- Action system: state / navigation / tool / resource / dialog / batch / conditional / notification.
- Tool response auto-merge into state.
- Resource subscription: standard and extended modes.
- Theme system: light/dark/system, color scheme, typography, spacing, radius, elevation.
- Theme binding via `{{theme.*}}`.
- Page lifecycle: `onInit`, `onDestroy`.
- MCP protocol integration: `resources/read`, `tools/call`, subscriptions, notifications.
- Security: input validation, resource access verification, state isolation, expression sandboxing.
- Accessibility: roles, keyboard navigation, touch targets, live regions.
- Internationalization: `{{i18n.key}}`, runtime language switching.
