# OSM-3D-Building-Quality-Assessment

Implementation of a framework that combines comparative metrics and machine learning to evaluate the quality of OpenStreetMap (OSM) 3D building data.

> ⚠️ **Note on loading time**  
> The interactive HTML files embed all building geometries, precomputed error metrics, and interactive layers in a single file.  
> When you open them in a browser for the first time, they may take **some time to load**, especially on machines with limited memory.

At this stage, this repository mainly provides the **interactive result visualisations** (three HTML maps for the study areas).  
If you are interested in the **full source code and processing pipeline**, please feel free to contact the author — the code can be shared upon reasonable request.

---

## 1. Repository contents

The directory `results_html/` contains three ZIP archives. After unzipping, you will obtain three standalone HTML files (the core result visualisations):

- `miyun_eval_multi_metrics.html`
- `ningbo_eval_multi_metrics.html`
- `xicheng_eval_multi_metrics.html`

Each HTML file is a **standalone interactive map** and can be opened directly in a modern web browser (e.g., Chrome, Firefox, Edge).

These three maps correspond to the three study areas used in the paper and allow you to:

- explore per-building error metrics (e.g., height difference, footprint discrepancy, 3D Hausdorff distance)
- compare OSM buildings against authoritative reference data
- inspect spatial patterns of errors via grid-based heat maps
- obtain per-building diagnostic summaries (via tooltips, popups, and an LLM-based helper)

---

## 2. How to open the interactive maps

1. Download or clone this repository.
2. Go to the `results_html/` folder.
3. Unzip each file:
   - `miyun_eval_multi_metrics.html.zip`
   - `ningbo_eval_multi_metrics.html.zip`
   - `xicheng_eval_multi_metrics.html.zip`
4. Open the extracted `.html` file (e.g., `miyun_eval_multi_metrics.html`) in your browser.

**Tips**
- For best performance, use Chrome/Edge and avoid opening multiple large HTML maps simultaneously.
- If the map appears blank at first, wait a few seconds for layers to finish loading.

---

## 3. Interactive map interface (per-building diagnostics)

This section introduces the main components of the interface and their basic functions.

> **Note on figures:**  
> GitHub does not reliably render PDFs inline as images in Markdown.  
> If you want these figures to display directly in the README, please export them as `.png` (or `.jpg`) and update the paths below.

- Interface overview (PDF): [Interactive HTML map interface overview](imageclear/Appendix/all_interface.pdf)
- Tooltip & popup panels (PDF): [Interactive feedback panels](imageclear/Appendix/info_interface.pdf)

### 3.1 Main interface elements

The interactive map contains five main elements:

1. **Zoom controls (upper left corner):**  
   Two buttons allow users to zoom the map view in or out (adjusting the map scale).

2. **Building layer visualization (center):**  
   The central view shows building footprints. Each building is color-coded by the selected error metric, with **green indicating smaller error** and **red indicating larger error**.

3. **Color legend (upper right corner):**  
   A horizontal color bar illustrates the value range for the currently selected metric (low → high error). It updates automatically when switching metrics. If multiple metrics are enabled, multiple color bars may appear in parallel.

4. **Base map selector (lower left, top section):**  
   Allows switching between base maps such as a standard OSM map or satellite imagery. The OSM map provides a clearer schematic view, while satellite imagery helps compare against real-world building outlines.

5. **Metric layer selector (lower left, bottom section):**  
   A checkbox panel to toggle evaluation metric layers. Multiple layers can be active at the same time. For example, you may enable a metric’s **grid heat map** together with its **per-building layer** to quickly locate high-error regions and identify which buildings may need improvement.

### 3.2 Tooltip and popup panels

- **Tooltip (hover):**  
  Hovering over a building triggers an instant tooltip showing the building’s ID and the raw values of all four error metrics for that building.

- **Popup (click):**  
  Clicking a building opens a popup window with:
  - a side-by-side outline comparison (**OSM footprint vs. reference data**)
  - the IoU value
  - a brief error diagnosis  
  The popup also includes an **LLM button** that can generate an automatic summary (Chinese or English) describing the building’s likely issues.

---

## 4. Recommended usage workflow

This section outlines a recommended workflow for using the interface to identify error “hotspots” and diagnose individual building issues.

- Step 1 figure (PDF): [Enable Hausdorff heat map](imageclear/Appendix/view_step1.pdf)
- Step 2 figure (PDF): [Zoom & hover for quick review](imageclear/Appendix/view_step2.pdf)
- Step 3 figure (PDF): [Detailed diagnostics popup](imageclear/Appendix/view_step3_new.pdf)

### Steps 1–2: locate hotspots

Turn on **both**:
- the **Hausdorff grid heatmap layer**, and
- the **building-level Hausdorff layer**

Red/orange grid cells indicate hotspot regions where errors are concentrated.

### Steps 3–5: drill down by zooming and hovering

Zoom into a hotspot area while keeping the Hausdorff building layer visible. Hover over buildings to quickly review their metric values and identify why certain buildings show large errors. This supports a smooth transition from a macro hotspot view to single-building diagnosis.

### Steps 6–7: validate issues with detailed popups (optional LLM summary)

If the hover tooltip does not fully explain the issue, click a building to open its detailed popup. Use it to:
- inspect the outline comparison (OSM vs. reference)
- confirm the IoU value
- read the concise diagnosis to validate the likely problem

Optionally, click the **LLM button** to obtain automatically generated suggestions for how to address the identified issues.

---

## Contact

If you would like access to the full processing pipeline and source code, please contact the author (code can be shared upon reasonable request).
