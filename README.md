# Lab 4 Drawing a Scene with Composite Shapes Using turtle

## Objectives

* Practice and gain understanding of the coding concepts **Generalization** and **Encapsulation**.
* Learn to develop code in a modular fashion by encapsulating **turtle** code into generalized functions.
* Apply generalized functions to solve a larger problem, by making **composite** pictures out of simple shape functions.
* Debugging **semantic** errors and fixing them.
    * **NOTE:** Examples of calling these functions are given with each function. The intention is for you to practice incremental development, and test each and every function as you create them. This will eliminate errors, and make your code cleaner in the end.

## Part 1: Drawing Basic Shapes


### Install, Import, and Setup Turtle
```python
import turtle

"""PUT YOUR FUNCTIONS HERE"""

# Create a turtle object
t = turtle.Turtle()

# Hide the turtle and set speed
t.speed(10)  # 1 is slow, 10 is fast, 0 is instant
t.hideturtle()

# Create a window to draw in
# Create a new turtle screen and set its background color
screen = turtle.Screen()
screen.bgcolor("darkblue")
# Set the width and height of the screen
screen.setup(width=600, height=600)
# Clear the screen
t.clear()

"""PUT YOUR DRAW CALLS TO FUNCTIONS HERE"""

# Close the turtle graphics window when clicked
turtle.exitonclick()
```

### Write this Function to Draw a Square

```python
def draw_square(t, length):
    """Draws a square with the given side length."""
    for _ in range(4):
        t.forward(length)
        t.left(90)

# Example usage
draw_square(t, 100)
```

### Write this Function to Draw a Circle
```python
def draw_circle(t, radius):
    """Draws a circle with the given radius."""
    t.circle(radius)

# Example usage
draw_circle(t, 50)
```

### Write this Function to Draw any Regular Polygon
```python
def draw_polygon(t, sides, length):
    """Draws a regular polygon with a given number of sides and side length."""
    angle = 360 / sides
    for _ in range(sides):
        t.forward(length)
        t.left(angle)

# Example usage
draw_polygon(t, 6, 50)  # Hexagon
```

## Part 2: Creating Composite Shapes

### Pumpkin!
* Here you will use the shapes functions created in Part 1 to create composite images.
* In the function below, you build a pumpkin using circles and stem using turtle functions.
```python
def draw_pumpkin(t, x, y, radius):
    """Draws a pumpkin (orange circle) at the given (x, y) location with a green stem."""
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.fillcolor("orange")
    t.begin_fill()
    t.circle(radius)
    t.end_fill()
    
    # Drawing the stem
    t.fillcolor("green")
    t.begin_fill()
    t.left(90)  # Point upwards
    t.forward(radius // 2)
    t.left(90)
    t.forward(radius // 5)
    t.left(90)
    t.forward(radius // 2)
    t.left(90)
    t.forward(radius // 5)
    t.end_fill()
```
* Now we'll use the polygon function to add the jack-o-lantern eyes and mouth!

### Adding the Face
```python
def draw_eye(t, x, y, size):
    """Draws one triangular eye at the given (x, y) position."""
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.fillcolor("yellow")
    t.begin_fill()
    draw_polygon(t, 3, size)
    t.end_fill()

def draw_mouth(t, x, y, width):
    """Draws a jagged mouth using a series of connected lines."""
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.fillcolor("yellow")
    t.begin_fill()
    for _ in range(5):  # Create a simple zigzag mouth
        t.forward(width // 5)
        t.left(120)
        t.forward(width // 5)
        t.right(120)
    t.end_fill()
```
* Let's test your new jack-o-lantern code.
```python
# Example of drawing a jack-o-lantern with eyes and a mouth
draw_pumpkin(t, 0, -100, 100)  # Draw the pumpkin
draw_eye(t, -40, 0, 30)  # Left eye
draw_eye(t, 40, 0, 30)   # Right eye
draw_mouth(t, -50, -50, 100)  # Mouth
```
* This pumpkin doesn't quite look right! When you test the **draw_pumpkin** function, it draws the stem at the bottom of the pumpkin.
* **Fix the function to draw the stem in the correct location.**
* This pumpkin still doesn't quote look right. When you draw the face, the mouth is mis-positioned and points in the wrong direction.
* **Fix the function to draw the mouth in the correct direction and location.**

## Part 3: Let the Stars Shine for You

### Drawing a Star
* First let's draw a single star!
```python
def draw_star(t, x, y, size):
    """Draws a star at the given (x, y) position."""
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.fillcolor("white")
    t.begin_fill()
    for _ in range(5):
        t.forward(size)
        t.right(144)  # 144 degrees is the angle to form a star
    t.end_fill()

# Example usage
draw_star(t, -100, 150, 30)  # Star in the sky
draw_star(t, 100, 180, 20)
```
* Next, add a function to fill the night sky with random stars!
* Consider moving the **import random** to the top of your code (it's not a rule, but is a convention).
```python
import random

def draw_sky(t, num_stars):
    """Draws a starry sky with the given number of stars."""
    for _ in range(num_stars):
        x = random.randint(-300, 300)
        y = random.randint(0, 300)
        size = random.randint(10, 30)
        draw_star(t, x, y, size)

# Example usage
draw_sky(t, 20)  # Draw 20 stars
```

## Part 4: Putting all the Incremental Development Together!
* In this final part, you will use the functions you've written to create a composite scene with multiple jack-o-lanterns under a starry sky.
```python
# Draw three jack-o-lanterns
draw_pumpkin(t, -150, -150, 100)
draw_eye(t, -190, -60, 30)  # Left eye
draw_eye(t, -110, -60, 30)  # Right eye
draw_mouth(t, -190, -100, 80)  # Mouth

draw_pumpkin(t, 0, -150, 80)
draw_eye(t, -20, -70, 25)
draw_eye(t, 20, -70, 25)
draw_mouth(t, -30, -110, 60)

draw_pumpkin(t, 150, -150, 100)
draw_eye(t, 110, -60, 30)
draw_eye(t, 190, -60, 30)
draw_mouth(t, 110, -100, 80)

# Draw the night sky
draw_sky(t, 30)
```
* OH NO! There is a problem with this code!
    * The jack-o-lanterns are TOO HIGH in their window! **Lower the jack-o-lanterns so that they remain proportionately the same, but are resting near the bottom.**
* OH NO! There is something else wrong!
    * Some of the random stars can touch the pumpkin stems or the pumpkins themselves. **Fix the code so that the stars can not reach the pumpkin stems.**

## Part 5: Reflection
* In a new **README.md**, reflect on how encapsulation and generalization helped us break down the drawing process for this scene.

## Part 6: Turn In!
[Review video of this process](https://redwoods.us-west-2.instructuremedia.com/embed/72299bfd-8420-4ad0-8af5-18fb8e32e50a)
1. **Create a GitHub Repository:**
   * Log in to your GitHub account.
   * Create a new repository with a suitable name (e.g., "python_lab4").
2. **Configure Git in PyCharm:**
   * Open the "Git" menu in PyCharm and initialize a Git repository for your project.
   * Add your GitHub remote repository by going to "Git" -> "Manage Remotes".
3. **Commit Changes:**
   * Stage all changes in your PyCharm project.
   * Commit the changes with a descriptive message (e.g., "Initial commit").
4. **Push to GitHub:**
   * Push the committed changes to your GitHub repository using the "Push" button in PyCharm.

### Submission
Submit the link from your GitHub repository containing your lab 4 repo to Canvas.