# Check If Circle and Rectangle Overlap

## Problem

Given a circle and a rectangle, check whether the circle overlaps the rectangle.

We are given:

* Circle center: `(xCenter, yCenter)`
* Circle radius: `radius`
* Rectangle corners: `(x1, y1)` and `(x2, y2)`

Return `true` if they overlap, otherwise return `false`.

## Approach

The main idea is to find the **closest point of the rectangle to the center of the circle**.

Let this closest point be `(xi, yi)`.

### 1. Find the closest X-coordinate

```cpp
if(x1 > xCenter)
    xi = x1;
else if(x2 < xCenter)
    xi = x2;
else
    xi = xCenter;
```

* If the circle's center is **left of the rectangle**, choose `x1`.
* If the circle's center is **right of the rectangle**, choose `x2`.
* If the center is already between `x1` and `x2`, choose `xCenter`.

### 2. Find the closest Y-coordinate

We use the same logic for the Y-axis:

```cpp
if(y1 > yCenter)
    yi = y1;
else if(y2 < yCenter)
    yi = y2;
else
    yi = yCenter;
```

Now `(xi, yi)` is the point on/in the rectangle closest to the circle's center.

### 3. Calculate Distance

Using the distance formula:

```text
d = √((xi - xCenter)² + (yi - yCenter)²)
```

If:

```text
d <= radius
```

the circle overlaps the rectangle.

## Code

```cpp
class Solution {
public:
    bool checkOverlap(int radius, int xCenter, int yCenter,
                      int x1, int y1, int x2, int y2) {

        int xi;
        int yi;

        // Find closest X-coordinate
        if(x1 > xCenter) {
            xi = x1;
        }
        else if(x2 < xCenter) {
            xi = x2;
        }
        else {
            xi = xCenter;
        }

        // Find closest Y-coordinate
        if(y1 > yCenter) {
            yi = y1;
        }
        else if(y2 < yCenter) {
            yi = y2;
        }
        else {
            yi = yCenter;
        }

        // Calculate distance
        int d = sqrt(
            (xi - xCenter) * (xi - xCenter) +
            (yi - yCenter) * (yi - yCenter)
        );

        return d <= radius;
    }
};
```

## Key Idea

```text
Circle Center
      ↓
Find Closest Point of Rectangle
      ↓
Calculate Distance
      ↓
Distance <= Radius ?
      ↓
   TRUE / FALSE
```

## Complexity

* **Time:** `O(1)`
* **Space:** `O(1)`

## Revision Shortcut

**Closest point → Distance → Compare with radius**

### Important

For X-coordinate, compare with `xCenter`.

For Y-coordinate, compare with `yCenter`.

```cpp
x → xCenter
y → yCenter
```
