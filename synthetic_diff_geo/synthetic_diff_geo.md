% Notes on Synthetic Differential Geometry
% Owen Lynch

# What is Synthetic Differential Geometry?

## What is Differential Geometry?

Differential geometry is the study of mathematical objects that are locally *smooth*, called manifolds. This means that if you are sitting in a manifold and you look around, as long as you don't look to far away, you will feel like you are in Euclidean space. One example of this is the Earth. For a long time, people thought the Earth was flat, because locally the Earth is very similar to $\mathbb{R}^2$. Eventually some people went all the way around the Earth (which you can't do in $\mathbb{R}^2$), which proved that the Earth was only locally flat, not globally flat, but you should give ancient people a break on the whole Earth is flat thing because it's honestly pretty hard to tell if you stay in a small region. Another example is spacetime. For a long time, people thought that we lived in a flat 4-dimensional space, where time was one dimension and space was the other three dimensions. Again, this is an easy mistake to make because locally, our reality looks pretty flat. However, just like the Earth, even though locally spacetime looks like $\mathbb{R^4}$ it actually has curvature. Whenever you ride in an airplane you see some weird curved flight plan that looks like it goes way off course. This is because the geometry of the sphere causes the shortest distance between two points to not be what it would be in the projection onto a flat map, even though locally the sphere looks pretty flat. Similarly, because spacetime is curved by gravity, the shortest distance between points is not always what you would expect if you thought that spacetime was flat. This is why light rays are "bent" when they pass by the sun -- they are following the shortest path like the airplane following a great circle.

Anyways, a typical introduction to differential geometry defines a $n$-dimensional manifold as some subset $M$ of $\mathbb{R}^N$ such that for any point $p \in M$ there exists an open set $V_\alpha \subset \mathbb{R}^n$, an open set $U_\alpha \subset \mathbb{R}^N$ and an injective map $\alpha : V_\alpha \to U_\alpha$ such that $\mathrm{im}(\alpha) \subset M$, $p \in \mathrm{im}(\alpha)$, and $\alpha$ is differentiable. For instance, the sphere is the set $\{ (x,y,z) | \sqrt{x^2 + y^2 + z^2} = 1\}$, and one $\alpha$ for part of the sphere is $\alpha(\theta, \phi) = (\cos\theta\cos\phi, \sin\theta\cos\phi, \sin\phi)$. This $\alpha$ covers *almost* all of the sphere, but if you try to extend it the whole sphere it no longer can be injective--when $\phi = \pi/2$ all of the values of $\theta$ get mapped to the same point. But as long as we only consider a small part of the sphere, this map is fine.

## The Synthetic Approach

One thing that's a bit odd about this is that when I think of geometry, I think of axioms and geometric objects, not numbers (*ewwww*!) and limits and patchwork collections of sets. Back when you learned geometry in highschool, there was probably a certain amount mucking around with sines and cosines, but probably a lot of the time you were doing proofs that barely mentioned numbers. In geometry, a line is a primitive object that satisfies axioms, not a set of points. Wouldn't it be nice if we could do the same thing in differential geometry? This, in a nutshell, is the essence of synthetic differential geometry: differential geometry from an axiomatic framework, as opposed to a coordinate framework.

# Infinitesmals

## Old-school Calculus

Back in the good old days before Herr Cantor and Monsieur Cauchy came along with their limits and mathematical rigor and messed everything up, calculus was much more intuitive. People worked with objects called infinitesmals, which represented infinitely small (but non-zero) quantities. Then, instead of mucking around with limits, you could just define the derivative as

$$ \dot{x}(t) = \frac{x(t + dt) - x(t)}{dt} $$

where $dt$ is an infinitesmal. For instance,

$$ \frac{(t + dt)^2 - t^2}{dt} = \frac{2tdt+dt^2}{dt} = \frac{2tdt}{dt} + dt = 2t + dt \approx 2t $$

After mathematicians stopped fangirling over limits, different ways of making this intuitive idea of infinitesmals rigorous started making the rounds. It turns out that there are several different ways of doing this, each with its own pros and cons. One of my favorite ways (which we will not be talking about today) uses Model Theory, another way uses weird things called ultrafilters. ^[which incidentally sounds like something Billy Mae would do a commercial on: "DO YOU HAVE A PROBLEM WITH SMELLY AIR? USE ULTRAFILTERS, ONLY $19.99 CALL NOW"]

## In synthetic differential geometry

The synthetic approach is to postulate the existence of a special set of infinitesmals that we shall refer to as $D$, which is defined as the set of numbers whose square is 0. Another way of putting it is that U is the equalizer of the following diagram.

\begin{figure}
\centering
\begin{tikzcd}
  R \arrow[r, "x \mapsto x^2", shift left] \arrow[r, "x \mapsto 0"', shift right] & R
\end{tikzcd}
\end{figure}

Then, we introduce the Kock axiom, which states that any map $f: D -> R$ can be written uniquely as $f(x) = f(0) + bd$ for some $b \in R$.
