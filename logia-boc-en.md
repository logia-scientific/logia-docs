# ✅ Translated version (English)

The **`logia.py`** file is a program in **Python with PyQt5 + Matplotlib + NumPy**, which creates a graphical application to **define mathematical functions and draw interactive scientific plots**. I will explain step by step and comment on the main blocks of the code:

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

## 🔹 Example of use

1. Open the program.
2. Write in a box: `sin(x)`.
3. Add another: `x**2 + 5`.
4. Set Xmin=-5, Xmax=5.
5. Click "Generate Plot from Functions".
6. The graph appears with both functions.

---

👉 In summary:
This script is an **interactive tool for drawing customized scientific plots**.
It’s like a mini version of MATLAB/Mathematica made in Python, with full control over style and mathematics.

---

