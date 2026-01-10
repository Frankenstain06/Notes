# <span style="color:#00FF00"><b>Vector</b></span>

### <span style="color:#000000; text-shadow: 0 0 10px #00c8ffff, 0 0 20px #00c8ffff, 0 0 30px #00c8ffff; animation: glow 3s ease-in-out infinite alternate;">Credit: REFAT</span>

<style>
@keyframes glow {
    0% {
        text-shadow: 0 0 5px #00c8ffff, 0 0 10px #00c8ffff, 0 0 15px #00c8ffff;
        opacity: 0.7;
    }
    100% {
        text-shadow: 0 0 20px #00c8ffff, 0 0 30px #00c8ffff, 0 0 40px #00c8ffff;
        opacity: 1;
    }
}
</style>

There are two main ways to measure quantities:
- <span style="color:#FF0000"><b>Scalars</b></span>: Value or magnitude without direction.
- <span style="color:#FF0000"><b>Vectors</b></span>: Have both magnitude and direction.

For example, <b>velocity</b> has both value and direction (vector), but <b>weight</b> does not (scalar).

---

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>1.</b></span>&nbsp;<span style="color:#0096FF"><b>Vectors in 3D Cartesian Space</b></span>

Vectors are represented by three components: $x$, $y$, and $z$.
- $x$-axis: $\hat{i}$ (length)
- $y$-axis: $\hat{j}$ (width)
- $z$-axis: $\hat{k}$ (height)

<img src="Photos/a.png" alt="Photo" width="400"/>

Example: $\vec{d} = 5\hat{i} + 6\hat{j} + 7\hat{k}$

---

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>2.</b></span>&nbsp;<span style="color:#0096FF"><b>Distance Formula in 3D</b></span>

The distance between points $P_1(x_1, y_1, z_1)$ and $P_2(x_2, y_2, z_2)$:
$$ d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2} $$
where $d$ is the distance, $P_1$ is the first point, $P_2$ is the second point.

If you swap the points:
$$ d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2 + (z_1 - z_2)^2} $$

<img src="Photos/b.png" alt="Photo" width="400"/>

This is a 1D line in 3D space.

---

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>3.</b></span>&nbsp;<span style="color:#0096FF"><b>Equations of Circles and Spheres</b></span>

Circle in 2D (center $(0,0)$): $x^2 + y^2 = r^2$

Sphere in 3D (center $(0,0,0)$): $x^2 + y^2 + z^2 = r^2$

Circle in 2D (center $(a, b)$): $(x - a)^2 + (y - b)^2 = r^2$


Changing the center shifts the sphere.

<span style="color:#FF0000"><b>Example:</b></span> Find the center and radius of the sphere $x^2 + y^2 + z^2 - 2x - 4y + 8z + 17 = 0$
- <b>Solution:</b>
    $\Rightarrow x^2 - 2x + y^2 - 4y + z^2 + 8z = -17$
    $\Rightarrow (x^2 - 2x + 1) + (y^2 - 4y + 4) + (z^2 + 8z + 16) = -17 + 1 + 4 + 16$
    $\Rightarrow (x - 1)^2 + (y - 2)^2 + (z + 4)^2 = 4$
    So, the center is $(1, 2, -4)$ and the radius is $r = \sqrt{4} = 2$.

$x^2 + z^2 = r^2$ is a circle in 2D, but in 3D it represents a cylinder.

<img src="Photos/c.png" alt="Photo" width="400"/>
<img src="Photos/d.png" alt="Photo" width="400" height="285"/>

If a sphere equation is missing one coordinate, it's a cylinder extending along that axis.

---

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>4.</b></span>&nbsp;<span style="color:#0096FF"><b>Vector Notation and Operations</b></span>

Bracket notation for 3D vector: $\langle a, b, c \rangle = \langle 1, -4, 2 \rangle$
Here, $a = 1$, $b = -4$, $c = 2$.

<span style="color:#0096FF"><b>Vector Arithmatics:</b></span> 
if v = <v1, v2, v3> and w = <w1, w2, w3> are vectors in 3-space and k is any
scalar, then  
v + w = <v1 + w1, v2 + w2, v3 + w3>  
v − w = <v1 − w1, v2 − w2, v3 − w3>  

$k\vec{v} = \langle kv_1, kv_2, kv_3 \rangle$

<span style="color:#0096FF"><b>Finding the length of a vector:</b></span> 

If $\vec{P_1P_2}$ is a vector in 3D space with initial point $P_1(x_1, y_1, z_1)$ and terminal point $P_2(x_2, y_2, z_2)$:
$\vec{P_1P_2} = \langle x_2 - x_1, y_2 - y_1, z_2 - z_1 \rangle$
The length is $|\vec{P_1P_2}| = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2}$

<span style="color:#0096FF"><b>Norm of a vector:</b></span> 

The norm (or length) of $\vec{v} = \langle v_1, v_2, v_3 \rangle$ is:
$$ \|\vec{v}\| = \sqrt{v_1^2 + v_2^2 + v_3^2} $$
$|\vec{v}| = \|\vec{v}\|$ (physics and math notation for magnitude).

<span style="color:#0096FF"><b>Unit vector:</b></span> 
A unit vector has magnitude 1.

<span style="color:#0096FF"><b>Normalizing a vector:</b></span> 

Normalization means turning any vector into a unit vector (length = 1) without changing its direction:
$$ \hat{v} = \frac{\vec{v}}{\|\vec{v}\|} $$

<span style="color:#0096FF"><b>Finding vector components from length and angle (2D):</b></span>

$$ \vec{v} = \|\vec{v}\| \cos\theta\,\hat{i} + \|\vec{v}\| \sin\theta\,\hat{j} $$
Here, $\|\vec{v}\|$ is the length and $\theta$ is the angle with the positive x-axis.

**Example:**
If $\|\vec{v}\| = 5$ and $\theta = 30^\circ$:
$$ \vec{v} = 5\cos(30^\circ)\hat{i} + 5\sin(30^\circ)\hat{j} $$
$$ \vec{v} = 5\left(\frac{\sqrt{3}}{2}\right)\hat{i} + 5\left(\frac{1}{2}\right)\hat{j} $$
$$ \vec{v} = \frac{5\sqrt{3}}{2}\hat{i} + \frac{5}{2}\hat{j} $$

<span style="color:#0096FF"><b>Reverse formulas:</b></span> 

$$ \|\vec{v}\| = \sqrt{v_x^2 + v_y^2} $$
$$ \hat{v} = \frac{\vec{v}}{\|\vec{v}\|} $$
$$ \theta = \cos^{-1}\left(\frac{v_x}{\|\vec{v}\|}\right) $$
$$ \theta = \sin^{-1}\left(\frac{v_y}{\|\vec{v}\|}\right) $$

---


<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>5.</b></span>&nbsp;<span style="color:#0096FF"><b>Dot Product of Two Vectors:</b></span> 

If $\vec{v} = \langle v_x, v_y, v_z \rangle$ and $\vec{w} = \langle w_x, w_y, w_z \rangle$ are two vectors in 3D space:
$$ \vec{v} \cdot \vec{w} = v_x w_x + v_y w_y + v_z w_z $$
$$ \vec{v} \cdot \vec{w} = |\vec{v}|\,|\vec{w}| \cos\theta $$
The dot product of two vectors is a scalar. The cross product of two vectors is a vector.
If two vector has a angle of 0 degrees, then they are in the same direction and the dot product is maximized and if the angle between them is 90 degrees, then the dot product is minimized (zero).

<span style="color:#0096FF"><b>Algebraic Properties of the Dot Product:</b></span> 

$ (a)\ \vec{u} \cdot \vec{v} = \vec{v} \cdot \vec{u} $
$ (b)\ \vec{u} \cdot (\vec{v} + \vec{w}) = \vec{u} \cdot \vec{v} + \vec{u} \cdot \vec{w} $
$ (c)\ k(\vec{u} \cdot \vec{v}) = (k\vec{u}) \cdot \vec{v} = \vec{u} \cdot (k\vec{v}) $
$ (d)\ \vec{v} \cdot \vec{v} = \|\vec{v}\|^2 $
$ (e)\ \vec{0} \cdot \vec{v} = 0 $

<span style="color:#0096FF"><b>Finding the Angle Between Vectors:</b></span> 

If $\vec{u}$ and $\vec{v}$ are two vectors in 3D space, the angle $\theta$ between them is:
$$ \cos \theta = \frac{\vec{u} \cdot \vec{v}}{\|\vec{u}\| \cdot \|\vec{v}\|} $$
$$ \theta = \cos^{-1}\left(\frac{\vec{u} \cdot \vec{v}}{\|\vec{u}\| \cdot \|\vec{v}\|}\right) $$

<span style="color:#0096FF"><b>Direction Angles for 3D:</b></span> 

If $\vec{v} = \langle v_x, v_y, v_z \rangle$ is a vector in 3D space, the direction angles $\alpha$, $\beta$, and $\gamma$ with respect to the positive x, y, and z axes are:
$$ \cos \alpha = \frac{v_x}{\|\vec{v}\|}, \quad \cos \beta = \frac{v_y}{\|\vec{v}\|}, \quad \cos \gamma = \frac{v_z}{\|\vec{v}\|} $$
$$ \alpha = \cos^{-1}\left(\frac{v_x}{\|\vec{v}\|}\right), \quad \beta = \cos^{-1}\left(\frac{v_y}{\|\vec{v}\|}\right), \quad \gamma = \cos^{-1}\left(\frac{v_z}{\|\vec{v}\|}\right) $$

<span style="color:#0096FF"><b>Decomposing Vectors into Orthogonal Components:</b></span> 

<img src="Photos/aa.png" alt="Vector decomposition diagram"/>

Here, the vector $\vec{v}$ is decomposed into its orthogonal components along the x-axis and y-axis, represented by the projections or lines onto each axis. The general formula is:
$$ \vec{v} = k_1\vec{e_1} + k_2\vec{e_2} $$

here, $\vec{e_1}$ and $\vec{e_2}$ are the unit vectors along the x-axis and y-axis, respectively, and $k_1$ and $k_2$ are the scalar components of $\vec{v}$ in the direction of $\vec{e_1}$ and $\vec{e_2}$.  
$$ k_1 = \|\vec{v}\| \cos \theta_1 = \vec{v} \cdot \vec{e_1}, \quad k_2 = \|\vec{v}\| \sin \theta_2 = \vec{v} \cdot \vec{e_2} $$
So, the final set of formula is,
$$ \vec{v} = (v \cdot \vec{e_1})\vec{e_1} + (v \cdot \vec{e_2})\vec{e_2} $$
or,
$$ \vec{v} = (|v|cos\theta_1)\vec{e_1} + (|v|sin\theta_2)\vec{e_2} $$

<span style="color:#0096FF"><b>Orthogonal Projection:</b></span> 

General formula:
$$ proj_{\vec{e}} \vec{v} = (v \cdot e) e $$
here, e = unit vector.
but if we want to use non unit vector $\vec{b}$. Then,
$$ \text{proj}_{\vec{b}} \vec{v} = (v \cdot \frac{\vec{b}}{\|\vec{b}\|}) \frac{\vec{b}}{\|\vec{b}\|} $$
here, we find the unit of $\vec{b}$ and followed the equation format.

Rearranging:
$$ \text{proj}_{\vec{b}} \vec{v} = \frac{\vec{v} \cdot \vec{b}}{\|\vec{b}\|^2} \vec{b} $$

---

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>6.</b></span>&nbsp;<span style="color:#0096FF"><b>Cross Product of Two Vectors:</b></span> 

The cross product of vectors $\vec{u} = \langle u_1, u_2, u_3 \rangle$ and $\vec{v} = \langle v_1, v_2, v_3 \rangle$ is:
$$ \vec{u} \times \vec{v} = \begin{vmatrix} 
\hat{i} & \hat{j} & \hat{k} \\
u_1 & u_2 & u_3 \\
v_1 & v_2 & v_3
\end{vmatrix} $$

$$ = \left|\begin{matrix} 
u_2 & u_3 \\
v_2 & v_3
\end{matrix}\right|\hat{i} - \left|\begin{matrix} 
u_1 & u_3 \\
v_1 & v_3
\end{matrix}\right|\hat{j} + \left|\begin{matrix} 
u_1 & u_2 \\
v_1 & v_2
\end{matrix}\right|\hat{k} $$

$$ = (u_2v_3 - u_3v_2)\hat{i} - (u_1v_3 - u_3v_1)\hat{j} + (u_1v_2 - u_2v_1)\hat{k} $$

If $\vec{v} \times \vec{w} = 0$, then $\vec{v}$ and $\vec{w}$ are parallel (or one of them is the zero vector).

There is another formula of the cross product:

$$ \vec{u} \times \vec{v} = \|\vec{u}\| \|\vec{v}\| \sin \theta \hat{n} $$

where $\hat{n}$ is the unit vector perpendicular to the plane formed by $\vec{u}$ and $\vec{v}$, and $\theta$ is the angle between $\vec{u}$ and $\vec{v}$.

<span style="color:#0096FF"><b>Scalar triple product:</b></span> 

$$ \vec{u} \cdot (\vec{v} \times \vec{w}) = \begin{vmatrix}
u_1 & u_2 & u_3 \\
v_1 & v_2 & v_3 \\
w_1 & w_2 & w_3
\end{vmatrix} $$

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>7.</b></span>&nbsp;<span style="color:#0096FF"><b>Parametric Equation:</b></span>
Simplest form:
$\overrightarrow{P_0P} = t\vec{v}$
here, t is a scalar and v is a direction vector.

This equation can be written as:
$\langle x - x_0, y - y_0, z - z_0 \rangle = t\langle a, b, c \rangle$

Which implies that:
$x - x_0 = ta$, $y - y_0 = tb$, $z - z_0 = tc$

Thus, it can be described by the `parametric equations of a line`:
$$x = x_0 + at, \quad y = y_0 + bt, \quad z = z_0 + ct$$

The vector equation of line in general using $\vec{r}$:
$$\vec{r} = \vec{r_0} + t\vec{v}$$
where $\vec{r_0}$ is a position vector to a point on the line, and $\vec{v}$ is a direction vector along the line.

<span style="color:#FFFFFF; background-color: #030503ff; border-radius: 5px;"><b>8.</b></span>&nbsp;<span style="color:#0096FF"><b>Vector planes:</b></span>
<img src="Photos/ab.png" alt="Vector plane diagram"/>
Here, we need to find the equation of a plane defined by a point $\vec{p_0}$ and a normal vector $\vec{n}$. $\vec{n}$ is perpendicular to the plane's surface. To achieve our goal of getting the plane equation we need to observe something. There is another point in the plane surface called $\vec{p}$. We will try to find the relationship between these vectors and will going to find the equation of a plane just by using the dot product. The process:

$$\vec{r} - \vec{r_0} = \vec{p_0} \cdot \vec{p}$$
We multiply the perpendicular vector $\vec{n}$ to both sides:
$$(\vec{r} - \vec{r_0}) \cdot \vec{n} = (\vec{p_0} \cdot \vec{p}) \cdot \vec{n}$$
If two vectors are perpendicular, their dot product is zero. Thus, we have:
$$(\vec{r} - \vec{r_0}) \cdot \vec{n} = 0$$
So,
$$\langle a, b, c \rangle \cdot \langle x - x_0, y - y_0, z - z_0 \rangle = 0$$
Expanding the dot product:
$$a(x - x_0) + b(y - y_0) + c(z - z_0) = 0$$
Here, $\vec{r} = \vec{p}$ and $\vec{r_0} = \vec{p_0}$. This is the final form and it is called **Point Normal Form**

**Example 1:** Find an equation of the plane passing through the point (3, −1, 7) and perpendicular to the vector n = ⟨4, 2, −5⟩.

**_Solution:_**
Given point, $p_0 (x_0, y_0, z_0) = (3, −1, 7)$
Normal vector, $n (a, b, c) = ⟨4, 2, −5⟩$

Using the Point Normal Form:
$$4(x - 3) + 2(y + 1) - 5(z - 7) = 0$$

Expanding this:
$$4x - 12 + 2y + 2 - 5z + 35 = 0$$
$$4x + 2y - 5z + 25 = 0$$

The equation of the plane is `4x + 2y - 5z + 25 = 0`
**Normal Vector:** The normal vector is a vector that is perpendicular to the surface of the plane. In this case, the normal vector is given by $n = ⟨4, 2, −5⟩$.

**Example 2:**  
<span style="color:red"> *Insight 1: If vectors are lying in the plane then they are always parallel to the plane's surface. They are not necessarily parallel to themselves.
Insight 2: In the below picture, vector a and b are parallel to each other but a and c are not. Also b and c are not parallel to each other. If we cross product a and b then the output would be zero vector which is not orthogonal thus it is not normal. If we cross product both a and c and b and c their output will be a new orthogonal vector which will be a normal to a, b and c vector.*</span>
<img src="Photos/ac.png" alt="Vector plane diagram"/>

Find an equation of the plane through the points $P_1$(1, 2, −1), $P_2$(2, 3, 1) and $P_3$(3, −1, 2).
**_Solution:_**
Since the points $P_1$, $P_2$, and $P_3$ lie in the plane, the vectors $\overrightarrow{P_1P_2} = \langle 1, 1, 2 \rangle$
and $\overrightarrow{P_1P_3} = \langle 2, -3, 3 \rangle$ are `parallel to the plane` but not `parallel to each other`. Therefore,
$$\overrightarrow{P_1P_2} \times \overrightarrow{P_1P_3} = \begin{vmatrix} 
\hat{i} & \hat{j} & \hat{k} \\
1 & 1 & 2 \\
2 & -3 & 3
\end{vmatrix}$$

$$= 9\hat{i} + \hat{j} - 5\hat{k}$$
Here $n = 9\hat{i} + \hat{j} - 5\hat{k}$ and it is normal to the plane, since it is orthogonal to both $\overrightarrow{P_1P_2}$ and $\overrightarrow{P_1P_3}$. By using this normal and the point $P_1(1, 2, -1)$ in the plane, we can obtain the `point-normal form`,
$$9(x - 1) + (y - 2) - 5(z + 1) = 0$$
which can be rewritten as
$$9x + y - 5z - 16 = 0$$

**What is a scalar multiple?**
When a vector is multiplied by a scalar (a real number), the result is a new vector that points in the same direction (if the scalar is positive) or the opposite direction (if the scalar is negative). For example, if $\vec{v} = \langle a, b, c \rangle$ is a vector and $k$ is a scalar, then the scalar multiple of $\vec{v}$ and $k$ creates a new vector b:
$$ b = k\vec{v} = \langle ka, kb, kc \rangle$$

**Angle between planes:**
The angle between two planes can be found using the normal vectors of the planes. If the normal vectors are $\vec{n_1}$ and $\vec{n_2}$, then the angle $\theta$ between the planes is given by:
$$\cos(\theta) = \frac{|\vec{n_1} \cdot \vec{n_2}|}{|\vec{n_1}| |\vec{n_2}|}$$

**Distance between a point and a plane**
The distance $d$ from a point $P_0(x_0, y_0, z_0)$ to a plane defined by the equation $Ax + By + Cz + D = 0$ is given by the formula:
$$d = \frac{|Ax_0 + By_0 + Cz_0 + D|}{\sqrt{A^2 + B^2 + C^2}}$$