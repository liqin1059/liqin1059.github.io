---
layout: post
title: ios自带样式
date: 2017-04-14 12:31:30
categories: css3
tags: [移动端]
---
IOS系统的button,input,select,radio,checkbox等标签都有自带的样式
	-webkit-appearance:none;appearance:none;outline:none;-webkit-tap-highlight-color:rgba(0,0,0,0);
加完发现没有默认样式的话，加上一下样式：
	-webkit-appearance:radio
### Webkit下的appearance属性值：

	checkbox
	radio
	push-button
	square-button
	button
	button-bevel
	listbox
	listitem
	menulist
	menulist-button
	menulist-text
	menulist-textfield
	scrollbarbutton-up
	scrollbarbutton-down
	scrollbarbutton-left
	scrollbarbutton-right
	scrollbartrack-horizontal
	scrollbartrack-vertical
	scrollbarthumb-horizontal
	scrollbarthumb-vertical
	scrollbargripper-horizontal
	scrollbargripper-vertical
	slider-horizontal
	slider-vertical
	sliderthumb-horizontal
	sliderthumb-vertical
	caret
	searchfield
	searchfield-decoration
	searchfield-results-decoration
	searchfield-results-button
	searchfield-cancel-button
	textfield
	textarea


### Mozilla下的appearance属性值

	none
	button
	checkbox
	checkbox-container
	checkbox-small
	dialog
	listbox
	menuitem
	menulist
	menulist-button
	menulist-textfield
	menupopup
	progressbar
	radio
	radio-container
	radio-small
	resizer
	scrollbar
	scrollbarbutton-down
	scrollbarbutton-left
	scrollbarbutton-right
	scrollbarbutton-up
	scrollbartrack-horizontal
	scrollbartrack-vertical
	separator
	statusbar
	tab
	tab-left-edge Obsolete
	tabpanels
	textfield
	textfield-multiline
	toolbar
	toolbarbutton
	toolbox
	-moz-mac-unified-toolbar
	-moz-win-borderless-glass
	-moz-win-browsertabbar-toolbox
	-moz-win-communications-toolbox
	-moz-win-glass
	-moz-win-media-toolbox
	tooltip
	treeheadercell
	treeheadersortarrow
	treeitem
	treetwisty
	treetwistyopen
	treeview
	window
