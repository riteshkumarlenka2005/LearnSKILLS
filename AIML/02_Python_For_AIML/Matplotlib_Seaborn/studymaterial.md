The Complete Matplotlib & Seaborn Mastery Guide
From Zero to Hero - A Professor's Comprehensive Guide
Table of Contents
Introduction & Setup
Matplotlib Fundamentals
Advanced Matplotlib Concepts
Seaborn Introduction & Basics
Advanced Seaborn
Real-World ML Applications
Best Practices & Optimization
Chapter 1: Introduction & Setup
1.1 What is Data Visualization and Why Does it Matter?
The Big Picture
Imagine you have 1 million numbers in a spreadsheet. If I ask you "What's the pattern?", you'd struggle for hours. But one simple graph can reveal the answer in seconds. That's the power of data visualization.

In Machine Learning:

Before Training: Understand your data distribution, spot outliers, find correlations
During Training: Monitor loss curves, track metrics across epochs
After Training: Visualize predictions, confusion matrices, feature importance
Why Matplotlib and Seaborn?
text

Matplotlib = The Engine (Low-level, Full Control)
Seaborn = The Sports Car (High-level, Beautiful by Default)
Matplotlib: Like painting with individual brush strokes - complete freedom but requires effort
Seaborn: Like Instagram filters - beautiful results quickly, built on Matplotlib

1.2 Installation & Environment Setup
Step-by-Step Installation
Bash

# Method 1: Using pip (Recommended for beginners)
pip install matplotlib seaborn numpy pandas

# Method 2: Using conda (Recommended for data scientists)
conda install matplotlib seaborn numpy pandas

# Verify installation
python -c "import matplotlib; print(matplotlib.__version__)"
python -c "import seaborn; print(seaborn.__version__)"
Your First Jupyter Notebook Setup
Python

# Cell 1: Essential Imports (Copy this to every notebook)
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import pandas as pd

# Magic command for Jupyter (makes plots appear inline)
%matplotlib inline

# Optional: For high-resolution plots
%config InlineBackend.figure_format = 'retina'

# Set default style
plt.style.use('default')
sns.set_theme()

print("✓ All libraries loaded successfully!")
Understanding the Imports
Python

# Let's break down each import:

import matplotlib.pyplot as plt
# 'pyplot' is your drawing board
# 'plt' is the short name (convention everyone uses)

import seaborn as sns
# 'seaborn' makes beautiful statistical plots
# 'sns' is the standard abbreviation (named after Samuel Norman Seaborn)

import numpy as np
# 'numpy' handles numerical arrays (your data)
# 'np' is the universal short form

import pandas as pd
# 'pandas' manages structured data (tables/DataFrames)
# 'pd' is the conventional abbreviation
Chapter 2: Matplotlib Fundamentals
2.1 The Anatomy of a Plot - Understanding the Building Blocks
The Hierarchy: Figure and Axes
Think of it like a house:

Figure = The entire house (the container)
Axes = Rooms in the house (where you actually draw)
Axis = The walls of the room (x-axis, y-axis)
Python

# Create your first plot - The Two Essential Lines
fig, ax = plt.subplots()  # This creates EVERYTHING you need

# Let's understand what just happened:
# fig = The entire canvas (Figure object)
# ax = The plotting area (Axes object)
# plt.subplots() = Function that creates both
Visual Breakdown
text

┌─────────────────────────────────────────────┐
│  Figure (fig)                               │
│  ┌───────────────────────────────────────┐  │
│  │ Axes (ax) - This is where you plot   │  │
│  │                                       │  │
│  │      ↑ Y-Axis                        │  │
│  │      │                                │  │
│  │      │     * (data points)           │  │
│  │      │  *                             │  │
│  │      │*                               │  │
│  │      └──────────→ X-Axis             │  │
│  │                                       │  │
│  └───────────────────────────────────────┘  │
│                                             │
└─────────────────────────────────────────────┘
2.2 Your First Plot - Step by Step
Example 1: Simple Line Plot (Crystal Clear Explanation)
Python

# Step 1: Create data
x = [1, 2, 3, 4, 5]  # X-axis values
y = [2, 4, 6, 8, 10]  # Y-axis values (y = 2*x)

# Step 2: Create figure and axes
fig, ax = plt.subplots()

# Step 3: Plot the data
ax.plot(x, y)

# Step 4: Show the plot
plt.show()
What happened?

We created two lists: x and y
fig, ax = plt.subplots() created our canvas and drawing area
ax.plot(x, y) drew a line connecting the points
plt.show() displayed it
Example 2: Making it Beautiful (Adding Details)
Python

# Same data
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

# Create plot
fig, ax = plt.subplots(figsize=(10, 6))  # figsize = (width, height) in inches

# Plot with styling
ax.plot(x, y, 
        color='blue',      # Line color
        linewidth=2,       # Thickness
        marker='o',        # Point markers (circles)
        markersize=8,      # Size of markers
        label='y = 2x')    # Label for legend

# Add labels and title
ax.set_xlabel('X Values', fontsize=12)
ax.set_ylabel('Y Values', fontsize=12)
ax.set_title('My First Beautiful Plot', fontsize=14, fontweight='bold')

# Add grid
ax.grid(True, alpha=0.3)  # alpha = transparency (0=invisible, 1=solid)

# Add legend
ax.legend()

plt.show()
Breaking down the new concepts:

Python

figsize=(10, 6)
# Width=10 inches, Height=6 inches
# Default is (6.4, 4.8)
# Bigger = more detail, but slower to render

marker='o'
# 'o' = circle
# 's' = square
# '^' = triangle
# '*' = star
# '.' = point

alpha=0.3
# Transparency: 0.0 (invisible) to 1.0 (solid)
# 0.3 = subtle, doesn't overpower the data
2.3 The Two Ways to Plot (Critical Concept)
Method 1: Pyplot Interface (plt.plot) - Quick and Easy
Python

# The "MATLAB-style" - Quick for simple plots
plt.plot([1, 2, 3], [1, 4, 9])
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Quick Plot')
plt.show()
When to use: Jupyter notebooks, quick analysis, single plots

Method 2: Object-Oriented Interface (ax.plot) - Professional Way
Python

# The "Professional" way - Full control
fig, ax = plt.subplots()
ax.plot([1, 2, 3], [1, 4, 9])
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_title('Professional Plot')
plt.show()
When to use: Production code, multiple subplots, complex figures

Side-by-Side Comparison
Python

# ❌ Pyplot way - Gets messy with multiple plots
plt.figure()
plt.subplot(1, 2, 1)
plt.plot([1, 2, 3], [1, 4, 9])
plt.subplot(1, 2, 2)
plt.plot([1, 2, 3], [1, 2, 3])
plt.show()

# ✅ OOP way - Clean and clear
fig, axes = plt.subplots(1, 2, figsize=(12, 4))
axes[0].plot([1, 2, 3], [1, 4, 9])
axes[1].plot([1, 2, 3], [1, 2, 3])
plt.show()
Professor's Recommendation:

Always use the Object-Oriented approach (fig, ax) in production code. It's clearer, more maintainable, and scales better.

2.4 Essential Plot Types - The Complete Guide
2.4.1 Line Plots (Time Series, Trends)
Python

# Use case: Stock prices, training loss, temperature over time

# Sample data: Temperature over a week
days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
temperature = [22, 24, 19, 23, 25, 27, 26]

fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(days, temperature, 
        marker='o', 
        linewidth=2, 
        markersize=10,
        color='orangered')

ax.set_xlabel('Day of Week', fontsize=12)
ax.set_ylabel('Temperature (°C)', fontsize=12)
ax.set_title('Weekly Temperature Trend', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)

plt.show()
Multiple Lines on Same Plot:

Python

# Comparing multiple models' performance
epochs = list(range(1, 11))
model1_loss = [0.9, 0.7, 0.5, 0.4, 0.35, 0.3, 0.28, 0.26, 0.25, 0.24]
model2_loss = [0.95, 0.8, 0.65, 0.55, 0.48, 0.42, 0.38, 0.35, 0.33, 0.31]

fig, ax = plt.subplots(figsize=(10, 6))

# Plot multiple lines
ax.plot(epochs, model1_loss, marker='o', label='Model 1 (CNN)', linewidth=2)
ax.plot(epochs, model2_loss, marker='s', label='Model 2 (RNN)', linewidth=2)

ax.set_xlabel('Epoch', fontsize=12)
ax.set_ylabel('Loss', fontsize=12)
ax.set_title('Training Loss Comparison', fontsize=14, fontweight='bold')
ax.legend(loc='upper right')  # Position of legend
ax.grid(True, alpha=0.3)

plt.show()
2.4.2 Scatter Plots (Relationships, Correlations)
Python

# Use case: Feature relationships, clustering visualization

# Sample data: Height vs Weight
np.random.seed(42)
height = np.random.normal(170, 10, 100)  # mean=170cm, std=10, 100 samples
weight = height * 0.8 + np.random.normal(0, 5, 100)  # Correlated with noise

fig, ax = plt.subplots(figsize=(10, 6))

ax.scatter(height, weight, 
           alpha=0.6,        # Transparency to see overlapping points
           s=50,             # Size of points
           c='steelblue',    # Color
           edgecolors='black',  # Border around points
           linewidth=0.5)

ax.set_xlabel('Height (cm)', fontsize=12)
ax.set_ylabel('Weight (kg)', fontsize=12)
ax.set_title('Height vs Weight Relationship', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)

plt.show()
Color-Coded Scatter Plot (3 Variables):

Python

# Visualizing clusters or categories
from sklearn.datasets import make_blobs

# Generate sample data with 3 clusters
X, y = make_blobs(n_samples=300, centers=3, random_state=42)

fig, ax = plt.subplots(figsize=(10, 6))

# Use 'c' parameter to color by category
scatter = ax.scatter(X[:, 0], X[:, 1], 
                     c=y,              # Color by cluster
                     cmap='viridis',   # Color map
                     s=50, 
                     alpha=0.6,
                     edgecolors='black',
                     linewidth=0.5)

# Add colorbar
plt.colorbar(scatter, ax=ax, label='Cluster')

ax.set_xlabel('Feature 1', fontsize=12)
ax.set_ylabel('Feature 2', fontsize=12)
ax.set_title('K-Means Clustering Visualization', fontsize=14, fontweight='bold')

plt.show()
2.4.3 Bar Plots (Categories, Comparisons)
Python

# Use case: Model accuracy comparison, category counts

# Sample data: Model performance
models = ['Logistic\nRegression', 'Random\nForest', 'SVM', 'Neural\nNetwork']
accuracy = [0.82, 0.89, 0.85, 0.91]

fig, ax = plt.subplots(figsize=(10, 6))

bars = ax.bar(models, accuracy, 
              color=['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A'],
              edgecolor='black',
              linewidth=1.5,
              alpha=0.8)

# Add value labels on bars
for bar in bars:
    height = bar.get_height()
    ax.text(bar.get_x() + bar.get_width()/2., height,
            f'{height:.2f}',
            ha='center', va='bottom', fontsize=11, fontweight='bold')

ax.set_ylabel('Accuracy', fontsize=12)
ax.set_title('Model Performance Comparison', fontsize=14, fontweight='bold')
ax.set_ylim(0, 1)  # Accuracy ranges from 0 to 1
ax.grid(axis='y', alpha=0.3)

plt.show()
Grouped Bar Chart:

Python

# Comparing multiple metrics across models
models = ['Model A', 'Model B', 'Model C']
precision = [0.85, 0.88, 0.82]
recall = [0.80, 0.85, 0.87]
f1_score = [0.82, 0.86, 0.84]

x = np.arange(len(models))  # Label locations
width = 0.25  # Width of bars

fig, ax = plt.subplots(figsize=(12, 6))

# Create bars
bars1 = ax.bar(x - width, precision, width, label='Precision', color='#FF6B6B')
bars2 = ax.bar(x, recall, width, label='Recall', color='#4ECDC4')
bars3 = ax.bar(x + width, f1_score, width, label='F1-Score', color='#45B7D1')

ax.set_xlabel('Models', fontsize=12)
ax.set_ylabel('Score', fontsize=12)
ax.set_title('Model Metrics Comparison', fontsize=14, fontweight='bold')
ax.set_xticks(x)
ax.set_xticklabels(models)
ax.legend()
ax.grid(axis='y', alpha=0.3)

plt.tight_layout()
plt.show()
2.4.4 Histograms (Distribution Analysis)
Python

# Use case: Understanding data distribution, checking normality

# Sample data: Test scores
np.random.seed(42)
scores = np.random.normal(75, 15, 1000)  # mean=75, std=15

fig, ax = plt.subplots(figsize=(10, 6))

n, bins, patches = ax.hist(scores, 
                           bins=30,           # Number of bins
                           color='skyblue', 
                           edgecolor='black',
                           alpha=0.7)

# Add mean line
mean_score = scores.mean()
ax.axvline(mean_score, color='red', linestyle='--', linewidth=2, label=f'Mean: {mean_score:.1f}')

ax.set_xlabel('Score', fontsize=12)
ax.set_ylabel('Frequency', fontsize=12)
ax.set_title('Distribution of Test Scores', fontsize=14, fontweight='bold')
ax.legend()
ax.grid(axis='y', alpha=0.3)

plt.show()
Understanding Bins:

Python

# Same data, different bin sizes - See the difference!
fig, axes = plt.subplots(1, 3, figsize=(15, 4))

bin_sizes = [10, 30, 100]
for ax, bins in zip(axes, bin_sizes):
    ax.hist(scores, bins=bins, color='skyblue', edgecolor='black', alpha=0.7)
    ax.set_title(f'Bins = {bins}', fontsize=12, fontweight='bold')
    ax.set_xlabel('Score')
    ax.set_ylabel('Frequency')

plt.tight_layout()
plt.show()
Key Insight:

Too few bins (10): Loses detail, overly smooth
Good bins (30): Shows distribution clearly
Too many bins (100): Noisy, hard to interpret
2.4.5 Box Plots (Statistical Summary)
Python

# Use case: Outlier detection, comparing distributions

# Sample data: Performance across different datasets
np.random.seed(42)
dataset1 = np.random.normal(80, 10, 100)
dataset2 = np.random.normal(75, 15, 100)
dataset3 = np.random.normal(85, 8, 100)

data = [dataset1, dataset2, dataset3]
labels = ['Dataset 1', 'Dataset 2', 'Dataset 3']

fig, ax = plt.subplots(figsize=(10, 6))

bp = ax.boxplot(data, 
                labels=labels,
                patch_artist=True,  # Fill with color
                notch=True,         # Notch for median confidence interval
                showmeans=True)     # Show mean as well

# Color the boxes
colors = ['#FF6B6B', '#4ECDC4', '#45B7D1']
for patch, color in zip(bp['boxes'], colors):
    patch.set_facecolor(color)
    patch.set_alpha(0.7)

ax.set_ylabel('Score', fontsize=12)
ax.set_title('Performance Across Datasets', fontsize=14, fontweight='bold')
ax.grid(axis='y', alpha=0.3)

plt.show()
Understanding Box Plot Components:

text

        ╭─── Maximum (or Q3 + 1.5*IQR)
        │
    ┌───┐
    │   │ ← Q3 (75th percentile)
    ├───┤ ← Median (50th percentile)
    │   │ ← Q1 (25th percentile)
    └───┘
        │
        ╰─── Minimum (or Q1 - 1.5*IQR)
        
    °   ← Outliers (beyond whiskers)
2.5 Customization Deep Dive
2.5.1 Colors - Complete Guide
Python

# Method 1: Named colors
colors_named = ['red', 'blue', 'green', 'orange', 'purple']

# Method 2: Hex codes (like in web design)
colors_hex = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A', '#98D8C8']

# Method 3: RGB tuples (values 0-1)
colors_rgb = [(1, 0, 0), (0, 1, 0), (0, 0, 1)]

# Method 4: Matplotlib color codes
colors_short = ['r', 'g', 'b', 'c', 'm', 'y', 'k']  # red, green, blue, cyan, magenta, yellow, black

# Example: Using different color methods
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Named colors
axes[0, 0].bar(range(5), [1, 2, 3, 4, 5], color=colors_named)
axes[0, 0].set_title('Named Colors', fontweight='bold')

# Hex colors
axes[0, 1].bar(range(5), [1, 2, 3, 4, 5], color=colors_hex)
axes[0, 1].set_title('Hex Colors', fontweight='bold')

# RGB colors
axes[1, 0].bar(range(3), [1, 2, 3], color=colors_rgb)
axes[1, 0].set_title('RGB Colors', fontweight='bold')

# Short codes
axes[1, 1].bar(range(7), [1, 2, 3, 4, 5, 6, 7], color=colors_short)
axes[1, 1].set_title('Short Codes', fontweight='bold')

plt.tight_layout()
plt.show()
Color Maps (Continuous Colors):

Python

# For heatmaps, gradients, etc.
fig, axes = plt.subplots(2, 3, figsize=(15, 8))

cmaps = ['viridis', 'plasma', 'coolwarm', 'RdYlGn', 'Blues', 'rainbow']
data = np.random.rand(10, 10)

for ax, cmap in zip(axes.flat, cmaps):
    im = ax.imshow(data, cmap=cmap)
    ax.set_title(cmap, fontweight='bold')
    plt.colorbar(im, ax=ax)

plt.tight_layout()
plt.show()
Choosing the Right Colormap:

Python

# Sequential: For ordered data (low to high)
# Examples: 'viridis', 'plasma', 'Blues', 'Greens'
# Use for: Heatmaps, intensity maps

# Diverging: For data with a meaningful center
# Examples: 'coolwarm', 'RdBu', 'RdYlGn'
# Use for: Correlation matrices, anomaly detection

# Qualitative: For categories (no order)
# Examples: 'tab10', 'Set3', 'Paired'
# Use for: Different classes, clusters
2.5.2 Line Styles and Markers
Python

# Complete reference
fig, ax = plt.subplots(figsize=(12, 6))

x = np.linspace(0, 10, 20)

# Line styles
styles = ['-', '--', '-.', ':']
labels_line = ['Solid', 'Dashed', 'Dash-dot', 'Dotted']

for i, (style, label) in enumerate(zip(styles, labels_line)):
    ax.plot(x, np.sin(x) + i*0.5, linestyle=style, linewidth=2, label=label)

ax.legend(loc='upper right')
ax.set_title('Line Styles', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)
plt.show()

# Markers
fig, ax = plt.subplots(figsize=(12, 6))

markers = ['o', 's', '^', 'D', '*', 'p', 'h', 'v', '<', '>']
labels_marker = ['Circle', 'Square', 'Triangle Up', 'Diamond', 'Star', 
                 'Pentagon', 'Hexagon', 'Triangle Down', 'Triangle Left', 'Triangle Right']

for i, (marker, label) in enumerate(zip(markers, labels_marker)):
    ax.plot(i, 0, marker=marker, markersize=15, label=label)

ax.set_xlim(-1, 10)
ax.set_ylim(-1, 1)
ax.legend(loc='upper center', ncol=5)
ax.set_title('Marker Styles', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)
plt.show()
2.5.3 Text and Annotations
Python

# Adding text to highlight important points
np.random.seed(42)
x = np.linspace(0, 10, 100)
y = np.sin(x) + np.random.normal(0, 0.1, 100)

fig, ax = plt.subplots(figsize=(12, 6))
ax.plot(x, y, linewidth=2, color='steelblue')

# Add simple text
ax.text(5, 0.5, 'Peak Region', fontsize=12, color='red', fontweight='bold')

# Add annotation with arrow
max_idx = np.argmax(y)
ax.annotate('Maximum Point', 
            xy=(x[max_idx], y[max_idx]),      # Point to annotate
            xytext=(x[max_idx]+1, y[max_idx]+0.3),  # Location of text
            fontsize=12,
            color='red',
            fontweight='bold',
            arrowprops=dict(facecolor='red', shrink=0.05, width=2))

# Add annotation for minimum
min_idx = np.argmin(y)
ax.annotate('Minimum Point', 
            xy=(x[min_idx], y[min_idx]),
            xytext=(x[min_idx]+1, y[min_idx]-0.3),
            fontsize=12,
            color='green',
            fontweight='bold',
            arrowprops=dict(facecolor='green', shrink=0.05, width=2))

ax.set_title('Annotations Example', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)
plt.show()
2.5.4 Legends - Complete Control
Python

fig, ax = plt.subplots(figsize=(12, 6))

x = np.linspace(0, 10, 100)
ax.plot(x, np.sin(x), label='sin(x)', linewidth=2)
ax.plot(x, np.cos(x), label='cos(x)', linewidth=2)
ax.plot(x, np.sin(x) * np.cos(x), label='sin(x)*cos(x)', linewidth=2)

# Legend positions:
# 'upper right', 'upper left', 'lower right', 'lower left', 'center'
# 'upper center', 'lower center', 'center left', 'center right', 'best'

ax.legend(loc='upper right',           # Position
          fontsize=12,                 # Font size
          frameon=True,                # Box around legend
          shadow=True,                 # Shadow effect
          fancybox=True,               # Rounded corners
          ncol=1,                      # Number of columns
          title='Functions',           # Legend title
          title_fontsize=14)

ax.set_title('Legend Customization', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)
plt.show()
2.5.5 Grids and Spines
Python

fig, axes = plt.subplots(2, 2, figsize=(14, 10))

x = np.linspace(0, 10, 100)
y = np.sin(x)

# Default
axes[0, 0].plot(x, y)
axes[0, 0].set_title('Default', fontweight='bold')

# Grid only
axes[0, 1].plot(x, y)
axes[0, 1].grid(True, alpha=0.5, linestyle='--', linewidth=0.7)
axes[0, 1].set_title('With Grid', fontweight='bold')

# Remove top and right spines
axes[1, 0].plot(x, y)
axes[1, 0].spines['top'].set_visible(False)
axes[1, 0].spines['right'].set_visible(False)
axes[1, 0].set_title('Clean Spines', fontweight='bold')

# Custom spines position
axes[1, 1].plot(x, y)
axes[1, 1].spines['left'].set_position('zero')
axes[1, 1].spines['bottom'].set_position('zero')
axes[1, 1].spines['top'].set_visible(False)
axes[1, 1].spines['right'].set_visible(False)
axes[1, 1].set_title('Centered Spines', fontweight='bold')

plt.tight_layout()
plt.show()
2.6 Subplots - The Complete Guide
2.6.1 Basic Subplots
Python

# Creating multiple plots in one figure

# Method 1: Simple grid
fig, axes = plt.subplots(2, 2, figsize=(12, 10))
# This creates a 2x2 grid (4 plots total)
# axes is now a 2D array: axes[row, col]

x = np.linspace(0, 10, 100)

# Access each subplot
axes[0, 0].plot(x, np.sin(x))
axes[0, 0].set_title('sin(x)')

axes[0, 1].plot(x, np.cos(x))
axes[0, 1].set_title('cos(x)')

axes[1, 0].plot(x, np.tan(x))
axes[1, 0].set_title('tan(x)')
axes[1, 0].set_ylim(-5, 5)

axes[1, 1].plot(x, x**2)
axes[1, 1].set_title('x²')

plt.tight_layout()  # Prevents overlap
plt.show()
2.6.2 Advanced Subplot Layouts
Python

# Method 2: Using subplot2grid for flexible layouts
fig = plt.figure(figsize=(12, 8))

# Create subplots with different sizes
ax1 = plt.subplot2grid((3, 3), (0, 0), colspan=3)  # Top row, spans all 3 columns
ax2 = plt.subplot2grid((3, 3), (1, 0), colspan=2)  # Middle left, spans 2 columns
ax3 = plt.subplot2grid((3, 3), (1, 2), rowspan=2)  # Right side, spans 2 rows
ax4 = plt.subplot2grid((3, 3), (2, 0))             # Bottom left
ax5 = plt.subplot2grid((3, 3), (2, 1))             # Bottom center

x = np.linspace(0, 10, 100)

ax1.plot(x, np.sin(x))
ax1.set_title('Main Plot - Full Width')

ax2.plot(x, np.cos(x))
ax2.set_title('Wide Plot')

ax3.plot(x, x**2)
ax3.set_title('Tall Plot')

ax4.scatter(x, np.random.rand(100))
ax4.set_title('Small 1')

ax5.scatter(x, np.random.rand(100))
ax5.set_title('Small 2')

plt.tight_layout()
plt.show()
2.6.3 GridSpec (Maximum Control)
Python

from matplotlib.gridspec import GridSpec

fig = plt.figure(figsize=(12, 8))
gs = GridSpec(3, 3, figure=fig, hspace=0.3, wspace=0.3)

# Create subplots using GridSpec
ax1 = fig.add_subplot(gs[0, :])    # First row, all columns
ax2 = fig.add_subplot(gs[1, :-1])  # Second row, first two columns
ax3 = fig.add_subplot(gs[1:, -1])  # Last column, last two rows
ax4 = fig.add_subplot(gs[-1, 0])   # Last row, first column
ax5 = fig.add_subplot(gs[-1, -2])  # Last row, second to last column

x = np.linspace(0, 10, 100)

ax1.plot(x, np.sin(x), 'b-', linewidth=2)
ax1.set_title('Top Panel')
ax1.grid(True, alpha=0.3)

ax2.plot(x, np.cos(x), 'r-', linewidth=2)
ax2.set_title('Middle Left Panel')
ax2.grid(True, alpha=0.3)

ax3.plot(x, np.tan(x), 'g-', linewidth=2)
ax3.set_title('Right Panel')
ax3.set_ylim(-5, 5)
ax3.grid(True, alpha=0.3)

ax4.scatter(x, np.random.rand(100), c='purple', alpha=0.5)
ax4.set_title('Bottom Left')

ax5.scatter(x, np.random.rand(100), c='orange', alpha=0.5)
ax5.set_title('Bottom Center')

plt.show()
Understanding GridSpec Parameters:

Python

# hspace: Vertical spacing between subplots (0 to 1)
# wspace: Horizontal spacing between subplots (0 to 1)

# Example: Different spacing
fig = plt.figure(figsize=(12, 4))

# No spacing
gs1 = GridSpec(2, 2, figure=fig, left=0.05, right=0.35, hspace=0, wspace=0)
for i in range(4):
    ax = fig.add_subplot(gs1[i])
    ax.text(0.5, 0.5, 'No Space', ha='center', va='center', fontsize=12)
    ax.set_xticks([])
    ax.set_yticks([])

# Medium spacing
gs2 = GridSpec(2, 2, figure=fig, left=0.4, right=0.7, hspace=0.3, wspace=0.3)
for i in range(4):
    ax = fig.add_subplot(gs2[i])
    ax.text(0.5, 0.5, 'Medium Space', ha='center', va='center', fontsize=12)
    ax.set_xticks([])
    ax.set_yticks([])

# Large spacing
gs3 = GridSpec(2, 2, figure=fig, left=0.75, right=1.0, hspace=0.6, wspace=0.6)
for i in range(4):
    ax = fig.add_subplot(gs3[i])
    ax.text(0.5, 0.5, 'Large Space', ha='center', va='center', fontsize=12)
    ax.set_xticks([])
    ax.set_yticks([])

plt.show()
2.6.4 Sharing Axes (Common Use Case)
Python

# When comparing similar data, share axes for easier comparison
fig, axes = plt.subplots(2, 2, figsize=(12, 10), 
                         sharex=True,   # All subplots share same x-axis
                         sharey=True)   # All subplots share same y-axis

x = np.linspace(0, 10, 100)

# Plot same x range with different functions
axes[0, 0].plot(x, np.sin(x))
axes[0, 0].set_title('sin(x)')

axes[0, 1].plot(x, np.sin(2*x))
axes[0, 1].set_title('sin(2x)')

axes[1, 0].plot(x, np.sin(3*x))
axes[1, 0].set_title('sin(3x)')

axes[1, 1].plot(x, np.sin(4*x))
axes[1, 1].set_title('sin(4x)')

# Labels only on outer subplots (because of sharing)
fig.text(0.5, 0.04, 'X Axis (shared)', ha='center', fontsize=12)
fig.text(0.04, 0.5, 'Y Axis (shared)', va='center', rotation='vertical', fontsize=12)

plt.tight_layout()
plt.show()
2.7 Figure Size and DPI (Quality Control)
Understanding Figure Size
Python

# figsize=(width, height) in INCHES
# DPI = Dots Per Inch (resolution)

# Low resolution (fast, small file, screen viewing)
fig, ax = plt.subplots(figsize=(8, 6), dpi=72)
ax.plot([1, 2, 3], [1, 4, 9])
ax.set_title('Low DPI (72) - Fast but pixelated when zoomed')
plt.savefig('low_res.png', dpi=72)
plt.show()

# Standard resolution (balanced)
fig, ax = plt.subplots(figsize=(8, 6), dpi=100)
ax.plot([1, 2, 3], [1, 4, 9])
ax.set_title('Standard DPI (100) - Good for most uses')
plt.savefig('standard_res.png', dpi=100)
plt.show()

# High resolution (slow, large file, publication quality)
fig, ax = plt.subplots(figsize=(8, 6), dpi=300)
ax.plot([1, 2, 3], [1, 4, 9])
ax.set_title('High DPI (300) - Publication quality')
plt.savefig('high_res.png', dpi=300)
plt.show()
DPI Guidelines:

72-100 DPI: Screen viewing, Jupyter notebooks, quick analysis
150 DPI: PowerPoint presentations, web display
300 DPI: Publications, journals, print
600 DPI: High-quality prints, posters
Saving Figures
Python

fig, ax = plt.subplots(figsize=(10, 6))
ax.plot([1, 2, 3], [1, 4, 9])

# Different formats
plt.savefig('my_plot.png', dpi=300)           # PNG: Raster, good for most uses
plt.savefig('my_plot.pdf', dpi=300)           # PDF: Vector, perfect for publications
plt.savefig('my_plot.svg')                     # SVG: Vector, editable in Illustrator
plt.savefig('my_plot.jpg', dpi=300, quality=95)  # JPEG: Smaller file, slight quality loss

# With transparent background
plt.savefig('my_plot.png', dpi=300, transparent=True)

# With tight bounding box (removes white space)
plt.savefig('my_plot.png', dpi=300, bbox_inches='tight')

# High quality for publication
plt.savefig('my_plot.png', dpi=300, bbox_inches='tight', 
            facecolor='white', edgecolor='none')

plt.show()
2.8 Styling - Making Professional Plots
2.8.1 Built-in Styles
Python

# See all available styles
print(plt.style.available)
# Output: ['Solarize_Light2', 'bmh', 'classic', 'dark_background', 'fast', 
#          'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn', ...]

# Using a style
plt.style.use('seaborn-v0_8-darkgrid')  # Use specific style

x = np.linspace(0, 10, 100)
fig, ax = plt.subplots(figsize=(10, 6))
ax.plot(x, np.sin(x), label='sin(x)')
ax.plot(x, np.cos(x), label='cos(x)')
ax.legend()
ax.set_title('Seaborn Style Example')
plt.show()

# Reset to default
plt.style.use('default')
2.8.2 Comparing Styles
Python

styles = ['default', 'seaborn-v0_8-darkgrid', 'ggplot', 'fivethirtyeight', 
          'bmh', 'dark_background']

fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.flatten()

x = np.linspace(0, 10, 100)

for ax, style in zip(axes, styles):
    with plt.style.context(style):  # Temporarily use style
        ax.plot(x, np.sin(x), label='sin(x)', linewidth=2)
        ax.plot(x, np.cos(x), label='cos(x)', linewidth=2)
        ax.set_title(style, fontsize=12, fontweight='bold')
        ax.legend()
        ax.grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
2.8.3 Custom Styling (rcParams)
Python

# Customize matplotlib globally
from matplotlib import rcParams

# Save default settings to restore later
default_params = rcParams.copy()

# Custom settings
rcParams['figure.figsize'] = (12, 6)
rcParams['font.size'] = 12
rcParams['font.family'] = 'serif'
rcParams['font.serif'] = ['Times New Roman']
rcParams['axes.labelsize'] = 14
rcParams['axes.titlesize'] = 16
rcParams['axes.titleweight'] = 'bold'
rcParams['xtick.labelsize'] = 12
rcParams['ytick.labelsize'] = 12
rcParams['legend.fontsize'] = 12
rcParams['lines.linewidth'] = 2
rcParams['lines.markersize'] = 8
rcParams['axes.grid'] = True
rcParams['grid.alpha'] = 0.3

# Now all plots will use these settings
x = np.linspace(0, 10, 100)
fig, ax = plt.subplots()
ax.plot(x, np.sin(x), label='sin(x)')
ax.plot(x, np.cos(x), label='cos(x)')
ax.set_xlabel('X axis')
ax.set_ylabel('Y axis')
ax.set_title('Custom Styled Plot')
ax.legend()
plt.show()

# Restore defaults
rcParams.update(default_params)
2.8.4 Context Managers for Temporary Styling
Python

# Temporarily change settings for one plot only
x = np.linspace(0, 10, 100)

# Normal plot
fig, ax = plt.subplots(figsize=(10, 4))
ax.plot(x, np.sin(x))
ax.set_title('Normal Style')
plt.show()

# Temporarily styled plot
with plt.rc_context({'axes.facecolor': 'lightgray', 
                     'axes.edgecolor': 'blue',
                     'axes.linewidth': 3,
                     'grid.color': 'white',
                     'grid.linewidth': 1.5}):
    fig, ax = plt.subplots(figsize=(10, 4))
    ax.plot(x, np.sin(x), color='darkblue', linewidth=3)
    ax.set_title('Temporarily Styled')
    ax.grid(True)
    plt.show()

# Back to normal
fig, ax = plt.subplots(figsize=(10, 4))
ax.plot(x, np.sin(x))
ax.set_title('Back to Normal')
plt.show()
Chapter 3: Advanced Matplotlib Concepts
3.1 3D Plots
3.1.1 Basic 3D Scatter Plot
Python

from mpl_toolkits.mplot3d import Axes3D

# Generate sample 3D data
np.random.seed(42)
n = 200
x = np.random.standard_normal(n)
y = np.random.standard_normal(n)
z = x**2 + y**2 + np.random.standard_normal(n)*0.1

# Create 3D plot
fig = plt.figure(figsize=(12, 8))
ax = fig.add_subplot(111, projection='3d')

# Scatter plot with color gradient
scatter = ax.scatter(x, y, z, c=z, cmap='viridis', s=50, alpha=0.6, edgecolors='black')

ax.set_xlabel('X Axis', fontsize=12)
ax.set_ylabel('Y Axis', fontsize=12)
ax.set_zlabel('Z Axis', fontsize=12)
ax.set_title('3D Scatter Plot', fontsize=14, fontweight='bold')

# Add colorbar
plt.colorbar(scatter, ax=ax, label='Z value', shrink=0.5)

plt.show()
3.1.2 3D Surface Plot
Python

# Create mesh grid
x = np.linspace(-5, 5, 50)
y = np.linspace(-5, 5, 50)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

# Create 3D surface
fig = plt.figure(figsize=(14, 6))

# Surface plot with color map
ax1 = fig.add_subplot(121, projection='3d')
surf = ax1.plot_surface(X, Y, Z, cmap='coolwarm', alpha=0.8, edgecolor='none')
ax1.set_title('Surface Plot', fontsize=14, fontweight='bold')
ax1.set_xlabel('X')
ax1.set_ylabel('Y')
ax1.set_zlabel('Z')
fig.colorbar(surf, ax=ax1, shrink=0.5)

# Wireframe plot
ax2 = fig.add_subplot(122, projection='3d')
ax2.plot_wireframe(X, Y, Z, color='blue', linewidth=0.5)
ax2.set_title('Wireframe Plot', fontsize=14, fontweight='bold')
ax2.set_xlabel('X')
ax2.set_ylabel('Y')
ax2.set_zlabel('Z')

plt.tight_layout()
plt.show()
3.1.3 3D Line Plot (Trajectory)
Python

# Parametric 3D line (spiral)
t = np.linspace(0, 10*np.pi, 1000)
x = np.sin(t)
y = np.cos(t)
z = t

fig = plt.figure(figsize=(12, 8))
ax = fig.add_subplot(111, projection='3d')

# Color the line by height
colors = plt.cm.viridis(z / z.max())
ax.plot(x, y, z, linewidth=2)
ax.scatter(x, y, z, c=z, cmap='viridis', s=10)

ax.set_xlabel('X', fontsize=12)
ax.set_ylabel('Y', fontsize=12)
ax.set_zlabel('Z (time)', fontsize=12)
ax.set_title('3D Trajectory (Spiral)', fontsize=14, fontweight='bold')

# Set viewing angle
ax.view_init(elev=20, azim=45)

plt.show()
3.2 Heatmaps and 2D Histograms
3.2.1 Heatmap (Correlation Matrix)
Python

# Generate sample correlation data
np.random.seed(42)
data = np.random.randn(5, 5)
corr_matrix = np.corrcoef(data)

fig, ax = plt.subplots(figsize=(10, 8))

# Create heatmap
im = ax.imshow(corr_matrix, cmap='RdBu_r', vmin=-1, vmax=1, aspect='auto')

# Add labels
labels = ['Var 1', 'Var 2', 'Var 3', 'Var 4', 'Var 5']
ax.set_xticks(np.arange(len(labels)))
ax.set_yticks(np.arange(len(labels)))
ax.set_xticklabels(labels)
ax.set_yticklabels(labels)

# Rotate x labels
plt.setp(ax.get_xticklabels(), rotation=45, ha="right", rotation_mode="anchor")

# Add correlation values as text
for i in range(len(labels)):
    for j in range(len(labels)):
        text = ax.text(j, i, f'{corr_matrix[i, j]:.2f}',
                       ha="center", va="center", color="black", fontweight='bold')

ax.set_title('Correlation Heatmap', fontsize=14, fontweight='bold')
plt.colorbar(im, ax=ax, label='Correlation')
plt.tight_layout()
plt.show()
3.2.2 2D Histogram (Density Plot)
Python

# Generate correlated 2D data
np.random.seed(42)
x = np.random.normal(0, 1, 10000)
y = x + np.random.normal(0, 0.5, 10000)

fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Regular scatter (too dense to see patterns)
axes[0].scatter(x, y, alpha=0.1, s=1)
axes[0].set_title('Scatter Plot (Hard to See Density)', fontsize=12, fontweight='bold')
axes[0].set_xlabel('X')
axes[0].set_ylabel('Y')

# 2D histogram (shows density clearly)
h = axes[1].hist2d(x, y, bins=50, cmap='YlOrRd')
axes[1].set_title('2D Histogram (Clear Density)', fontsize=12, fontweight='bold')
axes[1].set_xlabel('X')
axes[1].set_ylabel('Y')
plt.colorbar(h[3], ax=axes[1], label='Count')

plt.tight_layout()
plt.show()
3.2.3 Hexbin Plot (Alternative to 2D Histogram)
Python

fig, ax = plt.subplots(figsize=(10, 8))

# Hexbin plot
hexbin = ax.hexbin(x, y, gridsize=30, cmap='Blues', mincnt=1)

ax.set_xlabel('X', fontsize=12)
ax.set_ylabel('Y', fontsize=12)
ax.set_title('Hexbin Plot (Cleaner than 2D Histogram)', fontsize=14, fontweight='bold')
plt.colorbar(hexbin, ax=ax, label='Count')

plt.show()
3.3 Contour Plots
Python

# Generate 2D function
x = np.linspace(-3, 3, 100)
y = np.linspace(-3, 3, 100)
X, Y = np.meshgrid(x, y)
Z = np.sin(X) * np.cos(Y)

fig, axes = plt.subplots(1, 3, figsize=(18, 5))

# Filled contour
contourf = axes[0].contourf(X, Y, Z, levels=20, cmap='RdYlBu_r')
axes[0].set_title('Filled Contour', fontsize=12, fontweight='bold')
plt.colorbar(contourf, ax=axes[0])

# Line contour
contour = axes[1].contour(X, Y, Z, levels=20, colors='black', linewidths=1)
axes[1].clabel(contour, inline=True, fontsize=8)  # Add labels
axes[1].set_title('Line Contour with Labels', fontsize=12, fontweight='bold')

# Combined
axes[2].contourf(X, Y, Z, levels=20, cmap='RdYlBu_r', alpha=0.7)
contour = axes[2].contour(X, Y, Z, levels=20, colors='black', linewidths=0.5, alpha=0.5)
axes[2].set_title('Combined', fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()
3.4 Error Bars and Confidence Intervals
3.4.1 Basic Error Bars
Python

# Sample data with uncertainty
x = np.arange(1, 11)
y = x**2
y_error = x * 2  # Error increases with x

fig, axes = plt.subplots(1, 2, figsize=(14, 5))

# Vertical error bars
axes[0].errorbar(x, y, yerr=y_error, 
                 fmt='o-',           # Format: circle markers with lines
                 linewidth=2,
                 markersize=8,
                 capsize=5,          # Size of error bar caps
                 capthick=2,
                 label='Data with error')

axes[0].set_xlabel('X', fontsize=12)
axes[0].set_ylabel('Y', fontsize=12)
axes[0].set_title('Vertical Error Bars', fontsize=14, fontweight='bold')
axes[0].legend()
axes[0].grid(True, alpha=0.3)

# Both vertical and horizontal error bars
x_error = np.random.rand(10) * 0.5
axes[1].errorbar(x, y, xerr=x_error, yerr=y_error,
                 fmt='s-',
                 linewidth=2,
                 markersize=8,
                 capsize=5,
                 capthick=2,
                 label='Data with X and Y error')

axes[1].set_xlabel('X', fontsize=12)
axes[1].set_ylabel('Y', fontsize=12)
axes[1].set_title('Horizontal and Vertical Error Bars', fontsize=14, fontweight='bold')
axes[1].legend()
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
3.4.2 Confidence Intervals (Shaded Regions)
Python

# Generate data with confidence interval
x = np.linspace(0, 10, 100)
y = np.sin(x)
confidence = 0.3

# Upper and lower bounds
y_upper = y + confidence
y_lower = y - confidence

fig, ax = plt.subplots(figsize=(12, 6))

# Plot mean line
ax.plot(x, y, 'b-', linewidth=2, label='Mean')

# Fill confidence interval
ax.fill_between(x, y_lower, y_upper, alpha=0.3, label='95% CI')

ax.set_xlabel('X', fontsize=12)
ax.set_ylabel('Y', fontsize=12)
ax.set_title('Confidence Interval Visualization', fontsize=14, fontweight='bold')
ax.legend()
ax.grid(True, alpha=0.3)

plt.show()
3.5 Polar Plots
Python

# Polar coordinate system (good for cyclical data)
theta = np.linspace(0, 2*np.pi, 100)
r = 1 + np.sin(5*theta)

fig, axes = plt.subplots(1, 2, figsize=(14, 6), subplot_kw=dict(projection='polar'))

# Line polar plot
axes[0].plot(theta, r, linewidth=2)
axes[0].set_title('Polar Line Plot', fontsize=14, fontweight='bold', pad=20)
axes[0].grid(True)

# Area polar plot
axes[1].fill(theta, r, alpha=0.5, color='orange')
axes[1].plot(theta, r, linewidth=2, color='red')
axes[1].set_title('Polar Area Plot', fontsize=14, fontweight='bold', pad=20)
axes[1].grid(True)

plt.tight_layout()
plt.show()
Polar Bar Chart (Rose Plot)
Python

# Use case: Wind direction frequency, cyclical patterns
categories = 8
angles = np.linspace(0, 2*np.pi, categories, endpoint=False).tolist()
values = [15, 20, 35, 30, 25, 40, 30, 20]

# Close the plot
angles += angles[:1]
values += values[:1]

fig, ax = plt.subplots(figsize=(8, 8), subplot_kw=dict(projection='polar'))

ax.bar(angles[:-1], values[:-1], width=2*np.pi/categories, 
       alpha=0.7, edgecolor='black', linewidth=2)

ax.set_theta_zero_location('N')  # Set 0 degrees to North
ax.set_theta_direction(-1)  # Clockwise
ax.set_title('Wind Rose Plot', fontsize=14, fontweight='bold', pad=20)

plt.show()
3.6 Animations
Python

from matplotlib.animation import FuncAnimation

# Create animated sine wave
fig, ax = plt.subplots(figsize=(10, 6))

x = np.linspace(0, 2*np.pi, 100)
line, = ax.plot(x, np.sin(x), linewidth=2)

ax.set_xlim(0, 2*np.pi)
ax.set_ylim(-1.5, 1.5)
ax.set_xlabel('X', fontsize=12)
ax.set_ylabel('Y', fontsize=12)
ax.set_title('Animated Sine Wave', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)

def animate(frame):
    line.set_ydata(np.sin(x + frame/10))  # Update data
    return line,

# Create animation
anim = FuncAnimation(fig, animate, frames=100, interval=50, blit=True)

# To save animation (requires ffmpeg):
# anim.save('sine_wave.gif', writer='pillow', fps=20)

plt.show()
Live Updating Plot (Simulating Real-Time Data)
Python

# Simulating sensor data stream
fig, ax = plt.subplots(figsize=(12, 6))

xdata, ydata = [], []
line, = ax.plot([], [], 'r-', linewidth=2)

ax.set_xlim(0, 100)
ax.set_ylim(-1, 1)
ax.set_xlabel('Time', fontsize=12)
ax.set_ylabel('Sensor Value', fontsize=12)
ax.set_title('Live Sensor Data', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)

def init():
    line.set_data([], [])
    return line,

def animate(frame):
    xdata.append(frame)
    ydata.append(np.sin(frame/10) + np.random.normal(0, 0.1))
    
    # Keep only last 100 points
    if len(xdata) > 100:
        xdata.pop(0)
        ydata.pop(0)
        ax.set_xlim(xdata[0], xdata[-1])
    
    line.set_data(xdata, ydata)
    return line,

anim = FuncAnimation(fig, animate, init_func=init, frames=200, 
                     interval=50, blit=True)

plt.show()
3.7 Inset Plots (Plot within Plot)
Python

# Main plot with zoomed inset
fig, ax = plt.subplots(figsize=(12, 8))

x = np.linspace(0, 10, 1000)
y = np.sin(x) + np.random.normal(0, 0.1, 1000)

ax.plot(x, y, linewidth=1, alpha=0.7)
ax.set_xlabel('X', fontsize=12)
ax.set_ylabel('Y', fontsize=12)
ax.set_title('Main Plot with Inset Zoom', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)

# Create inset axes
# [x, y, width, height] in figure coordinates (0 to 1)
axins = ax.inset_axes([0.5, 0.5, 0.45, 0.45])

# Plot zoomed region
zoom_region = (x > 4) & (x < 6)
axins.plot(x[zoom_region], y[zoom_region], linewidth=2, color='red')
axins.set_xlim(4, 6)
axins.set_ylim(-0.5, 0.5)
axins.grid(True, alpha=0.3)

# Indicate zoomed region on main plot
ax.indicate_inset_zoom(axins, edgecolor='red', linewidth=2)

plt.show()
3.8 Multiple Y-Axes (Twin Axes)
Python

# Use case: Plotting variables with different scales
x = np.linspace(0, 10, 100)
y1 = np.sin(x)          # Scale: -1 to 1
y2 = np.exp(x/3)        # Scale: 1 to 30

fig, ax1 = plt.subplots(figsize=(12, 6))

# First y-axis
color = 'tab:blue'
ax1.set_xlabel('X', fontsize=12)
ax1.set_ylabel('sin(x)', color=color, fontsize=12)
ax1.plot(x, y1, color=color, linewidth=2, label='sin(x)')
ax1.tick_params(axis='y', labelcolor=color)
ax1.grid(True, alpha=0.3)

# Create second y-axis
ax2 = ax1.twinx()
color = 'tab:red'
ax2.set_ylabel('exp(x/3)', color=color, fontsize=12)
ax2.plot(x, y2, color=color, linewidth=2, label='exp(x/3)')
ax2.tick_params(axis='y', labelcolor=color)

# Title
ax1.set_title('Multiple Y-Axes Example', fontsize=14, fontweight='bold')

# Combine legends
lines1, labels1 = ax1.get_legend_handles_labels()
lines2, labels2 = ax2.get_legend_handles_labels()
ax1.legend(lines1 + lines2, labels1 + labels2, loc='upper left')

plt.tight_layout()
plt.show()
3.9 Broken Axis (Discontinuous Axis)
Python

# Use case: Data with outliers or two distinct ranges
from matplotlib.patches import Rectangle

# Data with outlier
x = [1, 2, 3, 4, 5, 6]
y = [10, 12, 15, 13, 14, 100]  # Last point is an outlier

fig, (ax1, ax2) = plt.subplots(2, 1, figsize=(10, 8), sharex=True)

# Plot on both axes
ax1.plot(x, y, 'o-', linewidth=2, markersize=8)
ax2.plot(x, y, 'o-', linewidth=2, markersize=8)

# Set limits to "break" the axis
ax1.set_ylim(80, 110)  # Upper range (outlier)
ax2.set_ylim(0, 20)    # Lower range (normal data)

# Hide spines between axes
ax1.spines['bottom'].set_visible(False)
ax2.spines['top'].set_visible(False)
ax1.xaxis.tick_top()
ax1.tick_params(labeltop=False)
ax2.xaxis.tick_bottom()

# Add break marks
d = 0.015  # Size of diagonal lines
kwargs = dict(transform=ax1.transAxes, color='k', clip_on=False)
ax1.plot((-d, +d), (-d, +d), **kwargs)
ax1.plot((1 - d, 1 + d), (-d, +d), **kwargs)

kwargs.update(transform=ax2.transAxes)
ax2.plot((-d, +d), (1 - d, 1 + d), **kwargs)
ax2.plot((1 - d, 1 + d), (1 - d, 1 + d), **kwargs)

ax2.set_xlabel('X', fontsize=12)
fig.text(0.04, 0.5, 'Y', va='center', rotation='vertical', fontsize=12)
ax1.set_title('Broken Axis for Outlier', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
3.10 Logarithmic Scales
Python

# Exponential data
x = np.linspace(0, 10, 100)
y = np.exp(x)

fig, axes = plt.subplots(2, 2, figsize=(14, 10))

# Linear scale (hard to see early values)
axes[0, 0].plot(x, y, linewidth=2)
axes[0, 0].set_title('Linear Scale (Hard to see small values)', fontweight='bold')
axes[0, 0].grid(True, alpha=0.3)

# Log scale Y
axes[0, 1].semilogy(x, y, linewidth=2)
axes[0, 1].set_title('Log Y Scale (Shows all values clearly)', fontweight='bold')
axes[0, 1].grid(True, alpha=0.3)

# Log scale X
axes[1, 0].semilogx(x + 1, y, linewidth=2)  # +1 to avoid log(0)
axes[1, 0].set_title('Log X Scale', fontweight='bold')
axes[1, 0].grid(True, alpha=0.3)

# Log-log scale
axes[1, 1].loglog(x + 1, y, linewidth=2)
axes[1, 1].set_title('Log-Log Scale', fontweight='bold')
axes[1, 1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
When to use logarithmic scales:

semilogy (log Y): Data spans many orders of magnitude (e.g., 1 to 10000)
semilogx (log X): Time series over long periods
loglog: Power law relationships (y = x^n becomes linear)
Chapter 4: Seaborn Introduction & Basics
4.1 What is Seaborn? Why Use It?
Key Differences from Matplotlib
Python

# Matplotlib: You control everything (more code)
fig, ax = plt.subplots(figsize=(10, 6))
ax.scatter(x, y)
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_title('Title')
ax.grid(True)

# Seaborn: Beautiful by default (less code)
sns.scatterplot(x=x, y=y)
plt.title('Title')
Seaborn's Superpowers:

Beautiful defaults: Professional-looking plots out of the box
Statistical plots: Built-in statistical visualizations
Themes: Consistent styling across plots
DataFrames: Works seamlessly with pandas
Color palettes: Sophisticated color schemes
Basic Setup
Python

import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# Set default theme
sns.set_theme()  # This makes ALL plots (even matplotlib) look better!

# Optional: Set specific style
sns.set_style("whitegrid")  # Options: white, dark, whitegrid, darkgrid, ticks
4.2 Seaborn Themes and Color Palettes
4.2.1 Built-in Styles
Python

# Compare all styles
styles = ['white', 'dark', 'whitegrid', 'darkgrid', 'ticks']

fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.flatten()

for ax, style in zip(axes, styles):
    sns.set_style(style)
    x = np.linspace(0, 10, 100)
    ax.plot(x, np.sin(x), linewidth=2)
    ax.set_title(f'Style: {style}', fontsize=14, fontweight='bold')
    ax.set_xlabel('X')
    ax.set_ylabel('sin(x)')

# Hide extra subplot
axes[-1].axis('off')

plt.tight_layout()
plt.show()

# Reset to default
sns.set_style('whitegrid')
4.2.2 Color Palettes
Python

# Seaborn has sophisticated color palettes
palettes = ['deep', 'muted', 'bright', 'pastel', 'dark', 'colorblind']

fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.flatten()

x = np.arange(6)
y = np.random.randint(10, 50, 6)

for ax, palette in zip(axes, palettes):
    sns.barplot(x=x, y=y, palette=palette, ax=ax)
    ax.set_title(f'Palette: {palette}', fontsize=14, fontweight='bold')
    ax.set_ylabel('Value')

plt.tight_layout()
plt.show()
Viewing Color Palette:

Python

# See the actual colors in a palette
fig, axes = plt.subplots(3, 2, figsize=(12, 8))
axes = axes.flatten()

palettes = ['deep', 'muted', 'bright', 'pastel', 'dark', 'colorblind']

for ax, palette in zip(axes, palettes):
    colors = sns.color_palette(palette)
    sns.palplot(colors, ax=ax)
    ax.set_title(palette, fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()
4.2.3 Custom Color Palettes
Python

# Create custom palette
custom_palette = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A', '#98D8C8', '#F7DC6F']

# Set as default
sns.set_palette(custom_palette)

# Example usage
x = ['A', 'B', 'C', 'D', 'E', 'F']
y = [10, 25, 15, 30, 20, 35]

plt.figure(figsize=(10, 6))
sns.barplot(x=x, y=y)
plt.title('Custom Color Palette', fontsize=14, fontweight='bold')
plt.show()

# Reset to default
sns.set_palette('deep')
4.3 Working with DataFrames (Seaborn's Strength)
4.3.1 Sample Dataset
Python

# Load built-in dataset
tips = sns.load_dataset('tips')
print(tips.head())

# Output:
#    total_bill   tip     sex smoker  day    time  size
# 0       16.99  1.01  Female     No  Sun  Dinner     2
# 1       10.34  1.66    Male     No  Sun  Dinner     3
# 2       21.01  3.50    Male     No  Sun  Dinner     3
# 3       23.68  3.31    Male     No  Sun  Dinner     2
# 4       24.59  3.61  Female     No  Sun  Dinner     4

print(tips.info())
# This shows data types and non-null counts
4.3.2 Basic Plots with DataFrames
Python

# Scatter plot with DataFrame
plt.figure(figsize=(10, 6))
sns.scatterplot(data=tips, x='total_bill', y='tip', hue='time', style='sex', s=100)
plt.title('Tips vs Total Bill', fontsize=14, fontweight='bold')
plt.show()

# Understanding parameters:
# data=tips : Use this DataFrame
# x='total_bill' : Column name for x-axis
# y='tip' : Column name for y-axis
# hue='time' : Color by this column (Lunch vs Dinner)
# style='sex' : Different markers for Male vs Female
# s=100 : Size of points
4.4 Essential Seaborn Plot Types
4.4.1 Scatter Plots (scatterplot)
Python

fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Basic scatter
sns.scatterplot(data=tips, x='total_bill', y='tip', ax=axes[0])
axes[0].set_title('Basic Scatter Plot', fontsize=14, fontweight='bold')

# Advanced scatter with multiple dimensions
sns.scatterplot(data=tips, x='total_bill', y='tip', 
                hue='day',        # Color by day
                size='size',      # Size by party size
                style='time',     # Marker style by time
                alpha=0.7,
                ax=axes[1])
axes[1].set_title('Multi-Dimensional Scatter Plot', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
4.4.2 Line Plots (lineplot)
Python

# Load time series data
flights = sns.load_dataset('flights')
print(flights.head())

# Output:
#    year month  passengers
# 0  1949   Jan         112
# 1  1949   Feb         118
# 2  1949   Mar         132

# Aggregate by year
yearly_passengers = flights.groupby('year')['passengers'].sum().reset_index()

plt.figure(figsize=(12, 6))
sns.lineplot(data=yearly_passengers, x='year', y='passengers', marker='o', linewidth=2)
plt.title('Yearly Passengers', fontsize=14, fontweight='bold')
plt.xlabel('Year', fontsize=12)
plt.ylabel('Total Passengers', fontsize=12)
plt.grid(True, alpha=0.3)
plt.show()
Line plot with confidence intervals:

Python

# Multiple observations per x value
plt.figure(figsize=(12, 6))
sns.lineplot(data=flights, x='month', y='passengers', 
             ci=95,  # 95% confidence interval (shaded area)
             marker='o', linewidth=2)
plt.title('Monthly Passengers (with 95% CI)', fontsize=14, fontweight='bold')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
4.4.3 Bar Plots (barplot)
Python

# Seaborn automatically calculates mean and confidence interval!
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Basic bar plot (shows mean tip by day)
sns.barplot(data=tips, x='day', y='tip', ax=axes[0])
axes[0].set_title('Average Tip by Day (with CI)', fontsize=14, fontweight='bold')

# Grouped bar plot
sns.barplot(data=tips, x='day', y='tip', hue='sex', ax=axes[1])
axes[1].set_title('Average Tip by Day and Gender', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
Key Insight:

Seaborn's barplot automatically computes the mean and shows error bars (confidence intervals). In Matplotlib, you'd have to calculate these manually!

4.4.4 Count Plots (countplot)
Python

# Shows count of observations in each category
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Simple count
sns.countplot(data=tips, x='day', ax=axes[0])
axes[0].set_title('Count of Tips by Day', fontsize=14, fontweight='bold')

# Stacked count (hue creates sub-groups)
sns.countplot(data=tips, x='day', hue='time', ax=axes[1])
axes[1].set_title('Count of Tips by Day and Time', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
4.4.5 Box Plots (boxplot)
Python

fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Basic box plot
sns.boxplot(data=tips, x='day', y='total_bill', ax=axes[0])
axes[0].set_title('Total Bill Distribution by Day', fontsize=14, fontweight='bold')

# Grouped box plot
sns.boxplot(data=tips, x='day', y='total_bill', hue='smoker', ax=axes[1])
axes[1].set_title('Total Bill by Day and Smoking Status', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
4.4.6 Violin Plots (violinplot)
Python

# Combines box plot with KDE (Kernel Density Estimation)
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Basic violin plot
sns.violinplot(data=tips, x='day', y='total_bill', ax=axes[0])
axes[0].set_title('Violin Plot (Shows Distribution)', fontsize=14, fontweight='bold')

# Split violin plot (easier comparison)
sns.violinplot(data=tips, x='day', y='total_bill', hue='sex', split=True, ax=axes[1])
axes[1].set_title('Split Violin Plot (Male vs Female)', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
When to use Violin vs Box plot:

Box plot: Quick statistical summary (median, quartiles, outliers)
Violin plot: Full distribution shape (can see bimodal distributions)
4.4.7 Strip Plots and Swarm Plots
Python

fig, axes = plt.subplots(1, 3, figsize=(18, 6))

# Strip plot (can have overlapping points)
sns.stripplot(data=tips, x='day', y='tip', ax=axes[0])
axes[0].set_title('Strip Plot (Points may overlap)', fontsize=12, fontweight='bold')

# Strip plot with jitter
sns.stripplot(data=tips, x='day', y='tip', jitter=True, alpha=0.5, ax=axes[1])
axes[1].set_title('Strip Plot with Jitter', fontsize=12, fontweight='bold')

# Swarm plot (no overlap, but slower)
sns.swarmplot(data=tips, x='day', y='tip', ax=axes[2])
axes[2].set_title('Swarm Plot (No overlap)', fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()
4.4.8 Combining Plots (Power Technique!)
Python

# Violin + Swarm = Best of both worlds!
plt.figure(figsize=(12, 6))

sns.violinplot(data=tips, x='day', y='total_bill', inner=None, color='lightgray')
sns.swarmplot(data=tips, x='day', y='total_bill', size=3, color='black', alpha=0.5)

plt.title('Violin + Swarm Plot (Distribution + Individual Points)', 
          fontsize=14, fontweight='bold')
plt.show()
4.5 Distribution Plots
4.5.1 Histograms (histplot)
Python

fig, axes = plt.subplots(2, 2, figsize=(14, 10))

# Basic histogram
sns.histplot(data=tips, x='total_bill', bins=20, ax=axes[0, 0])
axes[0, 0].set_title('Basic Histogram', fontweight='bold')

# With KDE (smoothed curve)
sns.histplot(data=tips, x='total_bill', kde=True, bins=20, ax=axes[0, 1])
axes[0, 1].set_title('Histogram + KDE', fontweight='bold')

# Multiple distributions
sns.histplot(data=tips, x='total_bill', hue='time', bins=20, ax=axes[1, 0])
axes[1, 0].set_title('Multiple Distributions', fontweight='bold')

# Stacked
sns.histplot(data=tips, x='total_bill', hue='time', multiple='stack', bins=20, ax=axes[1, 1])
axes[1, 1].set_title('Stacked Histogram', fontweight='bold')

plt.tight_layout()
plt.show()
4.5.2 KDE Plots (kdeplot)
Python

# Kernel Density Estimation - smooth distribution
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# 1D KDE
sns.kdeplot(data=tips, x='total_bill', fill=True, ax=axes[0])
axes[0].set_title('1D KDE Plot', fontsize=14, fontweight='bold')

# Multiple KDEs
sns.kdeplot(data=tips, x='total_bill', hue='time', fill=True, alpha=0.5, ax=axes[1])
axes[1].set_title('Multiple KDE Plots', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
4.5.3 2D KDE (Bivariate Distribution)
Python

fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# 2D KDE with contours
sns.kdeplot(data=tips, x='total_bill', y='tip', ax=axes[0])
axes[0].set_title('2D KDE (Contours)', fontsize=14, fontweight='bold')

# 2D KDE filled
sns.kdeplot(data=tips, x='total_bill', y='tip', fill=True, cmap='viridis', ax=axes[1])
axes[1].set_title('2D KDE (Filled)', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
4.5.4 Distribution Plot (displot) - FacetGrid Wrapper
Python

# displot creates a figure-level plot (with multiple subplots)
sns.displot(data=tips, x='total_bill', hue='time', kind='hist', 
            kde=True, height=6, aspect=1.5)
plt.title('Distribution Plot with FacetGrid', fontsize=14, fontweight='bold', y=1.02)
plt.show()

# With multiple rows/columns
sns.displot(data=tips, x='total_bill', col='time', row='sex', 
            kind='kde', fill=True, height=4, aspect=1.2)
plt.show()
4.6 Categorical Plots
4.6.1 Categorical Plot (catplot) - Unified Interface
Python

# catplot is a figure-level function that can create various categorical plots

# Bar plot
sns.catplot(data=tips, x='day', y='tip', kind='bar', height=6, aspect=1.5)
plt.title('Bar Plot via catplot', fontsize=14, fontweight='bold', y=1.02)
plt.show()

# Box plot
sns.catplot(data=tips, x='day', y='tip', kind='box', height=6, aspect=1.5)
plt.title('Box Plot via catplot', fontsize=14, fontweight='bold', y=1.02)
plt.show()

# Violin plot
sns.catplot(data=tips, x='day', y='tip', kind='violin', height=6, aspect=1.5)
plt.title('Violin Plot via catplot', fontsize=14, fontweight='bold', y=1.02)
plt.show()
4.6.2 Point Plots (pointplot)
Python

# Shows point estimate and confidence interval
plt.figure(figsize=(12, 6))
sns.pointplot(data=tips, x='day', y='tip', hue='sex')
plt.title('Point Plot (Shows Mean with CI)', fontsize=14, fontweight='bold')
plt.show()
4.7 Regression Plots
4.7.1 Linear Regression Plot (regplot)
Python

fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Basic regression plot
sns.regplot(data=tips, x='total_bill', y='tip', ax=axes[0])
axes[0].set_title('Linear Regression Plot', fontsize=14, fontweight='bold')

# With scatter customization
sns.regplot(data=tips, x='total_bill', y='tip', 
            scatter_kws={'alpha': 0.5, 's': 50}, 
            line_kws={'color': 'red', 'linewidth': 2},
            ax=axes[1])
axes[1].set_title('Customized Regression Plot', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
4.7.2 Regression Plot with Categories (lmplot)
Python

# lmplot is figure-level, creates subplots automatically
sns.lmplot(data=tips, x='total_bill', y='tip', hue='smoker', height=6, aspect=1.5)
plt.title('Regression by Smoking Status', fontsize=14, fontweight='bold', y=1.02)
plt.show()

# Separate plots for each category
sns.lmplot(data=tips, x='total_bill', y='tip', col='time', row='sex', height=4)
plt.show()
4.7.3 Residual Plot (residplot)
Python

# Check if linear regression is appropriate
plt.figure(figsize=(12, 6))
sns.residplot(data=tips, x='total_bill', y='tip', lowess=True)
plt.title('Residual Plot (Check Regression Assumptions)', fontsize=14, fontweight='bold')
plt.axhline(0, color='red', linestyle='--', linewidth=2)
plt.show()

# If points randomly scattered around 0: Good linear fit
# If pattern exists: Linear regression may not be appropriate
4.8 Matrix Plots
4.8.1 Heatmap (heatmap)
Python

# Correlation matrix
numeric_tips = tips.select_dtypes(include=[np.number])
corr = numeric_tips.corr()

plt.figure(figsize=(10, 8))
sns.heatmap(corr, 
            annot=True,        # Show numbers in cells
            fmt='.2f',         # Format: 2 decimal places
            cmap='coolwarm',   # Color map
            center=0,          # Center colormap at 0
            square=True,       # Square cells
            linewidths=1,      # Lines between cells
            cbar_kws={'label': 'Correlation'})
plt.title('Correlation Heatmap', fontsize=14, fontweight='bold')
plt.show()
4.8.2 Cluster Map (clustermap)
Python

# Hierarchical clustering of rows and columns
flights_pivot = flights.pivot(index='month', columns='year', values='passengers')

sns.clustermap(flights_pivot, 
               cmap='YlGnBu', 
               figsize=(12, 10),
               annot=True,
               fmt='d',
               linewidths=0.5)
plt.title('Clustered Heatmap', fontsize=14, fontweight='bold', y=1.02)
plt.show()
4.9 Pair Plots (Powerful for ML)
4.9.1 Basic Pair Plot
Python

# Load iris dataset
iris = sns.load_dataset('iris')

# Creates scatter plots for all pairs of variables
sns.pairplot(iris, hue='species', height=2.5)
plt.show()

# This single line of code creates 16 plots!
# Diagonal: Distribution of each variable
# Off-diagonal: Scatter plots of all pairs
Understanding the output:

Diagonal: Shows distribution of each feature
Off-diagonal: Shows relationship between feature pairs
hue='species': Colors points by species
4.9.2 Customized Pair Plot
Python

# Custom diagonal and off-diagonal plots
sns.pairplot(iris, hue='species', 
             diag_kind='kde',      # KDE on diagonal instead of histogram
             markers=['o', 's', 'D'],  # Different markers for each species
             palette='Set2',
             height=2.5)
plt.show()
4.10 Joint Plots (Bivariate + Distributions)
Python

# Combines scatter plot with marginal distributions
fig = sns.jointplot(data=tips, x='total_bill', y='tip', kind='scatter', height=8)
plt.show()

# Different kinds
kinds = ['scatter', 'kde', 'hist', 'hex', 'reg', 'resid']

for kind in kinds:
    sns.jointplot(data=tips, x='total_bill', y='tip', kind=kind, height=6)
    plt.suptitle(f'Joint Plot: {kind}', fontsize=14, fontweight='bold', y=1.02)
    plt.show()
Joint plot kinds:

scatter: Classic scatter with marginal histograms
kde: 2D KDE with marginal KDEs
hist: 2D histogram
hex: Hexbin plot
reg: Regression plot
resid: Residual plot
Chapter 5: Advanced Seaborn
5.1 FacetGrid - Complete Control
5.1.1 Understanding FacetGrid
Python

# FacetGrid creates multiple subplots based on data structure
g = sns.FacetGrid(tips, col='time', row='sex', height=4, aspect=1.2)
g.map(sns.scatterplot, 'total_bill', 'tip')
g.add_legend()
plt.show()

# Breakdown:
# col='time': Create columns for Lunch and Dinner
# row='sex': Create rows for Male and Female
# g.map(): Apply function to each subplot
5.1.2 Advanced FacetGrid
Python

# Custom function in FacetGrid
def custom_plot(x, y, **kwargs):
    ax = plt.gca()
    ax.scatter(x, y, **kwargs)
    ax.axhline(y.mean(), color='red', linestyle='--', linewidth=2)
    ax.text(0.05, 0.95, f'Mean: {y.mean():.2f}', 
            transform=ax.transAxes, fontsize=12, va='top')

g = sns.FacetGrid(tips, col='day', col_wrap=2, height=4, aspect=1.2)
g.map(custom_plot, 'total_bill', 'tip', alpha=0.6)
plt.show()
5.1.3 FacetGrid with Different Plot Types
Python

# Combine multiple plot types
g = sns.FacetGrid(tips, col='time', hue='sex', height=6, aspect=1.2)
g.map(sns.scatterplot, 'total_bill', 'tip', alpha=0.6, s=100)
g.map(sns.regplot, 'total_bill', 'tip', scatter=False, color='black')
g.add_legend()
plt.show()
5.2 PairGrid - Customized Pair Plots
Python

# Complete control over pair plot
g = sns.PairGrid(iris, hue='species', height=2.5)
g.map_upper(sns.scatterplot, s=50, alpha=0.6)  # Upper triangle: scatter
g.map_lower(sns.kdeplot, fill=True, alpha=0.5)  # Lower triangle: KDE
g.map_diag(sns.histplot, kde=True)  # Diagonal: histogram + KDE
g.add_legend()
plt.show()
Understanding the structure:

text

     Var1  Var2  Var3
Var1 [D]   [U]   [U]
Var2 [L]   [D]   [U]
Var3 [L]   [L]   [D]

D = Diagonal
U = Upper triangle
L = Lower triangle
5.3 JointGrid - Customized Joint Plots
Python

# Full control over joint plot
g = sns.JointGrid(data=tips, x='total_bill', y='tip', height=8)
g.plot_joint(sns.scatterplot, s=100, alpha=0.6)
g.plot_marginals(sns.histplot, kde=True, bins=20)
plt.show()

# Different combinations
g = sns.JointGrid(data=tips, x='total_bill', y='tip', height=8)
g.plot_joint(sns.kdeplot, fill=True, cmap='Blues')
g.plot_marginals(sns.kdeplot, fill=True, alpha=0.5)
plt.show()
5.4 Custom Color Palettes (Advanced)
5.4.1 Sequential Palettes
Python

# For ordered data (low to high)
fig, axes = plt.subplots(3, 3, figsize=(15, 12))
axes = axes.flatten()

# Different sequential palettes
palettes = ['Blues', 'Greens', 'Reds', 'Purples', 'Oranges', 
            'YlOrRd', 'YlGnBu', 'RdPu', 'BuPu']

for ax, pal in zip(axes, palettes):
    colors = sns.color_palette(pal, 8)
    sns.barplot(x=list(range(8)), y=[1]*8, palette=colors, ax=ax)
    ax.set_title(pal, fontsize=12, fontweight='bold')
    ax.set_ylim(0, 1.2)

plt.tight_layout()
plt.show()
5.4.2 Diverging Palettes
Python

# For data with meaningful center (e.g., -1 to +1)
fig, axes = plt.subplots(2, 3, figsize=(15, 8))
axes = axes.flatten()

palettes = ['RdBu', 'RdYlGn', 'Spectral', 'coolwarm', 'BrBG', 'PiYG']

for ax, pal in zip(axes, palettes):
    colors = sns.color_palette(pal, 11)
    sns.barplot(x=list(range(11)), y=[1]*11, palette=colors, ax=ax)
    ax.set_title(pal, fontsize=12, fontweight='bold')
    ax.set_ylim(0, 1.2)

plt.tight_layout()
plt.show()
5.4.3 Creating Custom Gradient
Python

# Create custom sequential palette
custom_palette = sns.light_palette('seagreen', as_cmap=True)

# Use in heatmap
data = np.random.rand(10, 10)
plt.figure(figsize=(10, 8))
sns.heatmap(data, cmap=custom_palette, annot=True, fmt='.2f')
plt.title('Custom Sequential Palette', fontsize=14, fontweight='bold')
plt.show()

# Create custom diverging palette
custom_div = sns.diverging_palette(250, 10, as_cmap=True)

data = np.random.randn(10, 10)
plt.figure(figsize=(10, 8))
sns.heatmap(data, cmap=custom_div, center=0, annot=True, fmt='.2f')
plt.title('Custom Diverging Palette', fontsize=14, fontweight='bold')
plt.show()
5.5 Combining Seaborn with Matplotlib
5.5.1 Mixing Both Libraries
Python

# Use Seaborn's beauty with Matplotlib's control
fig, axes = plt.subplots(2, 2, figsize=(14, 10))

# Seaborn plot
sns.scatterplot(data=tips, x='total_bill', y='tip', hue='time', ax=axes[0, 0])
axes[0, 0].set_title('Seaborn Scatter', fontweight='bold')

# Add matplotlib annotations
max_tip_idx = tips['tip'].idxmax()
max_tip_row = tips.loc[max_tip_idx]
axes[0, 0].annotate('Highest Tip', 
                     xy=(max_tip_row['total_bill'], max_tip_row['tip']),
                     xytext=(40, 9),
                     arrowprops=dict(facecolor='red', shrink=0.05),
                     fontsize=12, fontweight='bold')

# Seaborn + matplotlib lines
sns.violinplot(data=tips, x='day', y='total_bill', ax=axes[0, 1])
axes[0, 1].axhline(tips['total_bill'].mean(), color='red', linestyle='--', linewidth=2, label='Mean')
axes[0, 1].set_title('Violin + Mean Line', fontweight='bold')
axes[0, 1].legend()

# Seaborn distribution + matplotlib customization
sns.histplot(data=tips, x='total_bill', kde=True, ax=axes[1, 0])
axes[1, 0].axvline(tips['total_bill'].median(), color='green', linestyle='--', linewidth=2, label='Median')
axes[1, 0].set_title('Histogram + Median', fontweight='bold')
axes[1, 0].legend()

# Complex combination
sns.boxplot(data=tips, x='day', y='tip', ax=axes[1, 1])
sns.swarmplot(data=tips, x='day', y='tip', color='black', alpha=0.3, size=3, ax=axes[1, 1])
axes[1, 1].set_title('Box + Swarm', fontweight='bold')

plt.tight_layout()
plt.show()
5.5.2 Subplots with Mixed Plots
Python

# Complex dashboard
fig = plt.figure(figsize=(16, 10))
gs = fig.add_gridspec(3, 3, hspace=0.3, wspace=0.3)

# Large scatter plot
ax1 = fig.add_subplot(gs[0:2, 0:2])
sns.scatterplot(data=tips, x='total_bill', y='tip', hue='time', style='sex', s=100, ax=ax1)
ax1.set_title('Main: Bill vs Tip', fontsize=14, fontweight='bold')

# Distribution of total_bill
ax2 = fig.add_subplot(gs[0, 2])
sns.histplot(data=tips, y='total_bill', kde=True, ax=ax2)
ax2.set_title('Bill Distribution', fontsize=12, fontweight='bold')

# Distribution of tip
ax3 = fig.add_subplot(gs[1, 2])
sns.histplot(data=tips, y='tip', kde=True, color='orange', ax=ax3)
ax3.set_title('Tip Distribution', fontsize=12, fontweight='bold')

# Box plots
ax4 = fig.add_subplot(gs[2, 0])
sns.boxplot(data=tips, x='day', y='total_bill', ax=ax4)
ax4.set_title('Bill by Day', fontsize=12, fontweight='bold')
ax4.tick_params(axis='x', rotation=45)

# Violin plot
ax5 = fig.add_subplot(gs[2, 1])
sns.violinplot(data=tips, x='day', y='tip', ax=ax5)
ax5.set_title('Tip by Day', fontsize=12, fontweight='bold')
ax5.tick_params(axis='x', rotation=45)

# Count plot
ax6 = fig.add_subplot(gs[2, 2])
sns.countplot(data=tips, x='day', hue='time', ax=ax6)
ax6.set_title('Counts by Day', fontsize=12, fontweight='bold')
ax6.tick_params(axis='x', rotation=45)

plt.show()
5.6 Statistical Annotations
5.6.1 Adding Statistical Test Results
Python

from scipy import stats

# T-test between groups
lunch_tips = tips[tips['time'] == 'Lunch']['tip']
dinner_tips = tips[tips['time'] == 'Dinner']['tip']

t_stat, p_value = stats.ttest_ind(lunch_tips, dinner_tips)

# Visualize with annotation
fig, ax = plt.subplots(figsize=(10, 6))
sns.boxplot(data=tips, x='time', y='tip', ax=ax)

# Add statistical annotation
y_max = tips['tip'].max()
ax.plot([0, 1], [y_max + 0.5, y_max + 0.5], 'k-', linewidth=2)
ax.text(0.5, y_max + 0.7, f'p = {p_value:.4f}', ha='center', fontsize=12, fontweight='bold')

ax.set_title('Tips by Time (with T-test)', fontsize=14, fontweight='bold')
plt.show()
5.6.2 Correlation Coefficient Annotation
Python

# Calculate correlation
corr_coef, p_val = stats.pearsonr(tips['total_bill'], tips['tip'])

# Plot with annotation
fig, ax = plt.subplots(figsize=(10, 6))
sns.regplot(data=tips, x='total_bill', y='tip', ax=ax)

# Add correlation text
ax.text(0.05, 0.95, f'r = {corr_coef:.3f}\np < 0.001', 
        transform=ax.transAxes, fontsize=14, fontweight='bold',
        verticalalignment='top',
        bbox=dict(boxstyle='round', facecolor='wheat', alpha=0.5))

ax.set_title('Bill vs Tip (with Correlation)', fontsize=14, fontweight='bold')
plt.show()
Chapter 6: Real-World ML Applications
6.1 Exploratory Data Analysis (EDA) Workflow
6.1.1 Complete EDA Pipeline
Python

# Load real ML dataset
from sklearn.datasets import load_boston
import pandas as pd

# Load data
boston = load_boston()
df = pd.DataFrame(boston.data, columns=boston.feature_names)
df['PRICE'] = boston.target

print(df.head())
print(df.info())
print(df.describe())

# Step 1: Check for missing values
plt.figure(figsize=(10, 6))
sns.heatmap(df.isnull(), cbar=False, cmap='viridis')
plt.title('Missing Values Heatmap', fontsize=14, fontweight='bold')
plt.show()

# Step 2: Distribution of target variable
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

sns.histplot(df['PRICE'], kde=True, bins=30, ax=axes[0])
axes[0].set_title('Price Distribution', fontsize=12, fontweight='bold')

stats.probplot(df['PRICE'], plot=axes[1])
axes[1].set_title('Q-Q Plot (Check Normality)', fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()

# Step 3: Correlation analysis
plt.figure(figsize=(12, 10))
corr = df.corr()
sns.heatmap(corr, annot=True, fmt='.2f', cmap='coolwarm', center=0, 
            square=True, linewidths=1)
plt.title('Feature Correlation Matrix', fontsize=14, fontweight='bold')
plt.show()

# Step 4: Identify highly correlated features with target
target_corr = corr['PRICE'].sort_values(ascending=False)
print("Features most correlated with PRICE:")
print(target_corr)

# Step 5: Visualize top correlations
top_features = target_corr[1:6].index.tolist()  # Top 5 (excluding PRICE itself)

fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.flatten()

for i, feature in enumerate(top_features):
    sns.scatterplot(data=df, x=feature, y='PRICE', alpha=0.5, ax=axes[i])
    sns.regplot(data=df, x=feature, y='PRICE', scatter=False, color='red', ax=axes[i])
    
    # Add correlation coefficient
    corr_val = df[[feature, 'PRICE']].corr().iloc[0, 1]
    axes[i].text(0.05, 0.95, f'r = {corr_val:.3f}', 
                 transform=axes[i].transAxes, fontsize=12, fontweight='bold',
                 verticalalignment='top')
    
    axes[i].set_title(f'{feature} vs PRICE', fontsize=12, fontweight='bold')

axes[-1].axis('off')  # Hide last subplot
plt.tight_layout()
plt.show()

# Step 6: Pair plot of top features
sns.pairplot(df[top_features + ['PRICE']], diag_kind='kde', height=2.5)
plt.show()
6.2 Classification Visualization
6.2.1 Decision Boundaries
Python

from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.svm import SVC

# Generate 2D classification data
X, y = make_classification(n_samples=200, n_features=2, n_redundant=0,
                          n_informative=2, n_clusters_per_class=1,
                          random_state=42)

# Train models
lr = LogisticRegression()
dt = DecisionTreeClassifier(max_depth=3)
svm = SVC(kernel='rbf')

models = [lr, dt, svm]
names = ['Logistic Regression', 'Decision Tree', 'SVM (RBF)']

# Plot decision boundaries
fig, axes = plt.subplots(1, 3, figsize=(18, 5))

for ax, model, name in zip(axes, models, names):
    model.fit(X, y)
    
    # Create mesh
    h = 0.02
    x_min, x_max = X[:, 0].min() - 1, X[:, 0].max() + 1
    y_min, y_max = X[:, 1].min() - 1, X[:, 1].max() + 1
    xx, yy = np.meshgrid(np.arange(x_min, x_max, h),
                         np.arange(y_min, y_max, h))
    
    # Predict on mesh
    Z = model.predict(np.c_[xx.ravel(), yy.ravel()])
    Z = Z.reshape(xx.shape)
    
    # Plot decision boundary
    ax.contourf(xx, yy, Z, alpha=0.3, cmap='RdYlBu')
    
    # Plot data points
    scatter = ax.scatter(X[:, 0], X[:, 1], c=y, cmap='RdYlBu', 
                         edgecolors='black', s=50)
    
    ax.set_title(name, fontsize=14, fontweight='bold')
    ax.set_xlabel('Feature 1', fontsize=12)
    ax.set_ylabel('Feature 2', fontsize=12)

plt.tight_layout()
plt.show()
6.2.2 Confusion Matrix Visualization
Python

from sklearn.metrics import confusion_matrix
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier

# Load iris dataset
iris = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris.data, iris.target, 
                                                     test_size=0.3, random_state=42)

# Train model
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)
y_pred = rf.predict(X_test)

# Confusion matrix
cm = confusion_matrix(y_test, y_pred)

# Visualize
fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Raw counts
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
            xticklabels=iris.target_names,
            yticklabels=iris.target_names, ax=axes[0])
axes[0].set_title('Confusion Matrix (Counts)', fontsize=14, fontweight='bold')
axes[0].set_ylabel('True Label', fontsize=12)
axes[0].set_xlabel('Predicted Label', fontsize=12)

# Normalized
cm_norm = cm.astype('float') / cm.sum(axis=1)[:, np.newaxis]
sns.heatmap(cm_norm, annot=True, fmt='.2f', cmap='Greens',
            xticklabels=iris.target_names,
            yticklabels=iris.target_names, ax=axes[1])
axes[1].set_title('Confusion Matrix (Normalized)', fontsize=14, fontweight='bold')
axes[1].set_ylabel('True Label', fontsize=12)
axes[1].set_xlabel('Predicted Label', fontsize=12)

plt.tight_layout()
plt.show()
6.2.3 ROC Curve and AUC
Python

from sklearn.metrics import roc_curve, auc
from sklearn.preprocessing import label_binarize
from sklearn.multiclass import OneVsRestClassifier

# Binarize labels for multi-class ROC
y_test_bin = label_binarize(y_test, classes=[0, 1, 2])
n_classes = y_test_bin.shape[1]

# Train classifier
classifier = OneVsRestClassifier(RandomForestClassifier(n_estimators=100, random_state=42))
y_score = classifier.fit(X_train, y_train).predict_proba(X_test)

# Compute ROC curve and AUC for each class
fpr = dict()
tpr = dict()
roc_auc = dict()

fig, ax = plt.subplots(figsize=(10, 8))

colors = ['blue', 'red', 'green']
for i in range(n_classes):
    fpr[i], tpr[i], _ = roc_curve(y_test_bin[:, i], y_score[:, i])
    roc_auc[i] = auc(fpr[i], tpr[i])
    
    ax.plot(fpr[i], tpr[i], color=colors[i], linewidth=2,
            label=f'{iris.target_names[i]} (AUC = {roc_auc[i]:.2f})')

# Plot diagonal (random classifier)
ax.plot([0, 1], [0, 1], 'k--', linewidth=2, label='Random Classifier')

ax.set_xlabel('False Positive Rate', fontsize=12)
ax.set_ylabel('True Positive Rate', fontsize=12)
ax.set_title('ROC Curves (One-vs-Rest)', fontsize=14, fontweight='bold')
ax.legend(loc='lower right', fontsize=11)
ax.grid(True, alpha=0.3)

plt.show()
6.3 Regression Visualization
6.3.1 Actual vs Predicted
Python

from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Using Boston dataset
X = df.drop('PRICE', axis=1)
y = df['PRICE']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Train model
lr = LinearRegression()
lr.fit(X_train, y_train)
y_pred = lr.predict(X_test)

# Metrics
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

# Visualize
fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Actual vs Predicted
axes[0].scatter(y_test, y_pred, alpha=0.6, s=50)
axes[0].plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], 
             'r--', linewidth=2, label='Perfect Prediction')
axes[0].set_xlabel('Actual Price', fontsize=12)
axes[0].set_ylabel('Predicted Price', fontsize=12)
axes[0].set_title(f'Actual vs Predicted (R² = {r2:.3f})', fontsize=14, fontweight='bold')
axes[0].legend()
axes[0].grid(True, alpha=0.3)

# Residual plot
residuals = y_test - y_pred
axes[1].scatter(y_pred, residuals, alpha=0.6, s=50)
axes[1].axhline(0, color='red', linestyle='--', linewidth=2)
axes[1].set_xlabel('Predicted Price', fontsize=12)
axes[1].set_ylabel('Residuals', fontsize=12)
axes[1].set_title(f'Residual Plot (MSE = {mse:.2f})', fontsize=14, fontweight='bold')
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
6.3.2 Feature Importance
Python

from sklearn.ensemble import RandomForestRegressor

# Train Random Forest
rf = RandomForestRegressor(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

# Get feature importance
importances = rf.feature_importances_
indices = np.argsort(importances)[::-1]

# Visualize
fig, ax = plt.subplots(figsize=(12, 8))

sns.barplot(x=importances[indices], y=X.columns[indices], palette='viridis', ax=ax)
ax.set_xlabel('Importance', fontsize=12)
ax.set_title('Feature Importance (Random Forest)', fontsize=14, fontweight='bold')
ax.grid(axis='x', alpha=0.3)

plt.tight_layout()
plt.show()
6.4 Clustering Visualization
6.4.1 K-Means Clustering
Python

from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs

# Generate data
X, y_true = make_blobs(n_samples=300, centers=4, random_state=42)

# Try different numbers of clusters
fig, axes = plt.subplots(2, 3, figsize=(18, 10))
axes = axes.flatten()

for i, k in enumerate([2, 3, 4, 5, 6, 7]):
    kmeans = KMeans(n_clusters=k, random_state=42)
    y_pred = kmeans.fit_predict(X)
    
    # Plot
    scatter = axes[i].scatter(X[:, 0], X[:, 1], c=y_pred, cmap='viridis', s=50, alpha=0.6)
    axes[i].scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1],
                   c='red', marker='X', s=200, edgecolors='black', linewidth=2)
    axes[i].set_title(f'K = {k} (Inertia: {kmeans.inertia_:.0f})', 
                     fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()
6.4.2 Elbow Method
Python

# Find optimal K
inertias = []
K_range = range(1, 11)

for k in K_range:
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(X)
    inertias.append(kmeans.inertia_)

# Plot elbow curve
fig, ax = plt.subplots(figsize=(10, 6))

ax.plot(K_range, inertias, 'bo-', linewidth=2, markersize=8)
ax.set_xlabel('Number of Clusters (K)', fontsize=12)
ax.set_ylabel('Inertia', fontsize=12)
ax.set_title('Elbow Method for Optimal K', fontsize=14, fontweight='bold')
ax.grid(True, alpha=0.3)

# Annotate elbow point (usually K=4 in this case)
ax.annotate('Elbow Point', xy=(4, inertias[3]), xytext=(6, inertias[3] + 500),
            arrowprops=dict(facecolor='red', shrink=0.05, width=2),
            fontsize=12, fontweight='bold')

plt.show()
6.5 Training Progress Visualization
6.5.1 Learning Curves
Python

# Simulated training history
epochs = np.arange(1, 51)
train_loss = 2.0 * np.exp(-epochs/10) + 0.1 + np.random.normal(0, 0.05, 50)
val_loss = 2.0 * np.exp(-epochs/12) + 0.2 + np.random.normal(0, 0.08, 50)

train_acc = 1 - train_loss/2
val_acc = 1 - val_loss/2

# Create subplot
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Loss plot
axes[0].plot(epochs, train_loss, 'b-', linewidth=2, label='Training Loss')
axes[0].plot(epochs, val_loss, 'r-', linewidth=2, label='Validation Loss')
axes[0].set_xlabel('Epoch', fontsize=12)
axes[0].set_ylabel('Loss', fontsize=12)
axes[0].set_title('Training and Validation Loss', fontsize=14, fontweight='bold')
axes[0].legend(fontsize=11)
axes[0].grid(True, alpha=0.3)

# Accuracy plot
axes[1].plot(epochs, train_acc, 'b-', linewidth=2, label='Training Accuracy')
axes[1].plot(epochs, val_acc, 'r-', linewidth=2, label='Validation Accuracy')
axes[1].set_xlabel('Epoch', fontsize=12)
axes[1].set_ylabel('Accuracy', fontsize=12)
axes[1].set_title('Training and Validation Accuracy', fontsize=14, fontweight='bold')
axes[1].legend(fontsize=11)
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
6.5.2 Cross-Validation Visualization
Python

from sklearn.model_selection import cross_val_score

# Perform cross-validation
models = {
    'Logistic Regression': LogisticRegression(max_iter=1000),
    'Random Forest': RandomForestClassifier(n_estimators=100),
    'SVM': SVC()
}

results = []
names = []

for name, model in models.items():
    scores = cross_val_score(model, iris.data, iris.target, cv=5, scoring='accuracy')
    results.append(scores)
    names.append(name)
    print(f'{name}: {scores.mean():.3f} (+/- {scores.std():.3f})')

# Visualize
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Box plot
axes[0].boxplot(results, labels=names)
axes[0].set_ylabel('Accuracy', fontsize=12)
axes[0].set_title('Cross-Validation Results (Box Plot)', fontsize=14, fontweight='bold')
axes[0].grid(axis='y', alpha=0.3)

# Violin plot
data_cv = pd.DataFrame({
    'Model': np.repeat(names, 5),
    'Accuracy': np.concatenate(results)
})

sns.violinplot(data=data_cv, x='Model', y='Accuracy', ax=axes[1])
sns.swarmplot(data=data_cv, x='Model', y='Accuracy', color='black', alpha=0.5, ax=axes[1])
axes[1].set_title('Cross-Validation Results (Violin Plot)', fontsize=14, fontweight='bold')

plt.tight_layout()
plt.show()
Chapter 7: Best Practices & Optimization
7.1 Performance Optimization
7.1.1 Large Datasets - Downsampling
Python

# Generate large dataset
np.random.seed(42)
large_X = np.random.randn(1000000, 2)
large_y = np.random.randint(0, 2, 1000000)

# Bad: Plot all points (slow!)
# plt.scatter(large_X[:, 0], large_X[:, 1], c=large_y)  # DON'T DO THIS

# Good: Downsample
sample_size = 5000
indices = np.random.choice(len(large_X), sample_size, replace=False)

plt.figure(figsize=(10, 6))
plt.scatter(large_X[indices, 0], large_X[indices, 1], c=large_y[indices], 
            alpha=0.5, s=10)
plt.title(f'Large Dataset Visualization ({sample_size:,} of {len(large_X):,} points)', 
          fontsize=14, fontweight='bold')
plt.show()
7.1.2 Using Hexbin for Dense Plots
Python

# For very dense scatter plots
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Regular scatter (hard to see density)
axes[0].scatter(large_X[indices, 0], large_X[indices, 1], alpha=0.1, s=1)
axes[0].set_title('Scatter (Hard to See Density)', fontsize=12, fontweight='bold')

# Hexbin (shows density clearly)
axes[1].hexbin(large_X[:, 0], large_X[:, 1], gridsize=50, cmap='YlOrRd', mincnt=1)
axes[1].set_title('Hexbin (Clear Density)', fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()
7.1.3 Rasterization for Vector Formats
Python

# When saving as PDF/SVG with many points
fig, ax = plt.subplots(figsize=(10, 6))

# Set rasterized=True for scatter plot
ax.scatter(large_X[indices, 0], large_X[indices, 1], 
           c=large_y[indices], alpha=0.5, s=10, rasterized=True)

ax.set_title('Rasterized Plot (Smaller PDF Size)', fontsize=14, fontweight='bold')

# Save as vector format
plt.savefig('rasterized_plot.pdf', dpi=300)
plt.show()

# Result: Text/lines are vector, points are raster = smaller file size
7.2 Publication-Quality Figures
7.2.1 Complete Publication Setup
Python

# Set publication style
plt.rcParams.update({
    'font.size': 11,
    'font.family': 'serif',
    'font.serif': ['Times New Roman'],
    'axes.labelsize': 12,
    'axes.titlesize': 14,
    'axes.titleweight': 'bold',
    'xtick.labelsize': 10,
    'ytick.labelsize': 10,
    'legend.fontsize': 10,
    'figure.titlesize': 16,
    'figure.dpi': 100,
    'savefig.dpi': 300,
    'savefig.bbox': 'tight',
    'savefig.pad_inches': 0.1,
    'lines.linewidth': 1.5,
    'lines.markersize': 6,
    'axes.linewidth': 1.2,
    'grid.alpha': 0.3,
    'grid.linewidth': 0.8
})

# Create publication-quality plot
fig, ax = plt.subplots(figsize=(6, 4))  # Typical journal column width

x = np.linspace(0, 10, 100)
ax.plot(x, np.sin(x), label='sin(x)', linewidth=2)
ax.plot(x, np.cos(x), label='cos(x)', linewidth=2)

ax.set_xlabel('Time (s)')
ax.set_ylabel('Amplitude')
ax.set_title('Oscillation Patterns')
ax.legend(frameon=True, fancybox=True, shadow=True)
ax.grid(True)

# Save in multiple formats
plt.savefig('publication_plot.pdf', dpi=300, bbox_inches='tight')
plt.savefig('publication_plot.png', dpi=300, bbox_inches='tight')
plt.savefig('publication_plot.svg', bbox_inches='tight')

plt.show()

# Reset to defaults
plt.rcdefaults()
7.2.2 Multi-Panel Figure for Papers
Python

# Typical multi-panel figure (A, B, C, D)
fig = plt.figure(figsize=(12, 10))
gs = fig.add_gridspec(2, 2, hspace=0.3, wspace=0.3)

# Panel A
ax1 = fig.add_subplot(gs[0, 0])
ax1.plot(x, np.sin(x), 'b-', linewidth=2)
ax1.set_xlabel('X')
ax1.set_ylabel('sin(X)')
ax1.set_title('(A) Sine Wave', fontsize=12, fontweight='bold', loc='left')
ax1.grid(True, alpha=0.3)

# Panel B
ax2 = fig.add_subplot(gs[0, 1])
ax2.plot(x, np.cos(x), 'r-', linewidth=2)
ax2.set_xlabel('X')
ax2.set_ylabel('cos(X)')
ax2.set_title('(B) Cosine Wave', fontsize=12, fontweight='bold', loc='left')
ax2.grid(True, alpha=0.3)

# Panel C
ax3 = fig.add_subplot(gs[1, 0])
ax3.scatter(np.random.randn(100), np.random.randn(100), alpha=0.5)
ax3.set_xlabel('Variable 1')
ax3.set_ylabel('Variable 2')
ax3.set_title('(C) Scatter Plot', fontsize=12, fontweight='bold', loc='left')
ax3.grid(True, alpha=0.3)

# Panel D
ax4 = fig.add_subplot(gs[1, 1])
data = np.random.randn(1000)
ax4.hist(data, bins=30, edgecolor='black', alpha=0.7)
ax4.set_xlabel('Value')
ax4.set_ylabel('Frequency')
ax4.set_title('(D) Distribution', fontsize=12, fontweight='bold', loc='left')
ax4.grid(axis='y', alpha=0.3)

# Overall title
fig.suptitle('Figure 1: Comprehensive Analysis', fontsize=16, fontweight='bold', y=0.98)

plt.savefig('multi_panel_figure.pdf', dpi=300, bbox_inches='tight')
plt.show()
7.3 Color Accessibility (Colorblind-Friendly)
Python

# Use colorblind-safe palettes
fig, axes = plt.subplots(2, 2, figsize=(14, 10))

x = np.arange(5)
y = np.random.randint(10, 50, 5)

# Bad: Default colors (not accessible)
axes[0, 0].bar(x, y, color=['red', 'green', 'blue', 'yellow', 'purple'])
axes[0, 0].set_title('❌ Not Colorblind Safe', fontsize=12, fontweight='bold')

# Good: Colorblind-safe palette
cb_palette = sns.color_palette('colorblind')
axes[0, 1].bar(x, y, color=cb_palette)
axes[0, 1].set_title('✓ Colorblind Safe (Seaborn)', fontsize=12, fontweight='bold')

# Good: Paired colors (high contrast)
axes[1, 0].bar(x, y, color=sns.color_palette('Paired'))
axes[1, 0].set_title('✓ High Contrast (Paired)', fontsize=12, fontweight='bold')

# Good: Using patterns in addition to color
bars = axes[1, 1].bar(x, y, color=cb_palette)
patterns = ['/', '\\', '|', '-', '+']
for bar, pattern in zip(bars, patterns):
    bar.set_hatch(pattern)
axes[1, 1].set_title('✓ Colors + Patterns (Best)', fontsize=12, fontweight='bold')

plt.tight_layout()
plt.show()
7.4 Common Mistakes and How to Avoid Them
7.4.1 Misleading Y-Axis
Python

# Example: Misleading vs honest axis
data = [98, 99, 100, 101, 102]
x = np.arange(len(data))

fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Misleading: Y-axis doesn't start at 0
axes[0].bar(x, data, color='red', alpha=0.7)
axes[0].set_ylim(97, 103)
axes[0].set_title('❌ Misleading (Exaggerates Difference)', fontsize=12, fontweight='bold', color='red')
axes[0].set_ylabel('Value')

# Honest: Y-axis starts at 0
axes[1].bar(x, data, color='green', alpha=0.7)
axes[1].set_ylim(0, max(data) * 1.1)
axes[1].set_title('✓ Honest (True Scale)', fontsize=12, fontweight='bold', color='green')
axes[1].set_ylabel('Value')

plt.tight_layout()
plt.show()
7.4.2 Chart Junk (Too Much Decoration)
Python

fig, axes = plt.subplots(1, 2, figsize=(14, 6))

x = [1, 2, 3, 4, 5]
y = [10, 25, 15, 30, 20]

# Bad: Too much decoration
axes[0].bar(x, y, color=['red', 'blue', 'green', 'orange', 'purple'],
           edgecolor='black', linewidth=3, alpha=0.5, hatch='///')
axes[0].set_facecolor('lightgray')
axes[0].grid(True, linestyle='--', linewidth=2, color='yellow', alpha=0.7)
axes[0].set_title('❌ Chart Junk (Distracting)', fontsize=12, fontweight='bold', 
                 bbox=dict(boxstyle='round', facecolor='red', alpha=0.3))

# Good: Clean and simple
axes[1].bar(x, y, color='steelblue', edgecolor='black', linewidth=1, alpha=0.8)
axes[1].grid(axis='y', alpha=0.3)
axes[1].set_title('✓ Clean Design (Easy to Read)', fontsize=12, fontweight='bold')
axes[1].set_ylabel('Value')

plt.tight_layout()
plt.show()
7.4.3 3D Pie Charts (Never Use!)
Python

# Don't use 3D pie charts - use bar plots instead
categories = ['A', 'B', 'C', 'D']
values = [25, 30, 20, 25]

fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Bad: Pie chart (hard to compare)
axes[0].pie(values, labels=categories, autopct='%1.1f%%', 
           explode=(0.1, 0, 0, 0), shadow=True)
axes[0].set_title('❌ Pie Chart (Hard to Compare)', fontsize=12, fontweight='bold', color='red')

# Good: Bar chart (easy to compare)
axes[1].bar(categories, values, color='steelblue', edgecolor='black', linewidth=1)
axes[1].set_ylabel('Value', fontsize=12)
axes[1].set_title('✓ Bar Chart (Easy to Compare)', fontsize=12, fontweight='bold', color='green')
axes[1].grid(axis='y', alpha=0.3)

plt.tight_layout()
plt.show()
7.5 Interactive Plots (Bonus: Plotly Integration)
Python

# While matplotlib is static, you can use plotly for interactivity
# Install: pip install plotly

import plotly.express as px

# Create interactive scatter plot
df_iris = px.data.iris()
fig = px.scatter(df_iris, x='sepal_width', y='sepal_length', 
                 color='species', size='petal_length',
                 hover_data=['petal_width'],
                 title='Interactive Iris Dataset')

# This will open in browser
# fig.show()

# Convert matplotlib to interactive (using mpld3)
# Install: pip install mpld3
import mpld3

fig, ax = plt.subplots(figsize=(10, 6))
ax.scatter(df['total_bill'], df['tip'], alpha=0.5)
ax.set_xlabel('Total Bill')
ax.set_ylabel('Tip')
ax.set_title('Interactive Matplotlib Plot')

# Create HTML
# html_str = mpld3.fig_to_html(fig)
# with open('interactive_plot.html', 'w') as f:
#     f.write(html_str)

plt.show()
7.6 Complete Workflow Example (End-to-End)
Python

# Real-world ML visualization workflow

# 1. Load and prepare data
from sklearn.datasets import load_wine
wine = load_wine()
df_wine = pd.DataFrame(wine.data, columns=wine.feature_names)
df_wine['target'] = wine.target
df_wine['class'] = df_wine['target'].map({0: 'Class 0', 1: 'Class 1', 2: 'Class 2'})

# 2. Set style
sns.set_style('whitegrid')
sns.set_palette('colorblind')

# 3. Exploratory analysis
fig = plt.figure(figsize=(18, 12))
gs = fig.add_gridspec(3, 3, hspace=0.3, wspace=0.3)

# Distribution of classes
ax1 = fig.add_subplot(gs[0, 0])
sns.countplot(data=df_wine, x='class', ax=ax1)
ax1.set_title('Class Distribution', fontsize=12, fontweight='bold')

# Correlation heatmap
ax2 = fig.add_subplot(gs[0, 1:])
corr = df_wine.drop(['target', 'class'], axis=1).corr()
sns.heatmap(corr, annot=False, cmap='coolwarm', center=0, ax=ax2)
ax2.set_title('Feature Correlation', fontsize=12, fontweight='bold')

# Feature distributions by class
features = ['alcohol', 'malic_acid', 'ash']
for i, feature in enumerate(features):
    ax = fig.add_subplot(gs[1, i])
    sns.violinplot(data=df_wine, x='class', y=feature, ax=ax)
    ax.set_title(f'{feature} by Class', fontsize=10, fontweight='bold')

# Scatter plot matrix (selected features)
ax3 = fig.add_subplot(gs[2, :])
selected = df_wine[['alcohol', 'malic_acid', 'class']]
for class_name in selected['class'].unique():
    class_data = selected[selected['class'] == class_name]
    ax3.scatter(class_data['alcohol'], class_data['malic_acid'], 
               label=class_name, alpha=0.6, s=50)
ax3.set_xlabel('Alcohol', fontsize=12)
ax3.set_ylabel('Malic Acid', fontsize=12)
ax3.set_title('Alcohol vs Malic Acid by Class', fontsize=12, fontweight='bold')
ax3.legend()
ax3.grid(True, alpha=0.3)

plt.savefig('wine_eda.png', dpi=300, bbox_inches='tight')
plt.show()

# 4. Model training and evaluation
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, confusion_matrix

X = df_wine.drop(['target', 'class'], axis=1)
y = df_wine['target']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)
y_pred = rf.predict(X_test)

# 5. Visualize results
fig, axes = plt.subplots(1, 2, figsize=(14, 6))

# Confusion matrix
cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', 
           xticklabels=wine.target_names,
           yticklabels=wine.target_names, ax=axes[0])
axes[0].set_title('Confusion Matrix', fontsize=14, fontweight='bold')
axes[0].set_ylabel('True Label')
axes[0].set_xlabel('Predicted Label')

# Feature importance
importances = rf.feature_importances_
indices = np.argsort(importances)[::-1][:10]

axes[1].barh(range(10), importances[indices], color='steelblue')
axes[1].set_yticks(range(10))
axes[1].set_yticklabels([wine.feature_names[i] for i in indices])
axes[1].set_xlabel('Importance', fontsize=12)
axes[1].set_title('Top 10 Feature Importances', fontsize=14, fontweight='bold')
axes[1].grid(axis='x', alpha=0.3)

plt.tight_layout()
plt.savefig('wine_results.png', dpi=300, bbox_inches='tight')
plt.show()

print("\nClassification Report:")
print(classification_report(y_test, y_pred, target_names=wine.target_names))
7.7 Quick Reference Cheat Sheet
Python

"""
MATPLOTLIB & SEABORN QUICK REFERENCE
====================================

ESSENTIAL IMPORTS
-----------------
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import pandas as pd

MATPLOTLIB BASICS
-----------------
# Create figure and axes
fig, ax = plt.subplots(figsize=(10, 6))

# Basic plots
ax.plot(x, y)                    # Line plot
ax.scatter(x, y)                 # Scatter plot
ax.bar(x, y)                     # Bar plot
ax.hist(x, bins=20)              # Histogram
ax.boxplot(data)                 # Box plot

# Customization
ax.set_xlabel('X Label')
ax.set_ylabel('Y Label')
ax.set_title('Title')
ax.legend()
ax.grid(True)

# Save
plt.savefig('plot.png', dpi=300, bbox_inches='tight')

SEABORN BASICS
--------------
# Set theme
sns.set_theme()

# Distribution plots
sns.histplot(data=df, x='column', kde=True)
sns.kdeplot(data=df, x='column')
sns.boxplot(data=df, x='category', y='value')
sns.violinplot(data=df, x='category', y='value')

# Categorical plots
sns.barplot(data=df, x='category', y='value')
sns.countplot(data=df, x='category')
sns.pointplot(data=df, x='category', y='value')

# Relationship plots
sns.scatterplot(data=df, x='x', y='y', hue='category')
sns.lineplot(data=df, x='x', y='y')
sns.regplot(data=df, x='x', y='y')

# Matrix plots
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')

# Multi-plot grids
sns.pairplot(df, hue='category')
sns.FacetGrid(df, col='category')

COLOR PALETTES
--------------
sns.color_palette('colorblind')  # Accessible
sns.color_palette('deep')        # Default
sns.color_palette('husl', 8)     # 8 colors

COMMON PARAMETERS
-----------------
figsize=(width, height)          # Figure size in inches
dpi=300                          # Resolution
alpha=0.5                        # Transparency (0-1)
linewidth=2                      # Line width
s=50                             # Marker size
hue='column'                     # Color by column
style='column'                   # Marker style by column
palette='colorblind'             # Color palette

BEST PRACTICES
--------------
1. Always use fig, ax = plt.subplots()
2. Use sns.set_theme() for better defaults
3. Label all axes and add titles
4. Use colorblind-safe palettes
5. Save at 300 DPI for publications
6. Use bbox_inches='tight' when saving
7. Choose appropriate plot types
8. Avoid 3D pie charts
9. Start Y-axis at 0 for bar charts (usually)
10. Keep it simple - less is more
"""
Final Words: From Beginner to Expert
Congratulations! You've completed the comprehensive Matplotlib and Seaborn guide. Here's what you've learned:

Core Concepts Mastered:
✅ Matplotlib architecture (Figure, Axes, Axis)
✅ All essential plot types
✅ Customization (colors, styles, annotations)
✅ Seaborn's statistical plots
✅ Working with DataFrames
✅ Advanced layouts and grids
✅ ML-specific visualizations
✅ Publication-quality figures
✅ Best practices and optimization
Your Next Steps:
Practice: Create plots for your own datasets
Explore: Try the built-in datasets (sns.load_dataset())
Experiment: Combine techniques from different sections
Apply: Use these skills in your ML projects
Share: Create beautiful visualizations for presentations
Remember:
Visualization is storytelling - every plot should have a clear message
Simplicity wins - don't overcomplicate
Iterate - your first plot rarely is your best plot
Context matters - different audiences need different visualizations
Resources for Continued Learning:
Matplotlib Documentation: https://matplotlib.org/stable/contents.html
Seaborn Documentation: https://seaborn.pydata.org/
Python Graph Gallery: https://python-graph-gallery.com/
From Data to Viz: https://www.data-to-viz.com/
You're now equipped to create any visualization you can imagine! 🎨📊📈

Happy Plotting! 🚀

This comprehensive guide was created with love for aspiring data scientists and ML engineers. Keep learning, keep visualizing!