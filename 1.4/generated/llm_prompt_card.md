<!-- GENERATED: do not edit. Source: specs/mcp_ui_dsl/spec/1.4/widgets/*.yaml. -->
# MCP UI DSL — LLM Prompt Card

Authoritative catalog of every widget type recognised by the MCP UI DSL runtime. Use as context when generating or editing DSL. Widget types and property names listed here are the only sanctioned ones; anything else is either a legacy alias (§17.3) or invalid.

Format per widget:
- `type` — canonical widget type name (camelCase).
- `aliases` — legacy names accepted by the runtime.
- `properties` — supported top-level properties (`?` = optional).
- `children` — how children are passed, if any.
- `events` — widget-level event handlers (Action payload).

## Advanced

### `barcode` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `value: string | binding`, `format?: string`, `width?: number`, `height?: number`, `displayValue?: boolean`, `foregroundColor?: Color`, `backgroundColor?: Color`

### `calendar` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `selectedDate?: string | binding`, `events?: binding`, `firstDate?: string`, `lastDate?: string`, `view?: string`, `onChange?: Action`, `backgroundColor?: Color`, `change?: Action`, `selectedColor?: Color`, `eventColor?: Color`, `firstDayOfWeek?: number | binding`, `height?: Dimension`, `onDateSelect?: Action`, `onMonthChange?: Action`, `primaryColor?: Color`, `showHeader?: boolean | binding`, `showWeekNumbers?: boolean | binding`, `todayColor?: Color`, `width?: Dimension`

### `canvas` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `backgroundColor?: string`, `commands?: array`, `height?: Dimension`, `width?: Dimension`

### `chart` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `chartType: string`, `data: object | array`, `data.datasets[].label?: string`, `data.datasets[].data: array<number>`, `data.datasets[].borderColor?: string`, `data.datasets[].backgroundColor?: string`, `options?: object`, `options.responsive?: boolean`, `options.animation.duration?: number`, `options.legend.position?: string`, `width?: number`, `height?: number`, `backgroundColor?: Color`, `gridColor?: Color`, `title?: string`, `colors?: array`, `labelColor?: Color`, `primaryColor?: Color`, `showGrid?: boolean | binding`, `showLabels?: boolean | binding`, `showLegend?: any`

### `codeEditor` *(since v1.0)*
- aliases: `code`
- properties: `click?: Action`, `tooltip?: string`, `copyable?: boolean`, `expandAll?: boolean`, `code?: string | binding`, `language?: string`, `theme?: string`, `readOnly?: boolean`, `showLineNumbers?: boolean`, `fontSize?: number`, `lineHeight?: number`, `tabSize?: number`, `width?: number`, `height?: number`, `backgroundColor?: Color`, `textColor?: Color`, `onChange?: Action`, `binding?: string`, `change?: Action`, `lineNumberColor?: Color`

### `dataTable` *(since v1.0)*
- aliases: `dataGrid`
- properties: `click?: Action`, `tooltip?: string`, `editable?: boolean`, `filterable?: boolean`, `resizableColumns?: boolean`, `virtualScroll?: boolean`, `rowHeight?: number`, `columns: array<Column>`, `columns[].key: string`, `columns[].label: string`, `columns[].width?: number`, `columns[].sortable?: boolean`, `columns[].align?: string`, `rows: array<object> | binding`, `selectable?: boolean`, `sortColumn?: binding`, `sortAscending?: binding`, `onSort?: Action`, `onRowTap?: Action`, `rowClick?: any`

### `diffViewer` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `oldValue: string | binding`, `newValue: string | binding`, `splitView?: boolean`, `language?: string`, `showLineNumbers?: boolean`, `contextLines?: number`, `highlightLines?: array<number>`

### `fileExplorer` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `items?: array<object> | binding`, `rootPath?: string`, `files?: array<string>`, `directories?: array<string>`, `showIcons?: boolean`, `showHidden?: boolean`, `expandAll?: boolean`, `width?: number`, `height?: number`, `selectedColor?: Color`, `onSelect?: Action`, `onOpen?: Action`, `backgroundColor?: Color`, `iconColor?: Color`, `open?: string`, `select?: Action`

### `gantt` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `tasks: array<object> | binding`, `viewMode?: string`, `range?: object`, `editable?: boolean`, `showProgress?: boolean`, `showDependencies?: boolean`, `todayMarker?: boolean`, `rowHeight?: number`
- events: `onTaskChange`, `onTaskClick`

### `gauge` *(since v1.0)*
- aliases: `meter`
- properties: `click?: Action`, `tooltip?: string`, `value: number`, `min?: number`, `max?: number`, `segments?: array<Segment>`, `size?: number`, `strokeWidth?: number`, `backgroundColor?: Color`, `valueColor?: Color`, `showLabel?: boolean`, `labelFormat?: string`, `startAngle?: number`, `sweepAngle?: number`

### `graph` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `data: array<Point> | binding`, `chartType?: string`, `width?: number`, `height?: number`, `showGrid?: boolean`, `showLabels?: boolean`, `lineColor?: Color`, `fillColor?: Color`, `gridColor?: Color`, `strokeWidth?: number`, `labelColor?: Color`

### `heatmap` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `data: array | binding`, `columnLabels?: array<string>`, `rowLabels?: array<string>`, `cellSize?: number`, `colorRange?: { low, high }`, `colorRange.low?: Color`, `colorRange.high?: Color`, `showValues?: boolean`, `onCellTap?: Action`, `cellGap?: any`, `colorScheme?: string`, `columns?: number`, `maxValue?: any`, `minValue?: any`, `showLabels?: boolean`

### `kanban` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `columns: array<object> | binding`, `itemTemplate: Widget`, `itemKey?: string`, `draggable?: boolean`, `columnWidth?: Dimension`, `optimistic?: boolean`
- events: `onCardMove`, `onCardClick`

### `lightbox` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `images: array<AssetRef>`, `initialIndex?: number`, `allowZoom?: boolean`, `maxZoom?: number`, `allowSwipe?: boolean`, `backgroundColor?: Color`, `onIndexChanged?: Action`, `onClose?: Action`

### `map` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `center?: { latitude, longitude }`, `latitude?: number`, `longitude?: number`, `zoom?: number`, `mapType?: string`, `markers?: array<Marker>`, `markers[].id: string`, `markers[].latitude: number`, `markers[].longitude: number`, `markers[].label?: string`, `markers[].icon?: string`, `markers[].color?: string`, `overlays?: array<Overlay>`, `overlays[].type: string`, `overlays[].points?: array<object{ latitude: number, longitude: number }>`, `overlays[].fillColor?: string`, `overlays[].strokeColor?: string`, `overlays[].strokeWidth?: number`, `onMarkerTap?: Action`, `onMapTap?: Action`, `backgroundColor?: Color`, `gridColor?: Color`, `height?: Dimension`, `interactive?: boolean | binding`, `markerColor?: Color`, `showCoordinates?: boolean | binding`, `showGrid?: boolean | binding`, `width?: Dimension`

### `markdown` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `text: string | binding`, `selectable?: boolean`, `width?: number`, `height?: number`, `fontSize?: number`, `textColor?: Color`, `backgroundColor?: Color`, `linkColor?: Color`, `codeBackgroundColor?: Color`, `onLinkTap?: Action`

### `mediaPlayer` *(since v1.0)*
- aliases: `video`, `audio`
- properties: `click?: Action`, `tooltip?: string`, `source: AssetRef`, `mediaType?: string`, `autoPlay?: boolean`, `loop?: boolean`, `muted?: boolean`, `volume?: number`, `controls?: boolean`, `poster?: AssetRef`, `waveform?: boolean`, `width?: number`, `height?: number`, `onPlay?: Action`, `onPause?: Action`, `onEnded?: Action`, `onTimeUpdate?: Action`, `onError?: Action`, `backgroundColor?: Color`, `duration?: Dimension`, `title?: string`, `accentColor?: Color`, `controlsColor?: Color`, `onSeek?: Action`

### `networkGraph` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `backgroundColor?: Color`, `edgeColor?: Color`, `edges?: array | binding`, `height?: Dimension`, `interactive?: boolean | binding`, `labelColor?: Color`, `layout?: string | binding`, `nodeColor?: Color`, `nodes?: array | binding`, `onEdgeTap?: Action`, `onNodeTap?: Action`, `width?: Dimension`

### `pdfViewer` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `src: AssetRef`, `page?: number | binding`, `zoom?: number | binding`, `showToolbar?: boolean`, `showPageNav?: boolean`, `showZoom?: boolean`, `fit?: string`, `height?: number | binding`
- events: `onLoad`, `onPageChange`, `onError`

### `qrCode` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `value: string | binding`, `size?: number`, `errorCorrection?: string`, `foregroundColor?: Color`, `backgroundColor?: Color`, `margin?: boolean`, `logo?: AssetRef`

### `richTextEditor` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `format?: string`, `toolbar?: array<string>`, `placeholder?: string`, `minHeight?: number`, `maxLength?: number`, `binding?: string`, `onChange?: Action`, `enabled?: boolean | binding`, `value?: string | binding`

### `signature` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: binding`, `penColor?: Color`, `penWidth?: number`, `width?: number`, `height?: number`, `backgroundColor?: Color`, `borderColor?: Color`, `showClearButton?: boolean`, `showGuide?: boolean`, `onSignatureEnd?: Action`, `onClear?: Action`, `borderWidth?: number`, `onSignatureStart?: Action`

### `spreadsheet` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `data: array<array> | binding`, `columns?: array<object>`, `rowHeaders?: boolean`, `columnHeaders?: boolean`, `editable?: boolean`, `formulas?: boolean`, `frozenRows?: number`, `frozenColumns?: number`
- events: `onChange`, `onCellSelect`

### `table` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `rows: array<object{ cells: array<Widget> }>`, `border?: { color, width }`, `defaultColumnWidth?: string | number`, `defaultVerticalAlignment?: string`, `columnWidths?: object`, `textDirection?: string`, `textBaseline?: any`

### `terminal` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `lines?: binding`, `prompt?: string`, `showInput?: boolean`, `maxLines?: number`, `width?: number`, `height?: number`, `fontSize?: number`, `backgroundColor?: Color`, `textColor?: Color`, `promptColor?: Color`, `onCommand?: Action`, `theme?: string`, `command?: string`

### `timeline` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `items: array<TimelineItem>`, `items[].title: string`, `items[].subtitle?: string`, `items[].icon?: string`, `items[].time?: string`, `items[].color?: string`, `orientation?: string`, `itemTemplate?: Widget`, `lineColor?: Color`, `lineWidth?: any`, `nodeSize?: any`, `spacing?: Dimension`

### `tree` *(since v1.0)*
- aliases: `treeView`
- properties: `click?: Action`, `tooltip?: string`, `checkable?: boolean`, `checkedKeys?: array<string> | binding`, `draggable?: boolean`, `data: array | binding`, `childrenKey?: string`, `indentation?: number`, `itemPadding?: EdgeInsets`, `itemTemplate?: Widget`, `expandable?: boolean`, `initiallyExpanded?: boolean`, `selectable?: boolean`, `showLines?: boolean`, `selectedColor?: Color`, `lineColor?: Color`, `width?: number`, `height?: number`, `onNodeTap?: Action`, `onSelect?: Action`, `onExpand?: Action`, `onCollapse?: Action`, `expandAll?: any`, `select?: Action`

### `webView` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `url?: string`, `html?: string`, `allowNavigation?: boolean`, `enableJavaScript?: boolean`, `enableZoom?: boolean`, `width?: number`, `height?: number`, `onPageStarted?: Action`, `onPageFinished?: Action`, `onError?: Action`, `backgroundColor?: Color`

## Animation

### `animatedAlign` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `alignment: Alignment`, `duration?: Dimension`, `curve?: AnimationCurve`, `onEnd?: Action`, `child: Widget`

### `animatedContainer`
- properties: `click?: Action`, `tooltip?: string`, `duration?: Dimension`, `curve?: AnimationCurve`, `width?: Dimension`, `height?: Dimension`, `padding?: EdgeInsets`, `margin?: EdgeInsets`, `alignment?: Alignment`, `decoration?: BoxDecoration`, `onEnd?: Action`, `child?: Widget`, `clipBehavior?: any`, `constraints?: object`, `foregroundDecoration?: any`, `transform?: any`, `transformAlignment?: Alignment`

### `animatedDefaultTextStyle` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `style: TextStyle`, `duration?: Dimension`, `curve?: AnimationCurve`, `onEnd?: Action`, `child: Widget`

### `animatedOpacity` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `opacity: number`, `duration?: Dimension`, `curve?: AnimationCurve`, `onEnd?: Action`, `child: Widget`

### `animatedPositioned` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `top?: Dimension`, `right?: Dimension`, `bottom?: Dimension`, `left?: Dimension`, `width?: Dimension`, `height?: Dimension`, `duration?: Dimension`, `curve?: AnimationCurve`, `onEnd?: Action`, `child: Widget`

### `hero` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `tag: string`, `child: Widget`, `transitionOnUserGestures?: boolean`, `flightShuttleBuilder?: Widget`

### `lottieAnimation`
- properties: `click?: Action`, `tooltip?: string`, `src: AssetRef`, `autoPlay?: boolean`, `loop?: boolean`, `backgroundColor?: Color`, `fit?: string | binding`, `height?: Dimension`, `onComplete?: Action`, `speed?: any`, `width?: Dimension`

### `opacity` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `opacity: number | binding`, `animated?: boolean`, `duration?: number`, `curve?: string`, `child: Widget`

### `rive` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `src: AssetRef`, `artboard?: string`, `animation?: string`, `stateMachine?: string`, `inputs?: object`, `fit?: string`, `alignment?: Alignment`, `width?: Dimension`, `height?: Dimension`

### `scrollAnimated` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `bindings: array<object>`, `child: Widget`

### `transform` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `rotate?: number`, `scale?: number | object`, `translate?: object`, `origin?: object`, `animated?: boolean`, `duration?: number`, `curve?: string`, `child: Widget`

## Dialog

### `alertDialog` *(since v1.0)*
- aliases: `alert`, `confirmDialog`
- properties: `click?: Action`, `tooltip?: string`, `title?: string`, `content?: string | Widget`, `dismissible?: boolean`, `onClose?: Action`, `actions?: array<object{ label: string, variant: string, primary: boolean, onTap: Action }>`, `alignment?: Alignment`, `backgroundColor?: Color`, `elevation?: Dimension`, `clipBehavior?: any`, `contentWidget?: any`, `insetPadding?: EdgeInsets`, `scrollable?: boolean`, `shadowColor?: Color`, `shape?: any`, `surfaceTintColor?: Color`, `titleWidget?: any`

### `bottomSheet`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `isDismissible?: boolean`, `enableDrag?: boolean`, `backgroundColor?: Color`, `shape?: object`, `onClose?: Action`, `elevation?: Dimension`, `clipBehavior?: any`, `constraints?: object`, `dragHandleColor?: Color`, `dragHandleSize?: any`, `onClosing?: Action`, `shadowColor?: Color`, `showDragHandle?: boolean`

### `customDialog`
- aliases: `modal`, `dialog`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `dismissible?: boolean`, `onClose?: Action`, `alignment?: Alignment`, `backgroundColor?: Color`, `content?: string`, `elevation?: Dimension`, `title?: string`, `actions?: array`, `clipBehavior?: any`, `insetPadding?: EdgeInsets`, `shadowColor?: Color`, `shape?: any`, `surfaceTintColor?: Color`

### `popover` *(since v1.4)*
- aliases: `hoverCard`
- properties: `click?: Action`, `tooltip?: string`, `content: Widget`, `child: Widget`, `open?: boolean | binding`, `trigger?: string`, `placement?: string`, `openDelay?: number`, `closeDelay?: number`, `dismissOnOutside?: boolean`
- events: `onOpen`, `onClose`

### `simpleDialog`
- properties: `click?: Action`, `tooltip?: string`, `title?: string`, `options?: array<Option>`, `children?: array<Widget>`, `onSelect?: Action`, `onClose?: Action`, `backgroundColor?: Color`, `elevation?: Dimension`, `contentPadding?: EdgeInsets`, `select?: Action`, `shape?: any`, `titlePadding?: Dimension`

### `snackBar`
- aliases: `toast`
- properties: `click?: Action`, `tooltip?: string`, `content: string`, `duration?: number`, `action?: SnackBarAction`, `onClose?: Action`, `backgroundColor?: Color`, `elevation?: Dimension`, `textColor?: Color`, `behavior?: string`, `closeIconColor?: Color`, `dismissDirection?: any`, `margin?: EdgeInsets`, `onVisible?: Action`, `padding?: EdgeInsets`, `shape?: any`, `showCloseIcon?: boolean`, `width?: Dimension`

## Display

### `avatar`
- properties: `click?: Action`, `tooltip?: string`, `src?: AssetRef`, `label?: string`, `size?: number`, `color?: Color`, `backgroundImage?: BackgroundImage`, `foregroundColor?: Color`, `icon?: IconRef`, `radius?: number`

### `badge`
- properties: `click?: Action`, `tooltip?: string`, `label?: string`, `color?: Color`, `child?: Widget`, `alignment?: Alignment`, `backgroundColor?: Color`, `textColor?: Color`, `isLabelVisible?: boolean`, `offset?: any`, `smallSize?: boolean`

### `banner`
- properties: `click?: Action`, `tooltip?: string`, `message: string`, `severity?: string`, `actions?: array<BannerAction>`, `onClose?: Action`

### `card`
- properties: `click?: Action`, `tooltip?: string`, `elevation?: string`, `margin?: EdgeInsets`, `shape?: string`, `color?: Color`, `child: Widget`, `clipBehavior?: any`, `semanticContainer?: boolean`, `shadowColor?: Color`, `surfaceTintColor?: Color`

### `chip`
- aliases: `tag`
- properties: `click?: Action`, `tooltip?: string`, `label: string`, `avatar?: Widget`, `selected?: boolean`, `variant?: string`, `onDelete?: Action`, `onTap?: Action`, `backgroundColor?: Color`, `elevation?: Dimension`, `labelStyle?: TextStyle`, `onPressed?: Action`, `delete?: Action`, `deleteIcon?: string`, `onDeleted?: Action`, `padding?: EdgeInsets`, `shadowColor?: Color`, `shape?: any`, `side?: any`

### `decoration`
- properties: `click?: Action`, `tooltip?: string`, `decoration?: BoxDecoration`, `color?: Color`, `borderRadius?: BorderRadius`, `border?: BoxBorder`, `gradient?: Gradient`, `image?: BackgroundImage`, `boxShadow?: array<BoxShadow>`, `shape?: string`, `backdropBlur?: number`, `child?: Widget`, `children?: array<Widget>`, `position?: any`

### `divider`
- properties: `click?: Action`, `tooltip?: string`, `thickness?: number`, `color?: Color`, `indent?: number`, `endIndent?: number`, `height?: Dimension`, `vertical?: boolean`

### `icon`
- properties: `click?: Action`, `tooltip?: string`, `icon: IconRef`, `size?: string`, `sizeToken?: string`, `color?: Color`, `shader?: Gradient`

### `image`
- properties: `click?: Action`, `tooltip?: string`, `src: AssetRef`, `width?: number`, `height?: number`, `fit?: string`, `alignment?: Alignment`, `fallback?: Widget`, `loading?: Widget`, `placeholder?: string`, `errorWidget?: string`, `fallbackBehavior?: string`, `fallbackUrl?: string | binding`

### `imageFilter` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `filter: string`, `intensity?: number`, `child: Widget`

### `kenBurnsImage` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `src: AssetRef`, `duration?: Dimension`, `intensity?: number`, `startAlignment?: Alignment`, `endAlignment?: Alignment`, `loop?: boolean`, `curve?: AnimationCurve`, `width?: Dimension`, `height?: Dimension`, `fit?: string`

### `placeholder`
- aliases: `skeleton`
- properties: `click?: Action`, `tooltip?: string`, `fallbackWidth?: number`, `fallbackHeight?: number`, `color?: Color`, `strokeWidth?: number`, `child?: Widget`

### `progressBar`
- aliases: `linearProgressIndicator`, `loadingIndicator`, `loading-indicator`, `progress-bar`, `progress`
- properties: `click?: Action`, `tooltip?: string`, `value?: number | binding`, `indicatorType?: string`, `color?: Color`, `backgroundColor?: Color`, `size?: Dimension`, `strokeWidth?: any`

### `richText`
- properties: `click?: Action`, `tooltip?: string`, `spans: array<Span>`, `style?: TextStyle`, `dropCap?: DropCap`, `textAlign?: string`, `textDirection?: string`, `maxLines?: number`, `overflow?: string`, `softWrap?: boolean`, `textScaleFactor?: any`

### `text`
- aliases: `label`
- properties: `click?: Action`, `tooltip?: string`, `text: string`, `variant?: string`, `style?: TextStyle`, `dropCap?: DropCap`, `maxLines?: number`, `overflow?: string`, `textAlign?: string`, `textDirection?: string`, `aria-label?: any`, `ariaLabel?: any`, `semanticsLabel?: any`, `softWrap?: any`, `textScaleFactor?: any`, `textTransform?: string | binding`, `value?: string | number | boolean | object | array`

### `tooltip`
- properties: `click?: Action`, `tooltip?: string`, `message: string`, `child: Widget`, `decoration?: BoxDecoration`, `textAlign?: string`, `enableFeedback?: boolean`, `excludeFromSemantics?: boolean`, `height?: Dimension`, `margin?: EdgeInsets`, `padding?: EdgeInsets`, `preferBelow?: boolean`, `richMessage?: any`, `showDuration?: any`, `textStyle?: any`, `triggerMode?: any`, `verticalOffset?: any`, `waitDuration?: number`

### `verticalDivider`
- properties: `click?: Action`, `tooltip?: string`, `width?: number`, `thickness?: number`, `color?: Color`, `indent?: number`, `endIndent?: number`

## Input

### `button`
- properties: `click?: Action`, `tooltip?: string`, `label: string`, `variant?: string`, `elevation?: string`, `icon?: IconRef`, `enabled?: boolean`, `onTap?: Action`, `onDoubleTap?: Action`, `onLongPress?: Action`, `backgroundColor?: Color`, `borderColor?: Color`, `foregroundColor?: Color`, `loading?: boolean`, `onSubmit?: Action`, `submit?: Action`, `aria-label?: any`, `ariaLabel?: string | binding`, `borderWidth?: any`, `disabled?: boolean | binding`, `double-click?: Action`, `doubleClick?: Action`, `fullWidth?: boolean`, `iconPosition?: any`, `long-press?: Action`, `longPress?: Action`, `size?: Dimension`

### `checkbox`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `change?: Action`, `bindTo?: string`, `tristate?: boolean`

### `checkboxGroup`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `options: array<Option>`, `orientation?: string`, `change?: Action`, `direction?: string`

### `colorPicker`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `showAlpha?: boolean`, `showLabel?: boolean`, `pickerType?: string`, `enableHistory?: boolean`

### `combobox` *(since v1.4)*
- aliases: `autocomplete`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `options?: array<Option>`, `allowCustom?: boolean`, `onSearch?: Action`, `minChars?: number`, `debounceMs?: number`, `placeholder?: string`

### `dateField`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `format?: string`, `firstDate?: string`, `lastDate?: string`, `mode?: string`, `locale?: string`, `errorText?: any`

### `datePicker`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `firstDate?: string`, `lastDate?: string`, `change?: Action`, `dateFormat?: string`, `icon?: IconRef`, `variant?: string`, `bindTo?: string`, `initialDate?: any`

### `dateRangePicker`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `startDate?: string`, `endDate?: string`, `label?: string`, `firstDate?: string`, `lastDate?: string`, `format?: string`, `locale?: string`, `change?: Action`, `endBinding?: string`, `errorText?: any`, `startBinding?: string`

### `dateTimePicker` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `min?: string`, `max?: string`, `dateFormat?: string`, `timeFormat?: string`, `minuteInterval?: number`, `timeZone?: string`

### `fileInput` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `dragDrop?: boolean`, `maxFiles?: number`, `preview?: boolean`, `crop?: boolean`, `aspectRatio?: number`, `accept?: array<string>`, `multiple?: boolean`, `maxBytes?: number`, `label?: string`, `onError?: Action`

### `form`
- properties: `click?: Action`, `tooltip?: string`, `children: array<Widget>`, `showErrorsOn?: string`, `onSubmit?: Action`

### `iconButton`
- properties: `click?: Action`, `tooltip?: string`, `icon: IconRef`, `size?: number`, `color?: Color`, `enabled?: boolean`, `onTap?: Action`, `alignment?: Alignment`, `disabledColor?: Color`, `enableFeedback?: any`, `fontFamily?: string`, `highlightColor?: Color`, `iconSize?: any`, `padding?: EdgeInsets`, `splashColor?: Color`, `splashRadius?: any`

### `multiSelect` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `options: array<Option>`, `placeholder?: string`, `maxSelections?: number`, `showChips?: boolean`, `selectAll?: boolean`, `searchable?: boolean`

### `numberField`
- aliases: `numberInput`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `showStepper?: boolean`, `label?: string`, `min?: number`, `max?: number`, `step?: number`, `decimalPlaces?: number`, `prefix?: string`, `suffix?: string`, `thousandSeparator?: boolean`, `change?: Action`, `format?: string`, `helperText?: string`, `hint?: string`, `decimals?: number`, `error?: boolean | binding`

### `numberStepper`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `min?: number`, `max?: number`, `step?: number`, `change?: Action`, `color?: Color`, `size?: string | binding`

### `otpInput` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `length?: number`, `inputType?: string`, `autoSubmit?: Action`, `masked?: boolean`, `autofill?: boolean`

### `radio`
- properties: `click?: Action`, `tooltip?: string`, `value: any`, `groupValue: any | binding`, `label?: string`, `onChange?: Action`, `binding?: string`, `change?: Action`, `fillColor?: Color`, `activeColor?: Color`, `bindTo?: string`, `focusColor?: Color`, `hoverColor?: Color`, `splashRadius?: any`

### `radioGroup`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `options: array<Option>`, `orientation?: string`, `direction?: string`

### `rangeSlider`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `min?: number`, `max?: number`, `divisions?: number`, `change?: Action`, `activeColor?: Color`, `bindTo?: string`, `inactiveColor?: Color`, `labels?: any`, `onChangeEnd?: Action`, `onChangeStart?: Action`, `values?: any`

### `rating`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `max?: number`, `icon?: IconRef`, `color?: Color`, `change?: Action`, `allowHalf?: boolean`, `emptyColor?: Color`, `maxRating?: any`, `readOnly?: boolean`, `size?: Dimension`

### `segmentedControl`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `options: array<Option>`, `variant?: string`

### `select`
- aliases: `dropdown`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `options: array<Option>`, `placeholder?: string`, `change?: Action`, `elevation?: Dimension`, `hint?: string`, `label?: string`, `disabledHint?: string`, `iconSize?: any`, `isExpanded?: boolean`, `itemHeight?: any`

### `slider`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: number`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `min?: number`, `max?: number`, `divisions?: number`, `change?: Action`, `activeColor?: Color`, `change-end?: any`, `change-start?: any`, `changeEnd?: any`, `changeStart?: any`, `inactiveColor?: Color`, `onChangeEnd?: Action`, `onChangeStart?: Action`, `thumbColor?: Color`

### `stepper`
- aliases: `steps`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `steps: array<Step>`, `currentStep?: number | binding`, `stepperType?: string`, `onStepTapped?: Action`, `onStepContinue?: Action`, `onStepCancel?: Action`, `margin?: EdgeInsets`, `physics?: string`

### `textInput` *(since v1.0)*
- aliases: `textField`, `textfield`, `textFormField`, `text-form-field`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | binding`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `placeholder?: string`, `helperText?: string`, `prefixIcon?: string`, `suffixIcon?: string`, `obscureText?: boolean`, `readOnly?: boolean`, `maxLines?: integer`, `maxLength?: integer`, `inputType?: string`, `showToggle?: boolean`, `defaultCountry?: string`, `validation?: ValidationConfig`, `debounce?: number`, `error?: string | boolean | binding`, `errorText?: string | binding`, `focus?: Action`, `keyboardType?: string`, `textInputAction?: any`
- events: `onChange`, `onSubmit`, `onFocus`, `onBlur`

### `timeField`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `format?: string`, `use24HourFormat?: boolean`, `mode?: string`, `errorText?: any`

### `timePicker`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `label?: string`, `use24HourFormat?: boolean`, `change?: Action`, `icon?: IconRef`, `timeFormat?: string`, `variant?: string`, `bindTo?: string`, `initialTime?: any`

### `toggle`
- aliases: `switch`
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `change?: Action`, `label?: string`

### `voiceInput` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `value?: string | number | boolean | object | array`, `enabled?: boolean`, `onChange?: Action`, `language?: string`, `continuous?: boolean`, `interimResults?: boolean`, `maxDuration?: number`, `showWaveform?: boolean`
- events: `onStart`, `onResult`, `onEnd`, `onError`

## Interaction

### `contextMenu` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `items: array<object>`, `enabled?: boolean`
- events: `onSelect`

### `dragTarget`
- properties: `click?: Action`, `tooltip?: string`, `canDrop?: binding`, `builder: Widget`, `children?: array<Widget>`, `onDrop?: Action`, `onDragEnter?: Action`, `onDragLeave?: Action`

### `draggable`
- properties: `click?: Action`, `tooltip?: string`, `data: any | binding`, `feedback?: Widget`, `childWhenDragging?: Widget`, `child: Widget`

### `gestureDetector`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `onTap?: Action`, `onDoubleTap?: Action`, `onLongPress?: Action`, `onPanStart?: Action`, `onPanUpdate?: Action`, `onPanEnd?: Action`, `double-click?: Action`, `long-press?: Action`, `longPress?: Action`, `onScaleUpdate?: Action`, `panEnd?: any`, `panStart?: any`

### `inkWell`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `borderRadius?: number`, `onTap?: Action`, `onLongPress?: Action`, `onDoubleTap?: Action`, `autofocus?: boolean`, `canRequestFocus?: boolean`, `customBorder?: any`, `double-click?: Action`, `enableFeedback?: boolean`, `excludeFromSemantics?: boolean`, `focusColor?: Color`, `highlightColor?: Color`, `hover?: Action`, `hoverColor?: Color`, `long-press?: Action`, `longPress?: Action`, `onHighlightChanged?: Action`, `onHover?: Action`, `onTapCancel?: Action`, `onTapDown?: Action`, `onTapUp?: Action`, `overlayColor?: Color`, `splashColor?: Color`, `splashRadius?: number | binding`

## Layout

### `accordion` *(since v1.4)*
- aliases: `collapsible`
- properties: `click?: Action`, `tooltip?: string`, `panels: array<object>`, `allowMultiple?: boolean`, `expandedIds?: array<string>`, `bordered?: boolean`, `icon?: IconRef`
- events: `onChange`

### `align`
- properties: `click?: Action`, `tooltip?: string`, `alignment?: Alignment`, `child: Widget`, `heightFactor?: any`, `widthFactor?: Dimension`

### `aspectRatio`
- properties: `click?: Action`, `tooltip?: string`, `aspectRatio?: number`, `child: Widget`

### `box` *(since v1.0)*
- aliases: `container`, `constrained`
- properties: `click?: Action`, `tooltip?: string`, `width?: Dimension`, `height?: Dimension`, `minWidth?: number`, `maxWidth?: number`, `minHeight?: number`, `maxHeight?: number`, `padding?: string`, `margin?: EdgeInsets`, `alignment?: Alignment`, `color?: Color`, `decoration?: BoxDecoration`, `constraints?: object`
- children: single (key: `child`)

### `center`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `heightFactor?: any`, `widthFactor?: Dimension`

### `conditional`
- properties: `click?: Action`, `tooltip?: string`, `condition?: boolean | binding`, `then?: Widget`, `else?: Widget`, `switch?: binding`, `cases?: array`, `default?: Widget`

### `expanded`
- properties: `click?: Action`, `tooltip?: string`, `flex?: number`, `child: Widget`

### `flexible`
- properties: `click?: Action`, `tooltip?: string`, `flex?: number`, `fit?: string`, `child: Widget`

### `fractionallySized`
- properties: `click?: Action`, `tooltip?: string`, `widthFactor?: number`, `heightFactor?: number`, `child: Widget`, `alignment?: Alignment`

### `indexedStack`
- properties: `click?: Action`, `tooltip?: string`, `index?: number | binding`, `alignment?: Alignment`, `children: array<Widget>`, `textDirection?: string`, `clipBehavior?: any`, `sizing?: any`

### `intrinsicHeight`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`

### `intrinsicWidth`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `stepHeight?: any`, `stepWidth?: any`

### `linear`
- aliases: `row`, `column`
- properties: `click?: Action`, `tooltip?: string`, `mainAxisSize?: string`, `direction: string`, `alignment?: string`, `distribution?: string`, `spacing?: number`, `children: array<Widget>`, `padding?: EdgeInsets`, `wrap?: boolean | binding`

### `margin`
- properties: `click?: Action`, `tooltip?: string`, `margin: EdgeInsets`, `child: Widget`

### `padding`
- properties: `click?: Action`, `tooltip?: string`, `padding: EdgeInsets`, `child: Widget`

### `positioned`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `bottom?: Dimension`, `left?: Dimension`, `right?: Dimension`, `top?: Dimension`, `height?: Dimension`, `width?: Dimension`

### `resizable` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `width?: number | binding`, `height?: number | binding`, `minWidth?: number`, `maxWidth?: number`, `minHeight?: number`, `maxHeight?: number`, `handles?: array<string>`, `keepAspectRatio?: boolean`
- events: `onResize`, `onResizeEnd`

### `safeArea`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `bottom?: boolean`, `left?: boolean`, `right?: boolean`, `top?: boolean`, `maintainBottomViewPadding?: boolean`, `minimum?: Dimension`

### `sizedBox`
- properties: `click?: Action`, `tooltip?: string`, `width?: number`, `height?: number`, `child?: Widget`

### `spacer`
- properties: `click?: Action`, `tooltip?: string`, `flex?: number`

### `splitter` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `children: array<Widget>`, `orientation?: string`, `sizes?: array<number> | binding`, `minSizes?: array<number>`, `gutterSize?: number`, `collapsible?: array<boolean>`
- events: `onDragEnd`

### `stack`
- properties: `click?: Action`, `tooltip?: string`, `alignment?: Alignment`, `fit?: string`, `children: array<Widget>`, `textDirection?: string`, `clipBehavior?: any`

### `visibility`
- properties: `click?: Action`, `tooltip?: string`, `visible?: boolean | binding`, `maintainSize?: boolean`, `maintainState?: boolean`, `replacement?: Widget`, `child?: Widget`, `children?: array<Widget>`, `maintainAnimation?: any`, `maintainInteractivity?: any`

### `wrap`
- properties: `click?: Action`, `tooltip?: string`, `direction?: string`, `spacing?: number`, `runSpacing?: number`, `alignment?: string`, `children: array<Widget>`, `crossAxisAlignment?: string`, `textDirection?: string`, `clipBehavior?: any`, `runAlignment?: any`, `verticalDirection?: any`

## List

### `carousel` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `items?: array | binding`, `itemTemplate?: Widget`, `children?: array<Widget>`, `scrollDirection?: string`, `viewportFraction?: number`, `loop?: boolean`, `autoPlay?: boolean | number | binding`, `initialIndex?: number`, `transition?: string`, `indicatorPosition?: string`, `onPageChanged?: Action`

### `grid`
- aliases: `gridview`
- properties: `click?: Action`, `tooltip?: string`, `items?: array | binding`, `itemTemplate?: Widget`, `children?: array<Widget>`, `columns: number | object`, `rowGap?: number`, `columnGap?: number`, `itemAspectRatio?: number`, `reverse?: boolean`, `scrollDirection?: string`, `template?: object`, `childAspectRatio?: Dimension`, `crossAxisSpacing?: Dimension`, `mainAxisExtent?: any`, `mainAxisSpacing?: Dimension`, `maxCrossAxisExtent?: any`, `padding?: EdgeInsets`, `physics?: string`, `shrinkWrap?: boolean`, `spacing?: Dimension`

### `list`
- aliases: `listView`, `listview`
- properties: `click?: Action`, `tooltip?: string`, `virtual?: boolean`, `itemHeight?: number`, `overscan?: number`, `items?: array | binding`, `itemTemplate?: Widget`, `children?: array<Widget>`, `spacing?: number`, `orientation?: string`, `emptyMessage?: string`, `itemExtent?: number`, `reverse?: boolean`, `scrollDirection?: string`, `template?: object`, `itemBuilder?: any`, `itemCount?: any`, `itemSpacing?: Dimension`, `padding?: EdgeInsets`, `physics?: string`, `scrollCacheExtent?: any`, `shrinkWrap?: boolean`

### `listItem`
- aliases: `listTile`, `list-tile`
- properties: `click?: Action`, `tooltip?: string`, `title?: string | Widget`, `subtitle?: string | Widget`, `leading?: Widget`, `trailing?: Widget`, `onTap?: Action`, `selected?: boolean`, `enabled?: boolean`, `onLongPress?: Action`, `textColor?: Color`, `contentPadding?: EdgeInsets`, `dense?: boolean`, `focusColor?: Color`, `hoverColor?: Color`, `iconColor?: Color`, `isThreeLine?: boolean`, `long-press?: Action`, `longPress?: Action`, `selectedTileColor?: Color`, `shape?: any`, `tileColor?: Color`

### `staggeredGrid` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `items?: array | binding`, `itemTemplate?: Widget`, `children?: array<Widget>`, `columns: number | object`, `mainAxisSpacing?: number`, `crossAxisSpacing?: number`, `padding?: EdgeInsets`, `scrollDirection?: string`

## Navigation

### `bottomNavigation`
- aliases: `bottomNav`, `bottomnavigationbar`
- properties: `click?: Action`, `tooltip?: string`, `selectedIndex?: number | binding`, `items: array<NavItem>`, `onChange?: Action`, `backgroundColor?: Color`, `change?: Action`, `elevation?: Dimension`, `onTap?: Action`, `bindTo?: string`, `currentIndex?: number`, `enableFeedback?: boolean`, `fixedColor?: Color`, `iconSize?: any`, `selectedFontSize?: any`, `selectedIconTheme?: any`, `selectedItemColor?: Color`, `selectedLabelStyle?: any`, `showSelectedLabels?: boolean`, `showUnselectedLabels?: boolean`, `unselectedFontSize?: any`, `unselectedIconTheme?: any`, `unselectedItemColor?: Color`, `unselectedLabelStyle?: any`

### `breadcrumb` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `items: array<object>`, `separator?: string`, `maxItems?: number`
- events: `onClick`

### `drawer`
- properties: `click?: Action`, `tooltip?: string`, `items?: array<DrawerItem>`, `children?: array<Widget>`, `header?: Widget`, `onSelect?: Action`, `onClose?: Action`, `backgroundColor?: Color`, `elevation?: Dimension`, `semanticLabel?: string | binding`, `shadowColor?: Color`, `shape?: any`, `surfaceTintColor?: Color`, `width?: Dimension`

### `floatingActionButton`
- properties: `click?: Action`, `tooltip?: string`, `icon?: IconRef`, `label?: string`, `onTap?: Action`, `backgroundColor?: Color`, `elevation?: Dimension`, `foregroundColor?: Color`, `onLongPress?: Action`, `autofocus?: boolean`, `clipBehavior?: any`, `disabledElevation?: any`, `focusColor?: Color`, `focusElevation?: any`, `heroTag?: any`, `highlightElevation?: any`, `hoverColor?: Color`, `hoverElevation?: any`, `isExtended?: boolean`, `long-press?: Action`, `longPress?: Action`, `materialTapTargetSize?: any`, `mini?: boolean`, `shape?: any`, `splashColor?: Color`

### `headerBar`
- aliases: `appbar`
- properties: `click?: Action`, `tooltip?: string`, `title?: string | Widget`, `leading?: Widget`, `actions?: array<Widget>`, `exitButton?: ExitButtonConfig | boolean`, `backgroundColor?: Color`, `elevation?: number`, `centerTitle?: boolean`, `bottom?: Dimension`, `foregroundColor?: Color`, `automaticallyImplyLeading?: boolean`, `bottomHeight?: any`, `bottomOpacity?: any`, `flexibleSpace?: any`, `shadowColor?: Color`, `shape?: any`, `toolbarHeight?: any`, `toolbarOpacity?: any`

### `link` *(since v1.4)*
- aliases: `navLink`
- properties: `click?: Action`, `tooltip?: string`, `label: string`, `route?: string`, `params?: object`, `url?: string`, `target?: string`, `activeWhen?: string | binding`, `underline?: string`, `icon?: IconRef`, `child?: Widget`
- events: `onClick`

### `menu` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `items: array<object>`, `selectedKey?: string | binding`, `openKeys?: array<string>`, `mode?: string`, `collapsed?: boolean | binding`
- events: `onSelect`

### `navigationRail`
- properties: `click?: Action`, `tooltip?: string`, `selectedIndex?: number | binding`, `items: array<NavItem>`, `onChange?: Action`, `backgroundColor?: Color`, `change?: Action`, `elevation?: Dimension`, `leading?: Widget`, `onSelect?: Action`, `trailing?: Widget`, `extended?: boolean`, `groupAlignment?: any`, `labelType?: any`, `minExtendedWidth?: any`, `minWidth?: Dimension`, `onDestinationSelected?: Action`, `select?: Action`, `selectedIconTheme?: any`, `selectedLabelTextStyle?: any`, `unselectedIconTheme?: any`, `unselectedLabelTextStyle?: any`

### `pagination` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `binding?: string`, `total: number`, `pageSize?: number`, `siblingCount?: number`, `showSizeChanger?: boolean`, `pageSizeOptions?: array<number>`, `showTotal?: boolean`, `current?: number | binding`
- events: `onChange`

### `popupMenuButton`
- aliases: `dropdownMenu`
- properties: `click?: Action`, `tooltip?: string`, `icon?: IconRef`, `items: array<MenuItem>`, `onSelect?: Action`, `change?: Action`, `color?: Color`, `elevation?: Dimension`, `onChange?: Action`, `enabled?: boolean`, `iconSize?: any`, `offset?: any`, `onCanceled?: Action`, `onOpened?: Action`, `onSelected?: Action`, `padding?: EdgeInsets`, `select?: Action`, `shadowColor?: Color`, `shape?: any`, `splashRadius?: any`, `surfaceTintColor?: Color`

### `tabBar`
- properties: `click?: Action`, `tooltip?: string`, `selectedIndex?: number | binding`, `tabs: array<Tab>`, `onChange?: Action`, `change?: Action`, `indicatorColor?: Color`, `labelStyle?: TextStyle`, `onTap?: Action`, `enableFeedback?: boolean`, `indicator?: any`, `indicatorPadding?: EdgeInsets`, `indicatorSize?: any`, `indicatorWeight?: any`, `isScrollable?: boolean`, `labelColor?: Color`, `labelPadding?: EdgeInsets`, `mouseCursor?: any`, `overlayColor?: Color`, `padding?: EdgeInsets`, `physics?: string`, `unselectedLabelColor?: Color`, `unselectedLabelStyle?: any`

### `tabBarView`
- properties: `click?: Action`, `tooltip?: string`, `selectedIndex?: number | binding`, `children: array<Widget>`, `dragStartBehavior?: any`, `physics?: string`

## Scroll

### `pageView`
- properties: `click?: Action`, `tooltip?: string`, `direction?: string`, `children: array<Widget>`, `initialPage?: number`, `loop?: boolean`, `scrollPhysics?: string`, `allowImplicitScrolling?: boolean`, `onPageChanged?: Action`, `onChange?: Action`, `reverse?: boolean`, `scrollDirection?: string`, `clipBehavior?: any`, `padEnds?: boolean`, `pageSnapping?: boolean`

### `scrollBar`
- properties: `click?: Action`, `tooltip?: string`, `thumbVisibility?: boolean`, `trackVisibility?: boolean`, `thickness?: number`, `radius?: number`, `child?: Widget`, `children?: array<Widget>`

### `scrollView`
- aliases: `scrollArea`
- properties: `click?: Action`, `tooltip?: string`, `direction?: string`, `padding?: EdgeInsets`, `scrollPhysics?: string`, `child?: Widget`, `children?: array<Widget>`, `slivers?: array<Sliver>`, `reverse?: boolean`, `scrollDirection?: string`, `physics?: string`, `primary?: boolean`

### `singleChildScrollView`
- properties: `click?: Action`, `tooltip?: string`, `direction?: string`, `padding?: EdgeInsets`, `child?: Widget`, `children?: array<Widget>`, `reverse?: boolean`, `scrollDirection?: string`, `clipBehavior?: any`, `physics?: string`, `primary?: boolean`

## Utility

### `accessibleWrapper`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `accessibility?: object`, `announceNavigation?: boolean`, `announceOnChange?: boolean`, `autoFocus?: boolean`, `focusGroup?: string`, `focusOrder?: number`, `liveRegion?: string`, `navigationMessage?: string`, `watchPath?: string`

### `baseline`
- properties: `click?: Action`, `tooltip?: string`, `baseline: number`, `baselineType?: string`, `child: Widget`

### `clipOval`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `clipBehavior?: any`

### `clipRRect`
- properties: `click?: Action`, `tooltip?: string`, `borderRadius?: BorderRadius`, `child: Widget`, `clipBehavior?: any`

### `dashboard` *(since v1.3)*
- properties: `click?: Action`, `tooltip?: string`, `content?: Widget`, `refreshInterval?: number`, `onTap?: Action`

### `errorBoundary`
- properties: `click?: Action`, `tooltip?: string`, `child: Widget`, `fallback?: Widget`, `onError?: Action`

### `errorRecovery`
- properties: `click?: Action`, `tooltip?: string`, `child?: Widget`, `children?: array<Widget>`, `fallback?: Widget`, `handlers?: object`, `onError?: Action`, `showDetails?: boolean`

### `fittedBox`
- properties: `click?: Action`, `tooltip?: string`, `fit?: string`, `alignment?: Alignment`, `child: Widget`, `clipBehavior?: any`

### `flow`
- properties: `click?: Action`, `tooltip?: string`, `children: array<Widget>`, `direction?: string`, `spacing?: number`, `alignment?: string`

### `layoutBuilder`
- properties: `click?: Action`, `tooltip?: string`, `breakpoints?: object`, `layouts?: object`, `default?: Widget`

### `lazy` *(since v1.0)*
- properties: `click?: Action`, `tooltip?: string`, `placeholder?: Widget`, `content?: Widget | object`, `child?: Widget`, `children?: array<Widget>`, `trigger?: string`, `onLoad?: Action`, `onError?: Action`, `delay?: number | binding`

### `limitedBox`
- properties: `click?: Action`, `tooltip?: string`, `maxWidth?: number`, `maxHeight?: number`, `child: Widget`

### `mediaQuery`
- properties: `click?: Action`, `tooltip?: string`, `condition?: object | binding`, `then?: Widget`, `else?: Widget`, `breakpoints?: object`, `defaultChild?: Widget`, `orElse?: object`

### `offlineFallback`
- properties: `click?: Action`, `tooltip?: string`, `online?: Widget`, `offline?: Widget`, `message?: string`, `icon?: IconRef`, `showRetry?: boolean`, `onRetry?: Action`, `isOnline?: boolean | binding`

### `permissionPrompt`
- properties: `click?: Action`, `tooltip?: string`, `permissions?: array<string>`, `permissionType?: string`, `style?: string`, `title?: string`, `description?: string`, `icon?: IconRef`, `allowPartial?: boolean`, `onAllow?: Action`, `onDeny?: Action`

### `use`
- properties: `click?: Action`, `tooltip?: string`, `template: string`, `params?: object`, `slots?: object`

### `view` *(since v1.4)*
- properties: `click?: Action`, `tooltip?: string`, `source: DefinitionSource`, `props?: object`, `fallback?: Widget`, `loading?: Widget`, `onError?: Action`, `theme?: string`

