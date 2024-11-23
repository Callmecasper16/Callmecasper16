- 👋 Hi, I’m @Callmecasper16
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.widgets import Button

# Set up the initial parameters for the fractals
width, height = 800, 800
max_iter = 256

# Function to generate the Mandelbrot set
def mandelbrot(c, max_iter):
    z = 0
    n = 0
    while abs(z) <= 2 and n < max_iter:
        z = z * z + c
        n += 1
    return n

# Function to generate the Burning Ship fractal
def burning_ship(c, max_iter):
    z = 0
    n = 0
    while abs(z) <= 2 and n < max_iter:
        z = complex(abs(z.real), abs(z.imag))**2 + c
        n += 1
    return n

# Function to generate the Feather fractal
def feather(c, max_iter):
    z = 0
    n = 0
    while abs(z) <= 2 and n < max_iter:
        z = (z.real * z.imag) + c
        n += 1
    return n

# Function to generate the SFX fractal
def sfx(c, max_iter):
    z = 0
    n = 0
    while abs(z) <= 2 and n < max_iter:
        z = z**3 + c
        n += 1
    return n

# Function to generate the Chickov Map fractal
def chickov(c, max_iter):
    z = 0
    n = 0
    while abs(z) <= 2 and n < max_iter:
        z = np.sin(z) + c
        n += 1
    return n

# Function to generate a fractal image based on the selected function
def generate_fractal(x_min, x_max, y_min, y_max, width, height, max_iter, fractal_function):
    # Generate a grid of complex numbers
    x_vals = np.linspace(x_min, x_max, width)
    y_vals = np.linspace(y_min, y_max, height)
    fractal_image = np.zeros((height, width))

    for i, x in enumerate(x_vals):
        for j, y in enumerate(y_vals):
            c = complex(x, y)
            fractal_image[j, i] = fractal_function(c, max_iter)
    
    return fractal_image

# Function to plot the selected fractal
def plot_fractal(ax, x_min, x_max, y_min, y_max, fractal_function):
    fractal_image = generate_fractal(x_min, x_max, y_min, y_max, width, height, max_iter, fractal_function)
    ax.imshow(fractal_image, cmap='hot', extent=(x_min, x_max, y_min, y_max))
    ax.set_title("Fractal Viewer")
    ax.set_xlabel("Real")
    ax.set_ylabel("Imaginary")
    plt.draw()

# Zoom functionality
def zoom(event, ax, x_min, x_max, y_min, y_max, fractal_function):
    zoom_factor = 0.5
    x_center = (x_min + x_max) / 2
    y_center = (y_min + y_max) / 2

    # Adjust the view window based on mouse click location
    x_min = x_center - (x_center - x_min) * zoom_factor
    x_max = x_center + (x_max - x_center) * zoom_factor
    y_min = y_center - (y_center - y_min) * zoom_factor
    y_max = y_center + (y_max - y_center) * zoom_factor

    plot_fractal(ax, x_min, x_max, y_min, y_max, fractal_function)
    return x_min, x_max, y_min, y_max

# Button actions for fractal selection
def select_mandelbrot(event):
    global x_min, x_max, y_min, y_max
    plot_fractal(ax, x_min, x_max, y_min, y_max, mandelbrot)

def select_burning_ship(event):
    global x_min, x_max, y_min, y_max
    plot_fractal(ax, x_min, x_max, y_min, y_max, burning_ship)

def select_feather(event):
    global x_min, x_max, y_min, y_max
    plot_fractal(ax, x_min, x_max, y_min, y_max, feather)

def select_sfx(event):
    global x_min, x_max, y_min, y_max
    plot_fractal(ax, x_min, x_max, y_min, y_max, sfx)

def select_chickov(event):
    global x_min, x_max, y_min, y_max
    plot_fractal(ax, x_min, x_max, y_min, y_max, chickov)

# Set initial view parameters
x_min, x_max, y_min, y_max = -2.0, 1.0, -1.5, 1.5

# Create a figure and axis for the fractal plot
fig, ax = plt.subplots(figsize=(8, 8))

# Plot the Mandelbrot set by default
plot_fractal(ax, x_min, x_max, y_min, y_max, mandelbrot)

# Add zoom functionality (interactive)
fig.canvas.mpl_connect('button_press_event', lambda event: zoom(event, ax, x_min, x_max, y_min, y_max, mandelbrot))

# Add buttons for fractal selection
ax_mandelbrot = plt.axes([0.1, 0.02, 0.1, 0.075])
ax_burning_ship = plt.axes([0.22, 0.02, 0.1, 0.075])
ax_feather = plt.axes([0.34, 0.02, 0.1, 0.075])
ax_sfx = plt.axes([0.46, 0.02, 0.1, 0.075])
ax_chickov = plt.axes([0.58, 0.02, 0.1, 0.075])

btn_mandelbrot = Button(ax_mandelbrot, 'Mandelbrot')
btn_burning_ship = Button(ax_burning_ship, 'Burning Ship')
btn_feather = Button(ax_feather, 'Feather')
btn_sfx = Button(ax_sfx, 'SFX')
btn_chickov = Button(ax_chickov, 'Chickov')

btn_mandelbrot.on_clicked(select_mandelbrot)
btn_burning_ship.on_clicked(select_burning_ship)
btn_feather.on_clicked(select_feather)
btn_sfx.on_clicked(select_sfx)
btn_chickov.on_clicked(select_chickov)

# Show the interactive plot
plt.show()

<!---
Callmecasper16/Callmecasper16 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
