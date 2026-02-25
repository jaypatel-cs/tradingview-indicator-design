# Custom TradingView Indicator (Pine Script v5) — Design Overview

## Overview
A custom TradingView indicator built in Pine Script v5 for mapping key intraday price levels and generating optional automated trade signals.  
This tool focuses on session-based range analysis, level clustering (“stacking”), and clean chart visualization for real-time decision support.

> **Source code is private** and is not included in this repository.

---

## What It Does
- Tracks session-based and time-based high/low ranges (New York timezone)
- Generates configurable Fibonacci-derived levels from those ranges
- Detects clusters of overlapping/nearby levels (“stacks”) within a user-defined tolerance
- Draws stack zones and optional midline “tradable” levels
- Optionally triggers automated BUY/SELL labels on first touch of the stack midline (with SL/TP visualization)

---

## Key Features

### Session & Time Anchors (NY Time)
- **Asia session** high/low tracking
- **London** time-window high/low range tracking
- **8:30** time-window high/low range tracking
- Daily reset behavior to ensure ranges update correctly each new trading day
- Optional **after 9:30 AM NY** signal filtering

### Fibonacci Level Engine
- User-defined fib level list (comma-separated)
- Level mapping computed both directions (H→L and L→H)
- Levels are collected first, then processed for stacking and drawing

### Level Clustering Engine
- Collects all generated Fibonacci levels across sessions
- Sorts levels by price
- Groups levels within configurable tolerance using transitive clustering
- Filters near-duplicate prices using tick-size epsilon
- Computes stack strength based on unique level count
- Draws visual zones only when strength threshold is met

### Visualization Controls
- Optional drawing toggles for:
  - Individual STDV lines and labels
  - Stack top/bottom zone lines
  - Stack midline
  - Stack center labels
- Supports chart object cleanup to prevent exceeding TradingView limits (lines/labels/boxes)
- Optional right-extension of levels

### Signal + Risk Visualization (Optional)
- Generates BUY/SELL label based on price location relative to stack midline on first touch
- Draws configurable SL/TP lines in points (tick-aware)
- “First-touch only” logic prevents repeated spam signals until the stack changes

---

## Configuration Highlights
- Timezone support (default: America/New_York)
- Stack tolerance (points)
- Minimum strength threshold to show a stack
- Offsets for placing lines/labels cleanly
- Manual session windows for London and 8:30 ranges
- Optional automated signaling with SL/TP plotting

---

## Technical Concepts Used
- Time/session filtering
- Stateful daily/session high-low tracking
- Array-based level collection and sorting
- Clustering/grouping logic with tolerance
- Chart object lifecycle management (create/delete + limits)
- Real-time event conditions (first-touch detection)

## Notes
This repository documents the **design and feature set** only.  
The Pine Script source remains private due to proprietary logic.
