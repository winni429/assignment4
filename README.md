# IDV Assignment 4 - Enhanced Interactive Line Chart

## Project Overview
This project upgrades the original bar chart to an **interactive line chart** using D3.js, based on Data1 (model performance metrics across datasets). It adds multiple interactive features (zooming, panning, legend filtering, point interactions) to improve data exploration.

## Key Upgrades from Original Version
| Feature | Original Bar Chart | Enhanced Line Chart |
|---------|--------------------|----------------------|
| Chart Type | Grouped Bar Chart | Smooth Line Chart (with curve interpolation) |
| Interactions | Metric switch + Hover tooltip | ✅ Metric switch<br>✅ Zoom (mouse wheel) & Pan (drag)<br>✅ Legend click (show/hide models)<br>✅ Data point hover (highlight line + tooltip)<br>✅ Data point click (detail alert) |
| Visual Polish | Basic bars | Smooth curves + Data points + Grid lines |
| Usability | Fixed view | Zoom to focus on details + Reset zoom |

## Data Source
Still using **Data1** from the assignment, including 3 metrics for 9 models across 4 datasets:
- **Metrics**: Std Acc (Standard Accuracy), CRR (Certified Robustness Rate), CRA (Certified Robust Accuracy)
- **Models**: ERM, DA, PGDT, TRADES, MART, RS, IBP, PRL, TandT
- **Datasets**: CIFAR100, CIFAR10, SVHN, MNIST

## How to Use the Interactive Features
### 1. Metric Switching
Click the metric buttons at the top to toggle between:
- `Standard Accuracy`: Default metric, shows base model performance
- `Certified Robustness Rate`: Shows model robustness against attacks
- `Certified Robust Accuracy`: Shows accurate performance under robustness constraints

### 2. Zoom & Pan
- **Zoom**: Roll the mouse wheel up/down to zoom in/out (scale range: 0.5x ~ 10x)
- **Pan**: Click and drag the chart to move (panning is limited to chart boundaries)
- **Reset**: Click `Reset Zoom/Pan` to restore the original view

### 3. Legend Filtering
Click any model name in the legend to:
- Hide the model (legend becomes faded, line/points disappear)
- Show the model again (click the faded legend item to restore)

### 4. Data Point Interactions
- **Hover**: Move the mouse over a data point to:
  - Show a tooltip with model, dataset, and exact metric value
  - Highlight the corresponding model line (thicker + darker color)
  - Enlarge the data point (from 6px to 8px radius)
- **Click**: Click a data point to open a detail alert (contains full data info)

## Technical Implementation Details
### 1. Line Chart Core
- **Smooth Curves**: Used `d3.curveMonotoneX` to create natural, non-crossing curves
- **Data Points**: Added circular markers for each (model, dataset) pair, with hover/click interactions
- **Grid Lines**: Horizontal dashed grid lines (10 intervals) for easier value reading

### 2. Interaction Mechanisms
| Interaction | D3 API Used | Reference |
|-------------|-------------|-----------|
| Zoom/Pan | `d3.zoom()`, `zoom.transform()`, `scaleExtent()` | 摘要1、6 |
| Hover/Click | `.on('mouseover', ...)`, `.on('mouseout', ...)`, `.on('click', ...)` | 摘要1、4、6 |
| Smooth Transitions | `.transition()`, `.duration()`, `.ease(d3.easeCubic)` | 摘要6 |
| Legend Filtering | Data binding + CSS class toggling | 摘要4 |

### 3. Performance Optimization
- **Data Binding Key**: Used `model-dataset` as the key for data points to avoid unnecessary DOM re-creation
- **Transition Duration**: Set to 800ms (easeCubic) for smooth but not slow animations
- **Zoom Limits**: Restricted zoom to 0.5x ~ 10x to prevent extreme views
- **Pan Boundaries**: Locked panning within the chart area to avoid empty views

## Deployment
1. Create a GitHub repo named `IDV-assignment4`
2. Upload `index.html` to the repo root
3. Enable GitHub Pages (Settings → Pages → Source: Main branch)
4. Access the chart at: `https://your-username.github.io/IDV-assignment4`
5. Submit the repo zip to e-dimension (per assignment requirements)

## Compliance with Assignment Requirements
| Requirement | Compliance Status |
|-------------|------------------|
| Use provided Data1 | ✅ Fully used Data1 (no invented values) |
| At least 1 chart | ✅ Enhanced line chart (meets clarity/readability requirements) |
| At least 1 interaction | ✅ 5+ interactions (metric switch, zoom, pan, legend filter, point hover/click) |
| At least 1 transition | ✅ Smooth transitions for line/points (800ms), zoom reset (800ms) |
| Deployment | ✅ GitHub Pages ready |