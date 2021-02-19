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

<p>Generally, there are two main ways to represent trajectories in 3D space - as a length \(l\) and angles from the origin \((\theta_y,\theta_z)\) or as a 3-dimensional vector \((x,y,z)\). Within game development, it is more natural to use the vector representation - the majority of physics engines all use this representation to calculate forces, velocities, impulses and more. However, it turns out that the representations are equivalent anyway, and a conversion exists between them. The example below highlights this for a simple case in 2D - we can convert the trajectory represented by length \(l\) and angle \(\theta_y\) to the same trajectory represented by the vector \((x,y)\) </p>

<table>
  <tr> <td> Angle representation </td> <td> Vector Representation </td> </tr>  
<\table>



<h2> Constructing Trajectories from Input </h2>

<h4> Launch Angles vs Velocity Vectors </h4>

<h4> Single Input (2D) </h4>

<h4> Double Input (2D) </h4>

<h4> Double Input (3D) </h4>

<h2> Keeping the Endpoint of a Trajectory Stable </h2>

Write the solution here, explanation follows:

<h4> Problem Definition </h4>

<h4> Determining the Endpoint Location </h4>

<h4> Determining the scale factor \(\alpha\) </h4>

