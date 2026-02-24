<!DOCTYPE html>

<html lang="en">
<head><meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>lab_M4L1_Land_Classification_CNN-ViT_Integration_Evaluation </title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .pm { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation.Marker */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0 solid transparent;
  border-right: 0 solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0 solid transparent;
  border-bottom: 0 solid transparent;
}

/*
 * Lumino
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
}

.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.lm-AccordionPanel[data-orientation='horizontal'] > .lm-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-CommandPalette-search {
  flex: 0 0 auto;
}

.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}

.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}

.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}

.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
  border: 1px solid transparent;
  background-color: transparent;
  position: absolute;
  z-index: 1;
  right: 3%;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 7px 0;
  display: none;
  vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
  content: 'X';
  display: block;
  width: 15px;
  height: 15px;
  text-align: center;
  color: #000;
  font-weight: normal;
  font-size: 12px;
  cursor: pointer;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-DockPanel {
  z-index: 0;
}

.lm-DockPanel-widget {
  z-index: 0;
}

.lm-DockPanel-tabBar {
  z-index: 1;
}

.lm-DockPanel-handle {
  z-index: 2;
}

.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}

.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}

.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}

.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}

.lm-Menu-item {
  display: table-row;
}

.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}

.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}

.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}

.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.lm-MenuBar-item {
  box-sizing: border-box;
}

.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}

.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}

.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}

.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}

.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-SplitPanel-child {
  z-index: 0;
}

.lm-SplitPanel-handle {
  z-index: 1;
}

.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}

.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}

.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}

.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}

.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}

.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
  touch-action: none; /* Disable native Drag/Drop */
}

.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}

.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
}

.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}

.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}

.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
  background: inherit;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabPanel-tabBar {
  z-index: 1;
}

.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.jp-Collapse-header {
  padding: 1px 12px;
  background-color: var(--jp-layout-color1);
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  text-transform: uppercase;
  user-select: none;
}

.jp-Collapser-icon {
  height: 16px;
}

.jp-Collapse-header-collapsed .jp-Collapser-icon {
  transform: rotate(-90deg);
  margin: auto 0;
}

.jp-Collapser-title {
  line-height: 25px;
}

.jp-Collapse-contents {
  padding: 0 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add-above: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5MikiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik00Ljc1IDQuOTMwNjZINi42MjVWNi44MDU2NkM2LjYyNSA3LjAxMTkxIDYuNzkzNzUgNy4xODA2NiA3IDcuMTgwNjZDNy4yMDYyNSA3LjE4MDY2IDcuMzc1IDcuMDExOTEgNy4zNzUgNi44MDU2NlY0LjkzMDY2SDkuMjVDOS40NTYyNSA0LjkzMDY2IDkuNjI1IDQuNzYxOTEgOS42MjUgNC41NTU2NkM5LjYyNSA0LjM0OTQxIDkuNDU2MjUgNC4xODA2NiA5LjI1IDQuMTgwNjZINy4zNzVWMi4zMDU2NkM3LjM3NSAyLjA5OTQxIDcuMjA2MjUgMS45MzA2NiA3IDEuOTMwNjZDNi43OTM3NSAxLjkzMDY2IDYuNjI1IDIuMDk5NDEgNi42MjUgMi4zMDU2NlY0LjE4MDY2SDQuNzVDNC41NDM3NSA0LjE4MDY2IDQuMzc1IDQuMzQ5NDEgNC4zNzUgNC41NTU2NkM0LjM3NSA0Ljc2MTkxIDQuNTQzNzUgNC45MzA2NiA0Ljc1IDQuOTMwNjZaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC43Ii8+CjwvZz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgOS41VjExLjVMMi41IDExLjVWOS41TDExLjUgOS41Wk0xMiA4QzEyLjU1MjMgOCAxMyA4LjQ0NzcyIDEzIDlWMTJDMTMgMTIuNTUyMyAxMi41NTIzIDEzIDEyIDEzTDIgMTNDMS40NDc3MiAxMyAxIDEyLjU1MjMgMSAxMlY5QzEgOC40NDc3MiAxLjQ0NzcxIDggMiA4TDEyIDhaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5MiI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KC0xIDAgMCAxIDEwIDEuNTU1NjYpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==);
  --jp-icon-add-below: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5OCkiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik05LjI1IDEwLjA2OTNMNy4zNzUgMTAuMDY5M0w3LjM3NSA4LjE5NDM0QzcuMzc1IDcuOTg4MDkgNy4yMDYyNSA3LjgxOTM0IDcgNy44MTkzNEM2Ljc5Mzc1IDcuODE5MzQgNi42MjUgNy45ODgwOSA2LjYyNSA4LjE5NDM0TDYuNjI1IDEwLjA2OTNMNC43NSAxMC4wNjkzQzQuNTQzNzUgMTAuMDY5MyA0LjM3NSAxMC4yMzgxIDQuMzc1IDEwLjQ0NDNDNC4zNzUgMTAuNjUwNiA0LjU0Mzc1IDEwLjgxOTMgNC43NSAxMC44MTkzTDYuNjI1IDEwLjgxOTNMNi42MjUgMTIuNjk0M0M2LjYyNSAxMi45MDA2IDYuNzkzNzUgMTMuMDY5MyA3IDEzLjA2OTNDNy4yMDYyNSAxMy4wNjkzIDcuMzc1IDEyLjkwMDYgNy4zNzUgMTIuNjk0M0w3LjM3NSAxMC44MTkzTDkuMjUgMTAuODE5M0M5LjQ1NjI1IDEwLjgxOTMgOS42MjUgMTAuNjUwNiA5LjYyNSAxMC40NDQzQzkuNjI1IDEwLjIzODEgOS40NTYyNSAxMC4wNjkzIDkuMjUgMTAuMDY5M1oiIGZpbGw9IiM2MTYxNjEiIHN0cm9rZT0iIzYxNjE2MSIgc3Ryb2tlLXdpZHRoPSIwLjciLz4KPC9nPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMi41IDUuNUwyLjUgMy41TDExLjUgMy41TDExLjUgNS41TDIuNSA1LjVaTTIgN0MxLjQ0NzcyIDcgMSA2LjU1MjI4IDEgNkwxIDNDMSAyLjQ0NzcyIDEuNDQ3NzIgMiAyIDJMMTIgMkMxMi41NTIzIDIgMTMgMi40NDc3MiAxMyAzTDEzIDZDMTMgNi41NTIyOSAxMi41NTIzIDcgMTIgN0wyIDdaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5OCI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KDEgMS43NDg0NmUtMDcgMS43NDg0NmUtMDcgLTEgNCAxMy40NDQzKSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bell: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE2IDE2IiB2ZXJzaW9uPSIxLjEiPgogICA8cGF0aCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzMzMzMzIgogICAgICBkPSJtOCAwLjI5Yy0xLjQgMC0yLjcgMC43My0zLjYgMS44LTEuMiAxLjUtMS40IDMuNC0xLjUgNS4yLTAuMTggMi4yLTAuNDQgNC0yLjMgNS4zbDAuMjggMS4zaDVjMC4wMjYgMC42NiAwLjMyIDEuMSAwLjcxIDEuNSAwLjg0IDAuNjEgMiAwLjYxIDIuOCAwIDAuNTItMC40IDAuNi0xIDAuNzEtMS41aDVsMC4yOC0xLjNjLTEuOS0wLjk3LTIuMi0zLjMtMi4zLTUuMy0wLjEzLTEuOC0wLjI2LTMuNy0xLjUtNS4yLTAuODUtMS0yLjItMS44LTMuNi0xLjh6bTAgMS40YzAuODggMCAxLjkgMC41NSAyLjUgMS4zIDAuODggMS4xIDEuMSAyLjcgMS4yIDQuNCAwLjEzIDEuNyAwLjIzIDMuNiAxLjMgNS4yaC0xMGMxLjEtMS42IDEuMi0zLjQgMS4zLTUuMiAwLjEzLTEuNyAwLjMtMy4zIDEuMi00LjQgMC41OS0wLjcyIDEuNi0xLjMgMi41LTEuM3ptLTAuNzQgMTJoMS41Yy0wLjAwMTUgMC4yOCAwLjAxNSAwLjc5LTAuNzQgMC43OS0wLjczIDAuMDAxNi0wLjcyLTAuNTMtMC43NC0wLjc5eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-bug-dot: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiPgogICAgICAgIDxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMTcuMTkgOEgyMFYxMEgxNy45MUMxNy45NiAxMC4zMyAxOCAxMC42NiAxOCAxMVYxMkgyMFYxNEgxOC41SDE4VjE0LjAyNzVDMTUuNzUgMTQuMjc2MiAxNCAxNi4xODM3IDE0IDE4LjVDMTQgMTkuMjA4IDE0LjE2MzUgMTkuODc3OSAxNC40NTQ5IDIwLjQ3MzlDMTMuNzA2MyAyMC44MTE3IDEyLjg3NTcgMjEgMTIgMjFDOS43OCAyMSA3Ljg1IDE5Ljc5IDYuODEgMThINFYxNkg2LjA5QzYuMDQgMTUuNjcgNiAxNS4zNCA2IDE1VjE0SDRWMTJINlYxMUM2IDEwLjY2IDYuMDQgMTAuMzMgNi4wOSAxMEg0VjhINi44MUM3LjI2IDcuMjIgNy44OCA2LjU1IDguNjIgNi4wNEw3IDQuNDFMOC40MSAzTDEwLjU5IDUuMTdDMTEuMDQgNS4wNiAxMS41MSA1IDEyIDVDMTIuNDkgNSAxMi45NiA1LjA2IDEzLjQyIDUuMTdMMTUuNTkgM0wxNyA0LjQxTDE1LjM3IDYuMDRDMTYuMTIgNi41NSAxNi43NCA3LjIyIDE3LjE5IDhaTTEwIDE2SDE0VjE0SDEwVjE2Wk0xMCAxMkgxNFYxMEgxMFYxMloiIGZpbGw9IiM2MTYxNjEiLz4KICAgICAgICA8cGF0aCBkPSJNMjIgMTguNUMyMiAyMC40MzMgMjAuNDMzIDIyIDE4LjUgMjJDMTYuNTY3IDIyIDE1IDIwLjQzMyAxNSAxOC41QzE1IDE2LjU2NyAxNi41NjcgMTUgMTguNSAxNUMyMC40MzMgMTUgMjIgMTYuNTY3IDIyIDE4LjVaIiBmaWxsPSIjNjE2MTYxIi8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBzaGFwZS1yZW5kZXJpbmc9Imdlb21ldHJpY1ByZWNpc2lvbiI+CiAgICA8cGF0aCBkPSJNNi41OSwzLjQxTDIsOEw2LjU5LDEyLjZMOCwxMS4xOEw0LjgyLDhMOCw0LjgyTDYuNTksMy40MU0xMi40MSwzLjQxTDExLDQuODJMMTQuMTgsOEwxMSwxMS4xOEwxMi40MSwxMi42TDE3LDhMMTIuNDEsMy40MU0yMS41OSwxMS41OUwxMy41LDE5LjY4TDkuODMsMTZMOC40MiwxNy40MUwxMy41LDIyLjVMMjMsMTNMMjEuNTksMTEuNTlaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-collapse-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNNiAxM3YyaDh2LTJ6IiAvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1jb25zb2xlLWljb24tYmFja2dyb3VuZC1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtY29uc29sZS1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIj4KICAgIDxwYXRoIGQ9Ik0xMDUgMTI3LjNoNDB2MTIuOGgtNDB6TTUxLjEgNzdMNzQgOTkuOWwtMjMuMyAyMy4zIDEwLjUgMTAuNSAyMy4zLTIzLjNMOTUgOTkuOSA4NC41IDg5LjQgNjEuNiA2Ni41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-delete: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CiAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIiAvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjI2MjYyIiBkPSJNNiAxOWMwIDEuMS45IDIgMiAyaDhjMS4xIDAgMi0uOSAyLTJWN0g2djEyek0xOSA0aC0zLjVsLTEtMWgtNWwtMSAxSDV2MmgxNFY0eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-duplicate: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTIuNzk5OTggMC44NzVIOC44OTU4MkM5LjIwMDYxIDAuODc1IDkuNDQ5OTggMS4xMzkxNCA5LjQ0OTk4IDEuNDYxOThDOS40NDk5OCAxLjc4NDgyIDkuMjAwNjEgMi4wNDg5NiA4Ljg5NTgyIDIuMDQ4OTZIMy4zNTQxNUMzLjA0OTM2IDIuMDQ4OTYgMi43OTk5OCAyLjMxMzEgMi43OTk5OCAyLjYzNTk0VjkuNjc5NjlDMi43OTk5OCAxMC4wMDI1IDIuNTUwNjEgMTAuMjY2NyAyLjI0NTgyIDEwLjI2NjdDMS45NDEwMyAxMC4yNjY3IDEuNjkxNjUgMTAuMDAyNSAxLjY5MTY1IDkuNjc5NjlWMi4wNDg5NkMxLjY5MTY1IDEuNDAzMjggMi4xOTA0IDAuODc1IDIuNzk5OTggMC44NzVaTTUuMzY2NjUgMTEuOVY0LjU1SDExLjA4MzNWMTEuOUg1LjM2NjY1Wk00LjE0MTY1IDQuMTQxNjdDNC4xNDE2NSAzLjY5MDYzIDQuNTA3MjggMy4zMjUgNC45NTgzMiAzLjMyNUgxMS40OTE3QzExLjk0MjcgMy4zMjUgMTIuMzA4MyAzLjY5MDYzIDEyLjMwODMgNC4xNDE2N1YxMi4zMDgzQzEyLjMwODMgMTIuNzU5NCAxMS45NDI3IDEzLjEyNSAxMS40OTE3IDEzLjEyNUg0Ljk1ODMyQzQuNTA3MjggMTMuMTI1IDQuMTQxNjUgMTIuNzU5NCA0LjE0MTY1IDEyLjMwODNWNC4xNDE2N1oiIGZpbGw9IiM2MTYxNjEiLz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNOS40MzU3NCA4LjI2NTA3SDguMzY0MzFWOS4zMzY1QzguMzY0MzEgOS40NTQzNSA4LjI2Nzg4IDkuNTUwNzggOC4xNTAwMiA5LjU1MDc4QzguMDMyMTcgOS41NTA3OCA3LjkzNTc0IDkuNDU0MzUgNy45MzU3NCA5LjMzNjVWOC4yNjUwN0g2Ljg2NDMxQzYuNzQ2NDUgOC4yNjUwNyA2LjY1MDAyIDguMTY4NjQgNi42NTAwMiA4LjA1MDc4QzYuNjUwMDIgNy45MzI5MiA2Ljc0NjQ1IDcuODM2NSA2Ljg2NDMxIDcuODM2NUg3LjkzNTc0VjYuNzY1MDdDNy45MzU3NCA2LjY0NzIxIDguMDMyMTcgNi41NTA3OCA4LjE1MDAyIDYuNTUwNzhDOC4yNjc4OCA2LjU1MDc4IDguMzY0MzEgNi42NDcyMSA4LjM2NDMxIDYuNzY1MDdWNy44MzY1SDkuNDM1NzRDOS41NTM2IDcuODM2NSA5LjY1MDAyIDcuOTMyOTIgOS42NTAwMiA4LjA1MDc4QzkuNjUwMDIgOC4xNjg2NCA5LjU1MzYgOC4yNjUwNyA5LjQzNTc0IDguMjY1MDdaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC41Ii8+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-error: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjE5IiByPSIyIi8+PHBhdGggZD0iTTEwIDNoNHYxMmgtNHoiLz48L2c+CjxwYXRoIGZpbGw9Im5vbmUiIGQ9Ik0wIDBoMjR2MjRIMHoiLz4KPC9zdmc+Cg==);
  --jp-icon-expand-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNMTEgMTBIOXYzSDZ2MmgzdjNoMnYtM2gzdi0yaC0zeiIgLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-dot: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWRvdCIgZmlsbD0iI0ZGRiI+CiAgICA8Y2lyY2xlIGN4PSIxOCIgY3k9IjE3IiByPSIzIj48L2NpcmNsZT4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-filter: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-folder-favorite: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgwVjB6IiBmaWxsPSJub25lIi8+PHBhdGggY2xhc3M9ImpwLWljb24zIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxNjE2MSIgZD0iTTIwIDZoLThsLTItMkg0Yy0xLjEgMC0yIC45LTIgMnYxMmMwIDEuMS45IDIgMiAyaDE2YzEuMSAwIDItLjkgMi0yVjhjMC0xLjEtLjktMi0yLTJ6bS0yLjA2IDExTDE1IDE1LjI4IDEyLjA2IDE3bC43OC0zLjMzLTIuNTktMi4yNCAzLjQxLS4yOUwxNSA4bDEuMzQgMy4xNCAzLjQxLjI5LTIuNTkgMi4yNC43OCAzLjMzeiIvPgo8L3N2Zz4K);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-home: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xMCAyMHYtNmg0djZoNXYtOGgzTDEyIDMgMiAxMmgzdjh6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUwLjk3OCA1MC45NzgiPgoJPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KCQk8cGF0aCBkPSJNNDMuNTIsNy40NThDMzguNzExLDIuNjQ4LDMyLjMwNywwLDI1LjQ4OSwwQzE4LjY3LDAsMTIuMjY2LDIuNjQ4LDcuNDU4LDcuNDU4CgkJCWMtOS45NDMsOS45NDEtOS45NDMsMjYuMTE5LDAsMzYuMDYyYzQuODA5LDQuODA5LDExLjIxMiw3LjQ1NiwxOC4wMzEsNy40NThjMCwwLDAuMDAxLDAsMC4wMDIsMAoJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoKCQkJIE00Mi4xMDYsNDIuMTA1Yy00LjQzMiw0LjQzMS0xMC4zMzIsNi44NzItMTYuNjE1LDYuODcyaC0wLjAwMmMtNi4yODUtMC4wMDEtMTIuMTg3LTIuNDQxLTE2LjYxNy02Ljg3MgoJCQljLTkuMTYyLTkuMTYzLTkuMTYyLTI0LjA3MSwwLTMzLjIzM0MxMy4zMDMsNC40NCwxOS4yMDQsMiwyNS40ODksMmM2LjI4NCwwLDEyLjE4NiwyLjQ0LDE2LjYxNyw2Ljg3MgoJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4KCQk8cGF0aCBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1MwoJCQljMC40NjgtMC41MzYsMC45MjMtMS4wNjIsMS4zNjctMS41NzVjMC42MjYtMC43NTMsMS4xMDQtMS40NzgsMS40MzYtMi4xNzVjMC4zMzEtMC43MDcsMC40OTUtMS41NDEsMC40OTUtMi41CgkJCWMwLTEuMDk2LTAuMjYtMi4wODgtMC43NzktMi45NzljLTAuNTY1LTAuODc5LTEuNTAxLTEuMzM2LTIuODA2LTEuMzY5Yy0xLjgwMiwwLjA1Ny0yLjk4NSwwLjY2Ny0zLjU1LDEuODMyCgkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkKCQkJYzEuMDYyLTEuNjQsMi44NTUtMi40ODEsNS4zNzgtMi41MjdjMi4xNiwwLjAyMywzLjg3NCwwLjYwOCw1LjE0MSwxLjc1OGMxLjI3OCwxLjE2LDEuOTI5LDIuNzY0LDEuOTUsNC44MTEKCQkJYzAsMS4xNDItMC4xMzcsMi4xMTEtMC40MSwyLjkxMWMtMC4zMDksMC44NDUtMC43MzEsMS41OTMtMS4yNjgsMi4yNDNjLTAuNDkyLDAuNjUtMS4wNjgsMS4zMTgtMS43MywyLjAwMgoJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5CgkJCUMyNi41ODksMzIuMjE4LDIzLjU3OCwzMi4yMTgsMjMuNTc4LDMyLjIxOHogTTIzLjU3OCwzOC4yMnYtMy40ODRoMy4wNzZ2My40ODRIMjMuNTc4eiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaW5zcGVjdG9yLWljb24tY29sb3IganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtanNvbi1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0Y5QTgyNSI+CiAgICA8cGF0aCBkPSJNMjAuMiAxMS44Yy0xLjYgMC0xLjcuNS0xLjcgMSAwIC40LjEuOS4xIDEuMy4xLjUuMS45LjEgMS4zIDAgMS43LTEuNCAyLjMtMy41IDIuM2gtLjl2LTEuOWguNWMxLjEgMCAxLjQgMCAxLjQtLjggMC0uMyAwLS42LS4xLTEgMC0uNC0uMS0uOC0uMS0xLjIgMC0xLjMgMC0xLjggMS4zLTItMS4zLS4yLTEuMy0uNy0xLjMtMiAwLS40LjEtLjguMS0xLjIuMS0uNC4xLS43LjEtMSAwLS44LS40LS43LTEuNC0uOGgtLjVWNC4xaC45YzIuMiAwIDMuNS43IDMuNSAyLjMgMCAuNC0uMS45LS4xIDEuMy0uMS41LS4xLjktLjEgMS4zIDAgLjUuMiAxIDEuNyAxdjEuOHpNMS44IDEwLjFjMS42IDAgMS43LS41IDEuNy0xIDAtLjQtLjEtLjktLjEtMS4zLS4xLS41LS4xLS45LS4xLTEuMyAwLTEuNiAxLjQtMi4zIDMuNS0yLjNoLjl2MS45aC0uNWMtMSAwLTEuNCAwLTEuNC44IDAgLjMgMCAuNi4xIDEgMCAuMi4xLjYuMSAxIDAgMS4zIDAgMS44LTEuMyAyQzYgMTEuMiA2IDExLjcgNiAxM2MwIC40LS4xLjgtLjEgMS4yLS4xLjMtLjEuNy0uMSAxIDAgLjguMy44IDEuNC44aC41djEuOWgtLjljLTIuMSAwLTMuNS0uNi0zLjUtMi4zIDAtLjQuMS0uOS4xLTEuMy4xLS41LjEtLjkuMS0xLjMgMC0uNS0uMi0xLTEuNy0xdi0xLjl6Ii8+CiAgICA8Y2lyY2xlIGN4PSIxMSIgY3k9IjEzLjgiIHI9IjIuMSIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSI4LjIiIHI9IjIuMSIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgPGcgY2xhc3M9ImpwLWp1cHl0ZXItaWNvbi1jb2xvciIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgIDxnIGNsYXNzPSJqcC1qdXB5dGVyLWljb24tY29sb3IiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launch: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMzIgMzIiIHdpZHRoPSIzMiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yNiwyOEg2YTIuMDAyNywyLjAwMjcsMCwwLDEtMi0yVjZBMi4wMDI3LDIuMDAyNywwLDAsMSw2LDRIMTZWNkg2VjI2SDI2VjE2aDJWMjZBMi4wMDI3LDIuMDAyNywwLDAsMSwyNiwyOFoiLz4KICAgIDxwb2x5Z29uIHBvaW50cz0iMjAgMiAyMCA0IDI2LjU4NiA0IDE4IDEyLjU4NiAxOS40MTQgMTQgMjggNS40MTQgMjggMTIgMzAgMTIgMzAgMiAyMCAyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4K);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-move-down: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMTIuNDcxIDcuNTI4OTlDMTIuNzYzMiA3LjIzNjg0IDEyLjc2MzIgNi43NjMxNiAxMi40NzEgNi40NzEwMVY2LjQ3MTAxQzEyLjE3OSA2LjE3OTA1IDExLjcwNTcgNi4xNzg4NCAxMS40MTM1IDYuNDcwNTRMNy43NSAxMC4xMjc1VjEuNzVDNy43NSAxLjMzNTc5IDcuNDE0MjEgMSA3IDFWMUM2LjU4NTc5IDEgNi4yNSAxLjMzNTc5IDYuMjUgMS43NVYxMC4xMjc1TDIuNTk3MjYgNi40NjgyMkMyLjMwMzM4IDYuMTczODEgMS44MjY0MSA2LjE3MzU5IDEuNTMyMjYgNi40Njc3NFY2LjQ2Nzc0QzEuMjM4MyA2Ljc2MTcgMS4yMzgzIDcuMjM4MyAxLjUzMjI2IDcuNTMyMjZMNi4yOTI4OSAxMi4yOTI5QzYuNjgzNDIgMTIuNjgzNCA3LjMxNjU4IDEyLjY4MzQgNy43MDcxMSAxMi4yOTI5TDEyLjQ3MSA3LjUyODk5WiIgZmlsbD0iIzYxNjE2MSIvPgo8L3N2Zz4K);
  --jp-icon-move-up: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMS41Mjg5OSA2LjQ3MTAxQzEuMjM2ODQgNi43NjMxNiAxLjIzNjg0IDcuMjM2ODQgMS41Mjg5OSA3LjUyODk5VjcuNTI4OTlDMS44MjA5NSA3LjgyMDk1IDIuMjk0MjYgNy44MjExNiAyLjU4NjQ5IDcuNTI5NDZMNi4yNSAzLjg3MjVWMTIuMjVDNi4yNSAxMi42NjQyIDYuNTg1NzkgMTMgNyAxM1YxM0M3LjQxNDIxIDEzIDcuNzUgMTIuNjY0MiA3Ljc1IDEyLjI1VjMuODcyNUwxMS40MDI3IDcuNTMxNzhDMTEuNjk2NiA3LjgyNjE5IDEyLjE3MzYgNy44MjY0MSAxMi40Njc3IDcuNTMyMjZWNy41MzIyNkMxMi43NjE3IDcuMjM4MyAxMi43NjE3IDYuNzYxNyAxMi40Njc3IDYuNDY3NzRMNy43MDcxMSAxLjcwNzExQzcuMzE2NTggMS4zMTY1OCA2LjY4MzQyIDEuMzE2NTggNi4yOTI4OSAxLjcwNzExTDEuNTI4OTkgNi40NzEwMVoiIGZpbGw9IiM2MTYxNjEiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtbm90ZWJvb2staWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iLTEwIC0xMCAxMzEuMTYxMzYxNjk0MzM1OTQgMTMyLjM4ODk5OTkzODk2NDg0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzA2OTk4IiBkPSJNIDU0LjkxODc4NSw5LjE5Mjc0MjFlLTQgQyA1MC4zMzUxMzIsMC4wMjIyMTcyNyA0NS45NTc4NDYsMC40MTMxMzY5NyA0Mi4xMDYyODUsMS4wOTQ2NjkzIDMwLjc2MDA2OSwzLjA5OTE3MzEgMjguNzAwMDM2LDcuMjk0NzcxNCAyOC43MDAwMzUsMTUuMDMyMTY5IHYgMTAuMjE4NzUgaCAyNi44MTI1IHYgMy40MDYyNSBoIC0yNi44MTI1IC0xMC4wNjI1IGMgLTcuNzkyNDU5LDAgLTE0LjYxNTc1ODgsNC42ODM3MTcgLTE2Ljc0OTk5OTgsMTMuNTkzNzUgLTIuNDYxODE5OTgsMTAuMjEyOTY2IC0yLjU3MTAxNTA4LDE2LjU4NjAyMyAwLDI3LjI1IDEuOTA1OTI4Myw3LjkzNzg1MiA2LjQ1NzU0MzIsMTMuNTkzNzQ4IDE0LjI0OTk5OTgsMTMuNTkzNzUgaCA5LjIxODc1IHYgLTEyLjI1IGMgMCwtOC44NDk5MDIgNy42NTcxNDQsLTE2LjY1NjI0OCAxNi43NSwtMTYuNjU2MjUgaCAyNi43ODEyNSBjIDcuNDU0OTUxLDAgMTMuNDA2MjUzLC02LjEzODE2NCAxMy40MDYyNSwtMTMuNjI1IHYgLTI1LjUzMTI1IGMgMCwtNy4yNjYzMzg2IC02LjEyOTk4LC0xMi43MjQ3NzcxIC0xMy40MDYyNSwtMTMuOTM3NDk5NyBDIDY0LjI4MTU0OCwwLjMyNzk0Mzk3IDU5LjUwMjQzOCwtMC4wMjAzNzkwMyA1NC45MTg3ODUsOS4xOTI3NDIxZS00IFogbSAtMTQuNSw4LjIxODc1MDEyNTc5IGMgMi43Njk1NDcsMCA1LjAzMTI1LDIuMjk4NjQ1NiA1LjAzMTI1LDUuMTI0OTk5NiAtMmUtNiwyLjgxNjMzNiAtMi4yNjE3MDMsNS4wOTM3NSAtNS4wMzEyNSw1LjA5Mzc1IC0yLjc3OTQ3NiwtMWUtNiAtNS4wMzEyNSwtMi4yNzc0MTUgLTUuMDMxMjUsLTUuMDkzNzUgLTEwZS03LC0yLjgyNjM1MyAyLjI1MTc3NCwtNS4xMjQ5OTk2IDUuMDMxMjUsLTUuMTI0OTk5NiB6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2ZmZDQzYiIgZD0ibSA4NS42Mzc1MzUsMjguNjU3MTY5IHYgMTEuOTA2MjUgYyAwLDkuMjMwNzU1IC03LjgyNTg5NSwxNi45OTk5OTkgLTE2Ljc1LDE3IGggLTI2Ljc4MTI1IGMgLTcuMzM1ODMzLDAgLTEzLjQwNjI0OSw2LjI3ODQ4MyAtMTMuNDA2MjUsMTMuNjI1IHYgMjUuNTMxMjQ3IGMgMCw3LjI2NjM0NCA2LjMxODU4OCwxMS41NDAzMjQgMTMuNDA2MjUsMTMuNjI1MDA0IDguNDg3MzMxLDIuNDk1NjEgMTYuNjI2MjM3LDIuOTQ2NjMgMjYuNzgxMjUsMCA2Ljc1MDE1NSwtMS45NTQzOSAxMy40MDYyNTMsLTUuODg3NjEgMTMuNDA2MjUsLTEzLjYyNTAwNCBWIDg2LjUwMDkxOSBoIC0yNi43ODEyNSB2IC0zLjQwNjI1IGggMjYuNzgxMjUgMTMuNDA2MjU0IGMgNy43OTI0NjEsMCAxMC42OTYyNTEsLTUuNDM1NDA4IDEzLjQwNjI0MSwtMTMuNTkzNzUgMi43OTkzMywtOC4zOTg4ODYgMi42ODAyMiwtMTYuNDc1Nzc2IDAsLTI3LjI1IC0xLjkyNTc4LC03Ljc1NzQ0MSAtNS42MDM4NywtMTMuNTkzNzUgLTEzLjQwNjI0MSwtMTMuNTkzNzUgeiBtIC0xNS4wNjI1LDY0LjY1NjI1IGMgMi43Nzk0NzgsM2UtNiA1LjAzMTI1LDIuMjc3NDE3IDUuMDMxMjUsNS4wOTM3NDcgLTJlLTYsMi44MjYzNTQgLTIuMjUxNzc1LDUuMTI1MDA0IC01LjAzMTI1LDUuMTI1MDA0IC0yLjc2OTU1LDAgLTUuMDMxMjUsLTIuMjk4NjUgLTUuMDMxMjUsLTUuMTI1MDA0IDJlLTYsLTIuODE2MzMgMi4yNjE2OTcsLTUuMDkzNzQ3IDUuMDMxMjUsLTUuMDkzNzQ3IHoiLz4KPC9zdmc+Cg==);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-share: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTSAxOCAyIEMgMTYuMzU0OTkgMiAxNSAzLjM1NDk5MDQgMTUgNSBDIDE1IDUuMTkwOTUyOSAxNS4wMjE3OTEgNS4zNzcxMjI0IDE1LjA1NjY0MSA1LjU1ODU5MzggTCA3LjkyMTg3NSA5LjcyMDcwMzEgQyA3LjM5ODUzOTkgOS4yNzc4NTM5IDYuNzMyMDc3MSA5IDYgOSBDIDQuMzU0OTkwNCA5IDMgMTAuMzU0OTkgMyAxMiBDIDMgMTMuNjQ1MDEgNC4zNTQ5OTA0IDE1IDYgMTUgQyA2LjczMjA3NzEgMTUgNy4zOTg1Mzk5IDE0LjcyMjE0NiA3LjkyMTg3NSAxNC4yNzkyOTcgTCAxNS4wNTY2NDEgMTguNDM5NDUzIEMgMTUuMDIxNTU1IDE4LjYyMTUxNCAxNSAxOC44MDgzODYgMTUgMTkgQyAxNSAyMC42NDUwMSAxNi4zNTQ5OSAyMiAxOCAyMiBDIDE5LjY0NTAxIDIyIDIxIDIwLjY0NTAxIDIxIDE5IEMgMjEgMTcuMzU0OTkgMTkuNjQ1MDEgMTYgMTggMTYgQyAxNy4yNjc0OCAxNiAxNi42MDE1OTMgMTYuMjc5MzI4IDE2LjA3ODEyNSAxNi43MjI2NTYgTCA4Ljk0MzM1OTQgMTIuNTU4NTk0IEMgOC45NzgyMDk1IDEyLjM3NzEyMiA5IDEyLjE5MDk1MyA5IDEyIEMgOSAxMS44MDkwNDcgOC45NzgyMDk1IDExLjYyMjg3OCA4Ljk0MzM1OTQgMTEuNDQxNDA2IEwgMTYuMDc4MTI1IDcuMjc5Mjk2OSBDIDE2LjYwMTQ2IDcuNzIyMTQ2MSAxNy4yNjc5MjMgOCAxOCA4IEMgMTkuNjQ1MDEgOCAyMSA2LjY0NTAwOTYgMjEgNSBDIDIxIDMuMzU0OTkwNCAxOS42NDUwMSAyIDE4IDIgeiBNIDE4IDQgQyAxOC41NjQxMjkgNCAxOSA0LjQzNTg3MDYgMTkgNSBDIDE5IDUuNTY0MTI5NCAxOC41NjQxMjkgNiAxOCA2IEMgMTcuNDM1ODcxIDYgMTcgNS41NjQxMjk0IDE3IDUgQyAxNyA0LjQzNTg3MDYgMTcuNDM1ODcxIDQgMTggNCB6IE0gNiAxMSBDIDYuNTY0MTI5NCAxMSA3IDExLjQzNTg3MSA3IDEyIEMgNyAxMi41NjQxMjkgNi41NjQxMjk0IDEzIDYgMTMgQyA1LjQzNTg3MDYgMTMgNSAxMi41NjQxMjkgNSAxMiBDIDUgMTEuNDM1ODcxIDUuNDM1ODcwNiAxMSA2IDExIHogTSAxOCAxOCBDIDE4LjU2NDEyOSAxOCAxOSAxOC40MzU4NzEgMTkgMTkgQyAxOSAxOS41NjQxMjkgMTguNTY0MTI5IDIwIDE4IDIwIEMgMTcuNDM1ODcxIDIwIDE3IDE5LjU2NDEyOSAxNyAxOSBDIDE3IDE4LjQzNTg3MSAxNy40MzU4NzEgMTggMTggMTggeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1iYWNrZ3JvdW5kLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgd2lkdGg9IjIwIiBoZWlnaHQ9IjIwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyIDIpIiBmaWxsPSIjMzMzMzMzIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUtaW52ZXJzZSIgZD0iTTUuMDU2NjQgOC43NjE3MkM1LjA1NjY0IDguNTk3NjYgNS4wMzEyNSA4LjQ1MzEyIDQuOTgwNDcgOC4zMjgxMkM0LjkzMzU5IDguMTk5MjIgNC44NTU0NyA4LjA4MjAzIDQuNzQ2MDkgNy45NzY1NkM0LjY0MDYyIDcuODcxMDkgNC41IDcuNzc1MzkgNC4zMjQyMiA3LjY4OTQ1QzQuMTUyMzQgNy41OTk2MSAzLjk0MzM2IDcuNTExNzIgMy42OTcyNyA3LjQyNTc4QzMuMzAyNzMgNy4yODUxNiAyLjk0MzM2IDcuMTM2NzIgMi42MTkxNCA2Ljk4MDQ3QzIuMjk0OTIgNi44MjQyMiAyLjAxNzU4IDYuNjQyNTggMS43ODcxMSA2LjQzNTU1QzEuNTYwNTUgNi4yMjg1MiAxLjM4NDc3IDUuOTg4MjggMS4yNTk3NyA1LjcxNDg0QzEuMTM0NzcgNS40Mzc1IDEuMDcyMjcgNS4xMDkzOCAxLjA3MjI3IDQuNzMwNDdDMS4wNzIyNyA0LjM5ODQ0IDEuMTI4OTEgNC4wOTU3IDEuMjQyMTkgMy44MjIyN0MxLjM1NTQ3IDMuNTQ0OTIgMS41MTU2MiAzLjMwNDY5IDEuNzIyNjYgMy4xMDE1NkMxLjkyOTY5IDIuODk4NDQgMi4xNzk2OSAyLjczNDM3IDIuNDcyNjYgMi42MDkzOEMyLjc2NTYyIDIuNDg0MzggMy4wOTE4IDIuNDA0MyAzLjQ1MTE3IDIuMzY5MTRWMS4xMDkzOEg0LjM4ODY3VjIuMzgwODZDNC43NDAyMyAyLjQyNzczIDUuMDU2NjQgMi41MjM0NCA1LjMzNzg5IDIuNjY3OTdDNS42MTkxNCAyLjgxMjUgNS44NTc0MiAzLjAwMTk1IDYuMDUyNzMgMy4yMzYzM0M2LjI1MTk1IDMuNDY2OCA2LjQwNDMgMy43NDAyMyA2LjUwOTc3IDQuMDU2NjRDNi42MTkxNCA0LjM2OTE0IDYuNjczODMgNC43MjA3IDYuNjczODMgNS4xMTEzM0g1LjA0NDkyQzUuMDQ0OTIgNC42Mzg2NyA0LjkzNzUgNC4yODEyNSA0LjcyMjY2IDQuMDM5MDZDNC41MDc4MSAzLjc5Mjk3IDQuMjE2OCAzLjY2OTkyIDMuODQ5NjEgMy42Njk5MkMzLjY1MDM5IDMuNjY5OTIgMy40NzY1NiAzLjY5NzI3IDMuMzI4MTIgMy43NTE5NUMzLjE4MzU5IDMuODAyNzMgMy4wNjQ0NSAzLjg3Njk1IDIuOTcwNyAzLjk3NDYxQzIuODc2OTUgNC4wNjgzNiAyLjgwNjY0IDQuMTc5NjkgMi43NTk3NyA0LjMwODU5QzIuNzE2OCA0LjQzNzUgMi42OTUzMSA0LjU3ODEyIDIuNjk1MzEgNC43MzA0N0MyLjY5NTMxIDQuODgyODEgMi43MTY4IDUuMDE5NTMgMi43NTk3NyA1LjE0MDYyQzIuODA2NjQgNS4yNTc4MSAyLjg4MjgxIDUuMzY3MTkgMi45ODgyOCA1LjQ2ODc1QzMuMDk3NjYgNS41NzAzMSAzLjI0MDIzIDUuNjY3OTcgMy40MTYwMiA1Ljc2MTcyQzMuNTkxOCA1Ljg1MTU2IDMuODEwNTUgNS45NDMzNiA0LjA3MjI3IDYuMDM3MTFDNC40NjY4IDYuMTg1NTUgNC44MjQyMiA2LjMzOTg0IDUuMTQ0NTMgNi41QzUuNDY0ODQgNi42NTYyNSA1LjczODI4IDYuODM5ODQgNS45NjQ4NCA3LjA1MDc4QzYuMTk1MzEgNy4yNTc4MSA2LjM3MTA5IDcuNSA2LjQ5MjE5IDcuNzc3MzRDNi42MTcxOSA4LjA1MDc4IDYuNjc5NjkgOC4zNzUgNi42Nzk2OSA4Ljc1QzYuNjc5NjkgOS4wOTM3NSA2LjYyMzA1IDkuNDA0MyA2LjUwOTc3IDkuNjgxNjRDNi4zOTY0OCA5Ljk1NTA4IDYuMjM0MzggMTAuMTkxNCA2LjAyMzQ0IDEwLjM5MDZDNS44MTI1IDEwLjU4OTggNS41NTg1OSAxMC43NSA1LjI2MTcyIDEwLjg3MTFDNC45NjQ4NCAxMC45ODgzIDQuNjMyODEgMTEuMDY0NSA0LjI2NTYyIDExLjA5OTZWMTIuMjQ4SDMuMzMzOThWMTEuMDk5NkMzLjAwMTk1IDExLjA2ODQgMi42Nzk2OSAxMC45OTYxIDIuMzY3MTkgMTAuODgyOEMyLjA1NDY5IDEwLjc2NTYgMS43NzczNCAxMC41OTc3IDEuNTM1MTYgMTAuMzc4OUMxLjI5Njg4IDEwLjE2MDIgMS4xMDU0NyA5Ljg4NDc3IDAuOTYwOTM4IDkuNTUyNzNDMC44MTY0MDYgOS4yMTY4IDAuNzQ0MTQxIDguODE0NDUgMC43NDQxNDEgOC4zNDU3SDIuMzc4OTFDMi4zNzg5MSA4LjYyNjk1IDIuNDE5OTIgOC44NjMyOCAyLjUwMTk1IDkuMDU0NjlDMi41ODM5OCA5LjI0MjE5IDIuNjg5NDUgOS4zOTI1OCAyLjgxODM2IDkuNTA1ODZDMi45NTExNyA5LjYxNTIzIDMuMTAxNTYgOS42OTMzNiAzLjI2OTUzIDkuNzQwMjNDMy40Mzc1IDkuNzg3MTEgMy42MDkzOCA5LjgxMDU1IDMuNzg1MTYgOS44MTA1NUM0LjIwMzEyIDkuODEwNTUgNC41MTk1MyA5LjcxMjg5IDQuNzM0MzggOS41MTc1OEM0Ljk0OTIyIDkuMzIyMjcgNS4wNTY2NCA5LjA3MDMxIDUuMDU2NjQgOC43NjE3MlpNMTMuNDE4IDEyLjI3MTVIOC4wNzQyMlYxMUgxMy40MThWMTIuMjcxNVoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMuOTUyNjQgNikiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtdGV4dC1lZGl0b3ItaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xNSAxNUgzdjJoMTJ2LTJ6bTAtOEgzdjJoMTJWN3pNMyAxM2gxOHYtMkgzdjJ6bTAgOGgxOHYtMkgzdjJ6TTMgM3YyaDE4VjNIM3oiLz4KPC9zdmc+Cg==);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-user: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE2IDdhNCA0IDAgMTEtOCAwIDQgNCAwIDAxOCAwek0xMiAxNGE3IDcgMCAwMC03IDdoMTRhNyA3IDAgMDAtNy03eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-users: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDM2IDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogPGcgY2xhc3M9ImpwLWljb24zIiB0cmFuc2Zvcm09Im1hdHJpeCgxLjczMjcgMCAwIDEuNzMyNyAtMy42MjgyIC4wOTk1NzcpIiBmaWxsPSIjNjE2MTYxIj4KICA8cGF0aCB0cmFuc2Zvcm09Im1hdHJpeCgxLjUsMCwwLDEuNSwwLC02KSIgZD0ibTEyLjE4NiA3LjUwOThjLTEuMDUzNSAwLTEuOTc1NyAwLjU2NjUtMi40Nzg1IDEuNDEwMiAwLjc1MDYxIDAuMzEyNzcgMS4zOTc0IDAuODI2NDggMS44NzMgMS40NzI3aDMuNDg2M2MwLTEuNTkyLTEuMjg4OS0yLjg4MjgtMi44ODA5LTIuODgyOHoiLz4KICA8cGF0aCBkPSJtMjAuNDY1IDIuMzg5NWEyLjE4ODUgMi4xODg1IDAgMCAxLTIuMTg4NCAyLjE4ODUgMi4xODg1IDIuMTg4NSAwIDAgMS0yLjE4ODUtMi4xODg1IDIuMTg4NSAyLjE4ODUgMCAwIDEgMi4xODg1LTIuMTg4NSAyLjE4ODUgMi4xODg1IDAgMCAxIDIuMTg4NCAyLjE4ODV6Ii8+CiAgPHBhdGggdHJhbnNmb3JtPSJtYXRyaXgoMS41LDAsMCwxLjUsMCwtNikiIGQ9Im0zLjU4OTggOC40MjE5Yy0xLjExMjYgMC0yLjAxMzcgMC45MDExMS0yLjAxMzcgMi4wMTM3aDIuODE0NWMwLjI2Nzk3LTAuMzczMDkgMC41OTA3LTAuNzA0MzUgMC45NTg5OC0wLjk3ODUyLTAuMzQ0MzMtMC42MTY4OC0xLjAwMzEtMS4wMzUyLTEuNzU5OC0xLjAzNTJ6Ii8+CiAgPHBhdGggZD0ibTYuOTE1NCA0LjYyM2ExLjUyOTQgMS41Mjk0IDAgMCAxLTEuNTI5NCAxLjUyOTQgMS41Mjk0IDEuNTI5NCAwIDAgMS0xLjUyOTQtMS41Mjk0IDEuNTI5NCAxLjUyOTQgMCAwIDEgMS41Mjk0LTEuNTI5NCAxLjUyOTQgMS41Mjk0IDAgMCAxIDEuNTI5NCAxLjUyOTR6Ii8+CiAgPHBhdGggZD0ibTYuMTM1IDEzLjUzNWMwLTMuMjM5MiAyLjYyNTktNS44NjUgNS44NjUtNS44NjUgMy4yMzkyIDAgNS44NjUgMi42MjU5IDUuODY1IDUuODY1eiIvPgogIDxjaXJjbGUgY3g9IjEyIiBjeT0iMy43Njg1IiByPSIyLjk2ODUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-word: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KIDxnIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzQxNDE0MSI+CiAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiA8L2c+CiA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSguNDMgLjA0MDEpIiBmaWxsPSIjZmZmIj4KICA8cGF0aCBkPSJtNC4xNCA4Ljc2cTAuMDY4Mi0xLjg5IDIuNDItMS44OSAxLjE2IDAgMS42OCAwLjQyIDAuNTY3IDAuNDEgMC41NjcgMS4xNnYzLjQ3cTAgMC40NjIgMC41MTQgMC40NjIgMC4xMDMgMCAwLjItMC4wMjMxdjAuNzE0cS0wLjM5OSAwLjEwMy0wLjY1MSAwLjEwMy0wLjQ1MiAwLTAuNjkzLTAuMjItMC4yMzEtMC4yLTAuMjg0LTAuNjYyLTAuOTU2IDAuODcyLTIgMC44NzItMC45MDMgMC0xLjQ3LTAuNDcyLTAuNTI1LTAuNDcyLTAuNTI1LTEuMjYgMC0wLjI2MiAwLjA0NTItMC40NzIgMC4wNTY3LTAuMjIgMC4xMTYtMC4zNzggMC4wNjgyLTAuMTY4IDAuMjMxLTAuMzA0IDAuMTU4LTAuMTQ3IDAuMjYyLTAuMjQyIDAuMTE2LTAuMDkxNCAwLjM2OC0wLjE2OCAwLjI2Mi0wLjA5MTQgMC4zOTktMC4xMjYgMC4xMzYtMC4wNDUyIDAuNDcyLTAuMTAzIDAuMzM2LTAuMDU3OCAwLjUwNC0wLjA3OTggMC4xNTgtMC4wMjMxIDAuNTY3LTAuMDc5OCAwLjU1Ni0wLjA2ODIgMC43NzctMC4yMjEgMC4yMi0wLjE1MiAwLjIyLTAuNDQxdi0wLjI1MnEwLTAuNDMtMC4zNTctMC42NjItMC4zMzYtMC4yMzEtMC45NzYtMC4yMzEtMC42NjIgMC0wLjk5OCAwLjI2Mi0wLjMzNiAwLjI1Mi0wLjM5OSAwLjc5OHptMS44OSAzLjY4cTAuNzg4IDAgMS4yNi0wLjQxIDAuNTA0LTAuNDIgMC41MDQtMC45MDN2LTEuMDVxLTAuMjg0IDAuMTM2LTAuODYxIDAuMjMxLTAuNTY3IDAuMDkxNC0wLjk4NyAwLjE1OC0wLjQyIDAuMDY4Mi0wLjc2NiAwLjMyNi0wLjMzNiAwLjI1Mi0wLjMzNiAwLjcwNHQwLjMwNCAwLjcwNCAwLjg2MSAwLjI1MnoiIHN0cm9rZS13aWR0aD0iMS4wNSIvPgogIDxwYXRoIGQ9Im0xMCA0LjU2aDAuOTQ1djMuMTVxMC42NTEtMC45NzYgMS44OS0wLjk3NiAxLjE2IDAgMS44OSAwLjg0IDAuNjgyIDAuODQgMC42ODIgMi4zMSAwIDEuNDctMC43MDQgMi40Mi0wLjcwNCAwLjg4Mi0xLjg5IDAuODgyLTEuMjYgMC0xLjg5LTEuMDJ2MC43NjZoLTAuODV6bTIuNjIgMy4wNHEtMC43NDYgMC0xLjE2IDAuNjQtMC40NTIgMC42My0wLjQ1MiAxLjY4IDAgMS4wNSAwLjQ1MiAxLjY4dDEuMTYgMC42M3EwLjc3NyAwIDEuMjYtMC42MyAwLjQ5NC0wLjY0IDAuNDk0LTEuNjggMC0xLjA1LTAuNDcyLTEuNjgtMC40NjItMC42NC0xLjI2LTAuNjR6IiBzdHJva2Utd2lkdGg9IjEuMDUiLz4KICA8cGF0aCBkPSJtMi43MyAxNS44IDEzLjYgMC4wMDgxYzAuMDA2OSAwIDAtMi42IDAtMi42IDAtMC4wMDc4LTEuMTUgMC0xLjE1IDAtMC4wMDY5IDAtMC4wMDgzIDEuNS0wLjAwODMgMS41LTJlLTMgLTAuMDAxNC0xMS4zLTAuMDAxNC0xMS4zLTAuMDAxNGwtMC4wMDU5Mi0xLjVjMC0wLjAwNzgtMS4xNyAwLjAwMTMtMS4xNyAwLjAwMTN6IiBzdHJva2Utd2lkdGg9Ii45NzUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddAboveIcon {
  background-image: var(--jp-icon-add-above);
}

.jp-AddBelowIcon {
  background-image: var(--jp-icon-add-below);
}

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}

.jp-BellIcon {
  background-image: var(--jp-icon-bell);
}

.jp-BugDotIcon {
  background-image: var(--jp-icon-bug-dot);
}

.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}

.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}

.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}

.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}

.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}

.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}

.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}

.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}

.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}

.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}

.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}

.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}

.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}

.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}

.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}

.jp-CodeCheckIcon {
  background-image: var(--jp-icon-code-check);
}

.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}

.jp-CollapseAllIcon {
  background-image: var(--jp-icon-collapse-all);
}

.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}

.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}

.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}

.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}

.jp-DeleteIcon {
  background-image: var(--jp-icon-delete);
}

.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}

.jp-DuplicateIcon {
  background-image: var(--jp-icon-duplicate);
}

.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}

.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}

.jp-ErrorIcon {
  background-image: var(--jp-icon-error);
}

.jp-ExpandAllIcon {
  background-image: var(--jp-icon-expand-all);
}

.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}

.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}

.jp-FileIcon {
  background-image: var(--jp-icon-file);
}

.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}

.jp-FilterDotIcon {
  background-image: var(--jp-icon-filter-dot);
}

.jp-FilterIcon {
  background-image: var(--jp-icon-filter);
}

.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}

.jp-FolderFavoriteIcon {
  background-image: var(--jp-icon-folder-favorite);
}

.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}

.jp-HomeIcon {
  background-image: var(--jp-icon-home);
}

.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}

.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}

.jp-InfoIcon {
  background-image: var(--jp-icon-info);
}

.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}

.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}

.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}

.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}

.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}

.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}

.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}

.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}

.jp-LaunchIcon {
  background-image: var(--jp-icon-launch);
}

.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}

.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}

.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}

.jp-ListIcon {
  background-image: var(--jp-icon-list);
}

.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}

.jp-MoveDownIcon {
  background-image: var(--jp-icon-move-down);
}

.jp-MoveUpIcon {
  background-image: var(--jp-icon-move-up);
}

.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}

.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}

.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}

.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}

.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}

.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}

.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}

.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}

.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}

.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}

.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}

.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}

.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}

.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}

.jp-RunIcon {
  background-image: var(--jp-icon-run);
}

.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}

.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}

.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}

.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}

.jp-ShareIcon {
  background-image: var(--jp-icon-share);
}

.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}

.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}

.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}

.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}

.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}

.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}

.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}

.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}

.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}

.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}

.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}

.jp-UserIcon {
  background-image: var(--jp-icon-user);
}

.jp-UsersIcon {
  background-image: var(--jp-icon-users);
}

.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}

.jp-WordIcon {
  background-image: var(--jp-icon-word);
}

.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.lm-TabBar .lm-TabBar-addButton {
  align-items: center;
  display: flex;
  padding: 4px;
  padding-bottom: 5px;
  margin-right: 1px;
  background-color: var(--jp-layout-color2);
}

.lm-TabBar .lm-TabBar-addButton:hover {
  background-color: var(--jp-layout-color1);
}

.lm-DockPanel-tabBar .lm-TabBar-tab {
  width: var(--jp-private-horizontal-tab-width);
}

.lm-DockPanel-tabBar .lm-TabBar-content {
  flex: unset;
}

.lm-DockPanel-tabBar[data-orientation='horizontal'] {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}

/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}

.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}

.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}

.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}

.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}

.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}

.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}

.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}

.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}

/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}

.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}

.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}

.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}

.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}

.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}

.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}

/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

.jp-icon-dot[fill] {
  fill: var(--jp-warn-color0);
}

.jp-jupyter-icon-color[fill] {
  fill: var(--jp-jupyter-icon-color, var(--jp-warn-color0));
}

.jp-notebook-icon-color[fill] {
  fill: var(--jp-notebook-icon-color, var(--jp-warn-color0));
}

.jp-json-icon-color[fill] {
  fill: var(--jp-json-icon-color, var(--jp-warn-color1));
}

.jp-console-icon-color[fill] {
  fill: var(--jp-console-icon-color, white);
}

.jp-console-icon-background-color[fill] {
  fill: var(--jp-console-icon-background-color, var(--jp-brand-color1));
}

.jp-terminal-icon-color[fill] {
  fill: var(--jp-terminal-icon-color, var(--jp-layout-color2));
}

.jp-terminal-icon-background-color[fill] {
  fill: var(
    --jp-terminal-icon-background-color,
    var(--jp-inverse-layout-color2)
  );
}

.jp-text-editor-icon-color[fill] {
  fill: var(--jp-text-editor-icon-color, var(--jp-inverse-layout-color3));
}

.jp-inspector-icon-color[fill] {
  fill: var(--jp-inspector-icon-color, var(--jp-inverse-layout-color3));
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* stylelint-disable selector-max-class, selector-max-compound-selectors */

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}

.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* stylelint-enable selector-max-class, selector-max-compound-selectors */

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) .jp-icon-hoverShow-content {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FormGroup-content fieldset {
  border: none;
  padding: 0;
  min-width: 0;
  width: 100%;
}

/* stylelint-disable selector-max-type */

.jp-FormGroup-content fieldset .jp-inputFieldWrapper input,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper select,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper textarea {
  font-size: var(--jp-content-font-size2);
  border-color: var(--jp-input-border-color);
  border-style: solid;
  border-radius: var(--jp-border-radius);
  border-width: 1px;
  padding: 6px 8px;
  background: none;
  color: var(--jp-ui-font-color0);
  height: inherit;
}

.jp-FormGroup-content fieldset input[type='checkbox'] {
  position: relative;
  top: 2px;
  margin-left: 0;
}

.jp-FormGroup-content button.jp-mod-styled {
  cursor: pointer;
}

.jp-FormGroup-content .checkbox label {
  cursor: pointer;
  font-size: var(--jp-content-font-size1);
}

.jp-FormGroup-content .jp-root > fieldset > legend {
  display: none;
}

.jp-FormGroup-content .jp-root > fieldset > p {
  display: none;
}

/** copy of `input.jp-mod-styled:focus` style */
.jp-FormGroup-content fieldset input:focus,
.jp-FormGroup-content fieldset select:focus {
  -moz-outline-radius: unset;
  outline: var(--jp-border-width) solid var(--md-blue-500);
  outline-offset: -1px;
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FormGroup-content fieldset input:hover:not(:focus),
.jp-FormGroup-content fieldset select:hover:not(:focus) {
  background-color: var(--jp-border-color2);
}

/* stylelint-enable selector-max-type */

.jp-FormGroup-content .checkbox .field-description {
  /* Disable default description field for checkbox:
   because other widgets do not have description fields,
   we add descriptions to each widget on the field level.
  */
  display: none;
}

.jp-FormGroup-content #root__description {
  display: none;
}

.jp-FormGroup-content .jp-modifiedIndicator {
  width: 5px;
  background-color: var(--jp-brand-color2);
  margin-top: 0;
  margin-left: calc(var(--jp-private-settingeditor-modifier-indent) * -1);
  flex-shrink: 0;
}

.jp-FormGroup-content .jp-modifiedIndicator.jp-errorIndicator {
  background-color: var(--jp-error-color0);
  margin-right: 0.5em;
}

/* RJSF ARRAY style */

.jp-arrayFieldWrapper legend {
  font-size: var(--jp-content-font-size2);
  color: var(--jp-ui-font-color0);
  flex-basis: 100%;
  padding: 4px 0;
  font-weight: var(--jp-content-heading-font-weight);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-arrayFieldWrapper .field-description {
  padding: 4px 0;
  white-space: pre-wrap;
}

.jp-arrayFieldWrapper .array-item {
  width: 100%;
  border: 1px solid var(--jp-border-color2);
  border-radius: 4px;
  margin: 4px;
}

.jp-ArrayOperations {
  display: flex;
  margin-left: 8px;
}

.jp-ArrayOperationsButton {
  margin: 2px;
}

.jp-ArrayOperationsButton .jp-icon3[fill] {
  fill: var(--jp-ui-font-color0);
}

button.jp-ArrayOperationsButton.jp-mod-styled:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* RJSF form validation error */

.jp-FormGroup-content .validationErrors {
  color: var(--jp-error-color0);
}

/* Hide panel level error as duplicated the field level error */
.jp-FormGroup-content .panel.errors {
  display: none;
}

/* RJSF normal content (settings-editor) */

.jp-FormGroup-contentNormal {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-FormGroup-contentItem {
  margin-left: 7px;
  color: var(--jp-ui-font-color0);
}

.jp-FormGroup-contentNormal .jp-FormGroup-description {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-default {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-fieldLabel {
  font-size: var(--jp-content-font-size1);
  font-weight: normal;
  min-width: 120px;
}

.jp-FormGroup-contentNormal fieldset:not(:first-child) {
  margin-left: 7px;
}

.jp-FormGroup-contentNormal .field-array-of-string .array-item {
  /* Display `jp-ArrayOperations` buttons side-by-side with content except
    for small screens where flex-wrap will place them one below the other.
  */
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-objectFieldWrapper .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

/* RJSF compact content (metadata-form) */

.jp-FormGroup-content.jp-FormGroup-contentCompact {
  width: 100%;
}

.jp-FormGroup-contentCompact .form-group {
  display: flex;
  padding: 0.5em 0.2em 0.5em 0;
}

.jp-FormGroup-contentCompact
  .jp-FormGroup-compactTitle
  .jp-FormGroup-description {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color2);
}

.jp-FormGroup-contentCompact .jp-FormGroup-fieldLabel {
  padding-bottom: 0.3em;
}

.jp-FormGroup-contentCompact .jp-inputFieldWrapper .form-control {
  width: 100%;
  box-sizing: border-box;
}

.jp-FormGroup-contentCompact .jp-arrayFieldWrapper .jp-FormGroup-compactTitle {
  padding-bottom: 7px;
}

.jp-FormGroup-contentCompact
  .jp-objectFieldWrapper
  .jp-objectFieldWrapper
  .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

.jp-FormGroup-contentCompact ul.error-detail {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
  padding-inline-start: 1em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-SidePanel {
  display: flex;
  flex-direction: column;
  min-width: var(--jp-sidebar-min-width);
  overflow-y: auto;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size1);
}

.jp-SidePanel-header {
  flex: 0 0 auto;
  display: flex;
  border-bottom: var(--jp-border-width) solid var(--jp-border-color2);
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin: 0;
  padding: 2px;
  text-transform: uppercase;
}

.jp-SidePanel-toolbar {
  flex: 0 0 auto;
}

.jp-SidePanel-content {
  flex: 1 1 auto;
}

.jp-SidePanel-toolbar,
.jp-AccordionPanel-toolbar {
  height: var(--jp-private-toolbar-height);
}

.jp-SidePanel-toolbar.jp-Toolbar-micro {
  display: none;
}

.lm-AccordionPanel .jp-AccordionPanel-title {
  box-sizing: border-box;
  line-height: 25px;
  margin: 0;
  display: flex;
  align-items: center;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  font-size: var(--jp-ui-font-size0);
}

.jp-AccordionPanel-title {
  cursor: pointer;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  text-transform: uppercase;
}

.lm-AccordionPanel[data-orientation='horizontal'] > .jp-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleLabel {
  user-select: none;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleCollapser {
  transform: rotate(-90deg);
  margin: auto 0;
  height: 16px;
}

.jp-AccordionPanel-title.lm-mod-expanded .lm-AccordionPanel-titleCollapser {
  transform: rotate(0deg);
}

.lm-AccordionPanel .jp-AccordionPanel-toolbar {
  background: none;
  box-shadow: none;
  border: none;
  margin-left: auto;
}

.lm-AccordionPanel .lm-SplitPanel-handle:hover {
  background: var(--jp-layout-color3);
}

.jp-text-truncated {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent::before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent::after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper:not(.multiple) {
  height: 28px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.jp-mod-styled:not([multiple]) {
  height: 32px;
}

select.jp-mod-styled[multiple] {
  max-height: 200px;
  overflow-y: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
  font-family: var(--jp-ui-font-family);
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-switch-color, var(--jp-border-color1));
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-switch-true-position-color, var(--jp-warn-color0));
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 8;
  overflow-x: hidden;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0;
  margin: 0;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0 6px;
  margin: 0;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent > span {
  padding: 0;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-WindowedPanel-outer {
  position: relative;
  overflow-y: auto;
}

.jp-WindowedPanel-inner {
  position: relative;
}

.jp-WindowedPanel-window {
  position: absolute;
  left: 0;
  right: 0;
  overflow: visible;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

body {
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
}

/* Disable native link decoration styles everywhere outside of dialog boxes */
a {
  text-decoration: unset;
  color: unset;
}

a:hover {
  text-decoration: unset;
  color: unset;
}

/* Accessibility for links inside dialog box text */
.jp-Dialog-content a {
  text-decoration: revert;
  color: var(--jp-content-link-color);
}

.jp-Dialog-content a:hover {
  text-decoration: revert;
}

/* Styles for ui-components */
.jp-Button {
  color: var(--jp-ui-font-color2);
  border-radius: var(--jp-border-radius);
  padding: 0 12px;
  font-size: var(--jp-ui-font-size1);

  /* Copy from blueprint 3 */
  display: inline-flex;
  flex-direction: row;
  border: none;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  text-align: left;
  vertical-align: middle;
  min-height: 30px;
  min-width: 30px;
}

.jp-Button:disabled {
  cursor: not-allowed;
}

.jp-Button:empty {
  padding: 0 !important;
}

.jp-Button.jp-mod-small {
  min-height: 24px;
  min-width: 24px;
  font-size: 12px;
  padding: 0 7px;
}

/* Use our own theme for hover styles */
.jp-Button.jp-mod-minimal:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Button.jp-mod-minimal {
  background: none;
}

.jp-InputGroup {
  display: block;
  position: relative;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
  padding-bottom: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-right: 28px;
  position: relative;
  width: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  font-weight: 400;
  height: 30px;
  line-height: 30px;
  outline: none;
  vertical-align: middle;
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input:disabled {
  cursor: not-allowed;
  resize: block;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input:disabled ~ span {
  cursor: not-allowed;
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color2);
}

.jp-InputGroupAction {
  position: absolute;
  bottom: 1px;
  right: 0;
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
  cursor: not-allowed;
  resize: block;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled ~ span {
  cursor: not-allowed;
}

/* Use our own theme for hover and option styles */
/* stylelint-disable-next-line selector-max-type */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}

select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-StatusBar-Widget {
  display: flex;
  align-items: center;
  background: var(--jp-layout-color2);
  min-height: var(--jp-statusbar-height);
  justify-content: space-between;
  padding: 0 10px;
}

.jp-StatusBar-Left {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-StatusBar-Middle {
  display: flex;
  align-items: center;
}

.jp-StatusBar-Right {
  display: flex;
  align-items: center;
  flex-direction: row-reverse;
}

.jp-StatusBar-Item {
  max-height: var(--jp-statusbar-height);
  margin: 0 2px;
  height: var(--jp-statusbar-height);
  white-space: nowrap;
  text-overflow: ellipsis;
  color: var(--jp-ui-font-color1);
  padding: 0 6px;
}

.jp-mod-highlighted:hover {
  background-color: var(--jp-layout-color3);
}

.jp-mod-clicked {
  background-color: var(--jp-brand-color1);
}

.jp-mod-clicked:hover {
  background-color: var(--jp-brand-color0);
}

.jp-mod-clicked .jp-StatusBar-TextItem {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-StatusBar-HoverItem {
  box-shadow: '0px 4px 4px rgba(0, 0, 0, 0.25)';
}

.jp-StatusBar-TextItem {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  line-height: 24px;
  color: var(--jp-ui-font-color1);
}

.jp-StatusBar-GroupItem {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-Statusbar-ProgressCircle svg {
  display: block;
  margin: 0 auto;
  width: 16px;
  height: 24px;
  align-self: normal;
}

.jp-Statusbar-ProgressCircle path {
  fill: var(--jp-inverse-layout-color3);
}

.jp-Statusbar-ProgressBar-progress-bar {
  height: 10px;
  width: 100px;
  border: solid 0.25px var(--jp-brand-color2);
  border-radius: 3px;
  overflow: hidden;
  align-self: center;
}

.jp-Statusbar-ProgressBar-progress-bar > div {
  background-color: var(--jp-brand-color2);
  background-image: linear-gradient(
    -45deg,
    rgba(255, 255, 255, 0.2) 25%,
    transparent 25%,
    transparent 50%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0.2) 75%,
    transparent 75%,
    transparent
  );
  background-size: 40px 40px;
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 14px;
  color: #fff;
  text-align: center;
  animation: jp-Statusbar-ExecutionTime-progress-bar 2s linear infinite;
}

.jp-Statusbar-ProgressBar-progress-bar p {
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  line-height: 10px;
  width: 100px;
}

@keyframes jp-Statusbar-ExecutionTime-progress-bar {
  0% {
    background-position: 0 0;
  }

  100% {
    background-position: 40px 40px;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty::after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px 24px 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-content.jp-Dialog-content-small {
  max-width: 500px;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus {
  outline: 1px solid var(--jp-accept-color-normal, var(--jp-brand-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus {
  outline: 1px solid var(--jp-warn-color-normal, var(--jp-error-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline: 1px solid var(--jp-reject-color-normal, var(--md-grey-600));
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-checkbox {
  padding-right: 5px;
}

.jp-Dialog-checkbox > input:focus-visible {
  outline: 1px solid var(--jp-input-active-border-color);
  outline-offset: 1px;
}

.jp-Dialog-spacer {
  flex: 1 1 auto;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error {
  padding: 6px;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error > pre {
  width: auto;
  padding: 10px;
  background: var(--jp-error-color3);
  border: var(--jp-border-width) solid var(--jp-error-color1);
  border-radius: var(--jp-border-radius);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  white-space: pre-wrap;
  word-wrap: break-word;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;
  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;
  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #a0f;
  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;
  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;
  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;
  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;
  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;
  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;
  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;
  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;
  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;
  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ff0;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;
  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;
  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;
  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;
  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;
  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;
  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0;
  padding: 0;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}

.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}

.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}

.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}

.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}

.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}

.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}

.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}

.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}

.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}

.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}

.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}

.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}

.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}

.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}

.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}

.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);

  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

/* stylelint-disable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0;
}

/* stylelint-enable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  table-layout: fixed;
  margin-left: auto;
  margin-bottom: 1em;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}

[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}

.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}

.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}

.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}

.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}

.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}

.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}

.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}

.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: var(--jp-ui-font-size0);
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-cursor-backdrop {
  position: fixed;
  width: 200px;
  height: 200px;
  margin-top: -100px;
  margin-left: -100px;
  will-change: transform;
  z-index: 100;
}

.lm-mod-drag-image {
  will-change: transform;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-lineFormSearch {
  padding: 4px 12px;
  background-color: var(--jp-layout-color2);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
  font-size: var(--jp-ui-font-size1);
}

.jp-lineFormCaption {
  font-size: var(--jp-ui-font-size0);
  line-height: var(--jp-ui-font-size1);
  margin-top: 4px;
  color: var(--jp-ui-font-color0);
}

.jp-baseLineForm {
  border: none;
  border-radius: 0;
  position: absolute;
  background-size: 16px;
  background-repeat: no-repeat;
  background-position: center;
  outline: none;
}

.jp-lineFormButtonContainer {
  top: 4px;
  right: 8px;
  height: 24px;
  padding: 0 12px;
  width: 12px;
}

.jp-lineFormButtonIcon {
  top: 0;
  right: 0;
  background-color: var(--jp-brand-color1);
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 4px 6px;
}

.jp-lineFormButton {
  top: 0;
  right: 0;
  background-color: transparent;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.jp-lineFormWrapper {
  overflow: hidden;
  padding: 0 8px;
  border: 1px solid var(--jp-border-color0);
  background-color: var(--jp-input-active-background);
  height: 22px;
}

.jp-lineFormWrapperFocusWithin {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-lineFormInput {
  background: transparent;
  width: 200px;
  height: 100%;
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  line-height: 28px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/
.jp-DocumentSearch-input {
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  font-size: var(--jp-ui-font-size1);
  background-color: var(--jp-layout-color0);
  font-family: var(--jp-ui-font-family);
  padding: 2px 1px;
  resize: none;
}

.jp-DocumentSearch-overlay {
  position: absolute;
  background-color: var(--jp-toolbar-background);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  border-left: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  top: 0;
  right: 0;
  z-index: 7;
  min-width: 405px;
  padding: 2px;
  font-size: var(--jp-ui-font-size1);

  --jp-private-document-search-button-height: 20px;
}

.jp-DocumentSearch-overlay button {
  background-color: var(--jp-toolbar-background);
  outline: 0;
}

.jp-DocumentSearch-overlay button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-overlay button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-overlay-row {
  display: flex;
  align-items: center;
  margin-bottom: 2px;
}

.jp-DocumentSearch-button-content {
  display: inline-block;
  cursor: pointer;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-button-content svg {
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-input-wrapper {
  border: var(--jp-border-width) solid var(--jp-border-color0);
  display: flex;
  background-color: var(--jp-layout-color0);
  margin: 2px;
}

.jp-DocumentSearch-input-wrapper:focus-within {
  border-color: var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper {
  all: initial;
  overflow: hidden;
  display: inline-block;
  border: none;
  box-sizing: border-box;
}

.jp-DocumentSearch-toggle-wrapper {
  width: 14px;
  height: 14px;
}

.jp-DocumentSearch-button-wrapper {
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
}

.jp-DocumentSearch-toggle-wrapper:focus,
.jp-DocumentSearch-button-wrapper:focus {
  outline: var(--jp-border-width) solid
    var(--jp-cell-editor-active-border-color);
  outline-offset: -1px;
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper,
.jp-DocumentSearch-button-content:focus {
  outline: none;
}

.jp-DocumentSearch-toggle-placeholder {
  width: 5px;
}

.jp-DocumentSearch-input-button::before {
  display: block;
  padding-top: 100%;
}

.jp-DocumentSearch-input-button-off {
  opacity: var(--jp-search-toggle-off-opacity);
}

.jp-DocumentSearch-input-button-off:hover {
  opacity: var(--jp-search-toggle-hover-opacity);
}

.jp-DocumentSearch-input-button-on {
  opacity: var(--jp-search-toggle-on-opacity);
}

.jp-DocumentSearch-index-counter {
  padding-left: 10px;
  padding-right: 10px;
  user-select: none;
  min-width: 35px;
  display: inline-block;
}

.jp-DocumentSearch-up-down-wrapper {
  display: inline-block;
  padding-right: 2px;
  margin-left: auto;
  white-space: nowrap;
}

.jp-DocumentSearch-spacer {
  margin-left: auto;
}

.jp-DocumentSearch-up-down-wrapper button {
  outline: 0;
  border: none;
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
  vertical-align: middle;
  margin: 1px 5px 2px;
}

.jp-DocumentSearch-up-down-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-up-down-button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-filter-button {
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-filter-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled:hover {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-search-options {
  padding: 0 8px;
  margin-left: 3px;
  width: 100%;
  display: grid;
  justify-content: start;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-items: stretch;
}

.jp-DocumentSearch-search-filter-disabled {
  color: var(--jp-ui-font-color2);
}

.jp-DocumentSearch-search-filter {
  display: flex;
  align-items: center;
  user-select: none;
}

.jp-DocumentSearch-regex-error {
  color: var(--jp-error-color0);
}

.jp-DocumentSearch-replace-button-wrapper {
  overflow: hidden;
  display: inline-block;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color0);
  margin: auto 2px;
  padding: 1px 4px;
  height: calc(var(--jp-private-document-search-button-height) + 2px);
}

.jp-DocumentSearch-replace-button-wrapper:focus {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-replace-button {
  display: inline-block;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;
  color: var(--jp-ui-font-color1);

  /* height - 2 * (padding of wrapper) */
  line-height: calc(var(--jp-private-document-search-button-height) - 2px);
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-replace-button:focus {
  outline: none;
}

.jp-DocumentSearch-replace-wrapper-class {
  margin-left: 14px;
  display: flex;
}

.jp-DocumentSearch-replace-toggle {
  border: none;
  background-color: var(--jp-toolbar-background);
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-replace-toggle:hover {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.cm-editor {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;

  /* Changed to auto to autogrow */
}

.cm-editor pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .cm-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

.jp-CodeMirrorEditor {
  cursor: text;
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.cm-editor.jp-mod-readOnly .cm-cursor {
  display: none;
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.cm-searching,
.cm-searching span {
  /* `.cm-searching span`: we need to override syntax highlighting */
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.cm-searching::selection,
.cm-searching span::selection {
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.jp-current-match > .cm-searching,
.jp-current-match > .cm-searching span,
.cm-searching > .jp-current-match,
.cm-searching > .jp-current-match span {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.jp-current-match > .cm-searching::selection,
.cm-searching > .jp-current-match::selection,
.jp-current-match > .cm-searching span::selection {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.cm-trailingspace {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAFCAYAAAB4ka1VAAAAsElEQVQIHQGlAFr/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7+r3zKmT0/+pk9P/7+r3zAAAAAAAAAAABAAAAAAAAAAA6OPzM+/q9wAAAAAA6OPzMwAAAAAAAAAAAgAAAAAAAAAAGR8NiRQaCgAZIA0AGR8NiQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQyoYJ/SY80UAAAAASUVORK5CYII=);
  background-position: center left;
  background-repeat: repeat-x;
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .cm-ySelectionCaret {
  position: relative;
  border-left: 1px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret > .cm-ySelectionInfo {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -1px;
  font-size: 0.95em;
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 101;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .cm-ySelectionInfo {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret:hover > .cm-ySelectionInfo {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser .jp-SidePanel-content {
  display: flex;
  flex-direction: column;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  flex-wrap: wrap;
  row-gap: 12px;
  border-bottom: none;
  height: auto;
  margin: 8px 12px 0;
  box-shadow: none;
  padding: 0;
  justify-content: flex-start;
}

.jp-FileBrowser-Panel {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0 2px;
  padding: 0 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0;
  padding-right: 2px;
  align-items: center;
  height: unset;
}

.jp-FileBrowser-toolbar > .jp-Toolbar-item .jp-ToolbarButtonComponent {
  width: 40px;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileSize-hidden {
  display: none;
}

.jp-FileBrowser .lm-AccordionPanel > h3:first-child {
  display: none;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-headerItem.jp-id-filesize {
  flex: 0 0 75px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-checkboxWrapper {
  /* Increases hit area of checkbox. */
  padding: 4px;
}

.jp-DirListing-header
  .jp-DirListing-checkboxWrapper
  + .jp-DirListing-headerItem {
  padding-left: 4px;
}

.jp-DirListing-content .jp-DirListing-checkboxWrapper {
  position: relative;
  left: -4px;
  margin: -4px 0 -4px -8px;
}

.jp-DirListing-checkboxWrapper.jp-mod-visible {
  visibility: visible;
}

/* For devices that support hovering, hide checkboxes until hovered, selected...
*/
@media (hover: hover) {
  .jp-DirListing-checkboxWrapper {
    visibility: hidden;
  }

  .jp-DirListing-item:hover .jp-DirListing-checkboxWrapper,
  .jp-DirListing-item.jp-mod-selected .jp-DirListing-checkboxWrapper {
    visibility: visible;
  }
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemText:focus {
  outline-width: 2px;
  outline-color: var(--jp-inverse-layout-color1);
  outline-style: solid;
  outline-offset: 1px;
}

.jp-DirListing-item.jp-mod-selected .jp-DirListing-itemText:focus {
  outline-color: var(--jp-layout-color1);
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-itemFileSize {
  flex: 0 0 90px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon::before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-OutputPrompt {
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-prompt {
  display: table-cell;
  vertical-align: top;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea .jp-RenderedText {
  padding-left: 1ch;
}

/**
 * Prompt overlay.
 */

.jp-OutputArea-promptOverlay {
  position: absolute;
  top: 0;
  width: var(--jp-cell-prompt-width);
  height: 100%;
  opacity: 0.5;
}

.jp-OutputArea-promptOverlay:hover {
  background: var(--jp-layout-color2);
  box-shadow: inset 0 0 1px var(--jp-inverse-layout-color0);
  cursor: zoom-out;
}

.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay:hover {
  cursor: zoom-in;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

.jp-TrimmedOutputs pre {
  background: var(--jp-layout-color3);
  font-size: calc(var(--jp-code-font-size) * 1.4);
  text-align: center;
  text-transform: uppercase;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/* Hide empty lines in the output area, for instance due to cleared widgets */
.jp-OutputArea-prompt:empty {
  padding: 0;
  border: 0;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0;
  width: 100%;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;

  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;

  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0 0.25em;
  margin: 0 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input::placeholder {
  opacity: 0;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

.jp-Stdin-input:focus::placeholder {
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

@media print {
  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-OutputPrompt {
    display: table-row;
    text-align: left;
  }

  .jp-OutputArea-child .jp-OutputArea-output {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }
}

/* Trimmed outputs warning */
.jp-TrimmedOutputs > a {
  margin: 10px;
  text-decoration: none;
  cursor: pointer;
}

.jp-TrimmedOutputs > a:hover {
  text-decoration: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Table of Contents
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toc-active-width: 4px;
}

.jp-TableOfContents {
  display: flex;
  flex-direction: column;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  height: 100%;
}

.jp-TableOfContents-placeholder {
  text-align: center;
}

.jp-TableOfContents-placeholderContent {
  color: var(--jp-content-font-color2);
  padding: 8px;
}

.jp-TableOfContents-placeholderContent > h3 {
  margin-bottom: var(--jp-content-heading-margin-bottom);
}

.jp-TableOfContents .jp-SidePanel-content {
  overflow-y: auto;
}

.jp-TableOfContents-tree {
  margin: 4px;
}

.jp-TableOfContents ol {
  list-style-type: none;
}

/* stylelint-disable-next-line selector-max-type */
.jp-TableOfContents li > ol {
  /* Align left border with triangle icon center */
  padding-left: 11px;
}

.jp-TableOfContents-content {
  /* left margin for the active heading indicator */
  margin: 0 0 0 var(--jp-private-toc-active-width);
  padding: 0;
  background-color: var(--jp-layout-color1);
}

.jp-tocItem {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-tocItem-heading {
  display: flex;
  cursor: pointer;
}

.jp-tocItem-heading:hover {
  background-color: var(--jp-layout-color2);
}

.jp-tocItem-content {
  display: block;
  padding: 4px 0;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow-x: hidden;
}

.jp-tocItem-collapser {
  height: 20px;
  margin: 2px 2px 0;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
}

.jp-tocItem-collapser:hover {
  background-color: var(--jp-layout-color3);
}

/* Active heading indicator */

.jp-tocItem-heading::before {
  content: ' ';
  background: transparent;
  width: var(--jp-private-toc-active-width);
  height: 24px;
  position: absolute;
  left: 0;
  border-radius: var(--jp-border-radius);
}

.jp-tocItem-heading.jp-tocItem-active::before {
  background-color: var(--jp-brand-color1);
}

.jp-tocItem-heading:hover.jp-tocItem-active::before {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;

  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Hiding collapsers in print mode.

Note: input and output wrappers have "display: block" propery in print mode.
*/

@media print {
  .jp-Collapser {
    display: none;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0;
  width: 100%;
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-InputArea-editor {
  display: table-cell;
  overflow: hidden;
  vertical-align: top;

  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  display: table-cell;
  vertical-align: top;
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-InputArea-editor {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }

  .jp-InputPrompt {
    display: table-row;
    text-align: left;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: table;
  table-layout: fixed;
  width: 100%;
}

.jp-Placeholder-prompt {
  display: table-cell;
  box-sizing: border-box;
}

.jp-Placeholder-content {
  display: table-cell;
  padding: 4px 6px;
  border: 1px solid transparent;
  border-radius: 0;
  background: none;
  box-sizing: border-box;
  cursor: pointer;
}

.jp-Placeholder-contentContainer {
  display: flex;
}

.jp-Placeholder-content:hover,
.jp-InputPlaceholder > .jp-Placeholder-content:hover {
  border-color: var(--jp-layout-color3);
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

.jp-PlaceholderText {
  white-space: nowrap;
  overflow-x: hidden;
  color: var(--jp-inverse-layout-color3);
  font-family: var(--jp-code-font-family);
}

.jp-InputPlaceholder > .jp-Placeholder-content {
  border-color: var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0;
  margin: 0;

  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 24em;
  margin-left: var(--jp-private-cell-scrolling-output-offset);
  resize: vertical;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea[style*='height'] {
  max-height: unset;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea::after {
  content: ' ';
  box-shadow: inset 0 0 6px 2px rgb(0 0 0 / 30%);
  width: 100%;
  height: 100%;
  position: sticky;
  bottom: 0;
  top: 0;
  margin-top: -50%;
  float: left;
  display: block;
  pointer-events: none;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-child {
  padding-top: 6px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay {
  left: calc(-1 * var(--jp-private-cell-scrolling-output-offset));
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  display: table-cell;
  width: 100%;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/* collapseHeadingButton (show always if hiddenCellsButton is _not_ shown) */
.jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  font-size: var(--jp-code-font-size);
  position: absolute;
  background-color: transparent;
  background-size: 25px;
  background-repeat: no-repeat;
  background-position-x: center;
  background-position-y: top;
  background-image: var(--jp-icon-caret-down);
  right: 0;
  top: 0;
  bottom: 0;
}

.jp-collapseHeadingButton.jp-mod-collapsed {
  background-image: var(--jp-icon-caret-right);
}

/*
 set the container font size to match that of content
 so that the nested collapse buttons have the right size
*/
.jp-MarkdownCell .jp-InputPrompt {
  font-size: var(--jp-content-font-size1);
}

/*
  Align collapseHeadingButton with cell top header
  The font sizes are identical to the ones in packages/rendermime/style/base.css
*/
.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='1'] {
  font-size: var(--jp-content-font-size5);
  background-position-y: calc(0.3 * var(--jp-content-font-size5));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='2'] {
  font-size: var(--jp-content-font-size4);
  background-position-y: calc(0.3 * var(--jp-content-font-size4));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='3'] {
  font-size: var(--jp-content-font-size3);
  background-position-y: calc(0.3 * var(--jp-content-font-size3));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='4'] {
  font-size: var(--jp-content-font-size2);
  background-position-y: calc(0.3 * var(--jp-content-font-size2));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='5'] {
  font-size: var(--jp-content-font-size1);
  background-position-y: top;
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='6'] {
  font-size: var(--jp-content-font-size0);
  background-position-y: top;
}

/* collapseHeadingButton (show only on (hover,active) if hiddenCellsButton is shown) */
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-collapseHeadingButton {
  display: none;
}

.jp-Notebook.jp-mod-showHiddenCellsButton
  :is(.jp-MarkdownCell:hover, .jp-mod-active)
  .jp-collapseHeadingButton {
  display: flex;
}

/* showHiddenCellsButton (only show if jp-mod-showHiddenCellsButton is set, which
is a consequence of the showHiddenCellsButton option in Notebook Settings)*/
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
  display: flex;
}

.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-showHiddenCellsButton {
  display: none;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Using block instead of flex to allow the use of the break-inside CSS property for
cell outputs.
*/

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-notebook-toolbar-padding: 2px 5px 2px 2px;
}

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: var(--jp-notebook-toolbar-padding);

  /* disable paint containment from lumino 2.0 default strict CSS containment */
  contain: style size !important;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

.jp-Toolbar-responsive-popup {
  position: absolute;
  height: fit-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: var(--jp-notebook-toolbar-padding);
  z-index: 1;
  right: 0;
  top: 0;
}

.jp-Toolbar > .jp-Toolbar-responsive-opener {
  margin-left: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-Notebook-ExecutionIndicator {
  position: relative;
  display: inline-block;
  height: 100%;
  z-index: 9997;
}

.jp-Notebook-ExecutionIndicator-tooltip {
  visibility: hidden;
  height: auto;
  width: max-content;
  width: -moz-max-content;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color1);
  text-align: justify;
  border-radius: 6px;
  padding: 0 5px;
  position: fixed;
  display: table;
}

.jp-Notebook-ExecutionIndicator-tooltip.up {
  transform: translateX(-50%) translateY(-100%) translateY(-32px);
}

.jp-Notebook-ExecutionIndicator-tooltip.down {
  transform: translateX(calc(-100% + 16px)) translateY(5px);
}

.jp-Notebook-ExecutionIndicator-tooltip.hidden {
  display: none;
}

.jp-Notebook-ExecutionIndicator:hover .jp-Notebook-ExecutionIndicator-tooltip {
  visibility: visible;
}

.jp-Notebook-ExecutionIndicator span {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  color: var(--jp-ui-font-color1);
  line-height: 24px;
  display: block;
}

.jp-Notebook-ExecutionIndicator-progress-bar {
  display: flex;
  justify-content: center;
  height: 100%;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*
 * Execution indicator
 */
.jp-tocItem-content::after {
  content: '';

  /* Must be identical to form a circle */
  width: 12px;
  height: 12px;
  background: none;
  border: none;
  position: absolute;
  right: 0;
}

.jp-tocItem-content[data-running='0']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background: none;
}

.jp-tocItem-content[data-running='1']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background-color: var(--jp-inverse-layout-color3);
}

.jp-tocItem-content[data-running='0'],
.jp-tocItem-content[data-running='1'] {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Notebook-footer {
  height: 27px;
  margin-left: calc(
    var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
      var(--jp-cell-padding)
  );
  width: calc(
    100% -
      (
        var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
          var(--jp-cell-padding) + var(--jp-cell-padding)
      )
  );
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  color: var(--jp-ui-font-color3);
  margin-top: 6px;
  background: none;
  cursor: pointer;
}

.jp-Notebook-footer:focus {
  border-color: var(--jp-cell-editor-active-border-color);
}

/* For devices that support hovering, hide footer until hover */
@media (hover: hover) {
  .jp-Notebook-footer {
    opacity: 0;
  }

  .jp-Notebook-footer:focus,
  .jp-Notebook-footer:hover {
    opacity: 1;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-side-by-side-output-size: 1fr;
  --jp-side-by-side-resized-cell: var(--jp-side-by-side-output-size);
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

/* stylelint-disable selector-max-class */

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}

.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt::before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-ActiveCellTool {
  padding: 12px 0;
  display: flex;
}

.jp-ActiveCellTool-Content {
  flex: 1 1 auto;
}

.jp-ActiveCellTool .jp-ActiveCellTool-CellContent {
  background: var(--jp-cell-editor-background);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  min-height: 29px;
}

.jp-ActiveCellTool .jp-InputPrompt {
  min-width: calc(var(--jp-cell-prompt-width) * 0.75);
}

.jp-ActiveCellTool-CellContent > pre {
  padding: 5px 4px;
  margin: 0;
  white-space: normal;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label,
.jp-NumberSetter label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0;
}

.jp-NumberSetter input {
  width: 100%;
  margin-top: 4px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Side-by-side Mode (.jp-mod-sideBySide)
|----------------------------------------------------------------------------*/
.jp-mod-sideBySide.jp-Notebook .jp-Notebook-cell {
  margin-top: 3em;
  margin-bottom: 3em;
  margin-left: 5%;
  margin-right: 5%;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell {
  display: grid;
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-output-size)
    );
  grid-template-rows: auto minmax(0, 1fr) auto;
  grid-template-areas:
    'header header header'
    'input handle output'
    'footer footer footer';
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell.jp-mod-resizedCell {
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-resized-cell)
    );
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellHeader {
  grid-area: header;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-inputWrapper {
  grid-area: input;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-outputWrapper {
  /* overwrite the default margin (no vertical separation needed in side by side move */
  margin-top: 0;
  grid-area: output;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellFooter {
  grid-area: footer;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle {
  grid-area: handle;
  user-select: none;
  display: block;
  height: 100%;
  cursor: ew-resize;
  padding: 0 var(--jp-cell-padding);
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle::after {
  content: '';
  display: block;
  background: var(--jp-border-color2);
  height: 100%;
  width: 5px;
}

.jp-mod-sideBySide.jp-Notebook
  .jp-CodeCell.jp-mod-resizedCell
  .jp-CellResizeHandle::after {
  background: var(--jp-border-color0);
}

.jp-CellResizeHandle {
  display: none;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0 2px 1px -1px var(--jp-shadow-umbra-color),
    0 1px 1px 0 var(--jp-shadow-penumbra-color),
    0 1px 3px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0 3px 1px -2px var(--jp-shadow-umbra-color),
    0 2px 2px 0 var(--jp-shadow-penumbra-color),
    0 1px 5px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0 2px 4px -1px var(--jp-shadow-umbra-color),
    0 4px 5px 0 var(--jp-shadow-penumbra-color),
    0 1px 10px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0 3px 5px -1px var(--jp-shadow-umbra-color),
    0 6px 10px 0 var(--jp-shadow-penumbra-color),
    0 1px 18px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0 5px 5px -3px var(--jp-shadow-umbra-color),
    0 8px 10px 1px var(--jp-shadow-penumbra-color),
    0 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0 7px 8px -4px var(--jp-shadow-umbra-color),
    0 12px 17px 2px var(--jp-shadow-penumbra-color),
    0 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0 8px 10px -5px var(--jp-shadow-umbra-color),
    0 16px 24px 2px var(--jp-shadow-penumbra-color),
    0 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0 10px 13px -6px var(--jp-shadow-umbra-color),
    0 20px 31px 3px var(--jp-shadow-penumbra-color),
    0 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0 11px 15px -7px var(--jp-shadow-umbra-color),
    0 24px 38px 3px var(--jp-shadow-penumbra-color),
    0 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-inverse-border-color: var(--md-grey-600);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;
  --jp-ui-font-family: system-ui, -apple-system, blinkmacsystemfont, 'Segoe UI',
    helvetica, arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;
  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);
  --jp-content-link-color: var(--md-blue-900);
  --jp-content-font-family: system-ui, -apple-system, blinkmacsystemfont,
    'Segoe UI', helvetica, arial, sans-serif, 'Apple Color Emoji',
    'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: menlo, consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);
  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);
  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);
  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);
  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;
  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;
  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);
  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);

  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;

  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-inverse-border-color);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: rgb(0, 54, 109);
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #a2f;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /*
    RTC user specific colors.
    These colors are used for the cursor, username in the editor,
    and the icon of the user.
  */

  --jp-collaborator-color1: #ffad8e;
  --jp-collaborator-color2: #dac83d;
  --jp-collaborator-color3: #72dd76;
  --jp-collaborator-color4: #00e4d0;
  --jp-collaborator-color5: #45d4ff;
  --jp-collaborator-color6: #e2b1ff;
  --jp-collaborator-color7: #ff9de6;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);

  /* Button colors */
  --jp-accept-color-normal: var(--md-blue-700);
  --jp-accept-color-hover: var(--md-blue-800);
  --jp-accept-color-active: var(--md-blue-900);
  --jp-warn-color-normal: var(--md-red-700);
  --jp-warn-color-hover: var(--md-red-800);
  --jp-warn-color-active: var(--md-red-900);
  --jp-reject-color-normal: var(--md-grey-600);
  --jp-reject-color-hover: var(--md-grey-700);
  --jp-reject-color-active: var(--md-grey-800);

  /* File or activity icons and switch semantic variables */
  --jp-jupyter-icon-color: #f37626;
  --jp-notebook-icon-color: #f37626;
  --jp-json-icon-color: var(--md-orange-700);
  --jp-console-icon-background-color: var(--md-blue-700);
  --jp-console-icon-color: white;
  --jp-terminal-icon-background-color: var(--md-grey-800);
  --jp-terminal-icon-color: var(--md-grey-200);
  --jp-text-editor-icon-color: var(--md-grey-700);
  --jp-inspector-icon-color: var(--md-grey-700);
  --jp-switch-color: var(--md-grey-400);
  --jp-switch-true-position-color: var(--md-orange-900);
}
</style>
<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.cm-editor.cm-s-jupyter .highlight pre {
/* weird, but --jp-code-padding defined to be 5px but 4px horizontal padding is hardcoded for pre.cm-line */
  padding: var(--jp-code-padding) 4px;
  margin: 0;

  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  color: inherit;

}

.jp-OutputArea-output pre {
  line-height: inherit;
  font-family: inherit;
}

.jp-RenderedText pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@page {
    margin: 0.5in; /* Margin for each printed piece of paper */
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}
</style>
<!-- Load mathjax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
<!-- MathJax configuration -->
<script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                messageStyle: 'none',
                CommonHTML: {
                    linebreaks: {
                    automatic: true
                    }
                }
            });

            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
<!-- End of mathjax configuration --><script type="module">
  document.addEventListener("DOMContentLoaded", async () => {
    const diagrams = document.querySelectorAll(".jp-Mermaid > pre.mermaid");
    // do not load mermaidjs if not needed
    if (!diagrams.length) {
      return;
    }
    const mermaid = (await import("https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.7.0/mermaid.esm.min.mjs")).default;
    const parser = new DOMParser();

    mermaid.initialize({
      maxTextSize: 100000,
      maxEdges: 100000,
      startOnLoad: false,
      fontFamily: window
        .getComputedStyle(document.body)
        .getPropertyValue("--jp-ui-font-family"),
      theme: document.querySelector("body[data-jp-theme-light='true']")
        ? "default"
        : "dark",
    });

    let _nextMermaidId = 0;

    function makeMermaidImage(svg) {
      const img = document.createElement("img");
      const doc = parser.parseFromString(svg, "image/svg+xml");
      const svgEl = doc.querySelector("svg");
      const { maxWidth } = svgEl?.style || {};
      const firstTitle = doc.querySelector("title");
      const firstDesc = doc.querySelector("desc");

      img.setAttribute("src", `data:image/svg+xml,${encodeURIComponent(svg)}`);
      if (maxWidth) {
        img.width = parseInt(maxWidth);
      }
      if (firstTitle) {
        img.setAttribute("alt", firstTitle.textContent);
      }
      if (firstDesc) {
        const caption = document.createElement("figcaption");
        caption.className = "sr-only";
        caption.textContent = firstDesc.textContent;
        return [img, caption];
      }
      return [img];
    }

    async function makeMermaidError(text) {
      let errorMessage = "";
      try {
        await mermaid.parse(text);
      } catch (err) {
        errorMessage = `${err}`;
      }

      const result = document.createElement("details");
      result.className = 'jp-RenderedMermaid-Details';
      const summary = document.createElement("summary");
      summary.className = 'jp-RenderedMermaid-Summary';
      const pre = document.createElement("pre");
      const code = document.createElement("code");
      code.innerText = text;
      pre.appendChild(code);
      summary.appendChild(pre);
      result.appendChild(summary);

      const warning = document.createElement("pre");
      warning.innerText = errorMessage;
      result.appendChild(warning);
      return [result];
    }

    async function renderOneMarmaid(src) {
      const id = `jp-mermaid-${_nextMermaidId++}`;
      const parent = src.parentNode;
      let raw = src.textContent.trim();
      const el = document.createElement("div");
      el.style.visibility = "hidden";
      document.body.appendChild(el);
      let results = null;
      let output = null;
      try {
        let { svg } = await mermaid.render(id, raw, el);
        svg = cleanMermaidSvg(svg);
        results = makeMermaidImage(svg);
        output = document.createElement("figure");
        results.map(output.appendChild, output);
      } catch (err) {
        parent.classList.add("jp-mod-warning");
        results = await makeMermaidError(raw);
        output = results[0];
      } finally {
        el.remove();
      }
      parent.classList.add("jp-RenderedMermaid");
      parent.appendChild(output);
    }


    /**
     * Post-process to ensure mermaid diagrams contain only valid SVG and XHTML.
     */
    function cleanMermaidSvg(svg) {
      return svg.replace(RE_VOID_ELEMENT, replaceVoidElement);
    }


    /**
     * A regular expression for all void elements, which may include attributes and
     * a slash.
     *
     * @see https://developer.mozilla.org/en-US/docs/Glossary/Void_element
     *
     * Of these, only `<br>` is generated by Mermaid in place of `\n`,
     * but _any_ "malformed" tag will break the SVG rendering entirely.
     */
    const RE_VOID_ELEMENT =
      /<\s*(area|base|br|col|embed|hr|img|input|link|meta|param|source|track|wbr)\s*([^>]*?)\s*>/gi;

    /**
     * Ensure a void element is closed with a slash, preserving any attributes.
     */
    function replaceVoidElement(match, tag, rest) {
      rest = rest.trim();
      if (!rest.endsWith('/')) {
        rest = `${rest} /`;
      }
      return `<${tag} ${rest}>`;
    }

    void Promise.all([...diagrams].map(renderOneMarmaid));
  });
</script>
<style>
  .jp-Mermaid:not(.jp-RenderedMermaid) {
    display: none;
  }

  .jp-RenderedMermaid {
    overflow: auto;
    display: flex;
  }

  .jp-RenderedMermaid.jp-mod-warning {
    width: auto;
    padding: 0.5em;
    margin-top: 0.5em;
    border: var(--jp-border-width) solid var(--jp-warn-color2);
    border-radius: var(--jp-border-radius);
    color: var(--jp-ui-font-color1);
    font-size: var(--jp-ui-font-size1);
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  .jp-RenderedMermaid figure {
    margin: 0;
    overflow: auto;
    max-width: 100%;
  }

  .jp-RenderedMermaid img {
    max-width: 100%;
  }

  .jp-RenderedMermaid-Details > pre {
    margin-top: 1em;
  }

  .jp-RenderedMermaid-Summary {
    color: var(--jp-warn-color2);
  }

  .jp-RenderedMermaid:not(.jp-mod-warning) pre {
    display: none;
  }

  .jp-RenderedMermaid-Summary > pre {
    display: inline-block;
    white-space: normal;
  }
</style>
<!-- End of mermaid configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<div style="text-align: center;">
<a href="https://cognitiveclass.ai/?utm_medium=Exinfluencer&amp;utm_source=Exinfluencer&amp;utm_content=000026UJ&amp;utm_term=10006555&amp;utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDL0321ENSkillsNetwork951-2022-01-01">
<img alt="No description has been provided for this image" src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DL0321EN-SkillsNetwork/image/IDSN-logo.png" width="400"/>
</a>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 align="left"><font size="6">Lab: Land Classification: CNN-Transformer Integration evaluation </font></h1>
<h2 align="left"><font size="5">Vision Transformer (ViT) Model Evaluation </font></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Estimated time: 90 minutes</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="Introdution">Introdution<a class="anchor-link" href="#Introdution">¶</a></h1><p>This notebook presents an end-to-end workflow for importing, testing, and evaluating two Vision Transformer (ViT) models developed in Keras and PyTorch, respectively.
The self-attention mechanism in the ViTs allows these models to learn complex and broad spatial dependencies, providing improved performance on a variety of vision tasks compared to traditional convolutional neural networks. However, the CNNs are adept in learning the local features very well and can be trained using relatively smaller datasets and is generally much more efficient in utilizing the computational resources, as compared to ViTs. A CNN-ViT hybrid architecture gains from both CNN and ViT model strengths, by getting local features extracted using CNNs, while the transformer part of the hybrid architecture can determine the global dependencies.</p>
<p>This lab focuses on model loading, prediction on sample data, and quantitative evaluation of the ViT models created using KEras and PyTorch. You'll explore the details of the framework-specific implementations, test the consistency of results, and gain practical experience comparing deep learning models across different Python ecosystems.</p>
<p>Upon completion, you will have a thorough understanding of loading the CNN-ViT hybrid models testing workflow, key evaluation metrics, and how high-level architectural concepts translate into practical model evaluation using both Keras and PyTorch.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Objectives">Objectives<a class="anchor-link" href="#Objectives">¶</a></h2><ul>
<li>Import and initialize pre-trained CNN - Vision Transformer hybrid models from two deep learning frameworks (Keras/TensorFlow and PyTorch).</li>
<li>Prepare and preprocess sample image data for inference.</li>
<li>Perform model inference and obtain prediction results from both models.</li>
<li>Compute and compare core evaluation metrics.</li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Table-of-Contents">Table of Contents<a class="anchor-link" href="#Table-of-Contents">¶</a></h2><ol>
<li><a href="#Dataset-download,-extraction-and-paths">Dataset download, extraction and paths</a></li>
<li><a href="#Pre-trained-model-download">Pre-trained model download</a></li>
<li><a href="#Package-installation">Package installation</a></li>
<li><a href="#Library-imports-and-setup">Library imports and setup</a></li>
<li><a href="#Fix-random-seed-for-reproducibility">Fix random seed for reproducibility</a></li>
<li><a href="#Defining-PyTorch-model-architecture">Defining PyTorch model architecture</a></li>
<li><a href="#Dataset-path-and-hyperparameters">Dataset path and hyperparameters</a></li>
<li><a href="#PyTorch-Dataloader">PyTorch Dataloader</a></li>
<li><a href="#----PyTorch-pre-trained-ViT-model-loading----">--- PyTorch pre-trained ViT model loading ---</a></li>
<li><a href="#PyTorch-model-inference-metrics">PyTorch model inference metrics</a></li>
<li><a href="#Keras-model-loading">Keras model loading</a></li>
<li><a href="#----Keras-pre-trained-ViT-model-loading----">Keras pre-trained ViT model loading</a></li>
<li><a href="#Define-dataloader">Define dataloader</a></li>
<li><a href="#Collecting-metrics-for-Keras-based-CNN-ViT-hybrid-model">Collecting metrics for Keras-based CNN-ViT hybrid model</a></li>
<li><a href="#Import-the-evaluation-metrics">Import the evaluation metrics</a></li>
<li><a href="#Keras-metrics-reporting">Keras metrics reporting</a></li>
<li><a href="#PyTorch-metrics-reporting">PyTorch metrics reporting</a></li>
<li><a href="#ROC-curve-plotting">ROC curve plotting</a></li>
<li><a href="#Comparing-model-performance">Comparing model performance</a></li>
<li><a href="#Summary-and-discussion">Summary and discussion</a></li>
<li><a href="#Conclusion">Conclusion</a></li>
</ol>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Dataset-download,-extraction-and-paths">Dataset download, extraction and paths<a class="anchor-link" href="#Dataset-download,-extraction-and-paths">¶</a></h2><p>We begin by downloading the dataset for evaluation of the models.
Here, you declare:</p>
<ol>
<li>The dataset URL from where the dataset would be downloaded.</li>
<li>The dataset downloading primary function, based on <code>skillsnetwork</code> library.</li>
<li>The dataset fallback downloading function, based on regular <code>http</code> downloading functions.</li>
</ol>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Define-root-directory-and-download-url">Define root directory and download <code>url</code><a class="anchor-link" href="#Define-root-directory-and-download-url">¶</a></h3><p>First, you define the root directory where all the data would be downloaded and extracted.
Here, the <code>dataset_url</code> is assigned a direct link to a tar archive hosted on IBM's cloud storage. This URL points to the satellite image dataset used for land classification tasks. Using a cloud-based URL ensures accessibility without local storage dependencies. This setup facilitates automated downloads later in the notebook.</p>
<p>If dealing with large datasets, monitor download times and implement retry mechanisms for robustness. This variable is key for the subsequent download functions, linking external data to the local workflow.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">data_dir</span> <span class="o">=</span> <span class="s2">"."</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">dataset_url</span> <span class="o">=</span> <span class="s2">"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/4Z1fwRR295-1O3PMQBH6Dg/images-dataSAT.tar"</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Data-download">Data download<a class="anchor-link" href="#Data-download">¶</a></h3><p>We begin by downloading the dataset for evaluation of the models.
Here, you declare:</p>
<ol>
<li>The dataset downloading primary function, based on <code>skillsnetwork</code> library.</li>
<li>The dataset fallback downloading function, based on regular <code>http</code> downloading functions.</li>
<li>Download the dataset</li>
</ol>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [3]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span><span class="w"> </span><span class="nn">os</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">skillsnetwork</span>

<span class="k">def</span><span class="w"> </span><span class="nf">check_skillnetwork_extraction</span><span class="p">(</span><span class="n">extract_dir</span><span class="p">):</span>
<span class="w">    </span><span class="sd">"""Check if the environment allows symlink creation for download/extraction."""</span>
    <span class="n">symlink_test</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">extract_dir</span><span class="p">,</span> <span class="s2">"symlink_test"</span><span class="p">)</span>
    <span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">symlink_test</span><span class="p">):</span>
        <span class="n">os</span><span class="o">.</span><span class="n">symlink</span><span class="p">(</span><span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">os</span><span class="o">.</span><span class="n">sep</span><span class="p">,</span> <span class="s2">"tmp"</span><span class="p">),</span> <span class="n">symlink_test</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">"Write permissions available for downloading and extracting the dataset tar file"</span><span class="p">)</span>
        <span class="n">os</span><span class="o">.</span><span class="n">unlink</span><span class="p">(</span><span class="n">symlink_test</span><span class="p">)</span>

<span class="k">async</span> <span class="k">def</span><span class="w"> </span><span class="nf">download_tar_dataset</span><span class="p">(</span><span class="n">url</span><span class="p">,</span> <span class="n">tar_path</span><span class="p">,</span> <span class="n">extract_dir</span><span class="p">):</span>
<span class="w">    </span><span class="sd">"""Download and extract dataset tar file asynchronously."""</span>
    <span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">tar_path</span><span class="p">):</span>
        <span class="k">try</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Downloading from </span><span class="si">{</span><span class="n">url</span><span class="si">}</span><span class="s2">..."</span><span class="p">)</span>
            <span class="kn">import</span><span class="w"> </span><span class="nn">httpx</span>
            <span class="k">async</span> <span class="k">with</span> <span class="n">httpx</span><span class="o">.</span><span class="n">AsyncClient</span><span class="p">()</span> <span class="k">as</span> <span class="n">client</span><span class="p">:</span>
                <span class="n">response</span> <span class="o">=</span> <span class="k">await</span> <span class="n">client</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="n">url</span><span class="p">,</span> <span class="n">follow_redirects</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
                <span class="n">response</span><span class="o">.</span><span class="n">raise_for_status</span><span class="p">()</span>
                <span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="n">tar_path</span><span class="p">,</span> <span class="s2">"wb"</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span>
                    <span class="n">f</span><span class="o">.</span><span class="n">write</span><span class="p">(</span><span class="n">response</span><span class="o">.</span><span class="n">content</span><span class="p">)</span>
            <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Successfully downloaded '</span><span class="si">{</span><span class="n">tar_path</span><span class="si">}</span><span class="s2">'."</span><span class="p">)</span>
        <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Download error: </span><span class="si">{</span><span class="n">e</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Dataset tar file already exists at: </span><span class="si">{</span><span class="n">tar_path</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
    <span class="kn">import</span><span class="w"> </span><span class="nn">tarfile</span>
    <span class="k">with</span> <span class="n">tarfile</span><span class="o">.</span><span class="n">open</span><span class="p">(</span><span class="n">tar_path</span><span class="p">,</span> <span class="s1">'r:*'</span><span class="p">)</span> <span class="k">as</span> <span class="n">tar_ref</span><span class="p">:</span>
        <span class="n">tar_ref</span><span class="o">.</span><span class="n">extractall</span><span class="p">(</span><span class="n">path</span><span class="o">=</span><span class="n">extract_dir</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Successfully extracted to '</span><span class="si">{</span><span class="n">extract_dir</span><span class="si">}</span><span class="s2">'."</span><span class="p">)</span>

<span class="k">try</span><span class="p">:</span>
    <span class="n">check_skillnetwork_extraction</span><span class="p">(</span><span class="n">data_dir</span><span class="p">)</span>
    <span class="k">await</span> <span class="n">skillsnetwork</span><span class="o">.</span><span class="n">prepare</span><span class="p">(</span><span class="n">url</span><span class="o">=</span><span class="n">dataset_url</span><span class="p">,</span> <span class="n">path</span><span class="o">=</span><span class="n">data_dir</span><span class="p">,</span> <span class="n">overwrite</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">e</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"Primary download/extraction method failed."</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"Falling back to manual download and extraction..."</span><span class="p">)</span>
    <span class="kn">import</span><span class="w"> </span><span class="nn">tarfile</span>
    <span class="kn">import</span><span class="w"> </span><span class="nn">httpx</span>
    <span class="kn">from</span><span class="w"> </span><span class="nn">pathlib</span><span class="w"> </span><span class="kn">import</span> <span class="n">Path</span>
    <span class="n">file_name</span> <span class="o">=</span> <span class="n">Path</span><span class="p">(</span><span class="n">dataset_url</span><span class="p">)</span><span class="o">.</span><span class="n">name</span>
    <span class="n">tar_path</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">data_dir</span><span class="p">,</span> <span class="n">file_name</span><span class="p">)</span>
    <span class="k">await</span> <span class="n">download_tar_dataset</span><span class="p">(</span><span class="n">dataset_url</span><span class="p">,</span> <span class="n">tar_path</span><span class="p">,</span> <span class="n">data_dir</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Write permissions available for downloading and extracting the dataset tar file
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Downloading images-dataSAT.tar:   0%|          | 0/20243456 [00:00&lt;?, ?it/s]</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>  0%|          | 0/6003 [00:00&lt;?, ?it/s]</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Saved to '.'
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Pre-trained-model-download">Pre-trained model download<a class="anchor-link" href="#Pre-trained-model-download">¶</a></h2><p>Now, define an asynchronous function to download model files from given URLs, if they are not already present locally.
You use <code>httpx</code> for asynchronous HTTP requests with error handling.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [4]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">async</span> <span class="k">def</span><span class="w"> </span><span class="nf">download_model</span><span class="p">(</span><span class="n">url</span><span class="p">,</span> <span class="n">model_path</span><span class="p">):</span>
    <span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">model_path</span><span class="p">):</span>
        <span class="k">try</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Downloading from </span><span class="si">{</span><span class="n">url</span><span class="si">}</span><span class="s2">..."</span><span class="p">)</span>
            <span class="kn">import</span><span class="w"> </span><span class="nn">httpx</span>
            <span class="k">async</span> <span class="k">with</span> <span class="n">httpx</span><span class="o">.</span><span class="n">AsyncClient</span><span class="p">()</span> <span class="k">as</span> <span class="n">client</span><span class="p">:</span>
                <span class="n">response</span> <span class="o">=</span> <span class="k">await</span> <span class="n">client</span><span class="o">.</span><span class="n">get</span><span class="p">(</span><span class="n">url</span><span class="p">,</span> <span class="n">follow_redirects</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
                <span class="n">response</span><span class="o">.</span><span class="n">raise_for_status</span><span class="p">()</span>
                <span class="k">with</span> <span class="nb">open</span><span class="p">(</span><span class="n">model_path</span><span class="p">,</span> <span class="s2">"wb"</span><span class="p">)</span> <span class="k">as</span> <span class="n">f</span><span class="p">:</span>
                    <span class="n">f</span><span class="o">.</span><span class="n">write</span><span class="p">(</span><span class="n">response</span><span class="o">.</span><span class="n">content</span><span class="p">)</span>
            <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Successfully downloaded '</span><span class="si">{</span><span class="n">model_path</span><span class="si">}</span><span class="s2">'."</span><span class="p">)</span>
        <span class="k">except</span> <span class="ne">Exception</span> <span class="k">as</span> <span class="n">e</span><span class="p">:</span>
            <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Download error: </span><span class="si">{</span><span class="n">e</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Model file already downloaded at: </span><span class="si">{</span><span class="n">model_path</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Model-paths-and-download">Model paths and download<a class="anchor-link" href="#Model-paths-and-download">¶</a></h2><p>In the cell below, you define the file paths and URLs for the Keras and PyTorch models and download them using the <code>download_model</code> function defined above.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [5]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">data_dir</span> <span class="o">=</span> <span class="s2">"."</span>

<span class="n">keras_model_url</span> <span class="o">=</span> <span class="s2">"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/7uNMQhNyTA8qSSDGn5Cc7A/keras-cnn-vit-ai-capstone.keras"</span>
<span class="n">keras_model_name</span> <span class="o">=</span> <span class="s2">"keras_cnn_vit_ai_capstone.keras"</span>
<span class="n">keras_model_path</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">data_dir</span><span class="p">,</span> <span class="n">keras_model_name</span><span class="p">)</span>

<span class="n">pytorch_state_dict_url</span> <span class="o">=</span> <span class="s2">"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/rFBrDlu1NNcAzir5Uww8eg/pytorch-cnn-vit-ai-capstone-model-state-dict.pth"</span>
<span class="n">pytorch_state_dict_name</span> <span class="o">=</span> <span class="s2">"pytorch_cnn_vit_ai_capstone_model_state_dict.pth"</span>
<span class="n">pytorch_state_dict_path</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">data_dir</span><span class="p">,</span> <span class="n">pytorch_state_dict_name</span><span class="p">)</span>

<span class="k">await</span> <span class="n">download_model</span><span class="p">(</span><span class="n">keras_model_url</span><span class="p">,</span> <span class="n">keras_model_path</span><span class="p">)</span>
<span class="k">await</span> <span class="n">download_model</span><span class="p">(</span><span class="n">pytorch_state_dict_url</span><span class="p">,</span> <span class="n">pytorch_state_dict_path</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Model file already downloaded at: ./keras_cnn_vit_ai_capstone.keras
Model file already downloaded at: ./pytorch_cnn_vit_ai_capstone_model_state_dict.pth
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Package-installation">Package installation<a class="anchor-link" href="#Package-installation">¶</a></h2><h3 id="Install-PyTorch,-SkLearn-library-and-Python-Packages-for-evaluation-metrics">Install PyTorch, SkLearn library and Python Packages for evaluation metrics<a class="anchor-link" href="#Install-PyTorch,-SkLearn-library-and-Python-Packages-for-evaluation-metrics">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>
<span class="o">%%</span><span class="n">capture</span> <span class="n">captured_output</span>
<span class="o">%</span><span class="n">pip</span> <span class="n">install</span> <span class="n">scikit</span><span class="o">-</span><span class="n">learn</span><span class="o">==</span><span class="mf">1.7.0</span> <span class="n">tensorflow</span><span class="o">==</span><span class="mf">2.19</span> <span class="n">numpy</span><span class="o">==</span><span class="mf">1.26</span> <span class="n">matplotlib</span><span class="o">==</span><span class="mf">3.9.2</span> <span class="n">skillsnetwork</span>
<span class="o">%</span><span class="n">pip</span> <span class="n">install</span> <span class="n">torch</span><span class="o">==</span><span class="mf">2.8.0</span><span class="o">+</span><span class="n">cpu</span> <span class="n">torchvision</span><span class="o">==</span><span class="mf">0.23.0</span><span class="o">+</span><span class="n">cpu</span> <span class="n">torchaudio</span><span class="o">==</span><span class="mf">2.8.0</span><span class="o">+</span><span class="n">cpu</span> \
    <span class="o">--</span><span class="n">index</span><span class="o">-</span><span class="n">url</span> <span class="n">https</span><span class="p">:</span><span class="o">//</span><span class="n">download</span><span class="o">.</span><span class="n">pytorch</span><span class="o">.</span><span class="n">org</span><span class="o">/</span><span class="n">whl</span><span class="o">/</span><span class="n">cpu</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>CPU times: user 15.1 ms, sys: 13.5 ms, total: 28.5 ms
Wall time: 2.51 s
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Library-imports-and-setup">Library imports and setup<a class="anchor-link" href="#Library-imports-and-setup">¶</a></h2><p>Import essential libraries for data manipulation, visualization, and suppresses warnings for cleaner notebook output.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">warnings</span>
<span class="n">warnings</span><span class="o">.</span><span class="n">filterwarnings</span><span class="p">(</span><span class="s1">'ignore'</span><span class="p">)</span>

<span class="kn">import</span><span class="w"> </span><span class="nn">os</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">time</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">httpx</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">random</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">numpy</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">np</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">tqdm</span><span class="w"> </span><span class="kn">import</span> <span class="n">tqdm</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">matplotlib.pyplot</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">plt</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>CPU times: user 391 ms, sys: 176 ms, total: 567 ms
Wall time: 599 ms
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="TensorFlow/Keras-library-imports">TensorFlow/Keras library imports<a class="anchor-link" href="#TensorFlow/Keras-library-imports">¶</a></h3><p>These imports set the environment variables to reduce TensorFlow logging noise and imports Keras modules for model building and training. They detect GPU availability for device assignment.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>
<span class="n">os</span><span class="o">.</span><span class="n">environ</span><span class="p">[</span><span class="s1">'TF_ENABLE_ONEDNN_OPTS'</span><span class="p">]</span> <span class="o">=</span> <span class="s1">'0'</span>
<span class="n">os</span><span class="o">.</span><span class="n">environ</span><span class="p">[</span><span class="s1">'TF_CPP_MIN_LOG_LEVEL'</span><span class="p">]</span> <span class="o">=</span> <span class="s1">'3'</span>

<span class="kn">import</span><span class="w"> </span><span class="nn">tensorflow</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">tf</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">tensorflow.keras</span><span class="w"> </span><span class="kn">import</span> <span class="n">layers</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">tensorflow.keras.preprocessing.image</span><span class="w"> </span><span class="kn">import</span> <span class="n">ImageDataGenerator</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">tensorflow.keras.models</span><span class="w"> </span><span class="kn">import</span> <span class="n">load_model</span>

<span class="n">gpu_list</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">config</span><span class="o">.</span><span class="n">list_physical_devices</span><span class="p">(</span><span class="s1">'GPU'</span><span class="p">)</span>
<span class="n">device</span> <span class="o">=</span> <span class="s2">"gpu"</span> <span class="k">if</span> <span class="n">gpu_list</span> <span class="o">!=</span> <span class="p">[]</span> <span class="k">else</span> <span class="s2">"cpu"</span>
<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"TensorFlow </span><span class="si">{</span><span class="n">tf</span><span class="o">.</span><span class="n">__version__</span><span class="si">}</span><span class="s2">  |  GPUs found: </span><span class="si">{</span><span class="n">tf</span><span class="o">.</span><span class="n">config</span><span class="o">.</span><span class="n">list_physical_devices</span><span class="p">(</span><span class="s1">'GPU'</span><span class="p">)</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr" tabindex="0">
<pre>WARNING: All log messages before absl::InitializeLog() is called are written to STDERR
E0000 00:00:1771692077.050273     943 cuda_dnn.cc:8579] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
E0000 00:00:1771692077.056650     943 cuda_blas.cc:1407] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
W0000 00:00:1771692077.074163     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.
W0000 00:00:1771692077.074188     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.
W0000 00:00:1771692077.074190     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.
W0000 00:00:1771692077.074192     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>TensorFlow 2.19.0  |  GPUs found: []
CPU times: user 2.48 s, sys: 384 ms, total: 2.86 s
Wall time: 2.88 s
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="PyTorch-library-imports">PyTorch library imports<a class="anchor-link" href="#PyTorch-library-imports">¶</a></h3><p>Import core PyTorch modules for model building, optimization, data loading, and functional utilities.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">torch</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">torch.nn</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">nn</span>
<span class="c1">#import torch.optim as optim</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">torchvision</span><span class="w"> </span><span class="kn">import</span> <span class="n">transforms</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">torchvision</span><span class="w"> </span><span class="kn">import</span> <span class="n">datasets</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">torch.utils.data</span><span class="w"> </span><span class="kn">import</span> <span class="n">DataLoader</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">torch.utils.data</span><span class="w"> </span><span class="kn">import</span>  <span class="n">random_split</span>
<span class="kn">import</span><span class="w"> </span><span class="nn">torch.nn.functional</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">F</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">"Imported libraries"</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Imported libraries
CPU times: user 2.08 s, sys: 457 ms, total: 2.54 s
Wall time: 2.69 s
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Fix-random-seed-for-reproducibility">Fix random seed for reproducibility<a class="anchor-link" href="#Fix-random-seed-for-reproducibility">¶</a></h2><p>Define <code>set_seed</code> to ensure reproducibility across Python, NumPy, TensorFlow, and PyTorch by seeding random generators and enabling deterministic cuDNN.</p>
<p>Set <code>SEED</code> to 7331. This is useful for consistent results in stochastic processes like training or inference.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#====================</span>
<span class="k">def</span><span class="w"> </span><span class="nf">set_seed</span><span class="p">(</span><span class="n">seed</span><span class="p">:</span> <span class="nb">int</span> <span class="o">=</span> <span class="mi">42</span><span class="p">)</span> <span class="o">-&gt;</span> <span class="kc">None</span><span class="p">:</span>
<span class="w">    </span><span class="sd">"""Seed Python, NumPy, tensorflow, and PyTorch (CPU &amp; all GPUs) and</span>
<span class="sd">    make cuDNN run in deterministic mode."""</span>
    <span class="c1"># ---- Python and NumPy -------------------------------------------</span>
    <span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="n">seed</span><span class="p">)</span>
    <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">seed</span><span class="p">(</span><span class="n">seed</span><span class="p">)</span>

    <span class="c1"># ---- Tensorflow -------------------------------------------------</span>
    <span class="n">tf</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">set_seed</span><span class="p">(</span><span class="n">seed</span><span class="p">)</span>

    <span class="c1"># ---- PyTorch (CPU  &amp;  GPU) --------------------------------------</span>
    <span class="n">torch</span><span class="o">.</span><span class="n">manual_seed</span><span class="p">(</span><span class="n">seed</span><span class="p">)</span>            
    <span class="n">torch</span><span class="o">.</span><span class="n">cuda</span><span class="o">.</span><span class="n">manual_seed_all</span><span class="p">(</span><span class="n">seed</span><span class="p">)</span>   

    <span class="c1"># ---- cuDNN: force repeatable convolutions -----------------------</span>
    <span class="n">torch</span><span class="o">.</span><span class="n">backends</span><span class="o">.</span><span class="n">cudnn</span><span class="o">.</span><span class="n">deterministic</span> <span class="o">=</span> <span class="kc">True</span> 
    <span class="n">torch</span><span class="o">.</span><span class="n">backends</span><span class="o">.</span><span class="n">cudnn</span><span class="o">.</span><span class="n">benchmark</span>     <span class="o">=</span> <span class="kc">False</span> 

<span class="c1">#====================</span>
<span class="n">SEED</span> <span class="o">=</span> <span class="mi">7331</span>
<span class="n">set_seed</span><span class="p">(</span><span class="n">SEED</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Global seed set to </span><span class="si">{</span><span class="n">SEED</span><span class="si">}</span><span class="s2"> - Processes are now deterministic."</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Global seed set to 7331 - Processes are now deterministic.
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Model-paths">Model paths<a class="anchor-link" href="#Model-paths">¶</a></h2><p>Check for the existence of the Keras and PyTorch model files. This ensures models are accessible before loading, preventing runtime errors. Use absolute paths for reliability.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">keras_model_path</span><span class="p">):</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"Unable to find the Keras model at give path. Please check..."</span><span class="p">)</span>
<span class="k">else</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Found the pre-trained Keras model:</span><span class="se">\n</span><span class="si">{</span><span class="n">keras_model_name</span><span class="si">}</span><span class="s2"> --at------&gt; </span><span class="si">{</span><span class="n">keras_model_path</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>

<span class="k">if</span> <span class="ow">not</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">exists</span><span class="p">(</span><span class="n">pytorch_state_dict_path</span><span class="p">):</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"Unable to find the PyTorch model at give path. Please check..."</span><span class="p">)</span>
<span class="k">else</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Found the pre-trained PyTorch model:</span><span class="se">\n</span><span class="si">{</span><span class="n">pytorch_state_dict_name</span><span class="si">}</span><span class="s2"> --at------&gt; </span><span class="si">{</span><span class="n">pytorch_state_dict_path</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Found the pre-trained Keras model:
keras_cnn_vit_ai_capstone.keras --at------&gt; ./keras_cnn_vit_ai_capstone.keras
Found the pre-trained PyTorch model:
pytorch_cnn_vit_ai_capstone_model_state_dict.pth --at------&gt; ./pytorch_cnn_vit_ai_capstone_model_state_dict.pth
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Defining-PyTorch-model-architecture">Defining PyTorch model architecture<a class="anchor-link" href="#Defining-PyTorch-model-architecture">¶</a></h2><p>In this cell, you will define the PyTorch CNN-ViT model architegcture, exactly as defined during the model training. You define the classes for CNN feature extractor, patch embedding, multi-head self-attention, transformer block, ViT, and CNN-ViT hybrid.</p>
<p>The <code>evaluate</code> function computes loss and accuracy. This architecture combines CNN local features with ViT global attention.</p>
<p>Parameters like depth and heads are configurable, and defined same as during training.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [12]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#====================</span>
<span class="k">class</span><span class="w"> </span><span class="nc">ConvNet</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
<span class="w">    </span><span class="sd">''' </span>
<span class="sd">    Class to define the architecture same as the imported pre-trained CNN model</span>
<span class="sd">    '''</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">num_classes</span><span class="p">:</span> <span class="nb">int</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="c1"># -------- convolutional feature extractor --------</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">features</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sequential</span><span class="p">(</span>
            <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">32</span><span class="p">,</span>  <span class="n">kernel_size</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">padding</span><span class="o">=</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm2d</span><span class="p">(</span><span class="mi">32</span><span class="p">),</span>
            <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">32</span><span class="p">,</span> <span class="mi">64</span><span class="p">,</span>  <span class="n">kernel_size</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">padding</span><span class="o">=</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm2d</span><span class="p">(</span><span class="mi">64</span><span class="p">),</span>
            <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">64</span><span class="p">,</span> <span class="mi">128</span><span class="p">,</span> <span class="n">kernel_size</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">padding</span><span class="o">=</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm2d</span><span class="p">(</span><span class="mi">128</span><span class="p">),</span>
            <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">128</span><span class="p">,</span> <span class="mi">256</span><span class="p">,</span> <span class="n">kernel_size</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">padding</span><span class="o">=</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm2d</span><span class="p">(</span><span class="mi">256</span><span class="p">),</span>
            <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">256</span><span class="p">,</span> <span class="mi">512</span><span class="p">,</span> <span class="n">kernel_size</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">padding</span><span class="o">=</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm2d</span><span class="p">(</span><span class="mi">512</span><span class="p">),</span>
            <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">512</span><span class="p">,</span> <span class="mi">1024</span><span class="p">,</span> <span class="n">kernel_size</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">padding</span><span class="o">=</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm2d</span><span class="p">(</span><span class="mi">1024</span><span class="p">),</span>
        <span class="p">)</span>

        <span class="c1"># -------- global pooling + classifier head --------</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">pool</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">AdaptiveAvgPool2d</span><span class="p">((</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">))</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">classifier</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sequential</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Flatten</span><span class="p">(),</span>                           <span class="c1"># flatten feature map of dimensions (1024 × 1 × 1) to 1024</span>
                                        <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">1024</span><span class="p">,</span> <span class="mi">2048</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">ReLU</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">BatchNorm1d</span><span class="p">(</span><span class="mi">2048</span><span class="p">),</span> <span class="n">nn</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="mf">0.4</span><span class="p">),</span> 
                                        <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">2048</span><span class="p">,</span> <span class="n">num_classes</span><span class="p">)</span>
                                       <span class="p">)</span>

    <span class="k">def</span><span class="w"> </span><span class="nf">forward_features</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">:</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">)</span> <span class="o">-&gt;</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">:</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">features</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
    
    <span class="k">def</span><span class="w"> </span><span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">:</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">)</span> <span class="o">-&gt;</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">:</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">forward_features</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>   <span class="c1"># features, dimensions:(B, 1024, H', W')</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pool</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>               <span class="c1"># global-average-pooling, dimensions: (B, 1024, 1, 1)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">classifier</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>         <span class="c1"># classifier, dimensions: (B, num_classes)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="c1">#====================</span>
<span class="k">class</span><span class="w"> </span><span class="nc">PatchEmbed</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">input_channel</span><span class="o">=</span><span class="mi">1024</span><span class="p">,</span> <span class="n">embed_dim</span><span class="o">=</span><span class="mi">768</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">proj</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="n">input_channel</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">,</span> <span class="n">kernel_size</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>  <span class="c1"># 1×1 conv</span>
    
    <span class="k">def</span><span class="w"> </span><span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">proj</span><span class="p">(</span><span class="n">x</span><span class="p">)</span><span class="o">.</span><span class="n">flatten</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>  <span class="c1"># (B,L,D)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="c1">#====================</span>
<span class="k">class</span><span class="w"> </span><span class="nc">MHSA</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">dim</span><span class="p">,</span> <span class="n">heads</span><span class="o">=</span><span class="mi">8</span><span class="p">,</span> <span class="n">dropout</span><span class="o">=</span><span class="mf">0.</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">heads</span> <span class="o">=</span> <span class="n">heads</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">scale</span> <span class="o">=</span> <span class="p">(</span><span class="n">dim</span> <span class="o">//</span> <span class="n">heads</span><span class="p">)</span> <span class="o">**</span> <span class="o">-</span><span class="mf">0.5</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">qkv</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="n">dim</span><span class="p">,</span> <span class="n">dim</span> <span class="o">*</span> <span class="mi">3</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">attn_drop</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="n">dropout</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">proj</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="n">dim</span><span class="p">,</span> <span class="n">dim</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">proj_drop</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="n">dropout</span><span class="p">)</span>
    
    <span class="k">def</span><span class="w"> </span><span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">B</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="n">D</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span>
        <span class="n">q</span><span class="p">,</span> <span class="n">k</span><span class="p">,</span> <span class="n">v</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">qkv</span><span class="p">(</span><span class="n">x</span><span class="p">)</span><span class="o">.</span><span class="n">chunk</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="n">dim</span><span class="o">=-</span><span class="mi">1</span><span class="p">)</span>
        <span class="n">q</span> <span class="o">=</span> <span class="n">q</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">B</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">heads</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>  <span class="c1"># (B, heads, N, d)</span>
        <span class="n">k</span> <span class="o">=</span> <span class="n">k</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">B</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">heads</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>
        <span class="n">v</span> <span class="o">=</span> <span class="n">v</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">B</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">heads</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>
        <span class="n">attn</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">matmul</span><span class="p">(</span><span class="n">q</span><span class="p">,</span> <span class="n">k</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="o">-</span><span class="mi">2</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">))</span> <span class="o">*</span> <span class="bp">self</span><span class="o">.</span><span class="n">scale</span>
        <span class="n">attn</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">attn_drop</span><span class="p">(</span><span class="n">attn</span><span class="o">.</span><span class="n">softmax</span><span class="p">(</span><span class="n">dim</span><span class="o">=-</span><span class="mi">1</span><span class="p">))</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">matmul</span><span class="p">(</span><span class="n">attn</span><span class="p">,</span> <span class="n">v</span><span class="p">)</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">reshape</span><span class="p">(</span><span class="n">B</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="n">D</span><span class="p">)</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">proj_drop</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">proj</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>

<span class="c1">#====================</span>
<span class="k">class</span><span class="w"> </span><span class="nc">TransformerBlock</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">dim</span><span class="p">,</span> <span class="n">heads</span><span class="p">,</span> <span class="n">mlp_ratio</span><span class="o">=</span><span class="mf">4.</span><span class="p">,</span> <span class="n">dropout</span><span class="o">=</span><span class="mf">0.</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">norm1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">LayerNorm</span><span class="p">(</span><span class="n">dim</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">attn</span>  <span class="o">=</span> <span class="n">MHSA</span><span class="p">(</span><span class="n">dim</span><span class="p">,</span> <span class="n">heads</span><span class="p">,</span> <span class="n">dropout</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">norm2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">LayerNorm</span><span class="p">(</span><span class="n">dim</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">mlp</span>   <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sequential</span><span class="p">(</span>
                                    <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="n">dim</span><span class="p">,</span> <span class="nb">int</span><span class="p">(</span><span class="n">dim</span> <span class="o">*</span> <span class="n">mlp_ratio</span><span class="p">)),</span>
                                    <span class="n">nn</span><span class="o">.</span><span class="n">GELU</span><span class="p">(),</span> <span class="n">nn</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="n">dropout</span><span class="p">),</span>
                                    <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="nb">int</span><span class="p">(</span><span class="n">dim</span> <span class="o">*</span> <span class="n">mlp_ratio</span><span class="p">),</span> <span class="n">dim</span><span class="p">),</span>
                                    <span class="n">nn</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="n">dropout</span><span class="p">))</span>
    
    <span class="k">def</span><span class="w"> </span><span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">attn</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">norm1</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">mlp</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">norm2</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="c1">#====================</span>
<span class="k">class</span><span class="w"> </span><span class="nc">ViT</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">in_ch</span><span class="o">=</span><span class="mi">1024</span><span class="p">,</span> <span class="n">num_classes</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span>
                 <span class="n">embed_dim</span><span class="o">=</span><span class="mi">768</span><span class="p">,</span> <span class="n">depth</span><span class="o">=</span><span class="mi">6</span><span class="p">,</span> <span class="n">heads</span><span class="o">=</span><span class="mi">8</span><span class="p">,</span>
                 <span class="n">mlp_ratio</span><span class="o">=</span><span class="mf">4.</span><span class="p">,</span> <span class="n">dropout</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="n">max_tokens</span><span class="o">=</span><span class="mi">50</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">patch</span> <span class="o">=</span> <span class="n">PatchEmbed</span><span class="p">(</span><span class="n">in_ch</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">)</span>           <span class="c1"># 1×1 conv</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">cls</span>   <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Parameter</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">))</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">pos</span>   <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Parameter</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">max_tokens</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">))</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">blocks</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">ModuleList</span><span class="p">([</span>
            <span class="n">TransformerBlock</span><span class="p">(</span><span class="n">embed_dim</span><span class="p">,</span> <span class="n">heads</span><span class="p">,</span> <span class="n">mlp_ratio</span><span class="p">,</span> <span class="n">dropout</span><span class="p">)</span>
            <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">depth</span><span class="p">)])</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">norm</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">LayerNorm</span><span class="p">(</span><span class="n">embed_dim</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">head</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="n">embed_dim</span><span class="p">,</span> <span class="n">num_classes</span><span class="p">)</span>

    <span class="k">def</span><span class="w"> </span><span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>                          <span class="c1"># x: (B,C,H,W)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">patch</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>                          <span class="c1"># (B,L,D)</span>
        <span class="n">B</span><span class="p">,</span> <span class="n">L</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">shape</span>
        <span class="bp">cls</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">cls</span><span class="o">.</span><span class="n">expand</span><span class="p">(</span><span class="n">B</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>           <span class="c1"># (B,1,D)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">cat</span><span class="p">((</span><span class="bp">cls</span><span class="p">,</span> <span class="n">x</span><span class="p">),</span> <span class="mi">1</span><span class="p">)</span>                 <span class="c1"># (B,L+1,D)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">pos</span><span class="p">[:,</span> <span class="p">:</span><span class="n">L</span> <span class="o">+</span> <span class="mi">1</span><span class="p">]</span>                <span class="c1"># match seq-len</span>
        <span class="k">for</span> <span class="n">blk</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">blocks</span><span class="p">:</span>
            <span class="n">x</span> <span class="o">=</span> <span class="n">blk</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">norm</span><span class="p">(</span><span class="n">x</span><span class="p">)[:,</span> <span class="mi">0</span><span class="p">])</span>       <span class="c1"># CLS token</span>

<span class="c1">#====================</span>
<span class="k">class</span><span class="w"> </span><span class="nc">CNN_ViT_Hybrid</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">num_classes</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">embed_dim</span><span class="o">=</span><span class="mi">768</span><span class="p">,</span> <span class="n">depth</span><span class="o">=</span><span class="mi">6</span><span class="p">,</span> <span class="n">heads</span><span class="o">=</span><span class="mi">8</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">cnn</span> <span class="o">=</span> <span class="n">ConvNet</span><span class="p">(</span><span class="n">num_classes</span><span class="p">)</span>            <span class="c1"># load weights later</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">vit</span> <span class="o">=</span> <span class="n">ViT</span><span class="p">(</span><span class="n">num_classes</span><span class="o">=</span><span class="n">num_classes</span><span class="p">,</span>
                       <span class="n">embed_dim</span><span class="o">=</span><span class="n">embed_dim</span><span class="p">,</span>
                       <span class="n">depth</span><span class="o">=</span><span class="n">depth</span><span class="p">,</span>
                       <span class="n">heads</span><span class="o">=</span><span class="n">heads</span><span class="p">)</span>
    
    <span class="k">def</span><span class="w"> </span><span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">vit</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">cnn</span><span class="o">.</span><span class="n">forward_features</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>

<span class="c1">#====================</span>
<span class="k">def</span><span class="w"> </span><span class="nf">evaluate</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">loader</span><span class="p">,</span> <span class="n">criterion</span><span class="p">,</span> <span class="n">device</span><span class="p">):</span>
    <span class="k">with</span> <span class="n">torch</span><span class="o">.</span><span class="n">no_grad</span><span class="p">():</span>
        <span class="n">model</span><span class="o">.</span><span class="n">eval</span><span class="p">()</span>
        <span class="n">loss_sum</span><span class="p">,</span> <span class="n">correct</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">0</span>
        <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">tqdm</span><span class="p">(</span><span class="n">loader</span><span class="p">,</span> <span class="n">desc</span><span class="o">=</span><span class="s2">"Validation"</span><span class="p">)):</span>
            <span class="n">x</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">to</span><span class="p">(</span><span class="n">device</span><span class="p">),</span> <span class="n">y</span><span class="o">.</span><span class="n">to</span><span class="p">(</span><span class="n">device</span><span class="p">)</span>
            <span class="n">out</span> <span class="o">=</span> <span class="n">model</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
            <span class="n">loss</span> <span class="o">=</span> <span class="n">criterion</span><span class="p">(</span><span class="n">out</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
            <span class="n">loss_sum</span> <span class="o">+=</span> <span class="n">loss</span><span class="o">.</span><span class="n">item</span><span class="p">()</span> <span class="o">*</span> <span class="n">x</span><span class="o">.</span><span class="n">size</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
            <span class="n">correct</span>  <span class="o">+=</span> <span class="p">(</span><span class="n">out</span><span class="o">.</span><span class="n">argmax</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span> <span class="o">==</span> <span class="n">y</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span><span class="o">.</span><span class="n">item</span><span class="p">()</span>
    <span class="k">return</span> <span class="n">loss_sum</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">loader</span><span class="o">.</span><span class="n">dataset</span><span class="p">),</span> <span class="n">correct</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">loader</span><span class="o">.</span><span class="n">dataset</span><span class="p">)</span><span class="c1"># Set device</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Dataset-path-and-hyperparameters">Dataset path and hyperparameters<a class="anchor-link" href="#Dataset-path-and-hyperparameters">¶</a></h2><p>Here, you set the dataset path and hyperparameters like image size, channels, batch size, classes, and labels. These are used for data loading and model configuration. Consistent dimensions ensure compatibility with model inputs.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Task-1:-Define-the-dataset-directory,-dataloader-and-model-hyperparameters.-The-dataloader-and-model-hyperparameters-should-be-same-as-used-during-training">Task 1: Define the dataset directory, dataloader and model hyperparameters. The dataloader and model hyperparameters should be same as used during training<a class="anchor-link" href="#Task-1:-Define-the-dataset-directory,-dataloader-and-model-hyperparameters.-The-dataloader-and-model-hyperparameters-should-be-same-as-used-during-training">¶</a></h2><ul>
<li><p>Define the <code>dataset_path</code></p>
</li>
<li><p>Define <strong>hyperparameters common dataloader</strong></p>
<ul>
<li><code>img_w</code>, <code>img_h = 64, 64</code></li>
<li><code>batch_size = 128</code></li>
<li><code>num_classes = 2</code></li>
<li><code>agri_class_labels = ["non-agri", "agri"]</code></li>
</ul>
</li>
<li><p>Define <strong>hyperparameters for PyTorch CNN-Vit Hybrid model</strong>. The values have to same as those used while training the hybrid model.</p>
<ul>
<li><code>depth = 3</code></li>
<li><code>attn_heads = 6</code></li>
<li><code>embed_dim = 768</code></li>
</ul>
</li>
</ul>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [15]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">## Please use the space below to write your answer</span>
<span class="n">dataset_path</span> <span class="o">=</span> <span class="n">os</span><span class="o">.</span><span class="n">path</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">data_dir</span><span class="p">,</span> <span class="s2">"images_dataSAT"</span><span class="p">)</span>

<span class="c1"># hyperparameters common dataloader</span>
<span class="n">img_w</span><span class="p">,</span> <span class="n">img_h</span> <span class="o">=</span> <span class="mi">64</span><span class="p">,</span> <span class="mi">64</span>
<span class="n">batch_size</span> <span class="o">=</span> <span class="mi">128</span>
<span class="n">num_classes</span> <span class="o">=</span> <span class="mi">2</span>
<span class="n">agri_class_labels</span> <span class="o">=</span> <span class="p">[</span><span class="s2">"non-agri"</span><span class="p">,</span> <span class="s2">"agri"</span><span class="p">]</span>

<span class="c1"># hyperparameters for PyTorch CNN-Vit Hybrid model</span>
<span class="n">depth</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">attn_heads</span> <span class="o">=</span> <span class="mi">6</span>
<span class="n">embed_dim</span> <span class="o">=</span> <span class="mi">768</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Double-click <strong>here</strong> for the solution.</p>
<!--
dataset_path = os.path.join(data_dir, "images_dataSAT")

# hyperparameters common dataloader
img_w, img_h = 64, 64
batch_size = 128
num_classes = 2
agri_class_labels = ["non-agri", "agri"]

# hyperparameters for PyTorch CNN-Vit Hybrid model
depth = 3
attn_heads = 6
embed_dim = 768
-->
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="PyTorch-Dataloader">PyTorch Dataloader<a class="anchor-link" href="#PyTorch-Dataloader">¶</a></h3><p>Defines transforms for resizing, tensor conversion, and normalization (ImageNet means/std).</p>
<p>Loads dataset with ImageFolder and creates DataLoader for batching without shuffling for evaluation.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [16]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">train_transform</span> <span class="o">=</span> <span class="n">transforms</span><span class="o">.</span><span class="n">Compose</span><span class="p">([</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">Resize</span><span class="p">((</span><span class="n">img_w</span><span class="p">,</span> <span class="n">img_h</span><span class="p">)),</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">ToTensor</span><span class="p">(),</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">Normalize</span><span class="p">([</span><span class="mf">0.485</span><span class="p">,</span> <span class="mf">0.456</span><span class="p">,</span> <span class="mf">0.406</span><span class="p">],</span> <span class="p">[</span><span class="mf">0.229</span><span class="p">,</span> <span class="mf">0.224</span><span class="p">,</span> <span class="mf">0.225</span><span class="p">])</span>
<span class="p">])</span>
<span class="n">full_dataset</span> <span class="o">=</span> <span class="n">datasets</span><span class="o">.</span><span class="n">ImageFolder</span><span class="p">(</span><span class="n">dataset_path</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">train_transform</span><span class="p">)</span>
<span class="n">test_loader</span> <span class="o">=</span> <span class="n">DataLoader</span><span class="p">(</span><span class="n">full_dataset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="n">batch_size</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Task-2:-Instantiate-PyTorch-model">Task 2: Instantiate PyTorch model<a class="anchor-link" href="#Task-2:-Instantiate-PyTorch-model">¶</a></h2><p>Check the availability of CUDA device and set the <code>device</code> parameter accordingly.</p>
<p>Based on the <code>CNN_ViT_Hybrid</code> function, instantiate the PyTorch model and move the model to the available <code>device</code></p>
<p>In this cell, you will:</p>
<ol>
<li>instantiate the PyTorch CNN_ViT_Hybrid with the previously declared model parameters</li>
<li>detect the device for model inference</li>
</ol>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [17]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">## Please use the space below to write your answer</span>
<span class="c1"># Check device availability</span>
<span class="n">device</span> <span class="o">=</span> <span class="s2">"cuda"</span> <span class="k">if</span> <span class="n">torch</span><span class="o">.</span><span class="n">cuda</span><span class="o">.</span><span class="n">is_available</span><span class="p">()</span> <span class="k">else</span> <span class="s2">"cpu"</span>

<span class="c1"># Create model instance</span>
<span class="n">pytorch_model</span> <span class="o">=</span> <span class="n">CNN_ViT_Hybrid</span><span class="p">(</span><span class="n">num_classes</span><span class="o">=</span><span class="n">num_classes</span><span class="p">,</span>
                      <span class="n">heads</span><span class="o">=</span><span class="n">attn_heads</span><span class="p">,</span>
                      <span class="n">depth</span><span class="o">=</span><span class="n">depth</span><span class="p">,</span>
                      <span class="n">embed_dim</span><span class="o">=</span><span class="n">embed_dim</span><span class="p">)</span><span class="o">.</span><span class="n">to</span><span class="p">(</span><span class="n">device</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Double-click <strong>here</strong> for the solution.</p>
<!--
# Check device availability
device = "cuda" if torch.cuda.is_available() else "cpu"

# Create model instance
pytorch_model = CNN_ViT_Hybrid(num_classes=num_classes,
                      heads=attn_heads,
                      depth=depth,
                      embed_dim=embed_dim).to(device)
-->
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [18]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Evaluating the PyTorch model on </span><span class="si">{</span><span class="n">device</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Evaluating the PyTorch model on cpu
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="----PyTorch-pre-trained-ViT-model-loading----">--- PyTorch pre-trained ViT model loading ---<a class="anchor-link" href="#----PyTorch-pre-trained-ViT-model-loading----">¶</a></h3><p>In this cell, you will load the PyTorch model state dict with <strong><code>strict=False</code></strong> for flexibility.</p>
<p>Thus, you prepare the model for inference.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [19]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Load pre-trained CNN-ViT hybrid model weights </span>
<span class="k">if</span> <span class="n">device</span><span class="o">==</span><span class="s2">"cpu"</span><span class="p">:</span>
    <span class="n">map_location</span><span class="o">=</span><span class="n">torch</span><span class="o">.</span><span class="n">device</span><span class="p">(</span><span class="s2">"cpu"</span><span class="p">)</span>
<span class="k">else</span><span class="p">:</span>
    <span class="n">map_location</span><span class="o">=</span><span class="n">torch</span><span class="o">.</span><span class="n">device</span><span class="p">(</span><span class="s2">"cuda"</span><span class="p">)</span>

<span class="n">pytorch_model</span><span class="o">.</span><span class="n">load_state_dict</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">load</span><span class="p">(</span><span class="n">pytorch_state_dict_path</span><span class="p">,</span> <span class="n">map_location</span><span class="o">=</span><span class="n">map_location</span><span class="p">),</span> <span class="n">strict</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">"Loaded model state dict, now getting predictions"</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Loaded model state dict, now getting predictions
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="PyTorch-model-inference-metrics">PyTorch model inference metrics<a class="anchor-link" href="#PyTorch-model-inference-metrics">¶</a></h3><p>Now, you perform:</p>
<ol>
<li>inference on test_loader</li>
<li>collecte prediction, labels, and probabilities (for class 1)</li>
<li>Uses no_grad for efficiency and eval mode</li>
<li>Use tqdm to show progress.</li>
<li>Move the data to the training device (CPU/GPU).</li>
</ol>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [20]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>
<span class="n">all_preds_pytorch</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">all_labels_pytorch</span> <span class="o">=</span> <span class="p">[]</span>
<span class="n">all_probs_pytorch</span> <span class="o">=</span> <span class="p">[]</span>

<span class="n">pytorch_model</span><span class="o">.</span><span class="n">eval</span><span class="p">()</span>
<span class="k">with</span> <span class="n">torch</span><span class="o">.</span><span class="n">no_grad</span><span class="p">():</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">images</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">tqdm</span><span class="p">(</span><span class="n">test_loader</span><span class="p">,</span> <span class="n">desc</span><span class="o">=</span><span class="s2">"Step"</span><span class="p">)):</span>
<span class="c1">#    for images, labels in test_loader:</span>
        <span class="n">images</span> <span class="o">=</span> <span class="n">images</span><span class="o">.</span><span class="n">to</span><span class="p">(</span><span class="n">device</span><span class="p">)</span>
        <span class="n">outputs</span> <span class="o">=</span> <span class="n">pytorch_model</span><span class="p">(</span><span class="n">images</span><span class="p">)</span>
        <span class="n">preds</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">argmax</span><span class="p">(</span><span class="n">outputs</span><span class="p">,</span> <span class="n">dim</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
        <span class="n">probs</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">softmax</span><span class="p">(</span><span class="n">outputs</span><span class="p">,</span> <span class="n">dim</span><span class="o">=</span><span class="mi">1</span><span class="p">)[:,</span> <span class="mi">1</span><span class="p">]</span>  <span class="c1"># probability for class 1</span>
        <span class="n">all_probs_pytorch</span><span class="o">.</span><span class="n">extend</span><span class="p">(</span><span class="n">probs</span><span class="o">.</span><span class="n">cpu</span><span class="p">())</span>
        <span class="n">all_preds_pytorch</span><span class="o">.</span><span class="n">extend</span><span class="p">(</span><span class="n">preds</span><span class="o">.</span><span class="n">cpu</span><span class="p">()</span><span class="o">.</span><span class="n">numpy</span><span class="p">()</span><span class="o">.</span><span class="n">flatten</span><span class="p">())</span>
        <span class="n">all_labels_pytorch</span><span class="o">.</span><span class="n">extend</span><span class="p">(</span><span class="n">labels</span><span class="o">.</span><span class="n">numpy</span><span class="p">())</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr" tabindex="0">
<pre>Step: 100%|██████████| 47/47 [01:12&lt;00:00,  1.54s/it]</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>CPU times: user 55.2 s, sys: 15.6 s, total: 1min 10s
Wall time: 1min 12s
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr" tabindex="0">
<pre>
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Keras-model-loading">Keras model loading<a class="anchor-link" href="#Keras-model-loading">¶</a></h2><p>To load the Keras based CNN-ViT hybrid model, you will</p>
<ul>
<li>define <strong>custom Keras layers</strong> with serialization for model saving/loading for:<ul>
<li><code>position embedding</code></li>
<li><code>transformer block</code></li>
</ul>
</li>
</ul>
<p>This step is essential for reconstructing the ViT architecture in Keras.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [21]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Positional embedding that Keras can track</span>
<span class="nd">@tf</span><span class="o">.</span><span class="n">keras</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">register_keras_serializable</span><span class="p">(</span><span class="n">package</span><span class="o">=</span><span class="s2">"Custom"</span><span class="p">)</span>
<span class="k">class</span><span class="w"> </span><span class="nc">AddPositionEmbedding</span><span class="p">(</span><span class="n">layers</span><span class="o">.</span><span class="n">Layer</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">num_patches</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">,</span> <span class="o">**</span><span class="n">kwargs</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">AddPositionEmbedding</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">(</span><span class="o">**</span><span class="n">kwargs</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">num_patches</span> <span class="o">=</span> <span class="n">num_patches</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">embed_dim</span>   <span class="o">=</span> <span class="n">embed_dim</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">pos</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">add_weight</span><span class="p">(</span>
            <span class="n">name</span><span class="o">=</span><span class="s2">"pos_embedding"</span><span class="p">,</span>
            <span class="n">shape</span><span class="o">=</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">num_patches</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">),</span>
            <span class="n">initializer</span><span class="o">=</span><span class="s2">"random_normal"</span><span class="p">,</span>
            <span class="n">trainable</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

    <span class="k">def</span><span class="w"> </span><span class="nf">call</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">tokens</span><span class="p">):</span>
        <span class="k">return</span> <span class="n">tokens</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">pos</span>

    <span class="k">def</span><span class="w"> </span><span class="nf">get_config</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="n">config</span> <span class="o">=</span> <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="n">get_config</span><span class="p">()</span>
        <span class="n">config</span><span class="o">.</span><span class="n">update</span><span class="p">({</span>
            <span class="s2">"num_patches"</span><span class="p">:</span> <span class="bp">self</span><span class="o">.</span><span class="n">num_patches</span><span class="p">,</span>
            <span class="s2">"embed_dim"</span><span class="p">:</span>   <span class="bp">self</span><span class="o">.</span><span class="n">embed_dim</span><span class="p">,</span>
        <span class="p">})</span>
        <span class="k">return</span> <span class="p">{</span><span class="o">**</span><span class="n">config</span><span class="p">}</span>

<span class="c1"># One Transformer encoder block</span>
<span class="nd">@tf</span><span class="o">.</span><span class="n">keras</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">register_keras_serializable</span><span class="p">(</span><span class="n">package</span><span class="o">=</span><span class="s2">"Custom"</span><span class="p">)</span>
<span class="k">class</span><span class="w"> </span><span class="nc">TransformerBlock</span><span class="p">(</span><span class="n">layers</span><span class="o">.</span><span class="n">Layer</span><span class="p">):</span>
    <span class="k">def</span><span class="w"> </span><span class="fm">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">embed_dim</span><span class="p">,</span> <span class="n">num_heads</span><span class="o">=</span><span class="mi">8</span><span class="p">,</span> <span class="n">mlp_dim</span><span class="o">=</span><span class="mi">2048</span><span class="p">,</span> <span class="n">dropout</span><span class="o">=</span><span class="mf">0.1</span><span class="p">,</span> <span class="o">**</span><span class="n">kwargs</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">TransformerBlock</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">(</span><span class="o">**</span><span class="n">kwargs</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">embed_dim</span> <span class="o">=</span> <span class="n">embed_dim</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">num_heads</span> <span class="o">=</span> <span class="n">num_heads</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">mlp_dim</span>   <span class="o">=</span> <span class="n">mlp_dim</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">dropout</span>   <span class="o">=</span> <span class="n">dropout</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">mha</span>  <span class="o">=</span> <span class="n">layers</span><span class="o">.</span><span class="n">MultiHeadAttention</span><span class="p">(</span><span class="n">num_heads</span><span class="p">,</span> <span class="n">key_dim</span><span class="o">=</span><span class="n">embed_dim</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">norm1</span> <span class="o">=</span> <span class="n">layers</span><span class="o">.</span><span class="n">LayerNormalization</span><span class="p">(</span><span class="n">epsilon</span><span class="o">=</span><span class="mf">1e-6</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">norm2</span> <span class="o">=</span> <span class="n">layers</span><span class="o">.</span><span class="n">LayerNormalization</span><span class="p">(</span><span class="n">epsilon</span><span class="o">=</span><span class="mf">1e-6</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">mlp</span> <span class="o">=</span> <span class="n">tf</span><span class="o">.</span><span class="n">keras</span><span class="o">.</span><span class="n">Sequential</span><span class="p">([</span>
            <span class="n">layers</span><span class="o">.</span><span class="n">Dense</span><span class="p">(</span><span class="n">mlp_dim</span><span class="p">,</span> <span class="n">activation</span><span class="o">=</span><span class="s2">"gelu"</span><span class="p">),</span>
            <span class="n">layers</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="n">dropout</span><span class="p">),</span>
            <span class="n">layers</span><span class="o">.</span><span class="n">Dense</span><span class="p">(</span><span class="n">embed_dim</span><span class="p">),</span>
            <span class="n">layers</span><span class="o">.</span><span class="n">Dropout</span><span class="p">(</span><span class="n">dropout</span><span class="p">)</span>
        <span class="p">])</span>

    <span class="k">def</span><span class="w"> </span><span class="nf">call</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">norm1</span><span class="p">(</span><span class="n">x</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">mha</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="n">x</span><span class="p">))</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">norm2</span><span class="p">(</span><span class="n">x</span> <span class="o">+</span> <span class="bp">self</span><span class="o">.</span><span class="n">mlp</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>

    <span class="c1"># ---- NEW ----</span>
    <span class="k">def</span><span class="w"> </span><span class="nf">get_config</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="n">config</span> <span class="o">=</span> <span class="nb">super</span><span class="p">()</span><span class="o">.</span><span class="n">get_config</span><span class="p">()</span>
        <span class="n">config</span><span class="o">.</span><span class="n">update</span><span class="p">({</span>
            <span class="s2">"embed_dim"</span><span class="p">:</span>  <span class="bp">self</span><span class="o">.</span><span class="n">embed_dim</span><span class="p">,</span>
            <span class="s2">"num_heads"</span><span class="p">:</span>  <span class="bp">self</span><span class="o">.</span><span class="n">num_heads</span><span class="p">,</span>
            <span class="s2">"mlp_dim"</span><span class="p">:</span>    <span class="bp">self</span><span class="o">.</span><span class="n">mlp_dim</span><span class="p">,</span>
            <span class="s2">"dropout"</span><span class="p">:</span>    <span class="bp">self</span><span class="o">.</span><span class="n">dropout</span><span class="p">,</span>
        <span class="p">})</span>
        <span class="k">return</span> <span class="p">{</span><span class="o">**</span><span class="n">config</span><span class="p">}</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="----Keras-pre-trained-ViT-model-loading----">--- Keras pre-trained ViT model loading ---<a class="anchor-link" href="#----Keras-pre-trained-ViT-model-loading----">¶</a></h3><p>Here, you will load the pre-trained Keras model using <strong><code>load_model</code></strong>, providing <strong>custom objects</strong> for deserialization of user-defined layers. This enables inference with the hybrid model.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># ------------------- load CNN-ViT hybrid model ------------------</span>
<span class="n">keras_model</span> <span class="o">=</span> <span class="n">load_model</span><span class="p">(</span><span class="n">keras_model_name</span><span class="p">,</span>
                         <span class="n">custom_objects</span><span class="o">=</span><span class="p">{</span>
                         <span class="s2">"AddPositionEmbedding"</span><span class="p">:</span> <span class="n">AddPositionEmbedding</span><span class="p">,</span>
                         <span class="s2">"TransformerBlock"</span><span class="p">:</span>     <span class="n">TransformerBlock</span>
                          <span class="p">})</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Define-dataloader">Define dataloader<a class="anchor-link" href="#Define-dataloader">¶</a></h3><p>In this cell, you create an ImageDataGenerator for rescaling and a generator for flowing images from directory, matching PyTorch setup for consistent evaluation.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">datagen</span> <span class="o">=</span> <span class="n">ImageDataGenerator</span><span class="p">(</span><span class="n">rescale</span><span class="o">=</span><span class="mf">1.</span><span class="o">/</span><span class="mi">255</span><span class="p">)</span>
<span class="n">prediction_generator</span> <span class="o">=</span> <span class="n">datagen</span><span class="o">.</span><span class="n">flow_from_directory</span><span class="p">(</span>
    <span class="n">dataset_path</span><span class="p">,</span>
    <span class="n">target_size</span><span class="o">=</span><span class="p">(</span><span class="n">img_w</span><span class="p">,</span> <span class="n">img_h</span><span class="p">),</span>
    <span class="n">batch_size</span><span class="o">=</span><span class="n">batch_size</span><span class="p">,</span>
    <span class="n">class_mode</span><span class="o">=</span><span class="s2">"binary"</span><span class="p">,</span>
    <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span>
<span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Found 6000 images belonging to 2 classes.
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Collecting-metrics-for-Keras-based-CNN-ViT-hybrid-model">Collecting metrics for Keras-based CNN-ViT hybrid model<a class="anchor-link" href="#Collecting-metrics-for-Keras-based-CNN-ViT-hybrid-model">¶</a></h3><p>Now, run the inference of the Keras-based CNN-ViT hybrid model and collect the evaluation metrics.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [24]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>

<span class="n">all_probs_keras</span> <span class="o">=</span> <span class="n">keras_model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">prediction_generator</span><span class="p">,</span> <span class="n">verbose</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">all_preds_keras</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">argmax</span><span class="p">(</span><span class="n">all_probs_keras</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">all_labels_keras</span> <span class="o">=</span> <span class="n">prediction_generator</span><span class="o">.</span><span class="n">classes</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre><span class="ansi-bold">47/47</span> <span class="ansi-green-fg">━━━━━━━━━━━━━━━━━━━━</span> <span class="ansi-bold">148s</span> 3s/step
CPU times: user 2min 14s, sys: 7.1 s, total: 2min 21s
Wall time: 2min 28s
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Import-the-evaluation-metrics">Import the evaluation metrics<a class="anchor-link" href="#Import-the-evaluation-metrics">¶</a></h2><p>Here you define the functions to compute and print classification metrics including accuracy, precision, recall, F1 score, ROC-AUC, confusion matrix, and log loss. These functions support both Keras and PyTorch model outputs.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [25]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="o">%%time</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">sklearn.metrics</span><span class="w"> </span><span class="kn">import</span> <span class="p">(</span><span class="n">accuracy_score</span><span class="p">,</span>
                             <span class="n">precision_score</span><span class="p">,</span>
                             <span class="n">recall_score</span><span class="p">,</span>
                             <span class="n">f1_score</span><span class="p">,</span>
                             <span class="n">roc_curve</span><span class="p">,</span> 
                             <span class="n">roc_auc_score</span><span class="p">,</span>
                             <span class="n">log_loss</span><span class="p">,</span>
                             <span class="n">classification_report</span><span class="p">,</span>
                             <span class="n">confusion_matrix</span><span class="p">,</span>
                             <span class="n">ConfusionMatrixDisplay</span><span class="p">,</span>
                            <span class="p">)</span>
<span class="kn">from</span><span class="w"> </span><span class="nn">sklearn.preprocessing</span><span class="w"> </span><span class="kn">import</span> <span class="n">label_binarize</span>

<span class="c1"># define a function to get the metrics comprehensively</span>
<span class="k">def</span><span class="w"> </span><span class="nf">model_metrics</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">,</span> <span class="n">class_labels</span><span class="p">):</span>
    <span class="n">y_prob</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">y_prob</span><span class="p">)</span>
    <span class="k">if</span> <span class="nb">len</span><span class="p">(</span><span class="n">y_prob</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span><span class="o">&lt;</span><span class="mi">2</span><span class="p">:</span>
        <span class="n">roc_score</span> <span class="o">=</span> <span class="n">roc_auc_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">)</span>
    <span class="k">elif</span> <span class="nb">len</span><span class="p">(</span><span class="n">y_prob</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span><span class="o">==</span><span class="mi">2</span><span class="p">:</span>
        <span class="n">roc_score</span> <span class="o">=</span> <span class="n">roc_auc_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">[:,</span><span class="mi">1</span><span class="p">])</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">roc_score</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span>
    <span class="n">metrics</span> <span class="o">=</span> <span class="p">{</span><span class="s1">'Accuracy'</span><span class="p">:</span> <span class="n">accuracy_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">),</span>
               <span class="s1">'Precision'</span><span class="p">:</span> <span class="n">precision_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">),</span>
               <span class="s1">'Recall'</span><span class="p">:</span> <span class="n">recall_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">),</span>
               <span class="s1">'Loss'</span><span class="p">:</span> <span class="n">log_loss</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">),</span>
               <span class="s1">'F1 Score'</span><span class="p">:</span> <span class="n">f1_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">),</span>
               <span class="s1">'ROC-AUC'</span><span class="p">:</span> <span class="n">roc_score</span><span class="p">,</span>
               <span class="s1">'Confusion Matrix'</span><span class="p">:</span> <span class="n">confusion_matrix</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">),</span>
               <span class="s1">'Classification Report'</span><span class="p">:</span> <span class="n">classification_report</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">,</span> <span class="n">target_names</span><span class="o">=</span><span class="n">class_labels</span><span class="p">,</span> <span class="n">digits</span><span class="o">=</span><span class="mi">4</span><span class="p">),</span>
               <span class="s2">"Class labels"</span><span class="p">:</span> <span class="n">class_labels</span>
              <span class="p">}</span>
    <span class="k">return</span> <span class="n">metrics</span>

<span class="c1">#function to print the metrics</span>
<span class="k">def</span><span class="w"> </span><span class="nf">print_metrics</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">,</span> <span class="n">class_labels</span><span class="p">,</span> <span class="n">model_name</span><span class="p">):</span>
    <span class="n">metrics</span> <span class="o">=</span> <span class="n">model_metrics</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">,</span> <span class="n">class_labels</span><span class="p">)</span>
    
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Evaluation metrics for the </span><span class="se">\033</span><span class="s2">[1m</span><span class="si">{</span><span class="n">model_name</span><span class="si">}</span><span class="se">\033</span><span class="s2">[0m"</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Accuracy: </span><span class="si">{</span><span class="s1">''</span><span class="si">:</span><span class="s2">&lt;1</span><span class="si">}{</span><span class="n">metrics</span><span class="p">[</span><span class="s2">"Accuracy"</span><span class="p">]</span><span class="si">:</span><span class="s2">.4f</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
    <span class="k">if</span> <span class="n">metrics</span><span class="p">[</span><span class="s2">"ROC-AUC"</span><span class="p">]</span> <span class="o">!=</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"ROC-AUC: </span><span class="si">{</span><span class="s1">''</span><span class="si">:</span><span class="s2">&lt;2</span><span class="si">}{</span><span class="n">metrics</span><span class="p">[</span><span class="s2">"ROC-AUC"</span><span class="p">]</span><span class="si">:</span><span class="s2">.4f</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Loss: </span><span class="si">{</span><span class="s1">''</span><span class="si">:</span><span class="s2">&lt;5</span><span class="si">}{</span><span class="n">metrics</span><span class="p">[</span><span class="s2">"Loss"</span><span class="p">]</span><span class="si">:</span><span class="s2">.4f</span><span class="si">}</span><span class="se">\n</span><span class="s2">"</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="sa">f</span><span class="s2">"Classification report:</span><span class="se">\n\n</span><span class="s2">  </span><span class="si">{</span><span class="n">metrics</span><span class="p">[</span><span class="s2">"Classification Report"</span><span class="p">]</span><span class="si">}</span><span class="s2">"</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"========= Confusion Matrix ========="</span><span class="p">)</span>
    <span class="n">disp</span> <span class="o">=</span> <span class="n">ConfusionMatrixDisplay</span><span class="p">(</span><span class="n">confusion_matrix</span><span class="o">=</span><span class="n">metrics</span><span class="p">[</span><span class="s2">"Confusion Matrix"</span><span class="p">],</span>
                                  <span class="n">display_labels</span><span class="o">=</span><span class="n">metrics</span><span class="p">[</span><span class="s2">"Class labels"</span><span class="p">])</span>

    <span class="n">disp</span><span class="o">.</span><span class="n">plot</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>CPU times: user 28.7 ms, sys: 20.9 ms, total: 49.5 ms
Wall time: 59.9 ms
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Keras-metrics-reporting">Keras metrics reporting<a class="anchor-link" href="#Keras-metrics-reporting">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Task-3:-Print-the-evaluation-metrics-using-print_metrics-function-for-the-Keras-ViT-model-with-name-Keras-CNN-Vit-Hybrid-Model">Task 3: Print the evaluation metrics using <code>print_metrics</code> function for the <strong>Keras</strong> ViT model with name <code>Keras CNN-Vit Hybrid Model</code><a class="anchor-link" href="#Task-3:-Print-the-evaluation-metrics-using-print_metrics-function-for-the-Keras-ViT-model-with-name-Keras-CNN-Vit-Hybrid-Model">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [26]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">## Please use the space below to write your answer</span>
<span class="n">print_metrics</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">all_labels_keras</span><span class="p">,</span>
              <span class="n">y_pred</span> <span class="o">=</span> <span class="n">all_preds_keras</span><span class="p">,</span>
              <span class="n">y_prob</span> <span class="o">=</span> <span class="n">all_probs_keras</span><span class="p">,</span>
              <span class="n">class_labels</span> <span class="o">=</span> <span class="n">agri_class_labels</span><span class="p">,</span>
              <span class="n">model_name</span> <span class="o">=</span> <span class="s2">"Keras CNN-Vit Hybrid Model"</span>
             <span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Evaluation metrics for the <span class="ansi-bold">Keras CNN-Vit Hybrid Model</span>
Accuracy:  0.9958
ROC-AUC:   0.9998
Loss:      0.0530

Classification report:

                precision    recall  f1-score   support

    non-agri     0.9927    0.9990    0.9958      3000
        agri     0.9990    0.9927    0.9958      3000

    accuracy                         0.9958      6000
   macro avg     0.9959    0.9958    0.9958      6000
weighted avg     0.9959    0.9958    0.9958      6000

========= Confusion Matrix =========
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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fPFFSdKMGTO0ePFizZ8/X7t27dLo0aN1++23a/369ZLKkq9+/fqpd+/eSk1N1d13360JEya4/DUJDAxUYmKifvjhB7344otasGCB5syZ4zBmz549WrZsmVauXKnVq1fru+++0/3332/fnpSUpEmTJmn69OlKS0vT008/rSeeeEKLFi1yOR4A1cgAUCMNHjzY6NOnj2EYhmGz2YyUlBTDarUajzzyiH17eHi4UVhYaN/nrbfeMqKjow2bzWZfV1hYaPj5+RmffPKJYRiG0aBBA2PWrFn27cXFxUajRo3s5zIMw+jSpYvxz3/+0zAMw0hPTzckGSkpKWeM8/PPPzckGb/++qt9XUFBgVGnTh1j06ZNDmOHDRtm3HbbbYZhGMajjz5qxMTEOGwfP378acf6M0nGBx98cNbts2fPNtq1a2f//OSTTxre3t7GoUOH7Os+/vhjw8vLyzh69KhhGIZx2WWXGUuWLHE4zrRp04z4+HjDMAxj//79hiTju+++O+t5AVQ/5tQANVhycrICAgJUXFwsm82mgQMHavLkyfbtsbGxDvNotm/frj179igwMNDhOAUFBdq7d69ycnJ09OhRdezY0b6tVq1aat++/WktqHKpqany9vZWly5dKhz3nj17dOrUKV133XUO64uKinTllVdKktLS0hzikKT4+PgKn6Pc0qVLNXfuXO3du1d5eXkqKSlRUFCQw5jGjRurYcOGDuex2WxKT09XYGCg9u7dq2HDhmn48OH2MSUlJQoODnY5HgDVh6QGqMG6deumV199VT4+PoqMjFStWo7/Zf39/R0+5+XlqV27dkpKSjrtWPXr1z+vGPz8/FzeJy8vT5L00UcfOSQTUtk8ocqyefNmDRo0SFOmTFFCQoKCg4P19ttv67nnnnM51gULFpyWZHl7e1darACqHkkNUIP5+/urefPmFR5/1VVXaenSpQoLCzutWlGuQYMG2rJlizp37iyprCKxbds2XXXVVWccHxsbK5vNpvXr16t79+6nbS+vFJWWltrXxcTEyGq1KiMj46wVnlatWtknPZf76quvzn2R/2PTpk1q0qSJJk6caF/3888/nzYuIyNDR44cUWRkpP08Xl5eio6OVnh4uCIjI7Vv3z4NGjTIpfMDqFmYKAx4kEGDBumSSy5Rnz59tGHDBu3fv1/r1q3Tgw8+qEOHDkmS/vnPf2rmzJlavny5fvzxR91///1OnzFz6aWXavDgwRo6dKiWL19uP+ayZcskSU2aNJHFYlFycrJ++eUX5eXlKTAwUI888ohGjx6tRYsWae/evfr222/10ksv2Sff3nvvvdq9e7fGjh2r9PR0LVmyRImJiS5db4sWLZSRkaG3335be/fu1dy5c8846dnX11eDBw/W9u3btWHDBj344IO65ZZbFBERIUmaMmWKZsyYoblz5+qnn37Sjh079Oabb+r55593KR4A1YukBvAgderU0RdffKHGjRurX79+atWqlYYNG6aCggJ75ebhhx/WHXfcocGDBys+Pl6BgYG66aabnB731Vdf1c0336z7779fLVu21PDhw5Wfny9JatiwoaZMmaIJEyYoPDxco0aNkiRNmzZNTzzxhGbMmKFWrVqpZ8+e+uijj9S0aVNJZfNc3nvvPS1fvlxt2rTR/Pnz9fTTT7t0vTfeeKNGjx6tUaNGqW3bttq0aZOeeOKJ08Y1b95c/fr10w033KAePXooLi7O4Zbtu+++WwsXLtSbb76p2NhYdenSRYmJifZYAZiDxTjb7EAAAAAToVIDAAA8AkkNAADwCCQ1AADAI5DUAAAAj0BSAwAAPAJJDQAA8AgkNQAAwCOQ1AAAAI9AUgMAADwCSQ0AAPAIJDUAAMAj/D9RpP+rklF0aAAAAABJRU5ErkJggg=="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Double-click <strong>here</strong> for the solution.</p>
<!--
print_metrics(y_true = all_labels_keras,
              y_pred = all_preds_keras,
              y_prob = all_probs_keras,
              class_labels = agri_class_labels,
              model_name = "Keras CNN-Vit Hybrid Model"
             )
-->
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="PyTorch-metrics-reporting">PyTorch metrics reporting<a class="anchor-link" href="#PyTorch-metrics-reporting">¶</a></h2>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Task-4:-Print-the-evaluation-metrics-using-print_metrics-function-for-the-PyTorch-ViT-model-with-model-name-PyTorch-CNN-Vit-Hybrid-Model">Task 4: Print the evaluation metrics using <code>print_metrics</code> function for the <strong>PyTorch</strong> ViT model with model name <code>PyTorch CNN-Vit Hybrid Model</code><a class="anchor-link" href="#Task-4:-Print-the-evaluation-metrics-using-print_metrics-function-for-the-PyTorch-ViT-model-with-model-name-PyTorch-CNN-Vit-Hybrid-Model">¶</a></h2>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [27]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">## Please use the space below to write your answer</span>
<span class="n">print_metrics</span><span class="p">(</span><span class="n">y_true</span> <span class="o">=</span> <span class="n">all_labels_pytorch</span><span class="p">,</span>
              <span class="n">y_pred</span> <span class="o">=</span> <span class="n">all_preds_pytorch</span><span class="p">,</span>
              <span class="n">y_prob</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">all_probs_pytorch</span><span class="p">),</span>
              <span class="n">class_labels</span> <span class="o">=</span> <span class="n">agri_class_labels</span><span class="p">,</span>
              <span class="n">model_name</span> <span class="o">=</span> <span class="s2">"PyTorch CNN-Vit Hybrid Model"</span>
             <span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>Evaluation metrics for the <span class="ansi-bold">PyTorch CNN-Vit Hybrid Model</span>
Accuracy:  0.9990
ROC-AUC:   1.0000
Loss:      0.0047

Classification report:

                precision    recall  f1-score   support

    non-agri     0.9990    0.9990    0.9990      3000
        agri     0.9990    0.9990    0.9990      3000

    accuracy                         0.9990      6000
   macro avg     0.9990    0.9990    0.9990      6000
weighted avg     0.9990    0.9990    0.9990      6000

========= Confusion Matrix =========
</pre>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Double-click <strong>here</strong> for the solution.</p>
<!--
print_metrics(y_true = all_labels_pytorch,
              y_pred = all_preds_pytorch,
              y_prob = np.array(all_probs_pytorch),
              class_labels = agri_class_labels,
              model_name = "PyTorch CNN-Vit Hybrid Model"
             )
-->
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="ROC-curve-plotting">ROC curve plotting<a class="anchor-link" href="#ROC-curve-plotting">¶</a></h2><p>First, define a function to plot ROC curves for binary or multi-class classification using scikit-learn's <code>roc_curve</code> and <code>roc_auc_score</code>. It handles both single-class and multi-class cases by binarizing labels if needed.</p>
<p>Next, plot the ROC curves for both the models.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [28]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="k">def</span><span class="w"> </span><span class="nf">plot_roc</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">,</span> <span class="n">model_name</span><span class="p">):</span>
    <span class="n">n_classes</span> <span class="o">=</span> <span class="n">y_prob</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]</span> <span class="k">if</span> <span class="n">y_prob</span><span class="o">.</span><span class="n">ndim</span> <span class="o">&gt;</span> <span class="mi">1</span> <span class="k">else</span> <span class="mi">1</span>
    <span class="k">if</span> <span class="n">n_classes</span> <span class="o">==</span> <span class="mi">1</span><span class="p">:</span>
        <span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">roc_curve</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">)</span>
        <span class="n">auc</span> <span class="o">=</span> <span class="n">roc_auc_score</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">y_prob</span><span class="p">)</span>
        <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="sa">f</span><span class="s1">'</span><span class="si">{</span><span class="n">model_name</span><span class="si">}</span><span class="s1"> (AUC = </span><span class="si">{</span><span class="n">auc</span><span class="si">:</span><span class="s1">.4f</span><span class="si">}</span><span class="s1">)'</span><span class="p">)</span>
    <span class="k">else</span><span class="p">:</span>
        <span class="n">y_true_bin</span> <span class="o">=</span> <span class="n">label_binarize</span><span class="p">(</span><span class="n">y_true</span><span class="p">,</span> <span class="n">classes</span><span class="o">=</span><span class="n">np</span><span class="o">.</span><span class="n">arange</span><span class="p">(</span><span class="n">n_classes</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">n_classes</span><span class="p">):</span>
            <span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="n">_</span> <span class="o">=</span> <span class="n">roc_curve</span><span class="p">(</span><span class="n">y_true_bin</span><span class="p">[:,</span> <span class="n">i</span><span class="p">],</span> <span class="n">y_prob</span><span class="p">[:,</span> <span class="n">i</span><span class="p">])</span>
            <span class="n">auc</span> <span class="o">=</span> <span class="n">roc_auc_score</span><span class="p">(</span><span class="n">y_true_bin</span><span class="p">[:,</span> <span class="n">i</span><span class="p">],</span> <span class="n">y_prob</span><span class="p">[:,</span> <span class="n">i</span><span class="p">])</span>
            <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">fpr</span><span class="p">,</span> <span class="n">tpr</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="sa">f</span><span class="s1">'</span><span class="si">{</span><span class="n">model_name</span><span class="si">}</span><span class="s1"> class </span><span class="si">{</span><span class="n">i</span><span class="si">}</span><span class="s1"> (AUC = </span><span class="si">{</span><span class="n">auc</span><span class="si">:</span><span class="s1">.4f</span><span class="si">}</span><span class="s1">)'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">'False Positive Rate'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">'True Positive Rate'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'ROC Curve'</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="ROC-curve-plotting-for-both-models">ROC curve plotting for both models<a class="anchor-link" href="#ROC-curve-plotting-for-both-models">¶</a></h3><p>Plot the ROC curves for both Keras and PyTorch models on the same figure for visual performance comparison.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [29]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">plot_roc</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">all_labels_keras</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">all_probs_keras</span><span class="p">[:,</span> <span class="mi">1</span><span class="p">]),</span> <span class="s2">"Keras Model"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
<span class="n">plot_roc</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">all_labels_pytorch</span><span class="p">),</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">all_probs_pytorch</span><span class="p">),</span> <span class="s2">"PyTorch Model"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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4evrq9Xm5+eHTz/9tNQxBQUFKCgo0LzPycmprPKgVgt8sPE09idlVto+iIiIqrsODW2wY2xng+2/RoWbjIwMODg4aLU5ODggJycHT548gbm5ebExYWFhmDNnTpXUF7juJI5cydJqU5jwmm0iInqxmBob9mdfjQo3FTF16lQEBwdr3ufk5MDFxaVS9vX7tfuaX3/SrSkm9mgOmUxWKfsiIiKiktWocOPo6IjMTO1TPpmZmbCysirxqA0AKBQKKBSKqigPyiI1AGDFkPbo2865SvZJRERE2mrUORNvb2/ExsZqte3fvx/e3t4Gquh/8gtVml+7N7AxXCFEREQvOIOGm8ePHyMxMRGJiYkA/r7VOzExETdu3ADw9yml4cOHa/p/+OGHSE1NxRdffIFLly5h5cqV2LJlCyZOnGiI8rX8M9w425R8FImIiIgqn0HDzR9//IH27dujffv2AIDg4GC0b98es2bNAgCkp6drgg4AuLm5Yc+ePdi/fz/c3d2xePFirF27ttrdBk5ERESGY9Brbl577TUIIUr9vKTVh1977TWcOXOmEqsiIiKimqxGXXNDRERE9CwMN0RERCQpDDdEREQkKQw3REREJCkMN0RERCQpDDd6UsZNX0RERFSFGG4qAZ8mRUREZDgMN0RERCQpDDdEREQkKQw3REREJCkMN0RERCQpDDdEREQkKQw3REREJCkMN3rCZW6IiIiqB4abSiDjQjdEREQGw3BDREREksJwQ0RERJLCcENERESSwnBDREREksJwQ0RERJLCcENERESSwnBDREREksJwoydCcBk/IiKi6oDhphLIuIofERGRwTDcEBERkaQw3BAREZGkMNwQERGRpDDcEBERkaQw3BAREZGkMNwQERGRpDDc6AlXuSEiIqoeGG6IiIhIUhhuiIiISFIYboiIiEhSGG6IiIhIUhhuiIiISFIYboiIiEhSGG6IiIhIUhhuiIiISFIYbvREcBU/IiKiaoHhRs9kMkNXQERE9GJjuCEiIiJJYbghIiIiSWG4ISIiIklhuCEiIiJJYbghIiIiSWG4ISIiIklhuNETAS50Q0REVB0w3OgZl7khIiIyLIYbIiIikhSGGyIiIpIUhhsiIiKSFIYbIiIikhSGGyIiIpIUhhsiIiKSFIYbIiIikhSDh5vw8HC4urrCzMwMnTp1wsmTJ8vsv3TpUrRo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zJkzqF+/vl6KqokEXqjlgoiIiKotncPNoEGDMHnyZGRkZEAmk0GtVuPYsWOYNGkShg8fXhk11igyGVe6ISIiMiSdw01oaChatmwJFxcXPH78GK1bt8arr74KHx8fzJgxozJqJCIiIio3nZ8tJZfLsWbNGsycORMXLlzA48eP0b59ezRr1qwy6iMiIiLSic7h5ujRo3jllVfQsGFDNGzYsDJqIiIiIqownU9LdevWDW5ubpg2bRqSkpIqoyYiIiKiCtM53Ny5cwefffYZDh06hDZt2sDDwwMLFy7ErVu3KqM+IiIiIp3oHG7s7Owwfvx4HDt2DCkpKXj33Xfx448/wtXVFd26dauMGomIiIjK7bkenOnm5oYpU6ZgwYIFaNu2LQ4dOqSvuoiIiIgqpMLh5tixYxg7diycnJwwZMgQtGnTBnv27NFnbTWK4Bp+RERE1YLOd0tNnToVUVFRuHPnDnr06IFly5ahf//+sLCwqIz6ahwu4UdERGRYOoebw4cP4/PPP8fAgQNhZ2dXGTURERERVZjO4ebYsWOVUQcRERGRXpQr3OzevRu9e/eGqakpdu/eXWbfN998Uy+FEREREVVEucKNv78/MjIyYG9vD39//1L7yWQyqFQqfdVGREREpLNyhRu1Wl3ir4mIiIiqG51vBV+/fj0KCgqKtSuVSqxfv14vRRERERFVlM7hJigoCNnZ2cXaHz16hKCgIL0URURERFRROocbIQRksuKrudy6dQvW1tZ6Kaom4hp+RERE1UO5bwVv3749ZDIZZDIZunfvDhOT/w1VqVS4du0aevXqVSlF1ihcxY+IiMigyh1unt4llZiYCD8/P9SuXVvzmVwuh6urK95++229F0hERESki3KHm5CQEACAq6srAgICYGZmVmlFEREREVWUzisUBwYGVkYdRERERHpRrnBja2uLy5cvw87ODnXq1CnxguKn7t+/r7fiiIiIiHRVrnDzzTffwNLSUvPrssINERERkSGVK9z881TUiBEjKqsWIiIiouem8zo3CQkJOH/+vOb9zz//DH9/f0ybNg1KpVKvxdUkQnClGyIioupA53DzwQcf4PLlywCA1NRUBAQEwMLCAlu3bsUXX3yh9wJrGp6wIyIiMiydw83ly5fh4eEBANi6dSu6du2KzZs3IzIyEtu3b9d3fUREREQ6qdDjF54+GfzAgQPo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"/>
</div>
</div>
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAjcAAAHHCAYAAABDUnkqAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjkuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8hTgPZAAAACXBIWXMAAA9hAAAPYQGoP6dpAABJsklEQVR4nO3deZxOdf/H8fc1Y65ZmBnck1mYGvsSWeM3llQmo0XcFVNkmUordSdFC4MKd6SV3AljSbZUbkRMUSSEsWQLI9uMJczYZoa5vr8/erjuLrOYa8zC8Xo+Htcj1/d8v+d8zkkz7875nnNsxhgjAAAAi/Ao6QIAAAAKE+EGAABYCuEGAABYCuEGAABYCuEGAABYCuEGAABYCuEGAABYCuEGAABYCuEGAABYCuEGAABYCuEGQJ7i4+Nls9mcn1KlSqlixYrq2bOnDh48mOMYY4ymTp2q2267TWXLlpWfn5/q1aunoUOH6syZM7lu66uvvtLdd9+toKAg2e12hYWFqXPnzvr+++/zVWt6erree+89NWvWTIGBgfLx8VGNGjXUu3dv7dy5s0D7D+DaY+PdUgDyEh8fr9jYWA0dOlSVK1dWenq6fvnlF8XHxysiIkJbtmyRj4+Ps39WVpa6dOmiWbNmqVWrVnrggQfk5+enn376SdOnT1edOnW0dOlSBQcHO8cYY/TYY48pPj5eDRs21EMPPaSQkBAlJyfrq6++0rp167Ry5Uo1b9481zqPHTumdu3aad26dbrvvvsUFRWlMmXKaMeOHZoxY4ZSUlKUmZlZpMcKwFXCAEAeJk2aZCSZtWvXurT379/fSDIzZ850aR82bJiRZPr165dtXfPmzTMeHh6mXbt2Lu0jR440ksy//vUv43A4so2bMmWKWb16dZ513nvvvcbDw8PMmTMn27L09HTz0ksv5Tk+v86fP28yMjIKZV0AigbhBkCecgs38+fPN5LMsGHDnG1nz5415cqVMzVq1DDnz5/PcX2xsbFGklm1apVzTPny5U2tWrXMhQsXClTjL7/8YiSZXr165at/69atTevWrbO19+jRw9x0003O70lJSUaSGTlypHnvvfdMlSpVjIeHh/nll1+Mp6enGTx4cLZ1bN++3UgyH330kbPtxIkT5oUXXjCVKlUydrvdVK1a1YwYMcJkZWW5va8ALo85NwAKZO/evZKkcuXKOdtWrFihEydOqEuXLipVqlSO47p37y5Jmj9/vnPM8ePH1aVLF3l6ehaolnnz5kmSunXrVqDxlzNp0iR99NFHevLJJ/Xuu+8qNDRUrVu31qxZs7L1nTlzpjw9PdWpUydJ0tmzZ9W6dWtNmzZN3bt314cffqgWLVro1VdfVd++fYukXuB6l/NPHwC4RGpqqo4dO6b09HStXr1aQ4YMkbe3t+677z5nn61bt0qS6tevn+t6Li7btm2byz/r1atX4NoKYx15OXDggHbt2qUbbrjB2RYTE6OnnnpKW7ZsUd26dZ3tM2fOVOvWrZ1zikaPHq3du3drw4YNql69uiTpqaeeUlhYmEaOHKmXXnpJ4eHhRVI3cL3izA2AfImKitINN9yg8PBwPfTQQypdurTmzZunSpUqOfucOnVKkuTv75/rei4uS0tLc/lnXmMupzDWkZcHH3zQJdhI0gMPPKBSpUpp5syZzrYtW7Zo69atiomJcbbNnj1brVq1Urly5XTs2DHnJyoqSllZWfrxxx+LpGbgesaZGwD5MmbMGNWoUUOpqamaOHGifvzxR3l7e7v0uRguLoacnFwagAICAi475nL+vo6yZcsWeD25qVy5cra2oKAgtWnTRrNmzdKbb74p6a+zNqVKldIDDzzg7Pf7779r06ZN2cLRRUeOHCn0eoHrHeEGQL40bdpUTZo0kSR17NhRLVu2VJcuXbRjxw6VKVNGklS7dm1J0qZNm9SxY8cc17Np0yZJUp06dSRJtWrVkiRt3rw51zGX8/d1tGrV6rL9bTabTA5PwcjKysqxv6+vb47tDz/8sGJjY5WYmKgGDRpo1qxZatOmjYKCgpx9HA6H7rrrLr3yyis5rqNGjRqXrReAe7gsBcBtnp6eGj58uA4dOqSPP/7Y2d6yZUuVLVtW06dPzzUoTJkyRZKcc3VatmypcuXK6Ysvvsh1zOW0b99ekjRt2rR89S9XrpxOnjyZrf2PP/5wa7sdO3aU3W7XzJkzlZiYqJ07d+rhhx926VO1alWdPn1aUVFROX5uvPFGt7YJ4PIINwAK5Pbbb1fTpk31/vvvKz09XZLk5+enfv36aceOHXr99dezjVmwYIHi4+MVHR2t//u//3OO6d+/v7Zt26b+/fvneEZl2rRpWrNmTa61REZGql27dvrss8/09ddfZ1uemZmpfv36Ob9XrVpV27dv19GjR51tGzdu1MqVK/O9/5JUtmxZRUdHa9asWZoxY4bsdnu2s0+dO3fWqlWrtHjx4mzjT548qQsXLri1TQCXxxOKAeTp4hOK165d67wsddGcOXPUqVMnffLJJ3r66acl/XVpJyYmRl9++aVuu+02Pfjgg/L19dWKFSs0bdo01a5dWwkJCS5PKHY4HOrZs6emTp2qRo0aOZ9QnJKSoq+//lpr1qzRzz//rMjIyFzrPHr0qNq2bauNGzeqffv2atOmjUqXLq3ff/9dM2bMUHJysjIyMiT9dXdV3bp1Vb9+fT3++OM6cuSIxo0bp+DgYKWlpTlvc9+7d68qV66skSNHuoSjv/v888/16KOPyt/fX7fffrvztvSLzp49q1atWmnTpk3q2bOnGjdurDNnzmjz5s2aM2eO9u7d63IZC0AhKNnH7AC42uX2ED9jjMnKyjJVq1Y1VatWdXkAX1ZWlpk0aZJp0aKFCQgIMD4+Pubmm282Q4YMMadPn851W3PmzDFt27Y15cuXN6VKlTKhoaEmJibGLFu2LF+1nj171owaNcrceuutpkyZMsZut5vq1aubPn36mF27drn0nTZtmqlSpYqx2+2mQYMGZvHixXk+xC83aWlpxtfX10gy06ZNy7HPqVOnzKuvvmqqVatm7Ha7CQoKMs2bNzejRo0ymZmZ+do3APnHmRsAAGApzLkBAACWQrgBAACWQrgBAACWQrgBAACWQrgBAACWQrgBAACWct29W8rhcOjQoUPy9/eXzWYr6XIAAEA+GGN06tQphYWFycMj73Mz1124OXTokMLDw0u6DAAAUAD79+9XpUqV8uxz3YUbf39/SX8dnICAgBKuBgAA5EdaWprCw8Odv8fzct2Fm4uXogICAgg3AABcY/IzpYQJxQAAwFIINwAAwFIINwAAwFIINwAAwFIINwAAwFIINwAAwFIINwAAwFIINwAAwFIINwAAwFIINwAAwFJKNNz8+OOPat++vcLCwmSz2fT1119fdsyyZcvUqFEjeXt7q1q1aoqPjy/yOgEAwLWjRMPNmTNnVL9+fY0ZMyZf/ZOSknTvvffqjjvuUGJiov71r3/piSee0OLFi4u4UgAAcK0o0Rdn3n333br77rvz3X/cuHGqXLmy3n33XUlS7dq1tWLFCr333nuKjo4uqjLzzRijc+ezSroMAABKnK+XZ75eclkUrqm3gq9atUpRUVEubdHR0frXv/6V65iMjAxlZGQ4v6elpRVJbcYYPTRuldb9caJI1g8AwLVk69Bo+dlLJmZcUxOKU1JSFBwc7NIWHBystLQ0nTt3Lscxw4cPV2BgoPMTHh5eJLWdO59FsAEA4CpwTZ25KYhXX31Vffv2dX5PS0srsoBz0a9vRMnP7lmk2wAA4Grm61VyvwevqXATEhKiw4cPu7QdPnxYAQEB8vX1zXGMt7e3vL29i6M8Jz+7Z4mdigMA4Hp3TV2WioyMVEJCgkvbkiVLFBkZWUIVAQCAq02JhpvTp08rMTFRiYmJkv661TsxMVH79u2T9Nclpe7duzv7P/3009qzZ49eeeUVbd++XWPHjtWsWbP04osvlkT5AADgKlSi4ebXX39Vw4YN1bBhQ0lS37591bBhQw0aNEiSlJyc7Aw6klS5cmUtWLBAS5YsUf369fXuu+/qs88+uypuAwcAAFeHEp0Ycvvtt8sYk+vynJ4+fPvtt2vDhg1FWBUAALiWXVNzbgAAAC6HcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACylxMPNmDFjFBERIR8fHzVr1kxr1qzJs//777+vmjVrytfXV+Hh4XrxxReVnp5eTNUCAICrXYmGm5kzZ6pv376Ki4vT+vXrVb9+fUVHR+vIkSM59p8+fboGDBiguLg4bdu2TRMmTNDMmTP12muvFXPlAADgalWi4Wb06NHq1auXYmNjVadOHY0bN05+fn6aOHFijv1//vlntWjRQl26dFFERITatm2rRx555LJnewAA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/PjxatWqlcqVK6dy5copKioqz/4AAOD6UuLhZubMmerbt6/i4uK0fv161a9fX9HR0Tpy5EiO/ZctW6ZHHnlEP/zwg1atWqXw8HC1bdtWBw8eLObKAQDA1chmjDElWUCzZs1066236uOPP5YkORwOhYeHq0+fPhowYMBlx2dlZalcuXL6+OOP1b1798v2T0tLU2BgoFJTUxUQEHDF9V90NvOC6gxaLEnaOjRafvZShbZuAACud+78/i7RMzeZmZlat26doqKinG0eHh6KiorSqlWr8rWOs2fP6vz58ypfvnxRlQkAAK4hJXp64dixY8rKylJwcLBLe3BwsLZv356vdfTv319hYWEuAenvMjIylJGR4fyelpZW8IIBAMBVr8Tn3FyJESNGaMaMGfrqq6/k4+OTY5/hw4crMDDQ+QkPDy/mKgEAQHEq0XATFBQkT09PHT582KX98OHDCgkJyXPsqFGjNGLECH333Xe65ZZbcu336quvKjU11fnZv39/odQOAACuTiUabux2uxo3bqyEhARnm8PhUEJCgiIjI3Md98477+jNN9/UokWL1KRJkzy34e3trYCAAJcPAACwrhK/padv377q0aOHmjRpoqZNm+r999/XmTNnFBsbK0nq3r27KlasqOHDh0uS/v3vf2vQoEGaPn26IiIilJKSIkkqU6aMypQpU2L7AQAArg4lHm5iYmJ09OhRDRo0SCkpKWrQoIEWLVrknGS8b98+eXj87wTTJ598oszMTD300EMu64mLi9PgwYOLs3QAAHAVKvHn3BQ3nnMDAMC155p5zg0AAEBhI9wAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLKVXSBQC4vhljdOHCBWVlZZV0KQBKmJeXlzw9Pa94PYQbACUmMzNTycnJOnv2bEmXAuAqYLPZVKlSJZUpU+aK1kO4AVAiHA6HkpKS5OnpqbCwMNntdtlstpIuC0AJMcbo6NGjOnDggKpXr35FZ3AINwBKRGZmphwOh8LDw+Xn51fS5QC4Ctxwww3au3evzp8/f0XhhgnFAEqUhwc/hgD8pbDO3vJTBQAAWArhBgAsLD4+XmXLli3pMnJ0++2361//+le+++d3XyZMmKC2bdsWvDAUiQEDBqhPnz7Fsi3CDQC4oWfPnrLZbLLZbLLb7apWrZqGDh2qCxcuXHZsfHy8c2xun7179xb9TlzG3r17ZbPZ5OnpqYMHD7osS05OVqlSpa6aWi+Vnp6ugQMHKi4uLtuyAwcOyG63q27dutmWXdznxMTEbMtyCmEbNmxQp06dFBwcLB8fH1WvXl29evXSzp07C2tXspk7d67atm2rf/zjH7nWmpPZs2erVq1a8vHxUb169bRw4UKX5cYYDRo0SKGhofL19VVUVJR+//13lz7Hjx9X165dFRAQoLJly+rxxx/X6dOnXfps2rRJrVq1ko+Pj8LDw/XOO++4LO/Xr58mT56sPXv2uL/zbiLcAICb2rVrp+TkZP3+++966aWXNHjwYI0cOfKy42JiYpScnOz8REZGqlevXi5t4eHh+a4jMzPzSnbjsipWrKgpU6a4tE2ePFkVK1Ys0u1eiTlz5iggIEAtWrTItiw+Pl6dO3dWWlqaVq9eXeBtzJ8/X//3f/+njIwMff7559q2bZumTZumwMBADRw48ErKz9OZM2fUsmVL/fvf/873mJ9//lmPPPKIHn/8cW3YsEEdO3ZUx44dtWXLFmefd955Rx9++KHGjRun1atXq3Tp0oqOjlZ6erqzT9euXfXbb79pyZIlmj9/vn788Uc9+eSTzuVpaWlq27atbrrpJq1bt04jR47U4MGD9emnnzr7BAUFKTo6Wp988skVHol8MNeZ1NRUI8mkpqYW6nrPZJw3N/Wfb27qP9+cyThfqOsGrOjcuXNm69at5ty5cyVdilt69OhhOnTo4NJ21113mf/7v/8zp0+fNv7+/mb27Nkuy7/66ivj5+dn0tLSXNpbt25tXnjhBef3P/74w9x///2mdOnSxt/f33Tq1MmkpKQ4l8fFxZn69eub8ePHm4iICGOz2Ywxxpw4ccI8+eSTpkKFCsbb29vcfPPN5r///a8xxphJkyaZwMBAs2jRIlOrVi1TunRpEx0dbQ4dOpTrPiYlJRlJ5o033jDVq1d3WVajRg0zcOBAI8kkJSU525ctW2ZuvfVWY7fbTUhIiOnfv785f/5/PwtPnz5tunXrZkqXLm1CQkLMqFGjsu1/enq6eemll0xYWJjx8/MzTZs2NT/88INz+cV9ycu9995r+vXrl63d4XCYKlWqmEWLFpn+/fubXr165bjPGzZsyDb273WeOXPGBAUFmY4dO+a4/RMnTuRZX2HIq9ZLde7c2dx7770ubc2aNTNPPfWUMeav4xISEmJGjhzpXH7y5Enj7e1tvvjiC2OMMVu3bjWSzNq1a519vv32W2Oz2czBgweNMcaMHTvWlCtXzmRkZDj79O/f39SsWdNl25MnTzaVKlXKtd68fi648/ubMzcArgrGGJ3NvFAiH2PMFdXu6+urzMxMlS5dWg8//LAmTZrksnzSpEl66KGH5O/vn+s6HA6HOnTooOPHj2v58uVasmSJ9uzZo5iYGJd+u3bt0pdffqm5c+cqMTFRDodDd999t1auXKlp06Zp69atGjFihMtttGfPntWoUaM0depU/fjjj9q3b5/69et32f26//77deLECa1YsUKStGLFCp04cULt27d36Xfw4EHdc889uvXWW7Vx40Z98sknmjBhgt566y1nn5dfflnLly/XN998o++++07Lli3T+vXrXdbTu3dvrVq1SjNmzNCmTZvUqVMntWvXLtslkrysWLFCTZo0ydb+ww8/6OzZs4qKitKjjz6qGTNm6MyZM/le70WLFy/WsWPH9Morr+S4PK85QU8//bTKlCmT56ewrVq1SlFRUS5t0dHRWrVqlSQpKSlJKSkpLn0CAwPVrFkzZ59Vq1apbNmyLsc1KipKHh4ezjNgq1at0m233Sa73e6ynR07dujEiRPOtqZNm+rAgQNFfkmT59wAuCqcO5+lOoMWl8i2tw6Nlp/d/R+HxhglJCRo8eLFzomSTzzxhJo3b67k5GSFhobqyJEjWrhwoZYuXZrnuhISErR582YlJSU5L01NmTJFN998s9auXatbb71V0l+XoqZMmaIbbrhBkvTdd99pzZo12rZtm2rUqCFJqlKlisu6z58/r3Hjxqlq1aqS/goRQ4cOvez+eXl56dFHH9XEiRPVsmVLTZw4UY8++qi8vLxc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Cn41+uijj8yNN95o7Ha7adq0qfnll1+cy1q3bm169Ojh0n/WrFmmRo0axm63m5tvvtksWLCgmCu+NrlznG+66SYjKdsnLi6u+Au/xrj79/nvCDf55+5x/vnnn02zZs2Mt7e3qVKlinn77bfNhQsXirnqa487x/n8+fNm8ODBpmrVqsbHx8eEh4ebZ5991pw4caL4C7+G/PDDDzn+vL14bHv06GFat26dbUyDBg2M3W43VapUMZMmTSryOm3GcP4NAABYB3NuAACApRBuAACApRBuAACApRBuAACApRBuAACApRBuAACApRBuAACApRBuALiIj49X2bJlS7qMArPZbPr666/z7NOzZ0917NixWOoBUPwIN4AF9ezZUzabLdtn165dJV2a4uPjnfV4eHioUqVKio2N1ZEjRwpl/cnJybr77rslSXv37pXNZlNiYqJLnw8++EDx8fGFsr3cDB482Lmfnp6eCg8P15NPPqnjx4+7tR6CGOA+3goOWFS7du00adIkl7YbbrihhKpxFRAQoB07dsjhcGjjxo2KjY3VoUOHtHjx4ite9+XeHi9JgYGBV7yd/Lj55pu1dOlSZWVladu2bXrssceUmpqqmTNnFsv2gesVZ24Ai/L29lZISIjLx9PTU6NHj1a9evVUunRphYeH69lnn9Xp06dzXc/GjRt1xx13yN/fXwEBAWrcuLF+/fVX5/IVK1aoVatW8vX1VXh4uJ5//nmdOXMmz9psNptCQkIUFhamu+++W88//7yWLl2qc+fOyeFwaOjQoapUqZK8vb3VoEEDLVq0yDk2MzNTvXv3VmhoqHx8fHTTTTdp+PDhLuu+eFmqcuXKkqSGDRvKZrPp9ttvl+R6NuTTTz9VWFiYy1u4JalDhw567LHHnN+/+eYbNWrUSD4+PqpSpYqGDBmiCxcu5LmfpUqVUkhIiCpWrKioqCh16tRJS5YscS7PysrS448/rsqVK8vX11c1a9bUBx984Fw+ePBgTZ48Wd98843zLNCyZcskSfv371fnzp1VtmxZlS9fXh06dNDevXvzrAe4XhBugOuMh4eHPvzwQ/3222+aPHmyvv/+e73yyiu59u/atasqVaqktWvXat26dRowYIC8vLwkSbt371a7du304IMPatOmTZo5c6ZWrFih3r17u1WTr6+vHA6HLly4oA8++EDvvvuuRo0apU2bNik6Olr333+/fv/9d0nShx9+qHnz5mnWrFnasWOHPv/8c0VEROS43jVr1kiSli5dquTkZM2dOzdbn06dOunPP//UDz/84Gw7fvy4Fi1apK5du0qSfvrpJ3Xv3l0vvPCCtm7dqv/85z+Kj4/X22+/ne993Lt3rxYvXiy73e5sczgcqlSpkmbPnq2tW7dq0KBBeu211zRr1ixJUr9+/dS5c2e1a9dOycnJSk5OVvPmzXX+/HlFR0fL399fP/30k1auXKkyZcqoXbt2yszMzHdNgGUV+as5ARS7Hj16GE9PT1O6dGnn56GHHsqx7+zZs80//vEP5/dJkyaZwMBA53d/f38THx+f49jHH3/cPPnkky5tP/30k/Hw8DDnzp3Lccyl69+5c6epUaOGadKkiTHGmLCwMPP222+7jLn11lvNs88+a4wxpk+fPubOO+80Docjx/VLMl999ZUxxpikpCQjyWzYsMGlz6VvNO/QoYN57LHHnN//85//mLCwMJOVlWWMMaZNmzZm2LBhLuuYOnWqCQ0NzbEGY4yJi4szHh4epnTp0sbHx8f59uTRo0fnOsYYY5577jnz4IMP5lrrxW3XrFnT5RhkZGQYX19fs3jx4jzXD1wPmHMDWNQdd9yhTz75xPm9dOnSkv46izF8+HBt375daWlpunDhgtLT03X27Fn5+fllW0/fvn31xBNPaOrUqc5LK1WrVpX01yWrTZs26fPPP3f2N8bI4XAoKSlJtWvXzrG21NRUlSlTRg6HQ+np6WrZsqU+++wzpaWl6dChQ2rRooVL/xYtWmjjxo2S/rqkdNddd6lmzZpq166d7rvvPrVt2/aKjlXXrl3Vq1cvjR07Vt7e3vr888/18MMPy8PDw7mfK1eudDlTk5WVledxk6SaNWtq3rx5Sk9P17Rp05SYmKg+ffq49BkzZowmTpyoffv26dy5c8rMzFSDBg3yrHfjxo3atWuX/P39XdrT09O1e/fuAhwBwFoIN4BFlS5dWtWqVXNp27t3r+677z4988wzevvtt1W+fHmtWLFCjz/+uDIzM3P8JT148GB16dJFCxYs0Lfffqu4uDjNmDFD//znP3X69Gk99dRTev7557ONu/HGG3Otzd/fX+vXr5eHh4dCQ0Pl6+srSUpLS7vsfjVq1EhJSUn69ttvtXTpUnXu3FlRUVGaM2fOZcfmpn379jLGaMGCBbr11lv1008/6b333nMuP336tIYMGaIHHngg21gfH59c12u3253/DkaMGKF7771XQ4YM0ZtvvilJmjFjhvr166d3331XkZGR8vf318iRI7V69eo86z19+rQaN27sEiovulomjQMliXADXEfWrVsnh8Ohd99913lW4uL8jrzUqFFDNWrU0IsvvqhHHnlEkyZN0j//+U81atRIW7duzRaiLsfDwyPHMQEBAQoLC9PKlSvVunVrZ/vKlSvVtGlTl34xMTGKiYnRQw89pHbt2un48eMqX768y/ouzm/JysrKsx4fHx898MAD+vzzz7Vr1y7VrFlTjRo1ci5v1KiRduzY4fZ+XuqNN97QnXfeqWeeeca5n82bN9ezzz7r7HPpmRe73Z6t/kaNGmnmzJmqUKGCAgICrqgmwIqYUAxcR6pVq6bz58/ro48+0p49ezR16lSNGzcu1/7nzp1T7969tWzZMv3xxx9auXKl1q5d67zc1L9/f/3888/q3bu3EhMT9fvvv+ubb75xe0Lx37388sv697//rZkzZ2rHjh0aMGCAEhMT9cILL0iSRo8erS+++ELbt2/Xzp07NXv2bIWEhOT44MEKFSrI19dXixYt0uHDh5Wamprrdrt27aoFCxZo4sSJzonEFw0aNEhTpkzRkCFD9Ntvv2nbtm2aMWOG3njjDbf2LTIyUrfccouGDRsmSapevbp+/fVXLV68WDt37tTAgQO1du1alzERERHatGmTduzYoWPHjun8+fPq2rWrgoKC1KFDB/30009KSkrSsmXL9Pzzz+vAgQNu1QRYUklP+gFQ+HKahHrR6NGjTWhoqPH19TXR0dFmypQpRpI5ceKEMcZ1wm9GRoZ5+OGHTXh4uLHb7SYsLMz07t3bZbLwmjVrzF133WXKlCljSpcubW655ZZsE4L/7tIJxZfKysoygwcPNhUrVjReXl6mfv365ttvv3Uu//TTT02DBg1M6dKlTUBAgGnTpo1Zv369c7n+NqHYGGPGjx9vwsPDjYeHh2ndunWuxycrK8uEhoYaSWb37t3Z6lq0aJFp3ry58fX1NQEBAaZp06bm008/zXU/4uLiTP369bO1f/HFF8bb29vs27fPpKenm549e5rAwEBTtmxZ88wzz5gBAwa4jDty5Ijz+EoyP/zwgzHGmOTkZNO9e3cTFBRkvL29TZUqVUyvXr1MampqrjUB1wubMcaUbLwCAAAoPFyWAgAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlvL/VPJDiN64XWEAAAAASUVORK5CYII="/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Comparing-model-performance">Comparing model performance<a class="anchor-link" href="#Comparing-model-performance">¶</a></h2><p>Now compare the performance of different models to understand which model would be the best performer for your land classification task.
Computed metrics for both models are used to generate a comparison table for key scores. This facilitates quick performance assessment between frameworks.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [30]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># get the Keras model performance metrics</span>
<span class="n">metrics_keras</span> <span class="o">=</span> <span class="n">model_metrics</span><span class="p">(</span><span class="n">all_labels_keras</span><span class="p">,</span> <span class="n">all_preds_keras</span><span class="p">,</span> <span class="n">all_probs_keras</span><span class="p">,</span> <span class="n">agri_class_labels</span><span class="p">)</span>

<span class="c1"># get the PyTorch model performance metrics</span>
<span class="n">metrics_pytorch</span> <span class="o">=</span> <span class="n">model_metrics</span><span class="p">(</span><span class="n">all_labels_pytorch</span><span class="p">,</span> <span class="n">all_preds_pytorch</span><span class="p">,</span> <span class="n">all_probs_pytorch</span><span class="p">,</span> <span class="n">agri_class_labels</span><span class="p">)</span>


<span class="c1"># Display the comparison of metrics</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">"</span><span class="si">{:&lt;18}</span><span class="s2"> | </span><span class="si">{:&lt;15}</span><span class="s2"> </span><span class="si">{:&lt;15}</span><span class="s2">"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="s1">'</span><span class="se">\033</span><span class="s1">[1m'</span><span class="o">+</span> <span class="s1">'Metric'</span> <span class="o">+</span> <span class="s1">'</span><span class="se">\033</span><span class="s1">[0m'</span><span class="p">,</span>
                                    <span class="s1">'Keras Model'</span><span class="p">,</span> 
                                    <span class="s1">'PyTorch Model'</span><span class="p">))</span>
<span class="nb">print</span><span class="p">((</span><span class="s2">""</span><span class="o">.</span><span class="n">join</span><span class="p">([</span><span class="s2">"-"</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">43</span><span class="p">)])))</span>
<span class="n">metrics_list</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'Accuracy'</span><span class="p">,</span> <span class="s1">'Precision'</span><span class="p">,</span> <span class="s1">'Recall'</span><span class="p">,</span> <span class="s1">'F1 Score'</span><span class="p">,</span> <span class="s1">'ROC-AUC'</span><span class="p">]</span>

<span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="n">metrics_list</span><span class="p">:</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">"</span><span class="si">{:&lt;18}</span><span class="s2"> | </span><span class="si">{:&lt;15.4f}</span><span class="s2"> </span><span class="si">{:&lt;15.4f}</span><span class="s2">"</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="s1">'</span><span class="se">\033</span><span class="s1">[1m'</span><span class="o">+</span><span class="n">k</span><span class="o">+</span><span class="s1">'</span><span class="se">\033</span><span class="s1">[0m'</span><span class="p">,</span>
                                              <span class="n">metrics_keras</span><span class="p">[</span><span class="n">k</span><span class="p">],</span>
                                              <span class="n">metrics_pytorch</span><span class="p">[</span><span class="n">k</span><span class="p">]))</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre><span class="ansi-bold">Metric</span>     | Keras Model     PyTorch Model  
-------------------------------------------
<span class="ansi-bold">Accuracy</span>   | 0.9958          0.9990         
<span class="ansi-bold">Precision</span>  | 0.9990          0.9990         
<span class="ansi-bold">Recall</span>     | 0.9927          0.9990         
<span class="ansi-bold">F1 Score</span>   | 0.9958          0.9990         
<span class="ansi-bold">ROC-AUC</span>    | 0.9998          1.0000         
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Summary-and-discussion">Summary and discussion<a class="anchor-link" href="#Summary-and-discussion">¶</a></h2><p>This notebook showcased a framework-agnostic workflow for importing, testing, and evaluating Vision Transformer models built in both Keras and PyTorch. By running the same input through each model, we examined the compatibility of results and gained practical experience handling architectural and data format variations.</p>
<p>Key insights include the criticality of input format alignment, the subtle differences in model serialization/loading, and the framework-induced variations in prediction outputs. For a more robust evaluation, repeat this process with a labeled validation dataset, compute further metrics (precision, recall, F1-score), and systematically analyze speed and resource usage.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Save-and-download-the-notebook-for-final-project-submission-and-evaluation">Save and download the notebook for <strong>final project</strong> submission and evaluation<a class="anchor-link" href="#Save-and-download-the-notebook-for-final-project-submission-and-evaluation">¶</a></h2><p>You will need to save and download the completed notebook for final project submission and evaluation.
<br/>For saving and downloading the completed notebook, please follow the steps given below:</p>
<font size="4">
<ol>
<li><strong>Complete</strong> all the tasks and questions given in the notebook.</li>
</ol>
<img alt="No description has been provided for this image" src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/nv4jHlPU5_R1q7ZJrZ69eg/DL0321EN-M1L1-Save-IPYNB-Screenshot-1.png" style="width:600px; border:0px solid black;"/>
<ol start="2">
<li><p><strong>Save</strong> the notebook.
<img alt="No description has been provided for this image" src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/9-WPWD4mW1d-RV5Il5otTg/DL0321EN-M1L1-Save-IPYNB-Screenshot-2.png" style="width:600px; border:0px solid black;"/></p>
</li>
<li><p>Identify and right click on the <strong>correct notebook file</strong> in the left pane.
<img alt="No description has been provided for this image" src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/RUSRPw7NT6Sof94B7-9naQ/DL0321EN-M1L1-Save-IPYNB-Screenshot-3.png" style="width:600px; border:0px solid black;"/></p>
</li>
<li><p>Click on <strong>Download</strong>.
<img alt="No description has been provided for this image" src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/HHry4GT-vhLEcRi1T_LHGg/DL0321EN-M1L1-Save-IPYNB-Screenshot-4.png" style="width:600px; border:0px solid black;"/></p>
</li>
<li><p>Download and <strong>Save</strong> the Jupyter notebook file on your computer <strong>for final submission</strong>.
<img alt="No description has been provided for this image" src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/hhsJbxc6R-T8_pXQGjMjvg/DL0321EN-M1L1-Save-IPYNB-Screenshot-5.png" style="width:600px; border:0px solid black;"/>
</p></li></ol></font>


</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2 id="Conclusion">Conclusion<a class="anchor-link" href="#Conclusion">¶</a></h2><p>Congratulations! You have successfully completed this lab and now you have a good understanding about loading custom pre-trained models, for both Keras and PyTorch frameworks. Using these pre-trained models, you can now evaluate their performance and also infer unknown datasets.
I hope you have learnt to apply the key concepts of Keras/Pytorch based classifiers, both traditional CNNs and more advanced and state-of-the-art, CNN-ViT hybrid models. Using this knowledge, now you should be able to tackle a variety of real world image classification problems. Good luck!</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h2>Author</h2>
<p><a href="https://www.linkedin.com/in/aggarwal-aman">Aman Aggarwal</a></p>
<p>Aman Aggarwal is a PhD working at the intersection of neuroscience, AI, and drug discovery. He specializes in quantitative microscopy and image processing.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<!--
## Change Log

|  Date (YYYY-MM-DD) |  Version | Changed By  |  Change Description |
|---|---|---|---|
| 2025-07-28  | 1.0  | Aman  |  Created the lab |

-->
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>© Copyright IBM Corporation. All rights reserved.</p>
</div>
</div>
</div>
</div>
</main>
</body>
</html>
