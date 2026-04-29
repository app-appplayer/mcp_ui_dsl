<!-- GENERATED: do not edit. Source: ../widgets/*.yaml. -->
# MCP UI DSL — LLM Prompt Card

Authoritative catalog of every widget type recognised by the MCP UI DSL runtime. Use as context when generating or editing DSL. Widget types and property names listed here are the only sanctioned ones; anything else is either a legacy alias (§17.3) or invalid.

Format per widget:
- `type` — canonical widget type name (camelCase).
- `aliases` — legacy names accepted by the runtime.
- `properties` — supported top-level properties (`?` = optional).
- `children` — how children are passed, if any.
- `events` — widget-level event handlers (Action payload).

## Advanced

### `calendar` *(since v1.0)*
- properties: `selectedDate?: string | binding`, `events?: binding`, `firstDate?: string`, `lastDate?: string`, `view?: string`, `onChange?: Action`

### `canvas` *(since v1.3)*

### `chart` *(since v1.0)*
- properties: `chartType: string`, `data: object | array`, `data.datasets[].label?: string`, `data.datasets[].data: number[]`, `data.datasets[].borderColor?: string`, `data.datasets[].backgroundColor?: string`, `options?: object`, `options.responsive?: boolean`, `options.animation.duration?: number`, `options.legend.position?: string`, `width?: number`, `height?: number`

### `codeEditor` *(since v1.0)*
- properties: `code: string | binding`, `language?: string`, `theme?: string`, `readOnly?: boolean`, `showLineNumbers?: boolean`, `fontSize?: number`, `lineHeight?: number`, `tabSize?: number`, `width?: number`, `height?: number`, `backgroundColor?: string`, `textColor?: string`, `onChange?: Action`

### `dataTable` *(since v1.0)*
- properties: `columns: `Column[]``, `columns[].key: string`, `columns[].label: string`, `columns[].width?: number`, `columns[].sortable?: boolean`, `columns[].align?: string`, `rows: binding`, `selectable?: boolean`, `sortColumn?: binding`, `sortAscending?: binding`, `onSort?: Action`, `onRowTap?: Action`

### `fileExplorer` *(since v1.0)*
- properties: `items?: binding`, `rootPath?: string`, `files?: string[]`, `directories?: string[]`, `showIcons?: boolean`, `showHidden?: boolean`, `expandAll?: boolean`, `width?: number`, `height?: number`, `selectedColor?: string`, `onSelect?: Action`, `onOpen?: Action`

### `gauge` *(since v1.0)*
- properties: `value: number`, `min?: number`, `max?: number`, `segments?: `Segment[]``, `size?: number`, `strokeWidth?: number`, `backgroundColor?: string`, `valueColor?: string`, `showLabel?: boolean`, `labelFormat?: string`, `startAngle?: number`, `sweepAngle?: number`

### `graph` *(since v1.0)*
- properties: `data?: `Point[]` `, `chartType?: string`, `width?: number`, `height?: number`, `showGrid?: boolean`, `showLabels?: boolean`, `lineColor?: Color`, `fillColor?: Color`, `gridColor?: Color`, `strokeWidth?: number`

### `heatmap` *(since v1.0)*
- properties: `data: array | binding`, `columnLabels?: string[]`, `rowLabels?: string[]`, `cellSize?: number`, `colorRange?: `{ low, high }``, `showValues?: boolean`, `onCellTap?: Action`

### `lazy` *(since v1.0)*
- properties: `placeholder?: Widget`, `content?: Widget | object`, `children?: Widget[]`, `trigger?: string`, `onLoad?: Action`, `onError?: Action`

### `map` *(since v1.0)*
- properties: `center?: `{ latitude, longitude }``, `latitude?: number`, `longitude?: number`, `zoom?: number`, `mapType?: string`, `markers?: `Marker[]``, `markers[].id: string`, `markers[].latitude: number`, `markers[].longitude: number`, `markers[].label?: string`, `markers[].icon?: string`, `markers[].color?: string`, `overlays?: `Overlay[]``, `overlays[].type: string`, `overlays[].points?: `{ latitude, longitude }[]``, `overlays[].fillColor?: string`, `overlays[].strokeColor?: string`, `overlays[].strokeWidth?: number`, `onMarkerTap?: Action`, `onMapTap?: Action`

### `markdown` *(since v1.0)*
- properties: `text?: string `, `selectable?: boolean`, `width?: number`, `height?: number`, `fontSize?: number`, `textColor?: string`, `linkColor?: string`, `codeBackgroundColor?: string`, `onLinkTap?: Action`

### `mediaPlayer` *(since v1.0)*
- properties: `source: string`, `mediaType?: string`, `autoPlay?: boolean`, `loop?: boolean`, `muted?: boolean`, `volume?: number`, `controls?: boolean`, `poster?: string`, `width?: number`, `height?: number`, `onPlay?: Action`, `onPause?: Action`, `onEnded?: Action`, `onTimeUpdate?: Action`, `onError?: Action`

### `networkGraph` *(since v1.0)*

### `signature` *(since v1.0)*
- properties: `binding?: binding`, `penColor?: string`, `penWidth?: number`, `width?: number`, `height?: number`, `backgroundColor?: string`, `borderColor?: string`, `showClearButton?: boolean`, `showGuide?: boolean`, `onSignatureEnd?: Action`, `onClear?: Action`

### `table` *(since v1.0)*
- properties: `rows: `{ cells: Widget[] }[]``, `border?: `{ color, width }``, `defaultColumnWidth?: string | number`, `defaultVerticalAlignment?: string`, `columnWidths?: object`

### `terminal` *(since v1.0)*
- properties: `lines?: binding`, `prompt?: string`, `showInput?: boolean`, `maxLines?: number`, `width?: number`, `height?: number`, `fontSize?: number`, `backgroundColor?: string`, `textColor?: string`, `promptColor?: string`, `onCommand?: Action`

### `timeline` *(since v1.0)*
- properties: `items: `TimelineItem[]``, `items[].title: string`, `items[].subtitle?: string`, `items[].icon?: string`, `items[].time?: string`, `items[].color?: string`, `orientation?: string`

### `tree` *(since v1.0)*
- properties: `data: array | binding`, `childrenKey?: string`, `indentation?: number`, `itemPadding?: EdgeInsets`, `itemTemplate?: Widget`, `expandable?: boolean`, `initiallyExpanded?: boolean`, `selectable?: boolean`, `showLines?: boolean`, `selectedColor?: Color`, `lineColor?: Color`, `width?: number`, `height?: number`, `onNodeTap?: Action`, `onSelect?: Action`, `onExpand?: Action`, `onCollapse?: Action`

### `webView` *(since v1.0)*
- properties: `url?: string`, `html?: string`, `allowNavigation?: boolean`, `enableJavaScript?: boolean`, `enableZoom?: boolean`, `width?: number`, `height?: number`, `onPageStarted?: Action`, `onPageFinished?: Action`, `onError?: Action`

## Animation

### `animatedContainer`
- properties: `duration?: number`, `curve?: string`, `decoration?: object`, `onEnd?: Action`, `child?: Widget`

### `lottieAnimation`
- properties: `src: string`, `autoPlay?: boolean`, `loop?: boolean`

### `opacity` *(since v1.3)*
- properties: `opacity: number | binding`, `animated?: boolean`, `duration?: number`, `curve?: string`, `child: Widget`

### `transform` *(since v1.3)*
- properties: `rotate?: number`, `scale?: number | object`, `translate?: object`, `origin?: object`, `animated?: boolean`, `duration?: number`, `curve?: string`, `child: Widget`

## Dialog

### `alertDialog` *(since v1.0)*
- aliases: `alert`
- properties: `title?: string`, `content?: string | Widget`, `dismissible?: boolean`, `actions?: array<object{ label: string, variant: string, primary: boolean, onTap: Action }>`

### `bottomSheet`
- properties: `child: Widget`, `isDismissible?: boolean`, `enableDrag?: boolean`, `backgroundColor?: string`, `shape?: object`

### `customDialog`
- properties: `child: Widget`, `dismissible?: boolean`

### `simpleDialog`
- properties: `title?: string`, `options?: Option[]`, `children?: Widget[]`, `onSelect?: Action`

### `snackBar`
- properties: `content: string`, `duration?: number`, `action?: SnackBarAction`

## Display

### `avatar`
- properties: `src?: string`, `label?: string`, `size?: number`, `color?: string`

### `badge`
- properties: `label?: string`, `color?: string`, `child?: Widget`

### `banner`
- properties: `message: string`, `severity?: string`, `actions?: BannerAction[]`

### `card`
- properties: `elevation?: number`, `margin?: EdgeInsets`, `shape?: object`, `color?: Color`, `child: Widget`

### `chip`
- properties: `label: string`, `avatar?: Widget`, `selected?: boolean`, `variant?: string`, `onDelete?: Action`, `onTap?: Action`

### `decoration`
- properties: `decoration?: object`, `color?: Color`, `borderRadius?: number`, `border?: object`, `gradient?: object`, `boxShadow?: array`, `child?: Widget`, `children?: Widget[]`

### `divider`
- properties: `thickness?: number`, `color?: string`, `indent?: number`, `endIndent?: number`

### `icon`
- properties: `icon: string | object`, `size?: number`, `color?: Color`

### `image`
- properties: `src: string`, `width?: number`, `height?: number`, `fit?: string`, `alignment?: string`

### `placeholder`
- properties: `fallbackWidth?: number`, `fallbackHeight?: number`, `color?: string`, `strokeWidth?: number`, `child?: Widget`

### `progressBar`
- aliases: `linearProgressIndicator`, `loadingIndicator`, `loading-indicator`, `progress-bar`, `progress`
- properties: `value?: number | binding`, `indicatorType?: string`, `color?: string`, `backgroundColor?: string`

### `richText`
- properties: `spans: Span[]`, `textAlign?: string`

### `text`
- properties: `text: string`, `style?: object`, `maxLines?: number`, `overflow?: string`, `textAlign?: string`

### `tooltip`
- properties: `message: string`, `child: Widget`

### `verticalDivider`
- properties: `width?: number`, `thickness?: number`, `color?: string`, `indent?: number`, `endIndent?: number`

## Input

### `button`
- properties: `label: string`, `variant?: string`, `icon?: string`, `enabled?: boolean`, `onTap?: Action`, `onDoubleTap?: Action`, `onLongPress?: Action`

### `checkbox`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`

### `checkboxGroup`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `options: Option[]`, `orientation?: string`

### `colorPicker`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `showAlpha?: boolean`, `showLabel?: boolean`, `pickerType?: string`, `enableHistory?: boolean`

### `dateField`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `format?: string`, `firstDate?: string`, `lastDate?: string`, `mode?: string`, `locale?: string`

### `datePicker`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `firstDate?: string`, `lastDate?: string`

### `dateRangePicker`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `startDate?: string`, `endDate?: string`, `label?: string`, `firstDate?: string`, `lastDate?: string`, `format?: string`, `locale?: string`

### `form`
- properties: `children: Widget[]`, `showErrorsOn?: string`, `onSubmit?: Action`

### `iconButton`
- properties: `icon: string`, `size?: number`, `color?: string`, `enabled?: boolean`, `onTap?: Action`

### `numberField`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `min?: number`, `max?: number`, `step?: number`, `decimalPlaces?: number`, `prefix?: string`, `suffix?: string`, `thousandSeparator?: string`

### `numberStepper`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `min?: number`, `max?: number`, `step?: number`

### `radio`
- properties: `value: any`, `groupValue: any | binding`, `label?: string`, `onChange?: Action`

### `radioGroup`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `options: Option[]`, `orientation?: string`

### `rangeSlider`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `min?: number`, `max?: number`, `divisions?: number`

### `rating`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `max?: number`, `icon?: string`, `color?: string`

### `segmentedControl`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `options: Option[]`, `variant?: string`

### `select`
- aliases: `dropdown`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `options: Option[]`, `placeholder?: string`

### `slider`
- properties: `binding?: string`, `value?: number`, `enabled?: boolean`, `onChange?: Action`, `min?: number`, `max?: number`, `divisions?: number`

### `stepper`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `steps: Step[]`, `currentStep?: number | binding`, `stepperType?: string`, `onStepTapped?: Action`, `onStepContinue?: Action`, `onStepCancel?: Action`

### `textInput` *(since v1.0)*
- aliases: `textField`, `textfield`, `textFormField`, `text-form-field`
- properties: `binding?: string`, `value?: string | binding`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `placeholder?: string`, `helperText?: string`, `prefixIcon?: string`, `suffixIcon?: string`, `obscureText?: boolean`, `readOnly?: boolean`, `maxLines?: integer`, `maxLength?: integer`, `inputType?: string`, `validation?: ValidationConfig`
- events: `onChange`, `onSubmit`, `onFocus`, `onBlur`

### `timeField`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `format?: string`, `use24HourFormat?: boolean`, `mode?: string`

### `timePicker`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `use24HourFormat?: boolean`

### `toggle`
- aliases: `switch`
- properties: `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`

## Interaction

### `dragTarget`
- properties: `canDrop?: binding`, `builder?: Widget`, `children?: Widget[]`, `onDrop?: Action`, `onDragEnter?: Action`, `onDragLeave?: Action`

### `draggable`
- properties: `data: any | binding`, `feedback?: Widget`, `childWhenDragging?: Widget`, `child: Widget`

### `gestureDetector`
- properties: `child: Widget`, `onTap?: Action`, `onDoubleTap?: Action`, `onLongPress?: Action`, `onPanStart?: Action`, `onPanUpdate?: Action`, `onPanEnd?: Action`

### `inkWell`
- properties: `child: Widget`, `borderRadius?: number`, `onTap?: Action`, `onLongPress?: Action`

## Layout

### `align`
- properties: `alignment?: string`, `child: Widget`

### `aspectRatio`
- properties: `aspectRatio?: number`, `child: Widget`

### `box` *(since v1.0)*
- aliases: `container`, `decoratedBox`, `constrainedBox`
- properties: `width?: number`, `height?: number`, `padding?: EdgeInsets`, `margin?: EdgeInsets`, `alignment?: string`, `color?: Color`, `decoration?: object{ color: Color, borderRadius: number, border: object, boxShadow: array<object>, gradient: object }`
- children: single (key: `child`)

### `center`
- properties: `child: Widget`

### `conditional`
- properties: `condition?: boolean | binding`, `then?: Widget`, `else?: Widget`, `switch?: binding`, `cases?: array`, `default?: Widget`

### `constrained`
- aliases: `constrainedBox`
- properties: `child: Widget`

### `expanded`
- properties: `flex?: number`, `child: Widget`

### `flexible`
- properties: `flex?: number`, `fit?: string`, `child: Widget`

### `fractionallySized`
- properties: `widthFactor?: number`, `heightFactor?: number`, `child: Widget`

### `indexedStack`
- properties: `index?: number | binding`, `alignment?: string`, `children: Widget[]`

### `intrinsicHeight`
- properties: `child: Widget`

### `intrinsicWidth`
- properties: `child: Widget`

### `linear`
- aliases: `row`, `column`
- properties: `mainAxisSize?: string`, `direction: string`, `alignment?: string`, `distribution?: string`, `spacing?: number`, `children: Widget[]`

### `margin`
- properties: `margin: EdgeInsets`, `child: Widget`

### `padding`
- properties: `padding: EdgeInsets`, `child: Widget`

### `positioned`
- properties: `child: Widget`

### `safeArea`
- properties: `child: Widget`

### `sizedBox`
- properties: `width?: number`, `height?: number`, `child?: Widget`

### `spacer`
- properties: `flex?: number`

### `stack`
- properties: `alignment?: string`, `fit?: string`, `children: Widget[]`

### `visibility`
- properties: `visible?: boolean | binding`, `maintainSize?: boolean`, `maintainState?: boolean`, `replacement?: Widget`, `child?: Widget`, `children?: Widget[]`

### `wrap`
- properties: `direction?: string`, `spacing?: number`, `runSpacing?: number`, `alignment?: string`, `children: Widget[]`

## List

### `grid`
- aliases: `gridview`
- properties: `items?: binding`, `itemTemplate?: Widget`, `children?: Widget[]`, `columns: number | object`, `rowGap?: number`, `columnGap?: number`, `itemAspectRatio?: number`

### `list`
- aliases: `listView`, `listview`
- properties: `items?: binding`, `itemTemplate?: Widget`, `children?: Widget[]`, `spacing?: number`, `orientation?: string`, `emptyMessage?: string`, `itemExtent?: number`

### `listItem`
- aliases: `listTile`, `list-tile`
- properties: `title?: string | Widget`, `subtitle?: string | Widget`, `leading?: Widget`, `trailing?: Widget`, `onTap?: Action`, `selected?: boolean`, `enabled?: boolean`

## Navigation

### `bottomNavigation`
- aliases: `bottomNav`, `bottomnavigationbar`
- properties: `selectedIndex?: number | binding`, `items: NavItem[]`, `onChange?: Action`

### `drawer`
- properties: `items?: DrawerItem[]`, `children?: Widget[]`, `header?: Widget`, `onSelect?: Action`

### `floatingActionButton`
- properties: `icon?: string`, `label?: string`, `onTap?: Action`

### `headerBar`
- aliases: `appbar`
- properties: `title?: string | Widget`, `leading?: Widget`, `actions?: Widget[]`, `exitButton?: ExitButtonConfig | boolean`, `backgroundColor?: string`, `elevation?: number`, `centerTitle?: boolean`

### `navigationRail`
- properties: `selectedIndex?: number | binding`, `items: NavItem[]`, `onChange?: Action`

### `popupMenuButton`
- properties: `icon?: string`, `items: MenuItem[]`, `onSelect?: Action`

### `tabBar`
- properties: `selectedIndex?: number | binding`, `tabs: Tab[]`, `onChange?: Action`

### `tabBarView`
- properties: `selectedIndex?: number | binding`, `children: Widget[]`

## Scroll

### `pageView`
- properties: `direction?: string`, `children: Widget[]`, `onPageChanged?: Action`

### `scrollBar`
- properties: `thumbVisibility?: boolean`, `trackVisibility?: boolean`, `thickness?: number`, `radius?: number`, `child?: Widget`, `children?: Widget[]`

### `scrollView`
- properties: `direction?: string`, `padding?: EdgeInsets`, `child?: Widget`, `children?: Widget[]`

### `singleChildScrollView`
- properties: `direction?: string`, `padding?: EdgeInsets`, `child?: Widget`, `children?: Widget[]`

## Utility

### `accessibleWrapper`
- properties: `child: Widget`, `accessibility?: object`

### `baseline`
- properties: `baseline: number`, `baselineType?: string`, `child: Widget`

### `clipOval`
- properties: `child: Widget`

### `clipRRect`
- properties: `borderRadius?: number | object`, `child: Widget`

### `dashboard` *(since v1.3)*
- properties: `content?: Widget`, `refreshInterval?: number`, `onTap?: Action`

### `errorBoundary`
- properties: `child: Widget`, `fallback?: Widget`, `onError?: Action`

### `errorRecovery`
- properties: `child?: Widget`, `children?: Widget[]`, `fallback?: Widget`, `handlers?: object`, `onError?: Action`, `showDetails?: boolean`

### `fittedBox`
- properties: `fit?: string`, `alignment?: string`, `child: Widget`

### `flow`
- properties: `children: Widget[]`, `direction?: string`, `spacing?: number`, `alignment?: string`

### `layoutBuilder`
- properties: `breakpoints?: object`, `layouts?: object`, `default?: Widget`

### `lazy`
- properties: `child: Widget`

### `limitedBox`
- properties: `maxWidth?: number`, `maxHeight?: number`, `child: Widget`

### `mediaQuery`
- properties: `condition?: object | binding`, `then?: Widget`, `else?: Widget`, `breakpoints?: object`, `defaultChild?: Widget`

### `offlineFallback`
- properties: `online?: Widget`, `offline?: Widget`, `message?: string`, `icon?: string`, `showRetry?: boolean`, `onRetry?: Action`, `isOnline?: boolean | binding`

### `permissionPrompt`
- properties: `permissions?: string[]`, `permissionType?: string`, `style?: string`, `title?: string`, `description?: string`, `icon?: string`, `allowPartial?: boolean`, `onAllow?: Action`, `onDeny?: Action`

### `use`
- aliases: `template`, `useTemplate`
- properties: `template: string`, `params?: object`, `slots?: object`

