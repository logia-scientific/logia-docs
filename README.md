Website and documentation for Logia.


- The **`logia.py`** file is a program in **Python with PyQt5 + Matplotlib + NumPy**, which creates a graphical application to **define mathematical functions and - draw interactive scientific plots**. I will explain step by step and comment on the main blocks of the code:

---

## 🔹 General Structure

* Uses **PyQt5** to create the graphical interface (menus, buttons, text boxes, etc.).
* Uses **Matplotlib** to draw the plots inside the window.
* Allows you to:

  * Write mathematical functions in text boxes (e.g., `sin(x)`, `x**2 + 5*x`).
  * Add/remove multiple functions.
  * Adjust **axis limits (X/Y)**.
  * Choose **linear or logarithmic scale**.
  * Show/hide **grid**, **legend**, and adjust curve style.
  * Customize **line, markers, and thickness**.

---

## 🔹 Main Classes and Functions

### 1. **Class `LogiaUI(QMainWindow)`**

This is the main application window.

* **Constructor `__init__`:**

  * Sets the window title and icon.
  * Creates the interface (`initUI()`).
  * Applies the stylesheet (`apply_stylesheet()`).
  * Adjusts window size and displays it.
  * Generates an initial plot (`plot_functions()`).

---

### 2. **`initUI()` – Graphical Interface**

* Creates the **central widget** with `QHBoxLayout` (left = control panel, right = plot area).

#### Side Panel (left)

* **Mathematical functions**:

  * Group box "Function Definitions".
  * `QScrollArea` to allow adding multiple functions.
  * Each entry is a `QLineEdit` + "X" button (remove).
* **Main buttons**:

  * "Add New Function Input" → adds a new function.
  * "Generate Plot from Functions" → draws the plot.
* **Global plot settings**:

  * Axis range (`QDoubleSpinBox` for Xmin/Xmax/Ymin/Ymax).
  * Visualization options (grid, legend, auto layout).
  * Curve customization (line type, width, marker).
  * Axis scale (linear or logarithmic).

#### Plot Area (right)

* A **`matplotlib Figure + Axes`** inserted via `FigureCanvasQTAgg`.
* Toolbar (`NavigationToolbar2QT`).
* Dark theme applied (background and grid colors).

---

### 3. **`apply_stylesheet()`**

Defines the **stylesheet (Qt CSS)**:

* Dark background.
* Blue buttons with hover effect.
* Text boxes styled like a terminal (`Consolas`, green for functions).
* Styled checkboxes, group boxes, and spinboxes.
* Modern and consistent appearance.

---

### 4. **Functions to manage inputs**

* **`add_function_entry()`** → creates a new line with `QLineEdit` + remove button.
* **`remove_function_entry()`** → deletes the chosen entry.

---

### 5. **`plot_functions()` – Drawing the plot**

* Clears the plot (`self.ax.clear()`).
* Reapplies dark style and axis settings.
* Checks limits (does not allow `Xmin >= Xmax`).
* Checks logarithmic scales (values must be > 0).
* Creates vector `x` with `np.linspace(x_start, x_end, 500)`.
* For each function:

  * Uses `eval()` with NumPy (`sin`, `cos`, etc.).
  * Plots the curve with chosen color, style, and marker.
  * If there’s an error → shows message in the title.
* Displays legend if enabled.
* Updates canvas (`self.canvas.draw()`).

---

### 6. **`clear_plots()`**

* Clears all plots.
* Restores initial configuration.
* Removes extra functions and clears inputs.

---

### 7. **`closeEvent()`**

* Properly closes the window and Matplotlib figure.

---

### 8. **Program Execution**

```python
if __name__ == '__main__':
    app = QApplication(sys.argv)
    logia_ui = LogiaUI()
    sys.exit(app.exec_())
```

This starts the Qt application.

---

# 📘 User Manual – Logia Scientific Software

## 🖥️ Introduction

**Logia Scientific Software** is a Python application (PyQt5 + Matplotlib) that allows you to **define mathematical functions and visualize their plots** interactively.

It works like a lightweight scientific visualization tool, similar to MATLAB or Mathematica.

---

## 🚀 How to Start

1. Make sure you have Python 3 installed on Windows, Linux, or Mac.
2. Install the required libraries:

   ```bash
   pip install pyqt5 matplotlib numpy
   ```
3. Run the program:

   ```bash
   python logia.py
   ```
4. The application will open with:

   * A **control panel** on the left.
   * A **plotting area** on the right.

---

## ✍️ Entering Functions

* Each function must be written in a **text field** on the left panel.
* Examples:

  * `sin(x)` → sine of x
  * `x**2 + 5*x` → quadratic polynomial
  * `pi * cos(x)` → cosine multiplied by pi
* Use **Python + NumPy expressions** (`sin`, `cos`, `exp`, `log`, etc.).
* You can add multiple functions:

  * Click **“Add Function”**.
  * To remove one, click the **X button** next to it.

---

## 📊 Plot Controls

The left panel contains multiple sections for customization.

### 🔹 Axis Ranges

* **X-min, X-max, Y-min, Y-max** → define axis limits.
* Invalid values (Xmin ≥ Xmax) will trigger an error message.

### 🔹 Display Options

* **Show Major Grid** → toggle major grid lines.
* **Show Minor Grid** → toggle minor grid lines.
* **Show Legend** → display legend with function formulas.
* **Auto Layout Adjust** → automatically adjust plot margins.

### 🔹 Curve Customization

* **Line Style** → solid, dashed, dotted, etc.
* **Line Width** → thickness of the curve.
* **Marker Style** → markers (circle, star, cross, etc.).
* **Marker Size** → size of markers.

### 🔹 Axis Scaling

* **X-axis Scale** → Linear or Logarithmic.
* **Y-axis Scale** → Linear or Logarithmic.
  ⚠️ Logarithmic scales only accept positive values.

---

## 🛠️ Main Actions

* **Add Function** → add a new function input field.
* **Generate Plot** → draw or update the plot with defined functions.
* **X (next to each function)** → remove that function input.

---

## 🎨 Plot Area

* Located on the right side of the window.
* Displays all defined functions.
* Includes Matplotlib toolbar for:

  * **Zooming**,
  * **Panning**,
  * **Saving the plot** as a PNG image.

---

## ⚠️ Error Messages

* **“Error: Invalid Axis Range!”** → when Xmin ≥ Xmax or Ymin ≥ Ymax.
* **“Error: Log Scale requires positive values!”** → when using log scale with values ≤ 0.
* **“Function Syntax Error”** (in console) → when a function is incorrectly written.

---

## ✅ Practical Example

1. In the first input box, type: `sin(x)`
2. Click **Add Function** and type: `x**2`
3. Set axis ranges:

   * X-min = -5, X-max = 5
   * Y-min = -10, Y-max = 10
4. Click **Generate Plot**.
5. The plot will show both functions: sine and quadratic.

---

## 🔚 Closing

* Simply close the window (the program will exit automatically).
* You can export plots via the Matplotlib toolbar button.

---

