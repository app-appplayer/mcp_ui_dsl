# MCP UI DSL — Changelog

## [1.4.0]

### New — 23 widgets, 20 aliases, 21 properties, 13 enums

A no-code builder was aligned to emit this DSL directly and reported what it had declared and could not publish: 108 palette components, 29 publishable, and of the 79-component gap, **58 had no name in this spec**. Everything below comes from that list, plus a scan that found string properties documenting their allowed values in prose rather than declaring them.

The classification matters more than the count, so it is stated: **21 were the same widget under another name** (aliases, §17.3.1) · **4 were already expressible** and blocked only by name mapping (`EmailInput`/`URLInput`/`PhoneInput` are `textInput.inputType`; `PasswordInput` is `obscureText`) · **8 needed properties, not widgets** · **23 were genuinely absent** · **6 were declined**.

**New Core widgets** — `fileInput`, `multiSelect`, `combobox`, `otpInput`, `dateTimePicker`, `accordion`, `popover`, `menu`, `contextMenu`, `breadcrumb`, `pagination`, `link`.

Two were kept separate rather than folded into flags on existing widgets. `multiSelect` is not `select.multiple` because the bound value changes shape — scalar to array — and a flag that silently changes the type of what lands in state is something an author discovers at runtime. `combobox` is an input rather than a `select` variant because its defining property is that a value *outside* the option list is legal.

**New Advanced widgets** — `qrCode`, `barcode`, `pdfViewer`, `diffViewer`, `richTextEditor`, `splitter`, `resizable`, `kanban`, `gantt`, `spreadsheet`. Required only at Advanced v1.4+ (§18.5.2), so a runtime claiming Advanced at v1.0–v1.3 is unaffected.

The three board-shaped ones are widgets rather than compositions for reasons worth recording. `kanban`: drop targets are the gaps *between* cards, not the cards, and a drop must report where in the destination it landed — a composition gets a board that looks right and reorders wrongly. `gantt`: bars are positioned by time, so row and header must share one scale through zoom and scroll. `spreadsheet`: the unit is a cell with a coordinate, not a record with fields, which is why it cannot be a mode of `dataTable`. All three report *intent* (`onCardMove`, `onTaskChange`, `onChange`) and leave application to the author, so a server-rejected move is never already applied on screen.

`richTextEditor` binds **HTML** (or Markdown). An editor's value format is a contract every consumer of the document inherits; a proprietary delta model would leave the content unreadable to anything but the editor that produced it. §7.5 sanitisation applies on the way in and out.

`spreadsheet` formulas evaluate under the §7.1 sandbox or not at all — a runtime that cannot meet it renders the last computed value instead. A cell that runs arbitrary text is the one place this widget could become an injection surface.

**New Client widget** — `voiceInput` (§18.3.3a). It sits on the far side of the line `fileInput` defines: picking a file is one act of choosing and the choosing is the consent, while a microphone is a continuous capture of the room. Denial, no device, and transcription failure all reach `onError` rather than silence.

**Declined, with the reason recorded.** `CustomComponent` (component code, dependencies, and CSS executed from the document) would void §7.1 entirely — a document carrying arbitrary code makes every host that renders it trust that code; `use` and `view` are the safe shapes for that slot. Five AI components (`ChatBot`, `AISearch`, `AIForm`, `AITable`, `AIAssistant`) are applications built on tool calls: what the spec owes them is how to reach an agent, which the `tool` action already provides, and defining their chrome would turn this spec into a UI kit.

**Prose enums are now declared** (§18.2.10 unaffected). Thirteen string properties listed their allowed values in `description` only, so `text.variant` rejected a typo while `button.variant` accepted one — same class of mistake, caught on one side. `banner.severity`, `button.variant`, `colorPicker.pickerType`, `dateField.mode`, `fittedBox.fit`, `flow.alignment`, `form.showErrorsOn`, `image.fit`, `linear.alignment`, `linear.distribution`, `permissionPrompt.style`, `segmentedControl.variant`, `stack.fit` now carry `enum`. `fileExplorer.items` was excluded on inspection: its backticked tokens are sibling property names, not values.

**Aliases** (§17.3.1) are read-only. A runtime MUST accept them; tools SHOULD emit canonical names, so a document round-tripped through an editor converges on one name rather than preserving whichever the author typed.

### New — Asset & Icon references ([`06_Runtime_Contract.md`](1.4/06_Runtime_Contract.md) §6.12, [`18_Conformance.md`](1.4/18_Conformance.md) §18.2.12)

Every slot that takes an asset now resolves through **one contract**. Before this, `AssetRef` existed as a primitive but only seven Extended-media slots referenced it — Core's `image.src`, `avatar.src`, `lottieAnimation.src`, and `icon.icon` were typed as bare strings, so the same value was declared in one slot and undeclared in the next. Runtime factories each hand-rolled their own scheme dispatch, and between all of them only `http(s)`, `assets/`, and `data:` were ever handled: exactly the three that a **synchronous** loader can build. `bundle://` and `client://` were declared by the spec and implemented by nobody.

**`AssetRef` gains an object form** — `{uri, origin?}`, read through MCP `resources/read`. No new scheme was minted for "an asset the server holds": MCP already reads an arbitrary resource uri and returns base64 `blob`, and `Origin` (§6.11) already says *which* server. Omitting `origin` resolves against the ambient origin, never the embedder's — the same rule §7.10 states for definitions.

**The scheme set is open.** The old `pattern` was a closed enumeration, so a host could not serve a form this document does not name. It now admits any RFC 3986 scheme, matching the openness `Origin` was already written with. A runtime meeting a scheme it does not implement treats it as an *unresolvable asset*, not a schema violation — an author cannot know in advance which runtime will render their page.

**Support is declared, not assumed.** §6.12.4 requires a runtime to publish which forms it resolves and to route the rest to the slot's declared fallback. It also forbids rendering an implementation detail in the asset's place: a box reading `Base64 not supported` states the runtime's limitation on the user's screen, when the author asked for a picture. §18.2.12 grades this in layers — `data:` and `assets/` are MUST because they need no I/O at all and a constrained device can always meet them; `bundle://` and `https?://` are SHOULD; `client://`, the object form, and unnamed schemes are MAY.

**§6.12.2 and §6.12.5 name the two failures that were live.** A binding must resolve *before* scheme dispatch — a slot dispatching on the literal `"{{item.picture}}"` fails on a correct document. And asset reads are asynchronous: a synchronous loader supports only the no-I/O forms while appearing to implement the contract.

**New `IconRef` primitive.** `icon.icon` documented three forms while the eight other icon slots (`button.icon`, `iconButton.icon`, `floatingActionButton.icon`, `popupMenuButton.icon`, `rating.icon`, `offlineFallback.icon`, `permissionPrompt.icon`, `headerBar.exitButton.icon`) were bare strings — a codepoint object could not be written outside the `icon` widget at all. The rule is now stated once: a name, a `{codepoint, …}` object, or any `AssetRef`, with a bare string carrying no known scheme read as a **name** so the zero-ceremony default is unchanged.

Narrowing, stated plainly: a bare string with no scheme and no `assets/` prefix is no longer a valid `AssetRef`, and an icon object must now be a codepoint or a `{uri, …}` rather than an arbitrary map. Every widget in this workspace was checked against both the old and new schema — 4,476 asset and icon widgets, **zero newly invalid**.

### New — `navigation.openUrl` ([`04_Actions.md`](1.4/04_Actions.md) §4.3.3)

Core had no way out of the application. Every `navigation` sub-action addresses an internal route; `client.httpRequest` sends a request rather than opening one and belongs to the Client Profile. A no-code app links outward as a matter of course, so this was a gap rather than an omission.

`webView` (also Core) renders a URL *inside* the app and is not a substitute — an external link shown in a `webView` traps the user in a frame the app controls, which is the wrong answer for terms links, mail addresses, and dialer URLs.

A host that cannot open the URL MUST report through `onError` rather than no-op: "pressed it and nothing happened" is indistinguishable from a broken document. [`07_Security.md`](1.4/07_Security.md) §7.3.4 governs schemes — `javascript:`, `data:`, and `file:` MUST NOT be opened, and the runtime MUST NOT attach session material of its own.

### New — `fileInput` widget ([`02_Widgets.md`](1.4/02_Widgets.md) §2.6.24)

A browser-rendered app could not accept a file at all: `client.selectFile` sits in the Client Profile behind a `file.read` grant, and no widget took file input (`signature` took user-drawn input, but nothing took a user-picked file).

The correction is a boundary, not a feature. Reading a path *the document names* reaches into the host's filesystem and rightly needs a grant. Receiving a file *the user chose in a picker* is the opposite act: the choosing is the consent, and the app learns nothing it was not handed. That is the trust level `signature` already sits at.

The selection lands in state as `[{name, size, mimeType, bytes?, path?}]`. `bytes` is a `data:` URI — hence a valid `AssetRef` — so a picked image renders with no upload round-trip. `path` is absent where the host has no filesystem. Transport stays out of scope: once the file is in state, sending it is an ordinary `tool` action.

### New — Entry & Identity ([`08_Client_Extensions.md`](1.4/08_Client_Extensions.md) §8.9)

A definition is often reached from outside the app — a scanned code, a tag, a link — and the viewer may or may not be signed in. §8.9 defines what a document may read about that arrival (`entry.*`), what it may read about the current principal (`identity.*`), and the one transition it may request (`identity.promote` / `identity.release`).

The design commitment: **identity is a parameter, not a fork.** A document renders usefully for a guest and offers more once identified, rather than existing in a public edition and a private edition. Requiring identification stays a host decision taken before render, so it never becomes a conditional in a layout.

`entry.params` is deliberately a separate root from `route.params`: route parameters say where in the document the viewer is, entry parameters say what was scanned to get here, and only the latter survives internal navigation. Both are read-only, both resolve to `null` on runtimes without host support, and §8.9.5 states plainly that neither is authority — every privileged operation is still authorized at the serving origin.

Binding prefixes registered in [`03_Data_Binding.md`](1.4/03_Data_Binding.md) §3.4/§3.5 and [`17_Naming.md`](1.4/17_Naming.md) §17.2.5; action names in §17.2.2 and the Action `type` enum.


**Composition** — one document may now render definitions served by origins other than its own. This is what lets a single application compose several MCP servers (a temperature sensor, a humidity sensor, and a controller presented as one product) with the *author* deciding how that looks.

### The gap this closes

v1.3 already defined how an application presents itself **when embedded** (§11.9 `dashboard`, which names "multi-app dashboards" explicitly). Nothing defined how an application **embeds**. The provider side existed; the consumer side did not. Meanwhile the spec was written in the singular throughout — §6.1 "communicates with *a* server" — so a definition fetched from elsewhere had nowhere to go.

Note what is deliberately *not* added: any mechanism for opening connections. Establishing outbound MCP connections is a host capability that already exists and is already the canonical path; this release defines only how a definition is *addressed and rendered* once a connection exists (§6.11.1).

### New — `DefinitionSource` ([`01_Core_Concepts.md`](1.4/01_Core_Concepts.md) §1.9)

Names the concept of *where a definition comes from*, with four forms: inline, a `ui://` URI on the current origin, a qualified `{ $ref, from }` reference to another origin, or a binding to a definition already held in state. Omitting `from` means the current origin, so **every v1.3 document keeps its exact meaning**.

`Origin` is deliberately open — `{ "connection": <id> }` is defined now; `{ "bundle": … }` / `{ "agent": … }` can follow without changing any document that already uses it.

The binding form matters as much as the qualified one: it covers agent-generated, cached, bundle-loaded, and runtime-composed definitions, not only definitions that came from a server.

### New — `view` widget ([`02_Widgets.md`](1.4/02_Widgets.md) §2.13.1)

Embeds a `DefinitionSource` anywhere in a tree — `source`, `props`, `fallback`, `loading`, `onError`, `theme`. This is what puts several origins on one screen.

### Changed — `RouteValue` accepts a `DefinitionSource` ([`01_Core_Concepts.md`](1.4/01_Core_Concepts.md) §1.2.1)

A whole route may be another origin's page. Combined with existing machinery this delivers three author choices for free: `initialRoute` to show it at launch, a `navigation` action to reveal it on tap, `navigation.items` to place it in the app's chrome. No new navigation concept was introduced.

### New — origin is a scope, not an argument (§1.9.5)

Normative and load-bearing. When a definition resolves from an origin, that origin becomes **ambient** for the resolved subtree: tool calls, resource reads, subscriptions, state, storage and permissions all scope to it. This is what lets a definition authored with no knowledge of any embedder — a device serving its own `ui://app` — render **unmodified** inside another application and still reach its own server.

The rejected alternative, a per-action origin field, would have required rewriting every embedded definition and would have made embedding a server you do not control impossible.

### New — origin isolation ([`07_Security.md`](1.4/07_Security.md) §7.10, [`08_Client_Extensions.md`](1.4/08_Client_Extensions.md) §8.8)

§8's existing rules are **not rewritten to be plural**. "Storage is scoped per MCP server identity; cross-server reads are prohibited" stays literally true — each embedded scope simply carries its own identity and the existing rules apply within it. Effective permissions are an **intersection** (embedder's grant toward that origin ∩ what the embedded definition requests); embedding never elevates. `props` is the only embedder→embedded channel.

### New — Composition Profile ([`18_Conformance.md`](1.4/18_Conformance.md) §18.7)

The conformance gate. Per §1.7.3 the support surface is declared by profile, not version — a host that cannot isolate scopes per origin does not claim it.

This is also the one place where §1.7.2's forward-compatibility allowance does **not** apply: a runtime without the profile MUST reject a `from`-carrying source rather than resolve `$ref` against its own origin. A permissive reading would render one server's UI under another's identity — a security failure, not a missing feature.

### Runtime contract ([`06_Runtime_Contract.md`](1.4/06_Runtime_Contract.md) §6.11)

Resolution order, one runtime scope per origin, notification routing, and failure/lifecycle: failure is local (a dead origin renders that view's `fallback`, siblings keep rendering), reconnect remounts, depth is bounded and origin cycles are detected.

### Compatibility

Purely additive. No existing field changes meaning; `from` absent is v1.3 behaviour. `version: "1.4"` is accepted alongside the earlier forms.


## [1.3.4]

Content-app capability tier — five-phase enrichment that turns the spec from a utility-app builder into a content-app builder (book / album / magazine / portfolio). All phases ship at the spec layer in this release; runtime first-cut wraps the M3 standard surfaces.

### New shared primitives ([`configs/_primitive/`](1.3/configs/_primitive/))

New cross-schema directory `configs/_primitive/` — single source of truth for primitives referenced from widgets / app / page / theme schemas. Codegen embeds each primitive's body into every output schema's `$defs` so each schema stays self-contained.

- `AssetRef` — five accepted scheme prefixes: `bundle://`, `https?://`, `data:`, `assets/`, `client://`. Migrated from `configs/app/AssetRef.yaml`. image / icon / BackgroundImage / videoPlayer / fontRegistry all reference this.
- `TextStyle` — inline text-style superset (16 fields including shader, fontFeatures, shadows). Migrated from `configs/theme/TextStyle.yaml`. Used by `theme.typography.<role>` AND `text.style` / `richText.style`.
- `BorderRadius` — per-corner radius. **Directional canonical** (RTL-aware per M3): `topStart` / `topEnd` / `bottomStart` / `bottomEnd` + `all` shorthand. Replaces `configs/theme/ShapeCorner.yaml` (visual coords).
- `Alignment` — 2D rectangle alignment. **Directional canonical** plus numeric `{x, y}` form. Used by box / align / stack / fittedBox / image / indexedStack / BackgroundImage.alignment / Gradient.begin/end/center.
- `Dimension` — number OR `{value, unit}` object form.
- `Gradient` — `linear` / `radial` / `sweep` discriminated by `type`; colors[] + stops[] + per-type endpoints + tileMode.
- `BoxBorder` / `BorderSide` — uniform-side or per-side border (color / width / style).
- `BoxShadow` — drop shadow (color / offset / blurRadius / spreadRadius).
- `BackgroundImage` — image fill behind a box. AssetRef + fit + alignment + opacity + colorFilter (5-mode subset) + repeat.
- `BoxDecoration` — composition wrapper (color / gradient / image / border / borderRadius / boxShadow / shape / backdropBlur).
- `Binding` — `^\{\{.*\}\}$` pattern accepted as an alt branch on every primitive — any primitive value may be substituted with a binding expression.
- `AnimationCurve` — 12 canonical curves (CSS 4 + M3 standard 3 + M3 emphasized 3 + bounce 2). Used by every implicit-anim widget + RouteTransition.
- `RouteTransition` — per-route page transition. 6 styles (slide / fade / scale / cube / sharedAxis / fadeThrough) + duration / curve / axis / reverse.
- `NavigationStyle` — visual styling for nav surfaces (background / indicator / divider / labels / icons / selected colors / elevation).
- `Span` — richText inline span. Discriminated oneOf: TextSpan (text + style + onTap + nested children) OR WidgetSpan (widget + alignment + baseline).
- `DropCap` — typographic drop-cap (lines / glyph override / per-cap style).
- `Sliver` — scrollView's `slivers` array element. Discriminated oneOf of 5 sliver shapes (sliverAppBar / sliverPersistentHeader / sliverList / sliverGrid / sliverFixedExtentList).

### Phase 1 — Decoration substrate ([`02_Widgets.md`](1.3/02_Widgets.md))

- `box` — `decoration` typed as `BoxDecoration`.
- `decoration` widget — full BoxDecoration via `decoration:` OR flat shorthand on every constituent field.
- `text` — `style: TextStyle` (binding string accepted), `dropCap: DropCap`. `style.shader` paints rendered glyphs through a gradient via shader mask.
- `richText` — `spans: array<Span>` formalising TextSpan / WidgetSpan; paragraph-level `style` (TextStyle); `dropCap` on first TextSpan.
- `icon` — five source forms (named / codepoint / URL / bundle SVG / data URI); `shader: Gradient` mutually exclusive with `color`.

### Phase 2 — Gallery layouts ([`02_Widgets.md`](1.3/02_Widgets.md) §2.7 / §2.9)

- `staggeredGrid` (since v1.3) — Pinterest-style masonry.
- `carousel` (since v1.3) — partial-viewport horizontal browser. viewportFraction + loop + autoPlay + transition (slide / fade / coverflow / depth) + indicatorPosition.
- `pageView` — `initialPage`, `loop`, `scrollPhysics`, `allowImplicitScrolling`.
- `scrollView` — sliver mode via `slivers` array (mutually exclusive with `child` / `children`).

### Phase 3 — Motion ([`16_Animations.md`](1.3/16_Animations.md))

- `hero` (since v1.3) — shared-element transition wrapper.
- `animatedOpacity` / `animatedAlign` / `animatedPositioned` / `animatedDefaultTextStyle` (since v1.3) — dedicated implicit-animation wrappers.
- `scrollAnimated` (since v1.3) — scroll-position-driven animation.
- `rive` (since v1.3) — Rive animation.
- `animatedContainer` — formalised `decoration: BoxDecoration`, `alignment: Alignment`, `curve: AnimationCurve`.
- `RouteValue` — wrapper form `{ page, transition }` carries a per-route `RouteTransition`. The prior un-grounded `pageTransition` and `sharedElementConfig` prose blocks are replaced (RouteTransition primitive + `hero` widget).

### Phase 4 — Media ([`02_Widgets.md`](1.3/02_Widgets.md) §2.5 / [`10_Advanced_Widgets.md`](1.3/10_Advanced_Widgets.md))

- `kenBurnsImage` (since v1.3) — image with slow zoom-and-pan animation.
- `imageFilter` (since v1.3) — colour / blur filter applied to a child subtree. 7 filter kinds (sepia / grayscale / blur / saturation / brightness / contrast / invert).
- `lightbox` (since v1.3) — full-screen modal image viewer with pinch-zoom and swipe.
- `mediaPlayer` — `source` / `poster` typed as `AssetRef`; new `waveform` boolean (audio mode only).

### Phase 5 — Theme & navigation polish ([`05_Theme.md`](1.3/05_Theme.md) / [`01_Core_Concepts.md`](1.3/01_Core_Concepts.md))

- `theme.preset` (since v1.3) — curated content-app theme bundle. 5 presets: `warm` / `cool` / `sepia` / `mono` / `highContrast`. Applied as base; other `theme.*` fields layer overrides.
- `theme.fonts` (since v1.3) — font asset registration. Per-family `weights` + `variableAxes` (`{tag, min, max, default}`) + `fallbacks`.
- `NavigationConfig.style` (since v1.3) — visual styling for the navigation surface (NavigationStyle).
- `NavItem.style` (since v1.3) — per-item override layered on top of NavigationConfig.style.

### Spec hygiene

- Cross-cutting primitives moved to `configs/_primitive/` from `configs/app/` (AssetRef) and `configs/theme/` (TextStyle / ShapeCorner). Single source of truth; codegen embeds body in every output schema.
- `BorderRadius` and `Alignment` adopt **directional** corner / token names (M3 canonical, RTL-aware). Visual aliases (`topLeft` / `topRight` / `bottomLeft` / `bottomRight`) accepted by the runtime only, not the schema.
- `17_Naming.md` — `| constrained | constrainedBox |` row removed and the catalog entry dropped. `constrained` / `constrainedBox` are pre-1.3 carryover with no spec presence; runtimes MAY retain them as backward-compat aliases of `box`.
- `clipRRect.borderRadius` typed as `BorderRadius` (was free `number | object`); description aligned to directional corner names.
- `AnimationCurve` named curves (§16.6.1) realigned with the 12-value primitive — replacing the prior ad-hoc 13-value list.
- Common widget `click` / `tooltip` field — every widget admits a `click: Action` (universal gesture surface) and `tooltip: string` (hover / long-press) at the common-property layer (§2.2 / §1.4.1). Additive — bundles that omit them are unaffected. Runtimes wrap the widget in a gesture / tooltip surface only when the field is present. `click` complements (does NOT replace) widget-local activation slots such as `button.onTap` / `iconButton.onTap` / `richText.spans[].onTap`; it is the canonical surface for making pure layout / decoration widgets (`box`, `card`, `linear`, `stack`, ...) tappable without nesting a `gestureDetector`.

### Schema / generated artifacts

- `schema/{widgets,app,page,theme}.schema.json`, `generated/widgets.md`, `generated/llm_prompt_card.md` regenerated.
- `widget_builders.g.dart` (generator) regrown to 134 builders (12 new). New helper methods on `MCPUIJsonGenerator`: `gradient` / `backgroundImage` / `navigationStyle` / `routeTransition`.
- `widgets/_common.yaml` — single yaml source of truth for common widget properties (currently `click` / `tooltip`). Both codegens load it at startup and merge every common property into each widget's effective property set (widget-declared same-named property wins). Result: every widget def in `widgets.schema.json` admits `click` / `tooltip`, and every `MCPUIWidgetBuilders.<widget>` exposes a typed `click` / `tooltip` parameter. Underscore prefix keeps it out of the per-widget yaml iteration.
- `tools/spec_codegen/bin/spec_codegen.dart` — loads `configs/_primitive/` + `configs/widget/` and embeds primitives in `widgets.schema.json $defs`.
- `tools/spec_codegen/bin/configs_codegen.dart` — seeds every config schema's `$defs` with the same shared primitives so each schema stays self-contained.
- `tools/spec_codegen/bin/drift_audit.dart` — runtime-only-legacy allow-list (`constrained`, `constrainedBox`); multi-class file scan (`*_factories.dart` accepted alongside `*_factory.dart`); regex fix for generic-return-type method extraction.

### Conformance

- 111 / 111 yaml example bundles validate.
- drift_audit reports **zero drift** across Sections B–J.

---

## [1.3.3]

- App / page / theme schema yaml-ised under `1.3/configs/<stem>/`; schemas now codegen from yaml ground truth.
- `ChannelDefinition` schema rebuilt to match § 8.6 prose; `ServiceDefinition` / `I18nConfig` / `TemplateLibraryRef` field names aligned with prose.
- `lazy.trigger` enum `viewport` → `visible`. `NavigationConfig` § 1.2.3 formalised.
- 7 dismissible widgets (dialog / drawer / banner / sheet / snackBar) gained `onClose` callback.
- New tools: `spec_consistency.dart` (spec internal audit), `configs_codegen.dart` (yaml → app/page/theme schema). `drift_audit.dart` excludes `.g.dart` mirrors from source corpus.

---

## [1.3.2]

### Widgets ([`02_Widgets.md`](1.3/02_Widgets.md))

- `box` — added `minWidth` / `maxWidth` / `minHeight` / `maxHeight` flat-form constraint properties so `box` is a true superset of the legacy `constrained` widget.
- Removed `constrained` from the canonical surface (yaml + schema + 02_Widgets section). Runtimes MAY retain it as a legacy alias of `box`.

### Theme tokens ([`widgets/`](1.3/widgets/))

- M3 token shorthand on `text.variant` (15 typography roles), `box.padding`, `card.shape` / `card.elevation`, `button.elevation`, `icon.size` / `sizeToken` — accept the M3 token name; resolved through `theme.<domain>.<token>`.

### Responsive ([`14_Responsive_Events.md`](1.3/14_Responsive_Events.md))

- Rewritten on M3 5-class FormFactor — `compact` / `medium` / `expanded` / `large` / `extraLarge` plus `embedded`. Earlier `xs` / `sm` / `md` / `lg` / `xl` labels removed.
- `{{runtime.breakpoint}}` renamed to `{{runtime.formFactor}}`.
- Per-form-factor property override map formalised (`{compact, medium, expanded, large, extraLarge, embedded, default}`) on every property.

### Schema / generated artifacts

- `schema/widgets.schema.json`, `schema/app.schema.json`, `generated/widgets.md`, `generated/llm_prompt_card.md` regenerated.

---

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
