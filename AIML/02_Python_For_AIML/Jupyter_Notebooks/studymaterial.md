The Complete Jupyter Notebook Masterclass
From Absolute Beginner to Advanced Professional
Table of Contents
Introduction
Chapter 1: Getting Started
Chapter 2: Basic Operations
Chapter 3: Intermediate Concepts
Chapter 4: Advanced Techniques
Chapter 5: Machine Learning Integration
Chapter 6: Professional Best Practices
Chapter 7: Troubleshooting & Optimization
Introduction
What is Jupyter Notebook?
Jupyter Notebook is an interactive web-based environment that allows you to:

Write and execute code in small chunks (cells)
Document your code with rich text, equations, and visualizations
Share your analysis with others in a readable format
Experiment with code without writing complete programs
The Name "Jupyter"
Ju = Julia
Py = Python
R = R
These are the three core programming languages it was designed to support, though it now supports 40+ languages.

Why Jupyter for Machine Learning?
Immediate Feedback: Run code and see results instantly
Visual Analysis: Display graphs, charts, and images inline
Documentation: Combine code with explanations
Reproducibility: Share complete analyses with others
Experimentation: Test different approaches easily
Real-World Use Cases
Data Scientists: Exploratory Data Analysis (EDA)
ML Engineers: Model prototyping and testing
Researchers: Scientific computing and publishing
Educators: Teaching programming and statistics
Analysts: Creating data reports
Chapter 1: Getting Started
1.1 Installation Methods
Method 1: Anaconda (Recommended for Beginners)
What is Anaconda?
Anaconda is a distribution of Python that includes Jupyter and 1,500+ popular packages.

Installation Steps:

Visit: https://www.anaconda.com/download
Download the installer for your operating system (Windows/Mac/Linux)
Run the installer (use default settings)
Wait for installation (2-5 GB download)
Verification:

Bash

# Open Terminal (Mac/Linux) or Anaconda Prompt (Windows)
jupyter notebook --version
# Should display: 6.x.x or 7.x.x
Method 2: pip (For Experienced Users)
Bash

# Step 1: Ensure Python is installed (3.7 or higher)
python --version

# Step 2: Install Jupyter
pip install notebook

# Step 3: Verify installation
jupyter notebook --version
Method 3: Google Colab (No Installation Required)
What is Google Colab?
A free, cloud-based Jupyter environment by Google.

Access:

Go to: https://colab.research.google.com
Sign in with Google account
Start coding immediately
Pros:

No setup required
Free GPU access
Cloud storage integration
Cons:

Requires internet connection
Session timeout after inactivity
Limited to Google ecosystem
1.2 Launching Jupyter Notebook
Method 1: From Command Line
Bash

# Navigate to your project folder
cd /path/to/your/project

# Launch Jupyter
jupyter notebook
What happens:

A web server starts on your computer
Your default browser opens automatically
You see the Jupyter dashboard at http://localhost:8888
Method 2: From Anaconda Navigator (GUI)
Open Anaconda Navigator
Click "Launch" under Jupyter Notebook
Browser opens with dashboard
Method 3: From Start Menu (Windows)
Search "Jupyter Notebook"
Click to launch
Default location: C:\Users\YourName
1.3 Understanding the Interface
The Dashboard
When you first open Jupyter, you see the Dashboard:

text

Jupyter
  Files | Running | Clusters
  
  [Upload] [New ▼]
  
  ☐ Name              Last Modified      Type
  ☐ data/             2 hours ago        Folder
  ☐ analysis.ipynb    30 minutes ago     Notebook
  ☐ README.md         1 day ago          File
Components:

Files Tab: Browse your file system
Running Tab: See active notebooks and terminals
Clusters Tab: Advanced parallel computing (ignore for now)
Upload Button: Upload files from your computer
New Dropdown: Create notebooks, folders, text files, terminals
1.4 Creating Your First Notebook
Step-by-Step Process
Click "New" → "Python 3" (or latest Python version)
A new tab opens with an empty notebook
You see "Untitled" at the top
One empty cell is ready for input
Renaming Your Notebook
Method 1: Click "Untitled" at the top

Type new name: "My_First_Notebook"
Press Enter
File saved as: My_First_Notebook.ipynb
Method 2: File menu → Rename

Important: The .ipynb extension is added automatically

ipynb = Interactive Python Notebook
It's actually a JSON file that stores your code and outputs
1.5 The Notebook Interface
Anatomy of a Notebook
text

┌─────────────────────────────────────────────────────┐
│ Jupyter  My_First_Notebook  [Last checkpoint: ...]  │
├─────────────────────────────────────────────────────┤
│ File Edit View Insert Cell Kernel Widgets Help     │
├─────────────────────────────────────────────────────┤
│ ⚫ ⏸ ⏹ ↻ ▶▶ [+] [✂] [📋] [📄] [⬆] [⬇] [▶] [■] [↻]  │
├─────────────────────────────────────────────────────┤
│ In [1]: ┌──────────────────────────────────────┐   │
│         │ # Your code goes here                │   │
│         │                                      │   │
│         └──────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
Key Elements:

Menu Bar: File, Edit, View, Insert, Cell, Kernel, Widgets, Help
Toolbar: Quick access buttons
Cell: Where you write code or text
In [1]: Input cell number (shows execution order)
1.6 Two Modes: Command vs Edit
Edit Mode (Green Border)
Purpose: Type content into cells

How to enter:

Click inside a cell, OR
Press Enter when cell is selected
Visual indicator: Green left border on cell

What you can do:

Type code or text
Use normal keyboard shortcuts (Ctrl+C, Ctrl+V)
Navigate with arrow keys within the cell
Command Mode (Blue Border)
Purpose: Navigate and manipulate cells

How to enter:

Press Esc from edit mode, OR
Click outside cell content area
Visual indicator: Blue left border on cell

What you can do:

Navigate between cells (Up/Down arrows)
Create/delete cells
Change cell types
Execute cells
Key Concept: Modal Interface
Think of it like Vim or other modal editors:

Edit Mode = Insert mode (editing content)
Command Mode = Normal mode (manipulating structure)
This is one of the most important concepts for efficiency!

Chapter 2: Basic Operations
2.1 Working with Cells
What is a Cell?
A cell is a container that holds either:

Code (Python, R, etc.)
Markdown (formatted text)
Raw (unformatted text - rarely used)
Cell Types
1. Code Cells (Default)
Python

# This is a code cell
print("Hello, World!")
Output:

text

Hello, World!
Characteristics:

Gray background when selected
Shows In [ ]: on the left
Shows Out[ ]: if there's output
Executes Python code
Displays results below
2. Markdown Cells
Markdown

# This is a Markdown Cell

You can write **bold** and *italic* text.

- Bullet points
- Lists
- Links: [Google](https://google.com)
When rendered, displays as:

This is a Markdown Cell
You can write bold and italic text.

Bullet points
Lists
Links: Google
Characteristics:

White background when selected
No In [ ]: indicator
Supports rich text formatting
Used for documentation and explanations
3. Raw Cells (Rarely Used)
text

This text is not executed or rendered.
Used for special export formats.
2.2 Creating and Deleting Cells
Creating New Cells
Method 1: Keyboard Shortcuts (Command Mode)

Press A → Insert cell Above
Press B → Insert cell Below
Method 2: Toolbar

Click + button
Method 3: Menu

Insert → Insert Cell Above/Below
Deleting Cells
Method 1: Keyboard (Command Mode)

Press D twice (DD) → Delete cell
Method 2: Menu

Edit → Delete Cells
Warning: Deletion is immediate (but can be undone with Z)

Undoing Deletion
Press Z in command mode → Undo cell deletion
2.3 Changing Cell Types
Quick Method (Keyboard Shortcuts in Command Mode)
Press M → Convert to Markdown
Press Y → Convert to code (pYthon)
Press R → Convert to Raw
Menu Method
Select cell
Cell → Cell Type → Choose type
Toolbar Method
Select cell
Use dropdown that shows "Code" or "Markdown"
2.4 Running Cells
The Core Workflow
Most Important Shortcuts:

Shift + Enter → Run cell and move to next
Ctrl + Enter → Run cell and stay
Alt + Enter → Run cell and insert new below
Example Workflow
Python

# Cell 1
a = 5
print(a)
Press Shift + Enter →

Output:

text

5
Cursor moves to next cell automatically.

Python

# Cell 2
b = 10
result = a + b  # 'a' is still in memory from Cell 1
print(result)
Press Shift + Enter →

Output:

text

15
Understanding Cell Execution Numbers
Python

In [1]: x = 100
In [2]: y = 200
In [1]: x = 999  # Re-ran Cell 1
In [3]: print(x + y)
Output:

text

1199
Key Points:

Numbers show execution order, not cell position
You can run cells in any order
Variables persist across cells in memory
Re-running a cell updates the variable
2.5 Essential Keyboard Shortcuts
Command Mode Shortcuts (Blue Border)
Shortcut	Action
A	Insert cell Above
B	Insert cell Below
DD	Delete cell
Z	Undo deletion
M	Convert to Markdown
Y	Convert to code
C	Copy cell
V	Paste cell below
X	Cut cell
Shift + V	Paste cell above
Shift + M	Merge selected cells
Up/Down	Navigate cells
Shift + Up/Down	Select multiple cells
Edit Mode Shortcuts (Green Border)
Shortcut	Action
Tab	Code completion or indent
Shift + Tab	Tooltip (function info)
Ctrl + ]	Indent
Ctrl + [	Dedent
Ctrl + A	Select all in cell
Ctrl + Z	Undo
Ctrl + /	Comment/uncomment
Universal Shortcuts (Work in Both Modes)
Shortcut	Action
Shift + Enter	Run and select next
Ctrl + Enter	Run and stay
Alt + Enter	Run and insert below
Ctrl + S	Save notebook
Pro Tip: Viewing All Shortcuts
In command mode, press H to see the complete list.

2.6 Saving and Checkpointing
Auto-Save
Jupyter auto-saves every 2 minutes by default.

Status indicator:

"Last Checkpoint: 2 minutes ago" (top right)
Manual Save
Methods:

Ctrl + S (keyboard)
Click save icon (toolbar)
File → Save and Checkpoint
Checkpoints vs. Saves
Save:

Updates the .ipynb file on disk
Overwrites previous content
Checkpoint:

Creates a backup in .ipynb_checkpoints/ folder
Allows you to revert
Reverting to Checkpoint
File → Revert to Checkpoint → Select checkpoint time

Use case: Accidentally deleted important code

2.7 Downloading and Exporting
File Formats You Can Export To
Notebook (.ipynb) - Native format
Python (.py) - Pure Python script
HTML (.html) - Web page (static)
Markdown (.md) - Text with formatting
PDF via LaTeX - Professional document
PDF via HTML - Simpler PDF
Slides (Reveal.js) - Presentations
How to Export
Menu Method:

File → Download as
Choose format
Command Line Method:

Bash

# Convert to HTML
jupyter nbconvert --to html My_Notebook.ipynb

# Convert to Python script
jupyter nbconvert --to python My_Notebook.ipynb

# Convert to PDF (requires LaTeX)
jupyter nbconvert --to pdf My_Notebook.ipynb
Sharing Notebooks
Option 1: Share .ipynb file

Recipient needs Jupyter installed
Full interactivity preserved
Option 2: Share HTML

Anyone can open in browser
No interactivity (read-only)
Option 3: GitHub

Upload .ipynb to GitHub
Automatic rendering in browser
Free and convenient
Option 4: nbviewer

Upload to GitHub or Gist
Paste URL into https://nbviewer.org
Share the nbviewer link
Chapter 3: Intermediate Concepts
3.1 Markdown Deep Dive
Why Learn Markdown?
In professional ML work, code alone isn't enough:

Explain your methodology
Document assumptions
Present findings
Create readable reports
Markdown makes your notebooks publication-ready.

Headings
Markdown

# Heading 1 (Largest)
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6 (Smallest)
Renders as:

Heading 1
Heading 2
Heading 3
Best Practice:

Use # for main title (once per notebook)
Use ## for major sections
Use ### for subsections
Text Formatting
Markdown

**Bold text**
*Italic text*
***Bold and Italic***
~~Strikethrough~~
`Inline code`
Renders as:

Bold text
Italic text
Bold and Italic
Strikethrough
Inline code

Lists
Unordered Lists:

Markdown

- Item 1
- Item 2
  - Nested item 2.1
  - Nested item 2.2
- Item 3
Renders as:

Item 1
Item 2
Nested item 2.1
Nested item 2.2
Item 3
Ordered Lists:

Markdown

1. First step
2. Second step
3. Third step
   1. Sub-step A
   2. Sub-step B
Renders as:

First step
Second step
Third step
Sub-step A
Sub-step B
Links and Images
Links:

Markdown

[Link text](https://example.com)
[Google](https://google.com)
Renders as:

Google

Images:

Markdown

![Alt text](image_url.jpg)
![Python Logo](https://www.python.org/static/community_logos/python-logo.png)
Local images:

Markdown

![My Plot](./images/plot.png)
Tables
Markdown

| Model | Accuracy | F1-Score |
|-------|----------|----------|
| Logistic Regression | 0.85 | 0.83 |
| Random Forest | 0.92 | 0.91 |
| Neural Network | 0.95 | 0.94 |
Renders as:

Model	Accuracy	F1-Score
Logistic Regression	0.85	0.83
Random Forest	0.92	0.91
Neural Network	0.95	0.94
Alignment:

Markdown

| Left | Center | Right |
|:-----|:------:|------:|
| Text | Text   | Text  |
Code Blocks
Syntax highlighting:

Markdown

```python
def hello():
    print("Hello, World!")
text


**Renders as:**

```python
def hello():
    print("Hello, World!")
Other languages:

Markdown

```javascript
console.log("Hello");
Bash

pip install pandas
text


---

### Mathematical Equations (LaTeX)

**Inline math:**

```markdown
The equation $E = mc^2$ is famous.
Renders as:

The equation 
E
=
m
c
2
E=mc 
2
  is famous.

Display math:

Markdown

$$
\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$
Renders as:

−
b
±
b
2
−
4
a
c
2
a
2a
−b± 
b 
2
 −4ac
​
 
​
 
Common ML equations:

Markdown

$$
\text{MSE} = \frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2
$$

$$
\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
$$

$$
P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}
$$
Blockquotes
Markdown

> This is a quote.
> It can span multiple lines.
>
> — Albert Einstein
Renders as:

This is a quote.
It can span multiple lines.

— Albert Einstein

Horizontal Rules
Markdown

---
***
___
All three render as:

HTML in Markdown
Markdown supports embedded HTML for advanced formatting:

Markdown

<div style="background-color: #f0f0f0; padding: 10px; border-radius: 5px;">
    <h3 style="color: #333;">Important Note</h3>
    <p>This uses HTML for custom styling.</p>
</div>
Use sparingly — defeats the purpose of simple Markdown.

3.2 Magic Commands
What are Magic Commands?
Magic commands are special shortcuts in Jupyter that start with % or %%.

% = Line magic (applies to one line)
%% = Cell magic (applies to entire cell)
They provide shortcuts for common tasks.

Line Magics (%)
%timeit - Measure execution time
Python

%timeit sum(range(1000))
Output:

text

47.3 µs ± 2.1 µs per loop (mean ± std. dev. of 7 runs, 10000 loops each)
Explanation:

Runs code multiple times
Calculates average time
Useful for optimization
%time - Single execution time
Python

%time sum(range(1000000))
Output:

text

CPU times: user 23.5 ms, sys: 1.2 ms, total: 24.7 ms
Wall time: 24.9 ms
%who - List variables
Python

x = 10
y = 20
name = "Alice"
%who
Output:

text

name	x	y
Variations:

%who - Names only
%who int - Only integers
%whos - Detailed info (type, value, size)
Python

%whos
Output:

text

Variable   Type    Data/Info
-----------------------------
name       str     Alice
x          int     10
y          int     20
%history - Show command history
Python

%history
Output:

text

1: x = 10
2: y = 20
3: print(x + y)
%pwd - Print working directory
Python

%pwd
Output:

text

'/Users/yourname/projects/ml_project'
%cd - Change directory
Python

%cd /path/to/directory
%ls - List files
Python

%ls
Output:

text

data/  models/  notebook.ipynb  README.md
%load - Load external file
Python

%load script.py
Loads contents of script.py into the cell.

%run - Execute external script
Python

%run preprocessing.py
Runs the script and imports all variables into namespace.

Cell Magics (%%)
%%timeit - Time entire cell
Python

%%timeit
total = 0
for i in range(1000):
    total += i
%%time - Time cell once
Python

%%time
import pandas as pd
df = pd.read_csv('large_file.csv')
%%writefile - Write cell to file
Python

%%writefile helper.py
def greet(name):
    return f"Hello, {name}!"
Creates: helper.py with the function.

%%bash - Run bash commands
Python

%%bash
echo "Hello from bash"
pwd
ls -la
%%html - Render HTML
Python

%%html
<h1 style="color: blue;">Custom HTML</h1>
<p>This is rendered as HTML.</p>
%%latex - Render LaTeX
Python

%%latex
\begin{align}
\nabla \times \vec{E} &= -\frac{\partial \vec{B}}{\partial t} \\
\nabla \times \vec{B} &= \mu_0\vec{J} + \mu_0\epsilon_0\frac{\partial \vec{E}}{\partial t}
\end{align}
Most Useful Magics for ML
%matplotlib - Configure plots
Python

%matplotlib inline
# Plots appear below cells (default in Jupyter)

%matplotlib notebook
# Interactive plots (zoom, pan)
%load_ext - Load extensions
Python

%load_ext autoreload
%autoreload 2
What it does:

Automatically reloads modules before executing code
Essential when developing custom Python modules
Use case:

You have utils.py:

Python

def process_data(df):
    return df.dropna()
In notebook:

Python

%load_ext autoreload
%autoreload 2

from utils import process_data

# Edit utils.py and add new function
# No need to restart kernel — changes are auto-loaded!
%config - Configure Jupyter
Python

# See current config
%config InlineBackend

# Change figure size
%config InlineBackend.figure_format = 'retina'  # High-res plots
%env - Environment variables
Python

# Set
%env MY_API_KEY=abc123

# Get
%env MY_API_KEY
Listing All Magics
Python

%lsmagic
Output:

text

Available line magics:
%alias  %autoawait  %autocall  %automagic  %autoreload  ...

Available cell magics:
%%!  %%HTML  %%SVG  %%bash  %%capture  %%debug  %%file  ...
Getting Help
Python

%timeit?
# Shows documentation for %timeit

%magic
# Complete guide to magic system
3.3 Shell Commands
Running Shell Commands in Jupyter
You can run terminal/command prompt commands directly in cells using !.

Basic Syntax
Python

!command
Examples
List files
Python

!ls  # Mac/Linux
!dir  # Windows
Check Python version
Python

!python --version
Output:

text

Python 3.9.7
Install packages
Python

!pip install pandas numpy matplotlib
Check installed packages
Python

!pip list
Create directory
Python

!mkdir data
Download file (using curl/wget)
Python

# Mac/Linux
!wget https://example.com/dataset.csv

# Windows (PowerShell)
!curl -O https://example.com/dataset.csv
View file contents
Python

!cat data.csv  # Mac/Linux
!type data.csv  # Windows
Capturing Output
Python

files = !ls
print(files)
print(type(files))
Output:

text

['data', 'models', 'notebook.ipynb']
<class 'IPython.utils.text.SList'>
Converting to list:

Python

file_list = list(!ls)
Passing Python Variables to Shell
Python

filename = "results.csv"
!head {filename}
Explanation:

Use {variable} to insert Python variables
Example with multiple variables:

Python

folder = "data"
file = "train.csv"
!cp {folder}/{file} ./backup/
Common Use Cases
1. Environment setup
Python

!pip install -r requirements.txt
!conda install tensorflow
2. Data download
Python

!kaggle datasets download -d username/dataset
!unzip dataset.zip
3. Git operations
Python

!git clone https://github.com/user/repo.git
!git status
!git add .
!git commit -m "Update analysis"
!git push
4. File management
Python

!mv old_name.csv new_name.csv
!rm temporary_file.txt
!cp source.csv destination.csv
5. System info
Python

!nvidia-smi  # Check GPU
!df -h  # Disk space
!free -h  # Memory usage (Linux)
Multi-line Shell Commands
Python

%%bash
echo "Starting process..."
cd data
ls -la
echo "Process complete"
3.4 Debugging in Jupyter
Types of Errors
1. Syntax Errors
Python

print("Hello"
Error:

text

  File "<ipython-input-1>", line 1
    print("Hello"
                 ^
SyntaxError: unexpected EOF while parsing
Fix: Add closing parenthesis

2. Runtime Errors
Python

x = 10 / 0
Error:

text

ZeroDivisionError: division by zero
3. Logical Errors
Python

# Intended to calculate average
total = 100
count = 5
average = total * count  # Wrong operator!
print(average)
Output:

text

500  # Should be 20
No error message — hardest to debug!

Basic Debugging Techniques
1. Print debugging
Python

def calculate_discount(price, discount):
    print(f"Price: {price}")  # Debug
    print(f"Discount: {discount}")  # Debug
    final_price = price - (price * discount)
    print(f"Final: {final_price}")  # Debug
    return final_price

result = calculate_discount(100, 0.2)
2. Type checking
Python

def add_numbers(a, b):
    print(f"Type of a: {type(a)}")
    print(f"Type of b: {type(b)}")
    return a + b

add_numbers("5", 10)  # Reveals type mismatch
3. Breaking code into cells
Python

# Cell 1: Load data
df = pd.read_csv('data.csv')
print(df.head())

# Cell 2: Clean data
df_clean = df.dropna()
print(df_clean.shape)

# Cell 3: Transform
df_final = df_clean.apply(transform_func)
print(df_final.describe())
Benefit: Identify exactly which cell causes error

The Python Debugger (pdb)
Method 1: %debug magic
Python

def buggy_function(x):
    y = x + 10
    z = y / (x - 5)  # Error when x = 5
    return z

buggy_function(5)
Error:

text

ZeroDivisionError: division by zero
Then run:

Python

%debug
Interactive debugger opens:

text

> <ipython-input-1>(3)buggy_function()
      2     y = x + 10
----> 3     z = y / (x - 5)
      4     return z

ipdb> x
5
ipdb> y
15
ipdb> x - 5
0
ipdb> quit
Commands:

variable_name - Print variable value
n - Next line
s - Step into function
c - Continue execution
q - Quit debugger
Method 2: Automatic debugging
Python

%pdb on
Now, whenever an error occurs, debugger starts automatically.

Python

%pdb off  # Turn off
Method 3: Breakpoints
Python

def complex_function(data):
    result = []
    for item in data:
        import pdb; pdb.set_trace()  # Breakpoint
        processed = item * 2
        result.append(processed)
    return result

complex_function([1, 2, 3])
Execution pauses at breakpoint, allowing inspection.

IPython Debugger (ipdb) - Enhanced
Better than pdb with syntax highlighting and tab completion.

Install:

Python

!pip install ipdb
Use:

Python

import ipdb

def my_function(x):
    y = x * 2
    ipdb.set_trace()  # Pause here
    z = y + 10
    return z

my_function(5)
Using assert for debugging
Python

def divide(a, b):
    assert b != 0, "Divisor cannot be zero"
    assert isinstance(a, (int, float)), "a must be a number"
    assert isinstance(b, (int, float)), "b must be a number"
    return a / b

divide(10, 0)
Error:

text

AssertionError: Divisor cannot be zero
Benefits:

Self-documenting code
Catches errors early
Clear error messages
Viewing Tracebacks
Python

import traceback

try:
    result = 10 / 0
except Exception as e:
    traceback.print_exc()
Output:

text

Traceback (most recent call last):
  File "<ipython-input-1>", line 2, in <module>
    result = 10 / 0
ZeroDivisionError: division by zero
%xmode - Exception detail level
Python

%xmode Plain  # Minimal traceback
%xmode Context  # Default
%xmode Verbose  # Maximum detail
Example:

Python

%xmode Verbose

def func1():
    func2()

def func2():
    func3()

def func3():
    x = 1 / 0

func1()
Shows complete call stack with local variables.

3.5 Output Management
Displaying Multiple Outputs
Default behavior:

Python

10 + 5
20 + 5
30 + 5
Output:

text

35
Only the last expression is displayed.

Solution 1: Print all

Python

print(10 + 5)
print(20 + 5)
print(30 + 5)
Output:

text

15
25
35
Solution 2: IPython display

Python

from IPython.display import display

display(10 + 5)
display(20 + 5)
display(30 + 5)
Output:

text

15
25
35
Suppressing Output
Problem:

Python

large_dataframe = pd.read_csv('huge_file.csv')  # Displays entire DataFrame
Solution: Add semicolon

Python

large_dataframe = pd.read_csv('huge_file.csv');
# No output
Alternative:

Python

_ = large_dataframe
Rich Display System
Displaying DataFrames
Python

import pandas as pd

df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
})

df  # Displays as formatted HTML table
Displaying Images
Python

from IPython.display import Image

Image('plot.png')
Image(url='https://example.com/image.jpg')
Displaying HTML
Python

from IPython.display import HTML

HTML('<h1>Custom HTML</h1><p>With <b>formatting</b></p>')
Displaying LaTeX
Python

from IPython.display import Latex

Latex(r'$E = mc^2$')
Displaying Videos
Python

from IPython.display import Video

Video('demo.mp4')
Video('https://example.com/video.mp4', width=600)
Displaying YouTube Videos
Python

from IPython.display import YouTubeVideo

YouTubeVideo('dQw4w9WgXcQ')  # Video ID
Progress Bars
Python

from tqdm.notebook import tqdm
import time

for i in tqdm(range(100)):
    time.sleep(0.1)
Shows animated progress bar.

Clearing Output
Python

from IPython.display import clear_output
import time

for i in range(10):
    clear_output(wait=True)
    print(f"Iteration {i}")
    time.sleep(1)
Effect: Updates in place instead of printing new lines

Styling DataFrames
Python

import pandas as pd

df = pd.DataFrame({
    'Score': [85, 92, 78, 95, 88],
    'Grade': ['B', 'A', 'C', 'A', 'B']
})

def highlight_high_scores(val):
    color = 'lightgreen' if val >= 90 else 'white'
    return f'background-color: {color}'

df.style.applymap(highlight_high_scores, subset=['Score'])
Displays DataFrame with conditional formatting.

Chapter 4: Advanced Techniques
4.1 Kernel Management
What is a Kernel?
The kernel is the computational engine that:

Executes your code
Maintains variables in memory
Manages the Python environment
Think of it as the "Python session" running in the background.

Kernel States
1. Idle (○)
Kernel is ready
Not executing code
White circle indicator
2. Busy (●)
Kernel is running code
Filled circle indicator
Cannot execute new cells until finished
3. Dead/Disconnected
Kernel crashed
Connection lost
Need to restart
Kernel Operations
Interrupt Kernel
When to use:

Infinite loop running
Code taking too long
Need to stop execution
How:

Click ⏹ (stop button), OR
Kernel menu → Interrupt
Example:

Python

# Infinite loop
while True:
    print("Running...")
Click interrupt to stop.

Restart Kernel
When to use:

Clear all variables from memory
Start fresh
After installing new packages
How:

Kernel menu → Restart
Warning: All variables lost!

Python

# Before restart
x = 100

# After restart
print(x)  # NameError: name 'x' is not defined
Restart & Clear Output
Kernel → Restart & Clear Output
Effect:

Restarts kernel
Removes all cell outputs
Clean slate
Restart & Run All
Kernel → Restart & Run All
Effect:

Restarts kernel
Executes all cells from top to bottom
Use case: Testing notebook reproducibility

Reconnecting to Kernel
If you see "Disconnected" or "No kernel":

Kernel → Reconnect
If that fails → Kernel → Restart
Changing Kernels
View available kernels:

Kernel → Change Kernel
Options might include:

Python 3.9
Python 3.10
R
Julia
Conda environments
Installing new kernels:

Bash

# Create conda environment
conda create -n ml_env python=3.9

# Activate it
conda activate ml_env

# Install kernel
python -m ipykernel install --user --name ml_env --display-name "Python (ML)"
Now "Python (ML)" appears in kernel list.

Kernel Best Practices
1. Regular Restarts
Restart kernel every few hours to:

Free memory
Avoid variable conflicts
Ensure reproducibility
2. Run All Cells Periodically
text

Kernel → Restart & Run All
Ensures notebook works from top to bottom.

3. Don't Rely on Cell Order
Bad practice:

Python

# Cell 10
x = 100

# Cell 5 (run after Cell 10)
print(x)  # Works but wrong!
Why bad:

If someone runs cells top-to-bottom, Cell 5 fails
Not reproducible
Good practice:

Define variables before using them in cell order.

4.2 Extensions and Plugins
What are Jupyter Extensions?
Extensions add features to Jupyter:

Table of contents
Code folding
Variable inspector
Auto-formatting
And much more
Installing Extensions
Method 1: nbextensions (Classic Notebook)
Bash

pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
Enable configurator:

Bash

pip install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
Access:

Start Jupyter
Go to Nbextensions tab
Check boxes to enable extensions
Essential Extensions
1. Table of Contents (TOC2)
Feature:

Generates TOC from markdown headings
Clickable navigation
Floating sidebar
Enable:

Nbextensions tab → Check "Table of Contents (2)"
Usage:

Automatically appears when headings present
2. Variable Inspector
Feature:

Shows all variables in memory
Updates in real-time
Like IDE variable explorer
Enable:

Nbextensions → Variable Inspector
Usage:

Click icon in toolbar
3. ExecuteTime
Feature:

Shows when cell was run
Displays execution duration
Enable:

Nbextensions → ExecuteTime
Output example:

text

Last executed: 2024-01-15 14:32:10
Execution time: 2.3s
4. Code Folding
Feature:

Collapse function/class definitions
Clean up long notebooks
Enable:

Nbextensions → Codefolding
Usage:

Click arrow next to line numbers
5. Autopep8
Feature:

Auto-format code to PEP 8 style
Enable:

Nbextensions → Autopep8
Install dependency:

Bash

pip install autopep8
Usage:

Click hammer icon or Ctrl+L
Before:

Python

def my_func(x,y):
    return x+y
After:

Python

def my_func(x, y):
    return x + y
6. Scratchpad
Feature:

Temporary cell for testing
Doesn't save to notebook
Enable:

Nbextensions → Scratchpad
Usage:

Click icon, test code, close without saving
7. Snippets
Feature:

Insert common code patterns
Enable:

Nbextensions → Snippets
Includes:

Pandas import
Matplotlib setup
File I/O templates
8. Spellchecker
Feature:

Checks spelling in markdown cells
Enable:

Nbextensions → Spellchecker
9. Collapsible Headings
Feature:

Collapse sections under headings
Organize long notebooks
Enable:

Nbextensions → Collapsible Headings
JupyterLab Extensions (Next-Gen Interface)
What is JupyterLab?

The new interface for Jupyter (vs. Classic Notebook).

Install:

Bash

pip install jupyterlab
jupyter lab
Installing extensions:

Bash

# Git integration
jupyter labextension install @jupyterlab/git

# TOC
jupyter labextension install @jupyterlab/toc

# Variable inspector
jupyter labextension install @lckr/jupyterlab_variableinspector
Note: JupyterLab 3.0+ uses pip for extensions:

Bash

pip install jupyterlab-git
Other Useful Tools
1. RISE (Presentations)
Feature: Turn notebooks into slideshows

Install:

Bash

pip install RISE
Usage:

View → Cell Toolbar → Slideshow
Choose slide type for each cell
Click presentation icon
2. nbconvert (Exporting)
Already included, but advanced usage:

Bash

# Custom template
jupyter nbconvert --to html --template lab notebook.ipynb

# Execute before exporting
jupyter nbconvert --to html --execute notebook.ipynb
3. Papermill (Parameterized Notebooks)
Feature: Run notebooks with parameters

Install:

Bash

pip install papermill
Usage:

Tag a cell as "parameters":

Python

# Parameters
dataset = "train.csv"
epochs = 10
Run with different values:

Bash

papermill input.ipynb output.ipynb -p dataset "test.csv" -p epochs 20
4.3 Working with Multiple Languages
IPython Magic for Other Languages
R Language
Install:

Bash

conda install -c r r-irkernel
In notebook:

Python

%load_ext rpy2.ipython
Cell magic:

Python

%%R
x <- c(1, 2, 3, 4, 5)
mean(x)
Output:

text

[1] 3
Passing variables between Python and R:

Python

# Python
import numpy as np
python_array = np.array([1, 2, 3, 4, 5])
Python

%%R -i python_array -o r_result
r_result <- mean(python_array)
print(r_result)
Python

# Back to Python
print(r_result)
SQL
Install:

Bash

pip install ipython-sql
Load extension:

Python

%load_ext sql
Connect to database:

Python

%sql sqlite:///mydatabase.db
Query:

Python

%%sql
SELECT * FROM users WHERE age > 25
With Pandas:

Python

result = %sql SELECT * FROM users
df = result.DataFrame()
JavaScript
Python

%%javascript
console.log("Hello from JavaScript");
alert("This is an alert!");
Bash/Shell
Python

%%bash
echo "Current directory:"
pwd
ls -la
Multiple Kernel Notebooks
Use case: Different sections need different languages

Solution: Use separate notebooks and share data via files

Example workflow:

data_cleaning.ipynb (Python) → saves clean_data.csv
statistical_analysis.ipynb (R) → reads clean_data.csv
visualization.ipynb (Python) → creates plots
4.4 Version Control with Git
Why Version Control?
Track changes over time
Collaborate with others
Revert mistakes
Maintain multiple versions
Problem with Notebooks in Git
Issue: .ipynb files are JSON with lots of metadata

Example diff:

Diff

{
  "cells": [
    {
-     "execution_count": 42,
+     "execution_count": 43,
      "metadata": {},
Challenges:

Execution numbers change
Output changes
Metadata changes
Large diffs for small code changes
Solution 1: nbdime (Notebook Diff and Merge)
Install:

Bash

pip install nbdime
Configure Git:

Bash

nbdime config-git --enable --global
Now Git uses nbdime for:

git diff on notebooks
Merge conflicts
View diff:

Bash

git diff notebook.ipynb
Shows code changes clearly, ignoring output.

Merge tool:

Bash

nbdime mergetool
Visual interface for resolving conflicts.

Solution 2: jupytext (Notebooks as Scripts)
Install:

Bash

pip install jupytext
Pair notebook with .py file:

Bash

jupytext --set-formats ipynb,py notebook.ipynb
Effect:

notebook.ipynb - Full notebook
notebook.py - Pure Python (for Git)
Only commit .py to Git:

Bash

# .gitignore
*.ipynb
!*.py
Advantages:

Clean diffs
Easy code review
Can edit in text editor
Disadvantage:

Lose output and formatting
Solution 3: Clear Output Before Commit
Manual:

Kernel → Restart & Clear Output
Save
Commit
Automated (pre-commit hook):

Install:

Bash

pip install nbconvert
Create .git/hooks/pre-commit:

Bash

#!/bin/bash
jupyter nbconvert --clear-output --inplace **/*.ipynb
git add **/*.ipynb
Make executable:

Bash

chmod +x .git/hooks/pre-commit
Effect: Automatically clears output before every commit

Solution 4: ReviewNB (GitHub App)
What: Visual diff tool for notebooks on GitHub

Setup:

Go to https://www.reviewnb.com/
Install GitHub app
View notebook diffs visually in PRs
Shows:

Code changes side-by-side
Output changes
Markdown rendering
Best Practices for Notebooks in Git
1. Separate Code and Experiments
Structure:

text

project/
├── src/
│   ├── data_processing.py
│   ├── models.py
│   └── utils.py
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_modeling.ipynb
│   └── 03_evaluation.ipynb
└── README.md
Commit:

src/ - Always committed
notebooks/ - Optionally committed (or with cleared outputs)
2. Name Notebooks Chronologically
text

01_data_download.ipynb
02_data_cleaning.ipynb
03_exploratory_analysis.ipynb
04_feature_engineering.ipynb
05_model_training.ipynb
06_model_evaluation.ipynb
3. Add README
Markdown

# Notebooks

## Order of Execution

1. `01_data_download.ipynb` - Downloads raw data
2. `02_data_cleaning.ipynb` - Cleans and preprocesses
3. `03_exploratory_analysis.ipynb` - EDA and visualization

## Requirements

Install dependencies:
```bash
pip install -r requirements.txt
text


#### 4. Use Relative Paths

**Bad:**

```python
df = pd.read_csv('/Users/alice/projects/ml/data/train.csv')
Good:

Python

import os
project_root = os.path.dirname(os.getcwd())
data_path = os.path.join(project_root, 'data', 'train.csv')
df = pd.read_csv(data_path)
Better:

Python

from pathlib import Path
data_path = Path('../data/train.csv')
df = pd.read_csv(data_path)
Common Git Workflows
Starting a Project
Bash

# Initialize repo
git init
git add .
git commit -m "Initial commit"

# Create GitHub repo
# Add remote
git remote add origin https://github.com/username/project.git
git push -u origin main
Daily Workflow
Bash

# Start work
git pull

# Make changes in notebook

# Clear output
jupyter nbconvert --clear-output --inplace notebook.ipynb

# Stage and commit
git add notebook.ipynb
git commit -m "Add feature engineering section"

# Push
git push
Branching for Experiments
Bash

# Create branch for experiment
git checkout -b experiment/random-forest

# Work on notebook

# Commit
git add .
git commit -m "Test random forest model"

# Merge if successful
git checkout main
git merge experiment/random-forest

# Delete branch
git branch -d experiment/random-forest
4.5 Configuration and Customization
Jupyter Configuration File
Location:

Bash

# Find config directory
jupyter --config-dir

# Typical locations:
# Mac/Linux: ~/.jupyter/
# Windows: C:\Users\YourName\.jupyter\
Generate default config:

Bash

jupyter notebook --generate-config
Creates: jupyter_notebook_config.py

Useful Configuration Options
Change Default Directory
Python

# jupyter_notebook_config.py
c.NotebookApp.notebook_dir = '/path/to/your/projects'
Auto-save Interval
Python

# Save every 60 seconds (default is 120)
c.FileContentsManager.checkpoints_kwargs = {'checkpoints_interval': 60}
Disable Token/Password (Local Use Only!)
Python

c.NotebookApp.token = ''
c.NotebookApp.password = ''
Warning: Only for local, trusted environments!

Open Browser Automatically
Python

c.NotebookApp.open_browser = True  # Default
c.NotebookApp.open_browser = False  # Disable
Custom Port
Python

c.NotebookApp.port = 8889  # Instead of default 8888
Custom CSS
Location: ~/.jupyter/custom/custom.css

Example: Wider cells

CSS

.container {
    width: 99% !important;
}
Example: Custom fonts

CSS

.CodeMirror {
    font-family: 'Fira Code', monospace;
    font-size: 14px;
}
Custom Keyboard Shortcuts
Access:

Help → Edit Keyboard Shortcuts
Or edit: ~/.jupyter/nbconfig/notebook.json

JSON

{
  "keys": {
    "command": {
      "bind": {
        "ctrl-k": "jupyter-notebook:move-cell-up",
        "ctrl-j": "jupyter-notebook:move-cell-down"
      }
    }
  }
}
Startup Scripts
Location: ~/.ipython/profile_default/startup/

Any .py or .ipy file here runs on kernel start

Example: ~/.ipython/profile_default/startup/00-imports.py

Python

# Auto-import common libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Set display options
pd.set_option('display.max_columns', 100)
pd.set_option('display.max_rows', 100)

print("Standard libraries imported")
Now these run automatically in every notebook!

Jupyter Themes
Install:

Bash

pip install jupyterthemes
List themes:

Bash

jt -l
Available themes:

chesterish
grade3
gruvboxd
gruvboxl
monokai
oceans16
onedork
solarizedd
solarizedl
Apply theme:

Bash

jt -t monokai
Customize:

Bash

jt -t monokai -f fira -fs 12 -cellw 90% -T -N
Options:

-f font
-fs font size
-cellw cell width
-T toolbar visible
-N notebook name visible
Revert to default:

Bash

jt -r
Chapter 5: Machine Learning Integration
5.1 Setting Up ML Environment
Creating a Project Structure
text

ml_project/
├── data/
│   ├── raw/
│   ├── processed/
│   └── external/
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_modeling.ipynb
│   └── 04_evaluation.ipynb
├── src/
│   ├── __init__.py
│   ├── data/
│   │   ├── __init__.py
│   │   └── make_dataset.py
│   ├── features/
│   │   ├── __init__.py
│   │   └── build_features.py
│   └── models/
│       ├── __init__.py
│       ├── train_model.py
│       └── predict_model.py
├── models/
│   └── trained_models.pkl
├── reports/
│   └── figures/
├── requirements.txt
├── README.md
└── .gitignore
Essential ML Libraries
Install:

Bash

pip install numpy pandas matplotlib seaborn scikit-learn jupyter
Full ML Stack:

Bash

pip install numpy pandas matplotlib seaborn scikit-learn \
            scipy statsmodels jupyter notebook ipywidgets \
            plotly tqdm lightgbm xgboost
Deep Learning:

Bash

pip install tensorflow
# OR
pip install torch torchvision
requirements.txt:

text

numpy==1.24.0
pandas==2.0.0
matplotlib==3.7.0
seaborn==0.12.0
scikit-learn==1.2.0
jupyter==1.0.0
notebook==6.5.0
Standard Import Block
Create in every notebook:

Python

# Data manipulation
import numpy as np
import pandas as pd

# Visualization
import matplotlib.pyplot as plt
import seaborn as sns

# ML
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score, classification_report

# Settings
%matplotlib inline
plt.style.use('seaborn-v0_8-darkgrid')
sns.set_palette("husl")

# Display settings
pd.set_option('display.max_columns', 100)
pd.set_option('display.max_rows', 100)
pd.set_option('display.precision', 3)

# Suppress warnings
import warnings
warnings.filterwarnings('ignore')

# Random seed for reproducibility
np.random.seed(42)

print("Libraries imported successfully!")
5.2 Data Loading and Exploration
Loading Data
CSV Files
Python

# Basic
df = pd.read_csv('data/train.csv')

# With options
df = pd.read_csv(
    'data/train.csv',
    sep=',',
    encoding='utf-8',
    index_col=0,
    parse_dates=['date_column'],
    na_values=['?', 'NA', 'null']
)
Excel Files
Python

df = pd.read_excel('data.xlsx', sheet_name='Sheet1')
SQL Databases
Python

import sqlite3

conn = sqlite3.connect('database.db')
df = pd.read_sql_query("SELECT * FROM users", conn)
conn.close()
JSON Files
Python

df = pd.read_json('data.json')
Large Files (Chunking)
Python

chunk_size = 10000
chunks = []

for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    # Process chunk
    processed = chunk[chunk['age'] > 18]
    chunks.append(processed)

df = pd.concat(chunks, ignore_index=True)
Initial Data Exploration
Python

# Shape
print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")

# First few rows
display(df.head())

# Last few rows
display(df.tail())

# Random sample
display(df.sample(5))

# Column names
print(df.columns.tolist())

# Data types
print(df.dtypes)

# Info summary
df.info()

# Statistical summary
df.describe()

# Include all columns
df.describe(include='all')

# Missing values
print(df.isnull().sum())

# Missing percentage
missing_pct = (df.isnull().sum() / len(df)) * 100
print(missing_pct[missing_pct > 0])

# Unique values per column
df.nunique()

# Memory usage
df.memory_usage(deep=True)
Visualization for EDA
Distribution Plots
Python

# Histogram
df['age'].hist(bins=30, figsize=(10, 6))
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Age Distribution')
plt.show()

# Multiple histograms
df.hist(figsize=(15, 10), bins=20)
plt.tight_layout()
plt.show()

# Density plot
df['salary'].plot(kind='density', figsize=(10, 6))
plt.xlabel('Salary')
plt.title('Salary Distribution')
plt.show()
Box Plots
Python

# Single variable
df.boxplot(column='age', figsize=(10, 6))
plt.show()

# By category
df.boxplot(column='salary', by='department', figsize=(12, 6))
plt.show()

# Seaborn version
sns.boxplot(data=df, x='department', y='salary')
plt.xticks(rotation=45)
plt.show()
Correlation Analysis
Python

# Correlation matrix
corr = df.corr()
print(corr)

# Heatmap
plt.figure(figsize=(12, 8))
sns.heatmap(corr, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Heatmap')
plt.show()

# High correlations only
threshold = 0.5
high_corr = corr[abs(corr) > threshold]
print(high_corr)
Scatter Plots
Python

# Basic
df.plot.scatter(x='age', y='salary', figsize=(10, 6))
plt.show()

# With color by category
colors = df['department'].map({'Sales': 'red', 'IT': 'blue', 'HR': 'green'})
df.plot.scatter(x='age', y='salary', c=colors, figsize=(10, 6))
plt.show()

# Seaborn pairplot
sns.pairplot(df, hue='target')
plt.show()
Count Plots
Python

# Value counts
df['category'].value_counts().plot(kind='bar', figsize=(10, 6))
plt.xlabel('Category')
plt.ylabel('Count')
plt.title('Category Distribution')
plt.show()

# Pie chart
df['category'].value_counts().plot(kind='pie', autopct='%1.1f%%', figsize=(8, 8))
plt.ylabel('')
plt.title('Category Proportions')
plt.show()
Interactive Widgets for Exploration
Python

from ipywidgets import interact, widgets

@interact(column=df.columns)
def plot_distribution(column):
    plt.figure(figsize=(10, 6))
    df[column].hist(bins=30)
    plt.xlabel(column)
    plt.ylabel('Frequency')
    plt.title(f'Distribution of {column}')
    plt.show()
5.3 Data Preprocessing
Handling Missing Values
Identify Missing
Python

# Count
print(df.isnull().sum())

# Visualize
import missingno as mno

mno.matrix(df)
plt.show()

mno.heatmap(df)
plt.show()
Remove Missing
Python

# Drop rows with any missing values
df_clean = df.dropna()

# Drop rows where specific column is missing
df_clean = df.dropna(subset=['important_column'])

# Drop columns with missing values
df_clean = df.dropna(axis=1)

# Drop if more than N missing
df_clean = df.dropna(thresh=len(df.columns) - 2)
Impute Missing
Python

# Fill with constant
df['age'].fillna(0, inplace=True)

# Fill with mean
df['age'].fillna(df['age'].mean(), inplace=True)

# Fill with median (better for outliers)
df['salary'].fillna(df['salary'].median(), inplace=True)

# Fill with mode (categorical)
df['category'].fillna(df['category'].mode()[0], inplace=True)

# Forward fill
df['value'].fillna(method='ffill', inplace=True)

# Backward fill
df['value'].fillna(method='bfill', inplace=True)

# Interpolate (time series)
df['temperature'].interpolate(method='linear', inplace=True)
Scikit-learn Imputer
Python

from sklearn.impute import SimpleImputer

# Numerical
imputer_num = SimpleImputer(strategy='mean')
df[['age', 'salary']] = imputer_num.fit_transform(df[['age', 'salary']])

# Categorical
imputer_cat = SimpleImputer(strategy='most_frequent')
df[['category']] = imputer_cat.fit_transform(df[['category']])
Encoding Categorical Variables
Label Encoding
Python

from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
df['category_encoded'] = le.fit_transform(df['category'])

# Decode
df['category_decoded'] = le.inverse_transform(df['category_encoded'])
When to use:

Ordinal categories (Small < Medium < Large)
Tree-based models (Random Forest, XGBoost)
When NOT to use:

Nominal categories with linear models (creates false ordering)
One-Hot Encoding
Python

# Pandas
df_encoded = pd.get_dummies(df, columns=['category'])

# With prefix
df_encoded = pd.get_dummies(df, columns=['category'], prefix='cat')

# Drop first (avoid multicollinearity)
df_encoded = pd.get_dummies(df, columns=['category'], drop_first=True)

# Scikit-learn
from sklearn.preprocessing import OneHotEncoder

ohe = OneHotEncoder(sparse=False, drop='first')
encoded = ohe.fit_transform(df[['category']])
encoded_df = pd.DataFrame(
    encoded,
    columns=ohe.get_feature_names_out(['category'])
)
When to use:

Nominal categories
Linear models, neural networks
Target Encoding
Python

# Group by category and calculate mean of target
target_means = df.groupby('category')['target'].mean()
df['category_encoded'] = df['category'].map(target_means)
Caution: Risk of overfitting, use cross-validation

Feature Scaling
Standardization (Z-score normalization)
Python

from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df[['age', 'salary']] = scaler.fit_transform(df[['age', 'salary']])

# Mean = 0, Std = 1
print(df[['age', 'salary']].mean())  # Close to 0
print(df[['age', 'salary']].std())   # Close to 1
When to use:

Features have different units
Algorithm assumes normal distribution (Logistic Regression, SVM, Neural Networks)
Normalization (Min-Max Scaling)
Python

from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
df[['age', 'salary']] = scaler.fit_transform(df[['age', 'salary']])

# Range: [0, 1]
print(df[['age', 'salary']].min())  # 0
print(df[['age', 'salary']].max())  # 1
When to use:

Need bounded range
Neural networks with sigmoid/tanh activation
Image data
Robust Scaling
Python

from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()
df[['age', 'salary']] = scaler.fit_transform(df[['age', 'salary']])
When to use:

Data has outliers
Uses median and IQR instead of mean and std
Feature Engineering
Creating New Features
Python

# Mathematical combinations
df['bmi'] = df['weight'] / (df['height'] ** 2)

# Binning
df['age_group'] = pd.cut(
    df['age'],
    bins=[0, 18, 30, 50, 100],
    labels=['Child', 'Young Adult', 'Adult', 'Senior']
)

# Date features
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day_of_week'] = df['date'].dt.dayofweek
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)

# Text features
df['name_length'] = df['name'].str.len()
df['word_count'] = df['text'].str.split().str.len()

# Aggregations
df['dept_avg_salary'] = df.groupby('department')['salary'].transform('mean')
Polynomial Features
Python

from sklearn.preprocessing import PolynomialFeatures

poly = PolynomialFeatures(degree=2, include_bias=False)
poly_features = poly.fit_transform(df[['age', 'salary']])

# Creates: age, salary, age^2, age*salary, salary^2
feature_names = poly.get_feature_names_out(['age', 'salary'])
poly_df = pd.DataFrame(poly_features, columns=feature_names)
Handling Outliers
Detect Outliers
Python

# IQR method
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[(df['salary'] < lower_bound) | (df['salary'] > upper_bound)]
print(f"Number of outliers: {len(outliers)}")

# Z-score method
from scipy import stats

z_scores = np.abs(stats.zscore(df['salary']))
outliers = df[z_scores > 3]
Remove Outliers
Python

df_clean = df[(df['salary'] >= lower_bound) & (df['salary'] <= upper_bound)]
Cap Outliers
Python

df['salary'] = df['salary'].clip(lower=lower_bound, upper=upper_bound)
5.4 Model Training and Evaluation
Train-Test Split
Python

from sklearn.model_selection import train_test_split

# Prepare data
X = df.drop('target', axis=1)
y = df['target']

# Split
X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,
    random_state=42,
    stratify=y  # Maintain class distribution
)

print(f"Training set: {X_train.shape}")
print(f"Test set: {X_test.shape}")
Classification Example
Python

from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# Train model
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

# Predictions
y_pred = model.predict(X_test)

# Accuracy
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy:.3f}")

# Detailed report
print(classification_report(y_test, y_pred))

# Confusion matrix
cm = confusion_matrix(y_test, y_pred)
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Confusion Matrix')
plt.show()

# Feature importance
feature_importance = pd.DataFrame({
    'feature': X.columns,
    'importance': model.feature_importances_
}).sort_values('importance', ascending=False)

plt.figure(figsize=(10, 6))
sns.barplot(data=feature_importance.head(10), x='importance', y='feature')
plt.title('Top 10 Important Features')
plt.show()
Regression Example
Python

from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score, mean_absolute_error

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Predictions
y_pred = model.predict(X_test)

# Metrics
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
mae = mean_absolute_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"RMSE: {rmse:.3f}")
print(f"MAE: {mae:.3f}")
print(f"R² Score: {r2:.3f}")

# Residual plot
residuals = y_test - y_pred
plt.scatter(y_pred, residuals, alpha=0.5)
plt.axhline(y=0, color='r', linestyle='--')
plt.xlabel('Predicted Values')
plt.ylabel('Residuals')
plt.title('Residual Plot')
plt.show()

# Actual vs Predicted
plt.scatter(y_test, y_pred, alpha=0.5)
plt.plot([y_test.min(), y_test.max()], [y_test.min(), y_test.max()], 'r--', lw=2)
plt.xlabel('Actual')
plt.ylabel('Predicted')
plt.title('Actual vs Predicted')
plt.show()
Cross-Validation
Python

from sklearn.model_selection import cross_val_score

# 5-fold CV
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

print(f"CV Scores: {scores}")
print(f"Mean: {scores.mean():.3f}")
print(f"Std: {scores.std():.3f}")

# Visualize
plt.figure(figsize=(10, 6))
plt.bar(range(1, 6), scores)
plt.axhline(scores.mean(), color='r', linestyle='--', label='Mean')
plt.xlabel('Fold')
plt.ylabel('Accuracy')
plt.title('Cross-Validation Scores')
plt.legend()
plt.show()
Hyperparameter Tuning
Grid Search
Python

from sklearn.model_selection import GridSearchCV

# Define parameter grid
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [None, 10, 20, 30],
    'min_samples_split': [2, 5, 10]
}

# Grid search
grid_search = GridSearchCV(
    RandomForestClassifier(random_state=42),
    param_grid,
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    verbose=2
)

grid_search.fit(X_train, y_train)

# Best parameters
print(f"Best parameters: {grid_search.best_params_}")
print(f"Best score: {grid_search.best_score_:.3f}")

# Use best model
best_model = grid_search.best_estimator_
Random Search
Python

from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint

# Define parameter distributions
param_dist = {
    'n_estimators': randint(50, 500),
    'max_depth': [None, 10, 20, 30, 40, 50],
    'min_samples_split': randint(2, 20)
}

# Random search
random_search = RandomizedSearchCV(
    RandomForestClassifier(random_state=42),
    param_distributions=param_dist,
    n_iter=20,
    cv=5,
    scoring='accuracy',
    n_jobs=-1,
    random_state=42,
    verbose=2
)

random_search.fit(X_train, y_train)

print(f"Best parameters: {random_search.best_params_}")
print(f"Best score: {random_search.best_score_:.3f}")
Saving and Loading Models
Python

import joblib

# Save model
joblib.dump(model, 'models/random_forest_model.pkl')

# Load model
loaded_model = joblib.load('models/random_forest_model.pkl')

# Use loaded model
predictions = loaded_model.predict(X_test)
Progress Tracking with tqdm
Python

from tqdm.notebook import tqdm

results = []

for n_estimators in tqdm([50, 100, 200, 500], desc="Training models"):
    model = RandomForestClassifier(n_estimators=n_estimators, random_state=42)
    model.fit(X_train, y_train)
    score = model.score(X_test, y_test)
    results.append({'n_estimators': n_estimators, 'accuracy': score})

results_df = pd.DataFrame(results)
print(results_df)
5.5 Visualization Best Practices
Matplotlib Customization
Python

# Set default figure size
plt.rcParams['figure.figsize'] = (12, 6)

# Set default DPI
plt.rcParams['figure.dpi'] = 100

# Set font sizes
plt.rcParams['font.size'] = 12
plt.rcParams['axes.labelsize'] = 14
plt.rcParams['axes.titlesize'] = 16
plt.rcParams['xtick.labelsize'] = 12
plt.rcParams['ytick.labelsize'] = 12
plt.rcParams['legend.fontsize'] = 12

# Set style
plt.style.use('seaborn-v0_8-darkgrid')
Creating Publication-Quality Plots
Python

fig, ax = plt.subplots(figsize=(10, 6))

# Plot
ax.plot(x, y1, label='Model 1', linewidth=2, marker='o')
ax.plot(x, y2, label='Model 2', linewidth=2, marker='s')

# Labels
ax.set_xlabel('Epochs', fontsize=14)
ax.set_ylabel('Accuracy', fontsize=14)
ax.set_title('Model Comparison', fontsize=16, fontweight='bold')

# Grid
ax.grid(True, alpha=0.3)

# Legend
ax.legend(loc='best', frameon=True, shadow=True)

# Tight layout
plt.tight_layout()

# Save
plt.savefig('reports/figures/model_comparison.png', dpi=300, bbox_inches='tight')

plt.show()
Subplots
Python

fig, axes = plt.subplots(2, 2, figsize=(15, 10))

# Plot 1
axes[0, 0].hist(df['age'], bins=30)
axes[0, 0].set_title('Age Distribution')

# Plot 2
axes[0, 1].scatter(df['age'], df['salary'])
axes[0, 1].set_title('Age vs Salary')

# Plot 3
df['category'].value_counts().plot(kind='bar', ax=axes[1, 0])
axes[1, 0].set_title('Category Counts')

# Plot 4
axes[1, 1].boxplot([df['salary'][df['category'] == cat] for cat in df['category'].unique()])
axes[1, 1].set_title('Salary by Category')

plt.tight_layout()
plt.show()
Interactive Plots with Plotly
Python

import plotly.express as px

# Interactive scatter
fig = px.scatter(
    df,
    x='age',
    y='salary',
    color='category',
    size='experience',
    hover_data=['name'],
    title='Interactive Scatter Plot'
)
fig.show()

# Interactive line plot
fig = px.line(
    df,
    x='date',
    y='value',
    title='Time Series'
)
fig.show()

# Interactive histogram
fig = px.histogram(
    df,
    x='salary',
    nbins=30,
    title='Salary Distribution'
)
fig.show()
Chapter 6: Professional Best Practices
6.1 Notebook Organization
Notebook Structure Template
Markdown

# Project Title

**Author:** Your Name  
**Date:** 2024-01-15  
**Objective:** Brief description of what this notebook does

---

## Table of Contents
1. [Setup](#setup)
2. [Data Loading](#data-loading)
3. [Exploratory Data Analysis](#eda)
4. [Data Preprocessing](#preprocessing)
5. [Model Training](#training)
6. [Evaluation](#evaluation)
7. [Conclusions](#conclusions)

---

## 1. Setup <a name="setup"></a>

### Import Libraries
```python
# Standard imports
import numpy as np
import pandas as pd
...
Configuration
Python

# Random seed
np.random.seed(42)

# Display settings
pd.set_option('display.max_columns', 100)
2. Data Loading <a name="data-loading"></a>
Python

df = pd.read_csv('data/train.csv')
[Continue with other sections...]

7. Conclusions <a name="conclusions"></a>
Key Findings
Finding 1
Finding 2
Next Steps
Step 1
Step 2
text


---

### Cell Organization

#### 1. One Task Per Cell

**Bad:**

```python
df = pd.read_csv('data.csv')
df = df.dropna()
df['new_col'] = df['a'] + df['b']
X = df.drop('target', axis=1)
y = df['target']
model = RandomForestClassifier()
model.fit(X, y)
Good:

Python

# Cell 1: Load data
df = pd.read_csv('data.csv')
Python

# Cell 2: Clean data
df = df.dropna()
Python

# Cell 3: Feature engineering
df['new_col'] = df['a'] + df['b']
Python

# Cell 4: Prepare features
X = df.drop('target', axis=1)
y = df['target']
Python

# Cell 5: Train model
model = RandomForestClassifier()
model.fit(X, y)
2. Use Clear Section Headers
Markdown

# Data Preprocessing
Markdown

## Handling Missing Values
Markdown

### Imputation Strategy
3. Comment Complex Code
Python

# Calculate weighted average of predictions
# Weight each model by its cross-validation score
weighted_pred = (
    cv_scores[0] * model1_pred +
    cv_scores[1] * model2_pred +
    cv_scores[2] * model3_pred
) / cv_scores.sum()
6.2 Code Quality
PEP 8 Style Guide
Variable Naming
Python

# Bad
x = 10
df1 = pd.read_csv('data.csv')
m = RandomForestClassifier()

# Good
customer_count = 10
customer_df = pd.read_csv('customer_data.csv')
rf_model = RandomForestClassifier()
Function Naming
Python

# Bad
def f(x):
    return x * 2

# Good
def double_value(number):
    """
    Doubles the input number.
    
    Args:
        number (int/float): The number to double
        
    Returns:
        int/float: The doubled value
    """
    return number * 2
Constants
Python

# Use uppercase
MAX_ITERATIONS = 1000
LEARNING_RATE = 0.01
DATA_PATH = 'data/train.csv'
Whitespace
Python

# Bad
x=5+3
if x>10:print(x)

# Good
x = 5 + 3
if x > 10:
    print(x)
Docstrings
Python

def train_model(X_train, y_train, model_type='rf', **kwargs):
    """
    Train a machine learning model.
    
    This function supports multiple model types and allows
    custom hyperparameters through keyword arguments.
    
    Parameters
    ----------
    X_train : pd.DataFrame or np.ndarray
        Training features
    y_train : pd.Series or np.ndarray
        Training labels
    model_type : str, default='rf'
        Type of model to train. Options: 'rf', 'lr', 'svm'
    **kwargs : dict
        Model-specific hyperparameters
        
    Returns
    -------
    model : object
        Trained scikit-learn model
        
    Examples
    --------
    >>> model = train_model(X_train, y_train, model_type='rf', n_estimators=100)
    >>> predictions = model.predict(X_test)
    
    Notes
    -----
    For best results, ensure data is preprocessed before training.
    """
    if model_type == 'rf':
        from sklearn.ensemble import RandomForestClassifier
        model = RandomForestClassifier(**kwargs)
    elif model_type == 'lr':
        from sklearn.linear_model import LogisticRegression
        model = LogisticRegression(**kwargs)
    else:
        raise ValueError(f"Unknown model type: {model_type}")
    
    model.fit(X_train, y_train)
    return model
Error Handling
Python

# Bad
df = pd.read_csv('data.csv')

# Good
try:
    df = pd.read_csv('data.csv')
except FileNotFoundError:
    print("Error: data.csv not found")
    print("Please ensure the file exists in the data/ directory")
except pd.errors.EmptyDataError:
    print("Error: data.csv is empty")
except Exception as e:
    print(f"Unexpected error: {e}")
Type Hints
Python

from typing import List, Tuple, Dict, Optional
import pandas as pd
import numpy as np

def preprocess_data(
    df: pd.DataFrame,
    numerical_cols: List[str],
    categorical_cols: List[str],
    target_col: str
) -> Tuple[np.ndarray, np.ndarray]:
    """
    Preprocess DataFrame for machine learning.
    
    Args:
        df: Input DataFrame
        numerical_cols: List of numerical column names
        categorical_cols: List of categorical column names
        target_col: Name of target column
        
    Returns:
        Tuple of (X, y) as numpy arrays
    """
    X = df[numerical_cols + categorical_cols]
    y = df[target_col]
    
    return X.values, y.values
6.3 Reproducibility
Setting Random Seeds
Python

import random
import numpy as np

# Python built-in random
random.seed(42)

# NumPy
np.random.seed(42)

# Scikit-learn (use random_state parameter)
from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier(random_state=42)

# TensorFlow
import tensorflow as tf
tf.random.set_seed(42)

# PyTorch
import torch
torch.manual_seed(42)
Environment Documentation
requirements.txt:

text

numpy==1.24.0
pandas==2.0.0
scikit-learn==1.2.0
matplotlib==3.7.0
seaborn==0.12.0
jupyter==1.0.0
Generate from current environment:

Bash

pip freeze > requirements.txt
Or use conda:

Bash

conda env export > environment.yml
Documenting Data Sources
Markdown

## Data Sources

### Training Data
- **File:** `data/train.csv`
- **Source:** Kaggle Competition XYZ
- **Download Date:** 2024-01-15
- **URL:** https://www.kaggle.com/datasets/xyz
- **Size:** 100,000 rows, 50 columns
- **License:** CC BY-SA 4.0

### External Data
- **File:** `data/external/demographics.csv`
- **Source:** US Census Bureau
- **Date:** 2020
- **URL:** https://census.gov/data/...
Recording Experiment Results
Python

import json
from datetime import datetime

# Record experiment
experiment = {
    'timestamp': datetime.now().isoformat(),
    'model': 'RandomForestClassifier',
    'hyperparameters': {
        'n_estimators': 100,
        'max_depth': 10,
        'random_state': 42
    },
    'data': {
        'train_size': len(X_train),
        'test_size': len(X_test),
        'features': X_train.shape[1]
    },
    'results': {
        'accuracy': 0.95,
        'f1_score': 0.93,
        'precision': 0.94,
        'recall': 0.92
    }
}

# Save to file
with open('experiments/experiment_001.json', 'w') as f:
    json.dump(experiment, f, indent=2)
6.4 Performance Optimization
Profiling Code
Time Profiling
Python

%%time
# Time single execution
df = pd.read_csv('large_file.csv')
Python

%%timeit
# Time multiple executions (average)
df['new_col'] = df['a'] + df['b']
Line Profiler
Install:

Bash

pip install line_profiler
Use:

Python

%load_ext line_profiler

def slow_function():
    result = []
    for i in range(10000):
        result.append(i ** 2)
    return result

%lprun -f slow_function slow_function()
Output shows time per line

Memory Profiler
Install:

Bash

pip install memory_profiler
Use:

Python

%load_ext memory_profiler

%memit df = pd.read_csv('large_file.csv')
Optimizing Pandas Operations
Use Vectorization
Python

# Bad (slow)
df['new_col'] = df.apply(lambda row: row['a'] + row['b'], axis=1)

# Good (fast)
df['new_col'] = df['a'] + df['b']
Avoid Iterating Rows
Python

# Bad (very slow)
for index, row in df.iterrows():
    df.at[index, 'new_col'] = row['a'] + row['b']

# Good
df['new_col'] = df['a'] + df['b']
Use Appropriate Data Types
Python

# Check memory usage
print(df.memory_usage(deep=True))

# Optimize dtypes
df['age'] = df['age'].astype('int8')  # If age < 128
df['category'] = df['category'].astype('category')  # For categorical data

# Downcast numerics
df['price'] = pd.to_numeric(df['price'], downcast='float')
Use Chunking for Large Files
Python

chunk_size = 10000
results = []

for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    processed = process_chunk(chunk)
    results.append(processed)

final_df = pd.concat(results, ignore_index=True)
Parallel Processing
Python

from joblib import Parallel, delayed

def process_item(item):
    # Heavy computation
    return item ** 2

# Sequential
results = [process_item(i) for i in range(1000)]

# Parallel
results = Parallel(n_jobs=-1)(delayed(process_item)(i) for i in range(1000))
Using GPU Acceleration
CuPy (NumPy on GPU)
Python

import cupy as cp

# CPU
x_cpu = np.random.rand(1000, 1000)
y_cpu = np.random.rand(1000, 1000)
%timeit np.dot(x_cpu, y_cpu)

# GPU
x_gpu = cp.random.rand(1000, 1000)
y_gpu = cp.random.rand(1000, 1000)
%timeit cp.dot(x_gpu, y_gpu)
RAPIDS (Pandas on GPU)
Python

import cudf

# CPU
df_cpu = pd.read_csv('large_file.csv')
%timeit df_cpu.groupby('category').mean()

# GPU
df_gpu = cudf.read_csv('large_file.csv')
%timeit df_gpu.groupby('category').mean()
6.5 Collaboration
Shared Notebook Platforms
1. Google Colab
Advantages:

Free GPU/TPU
No setup required
Easy sharing (like Google Docs)
Real-time collaboration
Share:

Click "Share" button
Set permissions
Send link
2. JupyterHub
What: Multi-user Jupyter server

Use case: Team sharing computational resources

3. Binder
What: Turn GitHub repo into interactive notebooks

Setup:

Push notebook to GitHub
Go to https://mybinder.org
Enter GitHub repo URL
Get shareable link
4. Kaggle Kernels
Advantages:

Free GPU
Datasets integrated
Public/private notebooks
Community
Notebook Reviews
Code Review Checklist
 Clear markdown documentation
 Code follows PEP 8
 No hardcoded paths
 Random seeds set
 Results reproducible
 Outputs cleared (or meaningful)
 Large outputs removed
 Visualizations have titles/labels
 Complex logic explained
 No sensitive data exposed
Using ReviewNB
Install ReviewNB GitHub app
Open Pull Request with notebook changes
Review shows visual diffs
Comment on specific cells
Approve/request changes
Pair Programming in Notebooks
Tools:

Colab: Built-in collaboration
VS Code Live Share: Real-time editing
JupyterLab Real-Time Collaboration: Extension for shared editing
Best Practices:

Use video call for communication
Driver-navigator pattern
Switch roles frequently
Commit often
Chapter 7: Troubleshooting & Optimization
7.1 Common Issues and Solutions
Issue 1: Kernel Crashes
Symptoms:

Kernel disconnected message
Cells stuck on "running"
Browser becomes unresponsive
Causes & Solutions:

Out of Memory
Python

# Check memory usage
import psutil
print(f"Memory usage: {psutil.virtual_memory().percent}%")

# Solution: Clear large variables
del large_dataframe
import gc
gc.collect()

# Use chunking
for chunk in pd.read_csv('file.csv', chunksize=10000):
    process(chunk)
Infinite Loop
Python

# Always have exit condition
max_iterations = 1000
count = 0
while condition and count < max_iterations:
    # Your code
    count += 1
Memory Leak
Python

# Bad
results = []
for i in range(1000000):
    results.append(expensive_operation(i))

# Good
def process_batch(batch):
    # Process and yield
    for item in batch:
        yield expensive_operation(item)

for result in process_batch(range(1000000)):
    handle(result)
Issue 2: ModuleNotFoundError
Error:

text

ModuleNotFoundError: No module named 'pandas'
Solutions:

Python

# Install in notebook
!pip install pandas

# Check which Python
!which python

# Check installed packages
!pip list

# Verify kernel
import sys
print(sys.executable)
If using conda:

Bash

# Install in correct environment
conda activate my_env
conda install pandas

# Add kernel
python -m ipykernel install --user --name my_env
Issue 3: Cells Out of Order
Problem:

Variables undefined when running top-to-bottom
Results not reproducible
Solution:

Python

# Always test
Kernel → Restart & Run All

# If fails, fix order
Prevention:

Define before use
Number notebooks: 01_, 02_, etc.
Use functions to avoid order dependency
Issue 4: Notebook Won't Load
Symptoms:

500 error
Loading forever
Corrupt file
Solutions:

Repair corrupt notebook
Bash

# Install nbformat
pip install nbformat

# Try to repair
python -c "import nbformat; nbformat.read('notebook.ipynb', as_version=4)"
Recover from checkpoint
Bash

ls .ipynb_checkpoints/
cp .ipynb_checkpoints/notebook-checkpoint.ipynb notebook.ipynb
View as JSON
Bash

cat notebook.ipynb
Look for syntax errors, fix manually.

Issue 5: Plots Not Showing
Solutions:

Python

# Ensure matplotlib inline
%matplotlib inline

# Re-import
import matplotlib.pyplot as plt

# Explicit show
plt.plot([1, 2, 3])
plt.show()

# Check backend
import matplotlib
print(matplotlib.get_backend())

# Change backend
%matplotlib notebook  # Interactive
%matplotlib inline    # Static
Issue 6: Slow Performance
Diagnose:

Python

%%time
# Your code here
Solutions:

Python

# Use vectorization
df['new'] = df['a'] + df['b']  # Not apply()

# Use query for filtering
df.query('age > 25 and salary > 50000')  # Faster than boolean indexing on large data

# Use categorical dtype
df['category'] = df['category'].astype('category')

# Parallel processing
from joblib import Parallel, delayed
results = Parallel(n_jobs=-1)(delayed(func)(i) for i in range(n))
Issue 7: Can't Connect to Kernel
Solutions:

Bash

# Check running notebooks
jupyter notebook list

# Kill specific server
jupyter notebook stop 8888

# Kill all
pkill -f jupyter

# Restart with clean slate
jupyter notebook --no-browser --port=8889
Issue 8: Version Conflicts
Error:

text

ImportError: cannot import name 'soft_unicode' from 'markupsafe'
Solutions:

Bash

# Create clean environment
conda create -n clean_env python=3.9
conda activate clean_env
pip install jupyter numpy pandas scikit-learn

# Or use venv
python -m venv clean_venv
source clean_venv/bin/activate
pip install jupyter numpy pandas scikit-learn
7.2 Advanced Tips & Tricks
Custom Magic Commands
Python

from IPython.core.magic import register_line_magic

@register_line_magic
def timemem(line):
    """Time and measure memory of code"""
    import time
    import tracemalloc
    
    tracemalloc.start()
    start_time = time.time()
    
    exec(line)
    
    current, peak = tracemalloc.get_traced_memory()
    elapsed = time.time() - start_time
    
    print(f"Time: {elapsed:.3f}s")
    print(f"Memory: {peak / 1024 / 1024:.2f} MB")
    
    tracemalloc.stop()

# Usage
%timemem df = pd.read_csv('large_file.csv')
Watermarking (Track Environment)
Python

# Install
!pip install watermark

# Usage
%load_ext watermark
%watermark -v -m -p numpy,pandas,sklearn -g -iv
Output:

text

Python 3.9.7
numpy: 1.24.0
pandas: 2.0.0
sklearn: 1.2.0
Git hash: abc123...
Auto-reload Modules
Python

%load_ext autoreload
%autoreload 2

# Now changes to .py files are auto-loaded
from mymodule import myfunction
Use case:

Developing package while testing in notebook
No need to restart kernel after editing source
Multi-cursor Editing
In Jupyter:

Hold Alt (Windows) or Option (Mac)
Click to create multiple cursors
Type to edit all at once
Or:

Select text
Press Ctrl+D (or Cmd+D) to select next occurrence
Edit all occurrences
Collapse All Cells
JavaScript

%%javascript
// Collapse all code cells
IPython.notebook.get_cells().forEach(function(cell) {
    if (cell.cell_type == 'code') {
        cell.collapse_output();
    }
});
Automatic Table of Contents
Python

%%html
<style>
#toc_container {
    background: #f9f9f9 none repeat scroll 0 0;
    border: 1px solid #aaa;
    display: table;
    font-size: 95%;
    margin-bottom: 1em;
    padding: 20px;
    width: auto;
}
</style>

<div id="toc_container">
<p class="toc_title">Contents</p>
<ul class="toc_list">
  <li><a href="#section1">1. Introduction</a></li>
  <li><a href="#section2">2. Data Loading</a></li>
  <li><a href="#section3">3. Analysis</a></li>
</ul>
</div>
Hide/Show Code
Python

%%html
<script>
code_show=true;
function code_toggle() {
    if (code_show){
        $('div.input').hide();
    } else {
        $('div.input').show();
    }
    code_show = !code_show
}
$( document ).ready(code_toggle);
</script>
<form action="javascript:code_toggle()">
    <input type="submit" value="Toggle Code">
</form>
Suppress Warnings
Python

import warnings
warnings.filterwarnings('ignore')

# Or specific warnings
warnings.filterwarnings('ignore', category=FutureWarning)
Run System Commands
Python

# Get output
files = !ls -la
print(files)

# Use Python variables
folder = "data"
!ls {folder}

# Chain commands
!cd data && ls | grep csv
Debugging with pdb
Python

def buggy_function(x, y):
    result = x + y
    import pdb; pdb.set_trace()  # Breakpoint
    return result * 2

buggy_function(5, 10)
pdb commands:

n - next line
c - continue
s - step into function
p variable - print variable
l - show code context
q - quit
Display Multiple DataFrames Side-by-Side
Python

from IPython.display import display_html

def display_side_by_side(*dfs, names=[]):
    html_str = ''
    if names:
        html_str += ('<tr>' + 
                     ''.join(f'<th style="text-align:center"><h3>{name}</h3></th>' 
                             for name in names) + 
                     '</tr>')
    html_str += ('<tr>' + 
                 ''.join(f'<td style="vertical-align:top">{df.to_html()}</td>' 
                         for df in dfs) + 
                 '</tr>')
    html_str = f'<table>{html_str}</table>'
    display_html(html_str, raw=True)

# Usage
display_side_by_side(df1, df2, df3, names=['Training', 'Validation', 'Test'])
Benchmark Multiple Approaches
Python

import timeit

def method1():
    return sum([x**2 for x in range(1000)])

def method2():
    return sum(x**2 for x in range(1000))

def method3():
    import numpy as np
    return np.sum(np.arange(1000)**2)

# Benchmark
results = {}
for name, func in [('List Comp', method1), ('Generator', method2), ('NumPy', method3)]:
    time = timeit.timeit(func, number=1000)
    results[name] = time

# Display
import pandas as pd
pd.DataFrame(results.items(), columns=['Method', 'Time (s)']).sort_values('Time (s)')
7.3 Keyboard Shortcuts Reference
Command Mode (Press Esc)
Shortcut	Action
Enter	Enter edit mode
A	Insert cell above
B	Insert cell below
M	Change to Markdown
Y	Change to Code
D, D	Delete cell
Z	Undo cell deletion
Shift + M	Merge cells
Ctrl + Shift + -	Split cell
↑/↓	Navigate cells
Shift + ↑/↓	Select multiple cells
Shift + J/K	Select cells (Vim-style)
C	Copy cell
X	Cut cell
V	Paste below
Shift + V	Paste above
I, I	Interrupt kernel
0, 0	Restart kernel
Space	Scroll down
Shift + Space	Scroll up
H	Show shortcuts
Edit Mode (Press Enter)
Shortcut	Action
Esc	Enter command mode
Tab	Code completion
Shift + Tab	Tooltip
Ctrl + ]	Indent
Ctrl + [	Dedent
Ctrl + A	Select all
Ctrl + Z	Undo
Ctrl + Y	Redo
Ctrl + Home	Go to cell start
Ctrl + End	Go to cell end
Ctrl + Left/Right	Move word
Ctrl + /	Toggle comment
Universal
Shortcut	Action
Shift + Enter	Run and select next
Ctrl + Enter	Run cell
Alt + Enter	Run and insert below
Ctrl + S	Save
7.4 Resources for Further Learning
Official Documentation
Jupyter Notebook: https://jupyter-notebook.readthedocs.io/
JupyterLab: https://jupyterlab.readthedocs.io/
IPython: https://ipython.readthedocs.io/
Tutorials
Jupyter Official Tutorial: https://jupyter.org/try
DataCamp: Jupyter Notebook Tutorial
Real Python: Jupyter Notebook Guide
Corey Schafer (YouTube): Jupyter Notebook Series
Books
"IPython Interactive Computing and Visualization Cookbook" by Cyrille Rossant
"Python Data Science Handbook" by Jake VanderPlas (Notebooks available on GitHub)
Communities
Stack Overflow: Tag jupyter-notebook
Jupyter Discourse: https://discourse.jupyter.org/
Reddit: r/JupyterNotebook
GitHub Discussions: https://github.com/jupyter/notebook/discussions
Awesome Lists
Awesome Jupyter: https://github.com/markusschanta/awesome-jupyter
Awesome JupyterLab: https://github.com/mauhai/awesome-jupyterlab
7.5 Final Project Template
Complete ML Project Notebook
Markdown

# [Project Name]: [Brief Description]

**Author:** [Your Name]  
**Email:** [your.email@example.com]  
**Date:** 2024-01-15  
**Last Updated:** 2024-01-15

---

## Executive Summary

[2-3 sentences describing the project, goal, and key findings]

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Setup](#2-setup)
3. [Data Loading](#3-data-loading)
4. [Exploratory Data Analysis](#4-exploratory-data-analysis)
5. [Data Preprocessing](#5-data-preprocessing)
6. [Feature Engineering](#6-feature-engineering)
7. [Model Training](#7-model-training)
8. [Model Evaluation](#8-model-evaluation)
9. [Conclusions and Next Steps](#9-conclusions-and-next-steps)
10. [References](#10-references)

---

## 1. Introduction

### 1.1 Business Problem

[Describe the problem you're solving]

### 1.2 Objectives

- Objective 1
- Objective 2
- Objective 3

### 1.3 Success Metrics

- Metric 1: Target value
- Metric 2: Target value

---

## 2. Setup

### 2.1 Import Libraries
```python
# [Import code]
2.2 Configuration
Python

# [Configuration code]
2.3 Helper Functions
Python

# [Utility functions]
3. Data Loading
3.1 Data Sources
Dataset 1: [Description, source, date]
Dataset 2: [Description, source, date]
3.2 Load Data
Python

# [Loading code]
3.3 Initial Inspection
Python

# [Inspection code]
Key Observations:

Observation 1
Observation 2
4. Exploratory Data Analysis
4.1 Data Structure
[Analysis and visualizations]

4.2 Univariate Analysis
[Distributions of individual variables]

4.3 Bivariate Analysis
[Relationships between variables]

4.4 Multivariate Analysis
[Complex interactions]

4.5 Key Findings
Finding 1
Finding 2
5. Data Preprocessing
5.1 Missing Values
[Strategy and implementation]

5.2 Outliers
[Detection and handling]

5.3 Encoding
[Categorical variable encoding]

5.4 Scaling
[Feature scaling]

6. Feature Engineering
6.1 New Features
[Created features and rationale]

6.2 Feature Selection
[Selection process and results]

7. Model Training
7.1 Train-Test Split
Python

# [Split code]
7.2 Baseline Model
[Simple model for comparison]

7.3 Model Selection
[Testing multiple models]

7.4 Hyperparameter Tuning
[Optimization process]

7.5 Final Model
[Best model and parameters]

8. Model Evaluation
8.1 Performance Metrics
[Detailed metrics]

8.2 Visualization
[ROC curves, confusion matrices, etc.]

8.3 Feature Importance
[Important features]

8.4 Error Analysis
[Where model fails]

9. Conclusions and Next Steps
9.1 Summary
[Key results]

9.2 Recommendations
Recommendation 1
Recommendation 2
9.3 Limitations
Limitation 1
Limitation 2
9.4 Future Work
Next step 1
Next step 2
10. References
Reference 1
Reference 2
Appendix
A. Additional Visualizations
[Supplementary plots]

B. Code Utilities
[Helper functions]

C. Environment
Python

%watermark -v -m -p numpy,pandas,sklearn
text


---

# Conclusion

Congratulations! You've completed the **Jupyter Notebook Masterclass**.

## Your Journey

You've learned:

1. ✅ **Basics**: Installation, interface, cells, modes
2. ✅ **Operations**: Shortcuts, magic commands, shell integration
3. ✅ **Intermediate**: Markdown, debugging, extensions
4. ✅ **Advanced**: Version control, configuration, multiple languages
5. ✅ **ML Integration**: Complete data science workflow
6. ✅ **Professional**: Best practices, collaboration, optimization
7. ✅ **Troubleshooting**: Common issues and solutions

## Next Steps

1. **Practice**: Create your own ML project
2. **Contribute**: Share notebooks on GitHub
3. **Teach**: Help others learn
4. **Explore**: Try JupyterLab, extensions, new tools
5. **Stay Updated**: Follow Jupyter blog and community

## Final Tips

- **Start Simple**: Don't overcomplicate early notebooks
- **Document Everything**: Future you will thank present you
- **Iterate**: First version doesn't need to be perfect
- **Share**: Get feedback from community
- **Keep Learning**: ML and tools evolve constantly

---

## Acknowledgments

Thank you for dedicating your time to learn Jupyter Notebook. This tool will be your companion throughout your ML career. Use it wisely, share generously, and keep exploring!

**Happy Coding! 🚀**

---

*This comprehensive guide is designed to be read once and understood completely. If any section is unclear, please revisit it or seek clarification from the Jupyter community.*

**Version:** 1.0  
**Last Updated:** 2024-01-15  
**Author:** Your Professor with 15 years of teaching experience

---