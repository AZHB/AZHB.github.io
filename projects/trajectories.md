---
layout: default
permalink: "/projects/trajectories/"
title: "Trajectories"
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

<h1> Implementing Trajectories in Games </h1>

This project will analyse some different methods of constructing trajectories from player input. It also features some code written to keep the endpoint of a trajectory stable whilst one component of the trajectory in 3-dimensional space is altered, as well as a discussion of the mathematics behind this approach. The trajectories have been implemented in 2D using the Godot Engine (see <a href="">this project</a> for more details) and in 3D using Unreal Engine (see <a href="">this project</a> for more details).

<h4> Launch Angles vs Velocity Vectors </h4>

<p>Generally, there are two main ways to represent trajectories in 3D space - as a length \(l\) and angles from the origin \((\theta_y,\theta_z)\) or as a 3-dimensional vector \((x,y,z)\). Within game development, it is more natural to use the vector representation - the majority of physics engines all use this representation to calculate forces, velocities, impulses and more. However, it turns out that the representations are equivalent anyway, and a conversion exists between them. The example below highlights this for a simple case in 2D - we can convert the trajectory represented by length \(l\) and angle \(\theta_y\) to the same trajectory represented by the vector \((x,y)\) </p>

<table>
  <tr> 
    <td> Angle representation </td> 
    <td> Vector Representation </td> 
  </tr>  
</table>

<p>
Some simple vector geometry provides the following conversions from \((x,y)\) to \(l\) and \(\theta_y\):

$$l = |(x,y)| = \sqrt{(x^2+y^2)}$$
$$\theta_y = \tan^{-1}(\frac{y}{x})$$

The reverse conversion is given by the equations:

$$x = l\cos(\theta_y)$$
$$y = l\sin(\theta_y)$$

Hence, since the conversion between trajectory representations is linear in its time complexity, the choice is largely irrelevant. As mentioned before, this report will choose to use the 3-dimensional vector \((x,y,z)\) as this is the preffered choice in game engines.
</p>

<h2> Constructing Trajectories from Input </h2>

In this section, we will consider a few methods of constructing a trajectory from player input. The difference between each method is essentially how many sources of input to take. With more sources of input, the player generally has a higher degree of precision. However, this does come at the cost of making the control scheme more complex and potentially lengthening the aiming process. This tradeoff should be carefully considered with regards to the design intent of the game being developed.

<h4> Single Input (2D) </h4>

Calculating a trajectory \((x,y)\) with a single input is possible in 2D. In my 2D Golf project, I use the user's mouse position to populate the trajectory vector \((x,y)\) with the following calculation:

$$(x,y) = (mouse_x - target_x, mouse_y - target_y)$$

Where \(mouse_x\) is the x-component of the mouse position and \(target_x\) is the x-component of the projectile to be launched. This method is quick and allows the user to generate any possible trajectory with only a single input (mouse movement).

<table style="margin-left:auto;margin-right:auto;margin-top:40px;width:50%;">
  <tr> <td> <img src="https://azhb.github.io/Trajectory2DOne.gif"> </td> </tr>
  <tr> <td style="text-align:center"> Generating a trajectory with a single input </td> </tr>
</table>

<h4> Double Input (2D) </h4>

<p>
For increased precision or to introduce additional gameplay mechanics, it may be preferable in some cases to calculate a trajectory in 2D using two input sources. Typically, this takes the form of first determining the direction of the trajectory and then determining the 'strength' of the launch. Mathematically, this is equivalent to detrmining a unit vector \((x_0,y_0)\) of length one and then scaling it by a scalar 'strength' number \(s\). The final trajectory is then:

$$(x,y) = (x_0,y_0) \times s = (sx_0,sy_0)$$

This is commonly seen in games like Golf Story (shown below), where the player first uses mouse/cursor movement to determine a direction unit vector \((x_0,y_0)\) and then interacts in some way with a 'strength' user interface (usually timing-based).
</p>

<table style="margin-left:auto;margin-right:auto;margin-top:40px;width:50%;">
  <tr> <td> <img src="https://azhb.github.io/GolfStory.png"> <a href="https://sidebargames.com/golfstory/"> Source </a> </td> </tr>
  <tr> <td style="text-align:center"> Golf Story uses a power bar (bottom) to set the scalar shot strength \(s\) </td> </tr>
</table>

<h4> Double Input (3D) </h4>

<p>
It is of course not possible to populate a trajectory vector in 3D space \((x,y,z)\) by using only mouse movement - there will be some trajectories that simply cannot be made, as even with predetermined \(x\) and \(y\) components there are an infinite number of trajectories as \(z\) varies. Hence, we must use at least two input sources. In my 3D golf prototype, I decided to use the mouse movement to determine the \(x\) and \(y\) components of the trajectory and the mouse wheel to determine the \(z\) component. This results in an intuitive and fast method of producing trajectories, whilst retaining a good level of precision.
</p>

<table style="margin-left:auto;margin-right:auto;margin-top:40px;width:75%">
  <tr> <td> blueprints here </td> </tr>
  <tr> <td style="text-align:center"> Replace with code when possible </td> </tr>
</table>

<table style="margin-left:auto;margin-right:auto;margin-top:40px;width:75%">
  <tr> <td> gif here </td> </tr>
  <tr> <td style="text-align:center"> Trajectory </td> </tr>
</table>

<p>
There is one aspect of this trajectory that could be remedied - keeping the endpoint of the trajectory stable as the \(z\) component changes. As you can see in the demonstration below, as the player scrolls the mouse wheel (and consequently alters the \(z\) component) the endpoint of the trajectory moves significantly. This can make it difficult for the player to aim precisely. The next section details an efficient method to tackle this problem and keep the endpoint of the trajectory stable.
</P>

<h2> Keeping the Endpoint of a Trajectory Stable </h2>

Write the solution here, explanation follows:

<h4> Problem Definition </h4>

<h4> Determining the Endpoint Location </h4>

<h4> Determining the scale factor \(\alpha\) </h4>

