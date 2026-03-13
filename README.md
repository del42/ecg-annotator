# ECG · ANNOTATOR

### Multi-Channel Physiological Signal Annotation Tool

*Md Sanzid Bin Hossain, PhD · © 2026*

---

## What Is This?

ECG Annotator is a **single HTML file** that lets you view, annotate, and export labeled physiological signal data. No installation, no server, no dependencies — just open the file in a browser and start annotating.

It also ships as a **native macOS/Windows desktop app** (~5–10MB) for offline use with native Save As dialogs.

It handles ECG (up to 12-lead), ICP, ABP, PPG, and any other signal channel. You can label individual heartbeats, mark time regions with clinical labels, measure intervals, and export everything as clean CSV files ready for machine learning pipelines.

---

## Two Ways to Use It

### Option A: Browser (Recommended for Sharing)

Open `ECG_Annotator.html` in **Chrome** or **Edge**. No installation needed. Works on any computer.

### Option B: Desktop App (Recommended for Daily Use)

Install the `.dmg` (macOS) or `.exe` (Windows) from the `releases/` folder. Benefits:
- Native **Save As** dialog — choose where to save your CSV files
- Runs as a standalone app in the Dock / Taskbar
- ~5–10MB, launches instantly
- Fully offline — no internet required

Both options use the exact same interface and features.

---

## Getting Started

### Step 1: Open the Tool

**Browser:** Open `ECG_Annotator.html` in Chrome or Edge (recommended). Firefox and Safari also work.

**Desktop App:** Double-click the installed app. First launch on macOS: right-click → Open.

### Step 2: Try the Demo

Click **▶ Demo** in the top bar. This loads a synthetic 16-channel dataset (12-lead ECG + ICP + ABP + PPG) so you can explore every feature without needing real data.

### Step 3: Load Your Own Data

1. Click **⬆ Load File** (or press `Ctrl/⌘ + O`)
2. Select your `.npy` signal file
3. Optionally load the `_meta.json` sidecar for channel names and colors
4. Optionally load a previous `_anno.csv` to resume an annotation session

### Step 4: Annotate

- Navigate records with `←` `→` arrow keys
- Click a label button (**Normal**, **PVC**, **PAC**, **Noise/Artifact**) or press `N`, `V`, `A`, `Q`
- Save with `Ctrl/⌘ + S`

---

## Three Annotation Modes

### ⊕ Point Mode (Beat Annotation)

Default mode. Label individual heartbeats.

1. R-peaks are auto-detected when you navigate to a record
2. A diamond marker shows the detected peak
3. Click a label button or press a shortcut key to annotate
4. **Drag** the diamond to correct the peak position
5. **Double-click** a peak to delete it (undoable)
6. **Single-click** a labeled peak to clear its label (undoable)

**Quick labels:**

| Button | Shortcut | Meaning |
|--------|----------|---------|
| Normal | `N` | Normal sinus beat |
| PVC | `V` | Premature Ventricular Complex |
| PAC | `A` | Premature Atrial Complex |
| Noise/Artifact | `Q` | Noise or artifact |

For more labels, click **＋ Ext** for 147 HEEDB labels, or **＋ Custom** for your own.

### ⬛ Region Mode (Rhythm / Morphology Annotation)

Annotate time spans — rhythms, conduction patterns, ST changes.

1. Click **⬛ Region** in the toolbar
2. Click and drag on the ECG to select a time span
3. Choose a label from the modal (147 HEEDB labels, searchable)
4. Drag edges to resize, or body to move

### 📏 Caliper Mode (Measurement)

Measure time intervals — PR, QRS, QT, RR intervals.

1. Click **📏 Caliper** in the toolbar
2. Click first point on the waveform
3. Click second point
4. Shows: **milliseconds**, **samples**, and **BPM**

Press **Esc** to return to Point mode from Region or Caliper.

---

## The Interface

```
┌─────────────────────────────────────────────────────────────┐
│  TOP BAR: Demo, Load/Save buttons, theme toggle, stats      │
├─────────────────────────────────────────────────────────────┤
│  LABEL TOOLBAR: Mode buttons, label buttons, Notes, CONF    │
├─────────────────────────────────────────────────────────────┤
│  R PEAKS BAR: Peak info, channel selector, Re-detect         │
├──────────┬──────────────────────────────────────────────────┤
│          │  ANN LANE: Annotation labels strip                │
│  LEFT    ├──────────────────────────────────────────────────┤
│  PANEL   │                                                   │
│          │  CHANNEL ROWS: ECG waveforms + other signals      │
│ Navigator│  (scrollable if many channels)                    │
│ Display  │                                                   │
│ Settings ├──────────────────────────────────────────────────┤
│ Leads    │  TIME BAR: Absolute time axis                     │
│ Annotns  │                                                   │
└──────────┴──────────────────────────────────────────────────┘
```

### Top Bar

| Element | Purpose |
|---------|---------|
| **▶ Demo** | Load synthetic demo data |
| **⬆ Load File** | Load `.npy` signal file |
| **⬆ Load Meta** | Load `_meta.json` channel config |
| **⬆ Load Anno CSV** | Resume from saved annotations |
| **⬆ Load Regions CSV** | Load saved region annotations |
| **●** | Red unsaved indicator (appears when you have unsaved work) |
| **⬇ Save Anno CSV** | Export beat annotations |
| **⬇ Save Regions CSV** | Export region annotations |
| **⬇ Export JSON** | Export everything as JSON |
| **✕ Clear** | Delete all annotations (undoable) |
| **☀/🌙** | Toggle light/dark theme |

### Label Toolbar

| Element | Purpose |
|---------|---------|
| **REC #** | Current record number |
| **Undo / Redo** | Action history (50 levels deep) |
| **Point / Region / Caliper** | Annotation mode selector |
| **Normal / PVC / PAC / Noise** | Quick beat labels |
| **＋ Ext** | 147 HEEDB extended labels (dropdown) |
| **＋ Custom** | Custom labels (dropdown with add/delete) |
| **✕ C** | Clear current label |
| **unlabeled/confirmed** | Record status |
| **Notes** | Attach clinical notes |
| **CONF ★★★★★** | Confidence rating (1–5) |
| **📊 Stats** | Annotation statistics popover |

### Left Panel

| Section | Purpose |
|---------|---------|
| **Record Navigator** | Prev/next, record number input, jump to unlabeled |
| **Display** | Amplitude and grid density sliders |
| **Window Metadata** | Window/stride settings |
| **Leads** | Show/hide channels (auto-resizes) |
| **Annotations** | List of annotations for current record |
| **Regions** | List of region annotations |

### ANN Lane

Thin strip at the top of channels showing all beat labels. Hover over any badge to see the full name.

---

## Keyboard Shortcuts

### Navigation

| Shortcut | Action |
|----------|--------|
| `←` `→` | Previous / next record |
| `Shift + ←` `Shift + →` | Jump to previous / next unlabeled record |

### Annotation

| Shortcut | Action |
|----------|--------|
| `N` | Normal |
| `V` | PVC |
| `A` | PAC |
| `Q` | Noise/Artifact |
| `C` | Clear label |
| `Esc` | Exit Region/Caliper → Point mode |

### File Operations

| Shortcut | Action |
|----------|--------|
| `Ctrl/⌘ + O` | Load signal file |
| `Ctrl/⌘ + M` | Load metadata |
| `Ctrl/⌘ + L` | Load annotation CSV |
| `Ctrl/⌘ + Shift + L` | Load regions CSV |
| `Ctrl/⌘ + S` | Save annotation CSV |
| `Ctrl/⌘ + Shift + S` | Save regions CSV |
| `Ctrl/⌘ + Z` | Undo |
| `Ctrl/⌘ + Y` | Redo |

---

## File Formats

### Input: Signal File (`.npy`)

3D NumPy array with shape `(records, timesteps, leads)` at 250 Hz.

### Input: Metadata (`_meta.json`)

Optional. Channel names, types, and colors:

```json
{
  "channel_names": ["ECG_I", "ECG_II", "ICP", "ABP", "PPG"],
  "channels": [
    {"name": "ECG_I", "type": "ecg", "color": "#c0392b"},
    {"name": "ICP",   "type": "icp", "color": "#8e44ad"}
  ]
}
```

Channel types: `ecg`, `icp`, `abp`, `ppg`. R-peak detection runs on `ecg` channels only.

### Output: Beat Annotation CSV (`*_anno.csv`)

One row per detected beat, sorted by absolute time. 20 columns:

| Column | Example | Meaning |
|--------|---------|---------|
| `record_idx` | 3 | 1-second segment index (floor of abs time) |
| `beat_idx` | 0 | Beat index within that second (0, 1, 2...) |
| `r_peak_abs_t` | 3.662 | Absolute time from recording start (seconds) |
| `r_peak_abs_sample` | 915 | Absolute sample index |
| `r_peak_detected` | true | Peak was found |
| `r_peak_was_auto` | true | Auto-detected or manually placed |
| `r_peak_corrected` | false | Position manually adjusted |
| `r_peak_amplitude` | 0.843 | Signal value at peak |
| `rr_interval_ms` | 833.2 | Time since previous beat (ms) |
| `heart_rate_bpm` | 72.0 | Instantaneous heart rate |
| `beat_label` | N | Short label code |
| `beat_type` | Normal | Full label name |
| `heedb_code` | | HEEDB code (if from extended labels) |
| `peak_ch` | ECG_II | Detection channel |
| `annotator_reviewed` | true | Human reviewed this beat |
| `note` | | Clinical note |
| `confidence` | 5 | Rating 1–5 |
| `annotator_id` | Sanzid | Who annotated |
| `source_file` | A003.npy | Signal filename |
| `labeled_at` | 2026-03-07T... | ISO timestamp |

### Output: Region Annotation CSV (`*_region_anno.csv`)

One row per region annotation. 11 columns:

| Column | Example | Meaning |
|--------|---------|---------|
| `id` | 1773074099498 | Unique ID |
| `abs_t_start` | 1.648 | Region start (absolute seconds) |
| `abs_t_end` | 3.280 | Region end (absolute seconds) |
| `duration_s` | 1.632 | Duration |
| `code` | NORMAL_SINUS_RHYTHM | HEEDB code |
| `label` | Normal sinus rhythm | Human-readable name |
| `heedb_type` | window | Category: window / beat / region |
| `note` | | Clinical note |
| `confidence` | 5 | Rating 1–5 |
| `annotator_id` | Sanzid | Who annotated |
| `createdAt` | 2026-03-07T... | ISO timestamp |

---

## HEEDB Labels (147)

Accessed via the **＋ Ext** dropdown with search and filter tabs.

| Category | Count | Examples |
|----------|-------|---------|
| **Rhythm** | 46 | Normal Sinus Rhythm, AFib, Sinus Brady/Tachy, VTach, SVT, Paced Rhythms, Bigeminy |
| **Beat** | 14 | PVC, PAC, PSVC, Fusion, Escape beats, Paced Complexes |
| **Region** | 87 | LBBB, RBBB, LVH, ST changes, T-wave inversions, Axis deviations, AV blocks, Infarct patterns |

---

## Custom Labels

Click **＋ Custom** in the toolbar:

- Dropdown shows all your custom labels — click to annotate
- Add new labels with the form at the bottom (name + color picker)
- Delete with the **✕** button next to each label
- Persists across sessions (saved in browser localStorage)

---

## Unsaved Work Protection

- Red **●** dot appears next to Save button when there are unsaved changes
- Closing the tab/app shows a warning dialog
- `Ctrl/⌘ + W` triggers a confirmation dialog
- Desktop app: native Save As dialog lets you choose where to save

---

## Annotation Statistics

Click **📊 Stats** in the toolbar to see:

- Progress bar (records visited / total with percentage)
- Beat label breakdown with colored bar charts and percentages
- Region annotation counts
- Annotator name and totals

---

## Undo / Redo

50-action deep history. Every annotation action is undoable:

| Action | Undoable |
|--------|----------|
| Label a beat (N, V, A, Q, HEEDB, custom) | ✅ |
| Clear a beat label (single-click labeled peak) | ✅ |
| Clear all labels for a record (✕ C button) | ✅ |
| Move a peak (drag) | ✅ |
| Add a peak (click empty zone) | ✅ |
| Delete a peak (double-click) | ✅ |
| Clear all peaks (✕ Clear peak button) | ✅ |
| Add a region annotation | ✅ |
| Delete a region annotation | ✅ |
| Resize / move a region | ✅ |
| Load regions CSV | ✅ |
| Clear all annotations (✕ Clear button) | ✅ |

---

## Channel Auto-Sizing

- **Few channels visible:** they expand to fill the screen
- **Many channels:** fixed heights with vertical scrolling
- **Toggle channels:** remaining ones redistribute automatically
- **Window resize:** channels adapt

---

## Window Metadata (Compact Mode)

For signal files where each record = 1 second:

- **Win** = display window length (default 5s)
- **Str** = stride between records (default 1s)
- Records stitch into a continuous display
- Highlighted zone marks where annotation clicks are active
- `absolute_time = record × stride + time_in_window`

---

## Demo Mode

Click **▶ Demo** for a synthetic 16-channel dataset:

- **12-Lead ECG**: I, II, III, aVR, aVL, aVF, V1–V6 with correct per-lead morphology
- **ICP**: Intracranial pressure with P1/P2/P3 peaks
- **ABP**: Arterial blood pressure with dicrotic notch
- **PPG**: Photoplethysmography with respiratory modulation
- 500 records, auto-detected R-peaks, pre-loaded annotations

---

## Dark Theme

Click **☀ Light** to switch to the green CRT terminal theme. Click again to return to light mode.

---

## Browser Support

| Browser | Status |
|---------|--------|
| Chrome / Edge | ✅ Full support |
| Firefox | ✅ Works |
| Safari | ✅ Works |

---

## Desktop App

The desktop app is built with [Tauri](https://tauri.app), which wraps the HTML in a native window using the system's WebKit engine.

| | Browser | Desktop App |
|---|---|---|
| **File size** | ~240 KB (.html) | ~5–10 MB (.dmg/.exe) |
| **Installation** | None | Double-click installer |
| **Save files** | Downloads to ~/Downloads | Native Save As dialog |
| **Works offline** | Yes (after opening) | Yes |
| **RAM usage** | Shares with browser | ~30–80 MB |
| **Platforms** | Any OS with a browser | macOS, Windows, Linux |

### Building from Source

Prerequisites (one-time): Xcode Command Line Tools, Rust, Node.js.

```bash
cd ecg-tauri-app
npx @tauri-apps/cli@latest build
```

See `BUILD.md` for detailed instructions.

### Updating the App

Replace the HTML and rebuild:

```bash
cp /path/to/new/ECG_Annotator.html ui/index.html
npx @tauri-apps/cli@latest build
```

---
