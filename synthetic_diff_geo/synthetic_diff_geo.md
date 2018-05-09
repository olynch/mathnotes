% A First Look at Synthetic Differential Geometry
% Owen Lynch

# Introduction

## What are these notes?

These notes are a summary of a book I am reading on synthetic geometry, along with context that I know from various sources. The book that I am reading is fairly dense, so I am hoping that these notes will be a more accessible introduction to a topic that I think by rights should be much more intuitive than the normal presentation of differential geometry. These notes will be updated when I have time: if you are viewing them currently know that they are INCOMPLETE and WIP.

## What is Synthetic Differential Geometry?

### What is Differential Geometry?

Differential geometry is the study of mathematical objects that are locally *smooth*, called manifolds. This means that if you are sitting in a manifold and you look around, as long as you don't look to far away, you will feel like you are in Euclidean space. One example of this is the Earth. For a long time, people thought the Earth was flat, because locally the Earth is very similar to $\mathbb{R}^2$. Eventually some people went all the way around the Earth (which you can't do in $\mathbb{R}^2$), which proved that the Earth was only locally flat, not globally flat, but you should give ancient people a break on the whole Earth is flat thing because it's honestly pretty hard to tell if you stay in a small region. Another example is spacetime. For a long time, people thought that we lived in a flat 4-dimensional space, where time was one dimension and space was the other three dimensions. Again, this is an easy mistake to make because locally, our reality looks pretty flat. However, just like the Earth, even though locally spacetime looks like $\mathbb{R}^4$ it actually has curvature. Whenever you ride in an airplane you see some weird curved flight plan that looks like it goes way off course. This is because the geometry of the sphere causes the shortest distance between two points to not be what it would be in the projection onto a flat map, even though locally the sphere looks pretty flat. Similarly, because spacetime is curved by gravity, the shortest distance between points is not always what you would expect if you thought that spacetime was flat. This is why light rays are "bent" when they pass by the sun -- they are following the shortest path like the airplane following a great circle.

Anyways, a typical introduction to differential geometry defines a $n$-dimensional manifold as some subset $M$ of $\mathbb{R}^N$ such that for any point $p \in M$ there exists an open set $V_\alpha \subset \mathbb{R}^n$, an open set $U_\alpha \subset \mathbb{R}^N$ and an injective map $\alpha : V_\alpha \to U_\alpha$ such that $\mathrm{im}(\alpha) \subset M$, $p \in \mathrm{im}(\alpha)$, and $\alpha$ is differentiable. For instance, the sphere is the set $\{ (x,y,z) | \sqrt{x^2 + y^2 + z^2} = 1\}$, and one $\alpha$ for part of the sphere is $\alpha(\theta, \phi) = (\cos\theta\cos\phi, \sin\theta\cos\phi, \sin\phi)$. This $\alpha$ covers *almost* all of the sphere, but if you try to extend it the whole sphere it no longer can be injective--when $\phi = \pi/2$ all of the values of $\theta$ get mapped to the same point. But as long as we only consider a small part of the sphere, this map is fine.

### The Synthetic Approach

One thing that's a bit odd about this is that when I think of geometry, I think of axioms and geometric objects, not limits and patchwork collections of sets. Back when you learned geometry in highschool, there was probably a certain amount mucking around with sines and cosines, but probably a lot of the time you were doing proofs that barely mentioned numbers. In geometry, a line is a primitive object that satisfies axioms, not a set of points. Wouldn't it be nice if we could do the same thing in differential geometry? This, in a nutshell, is the essence of synthetic differential geometry: differential geometry from an axiomatic framework, as opposed to a coordinate framework.

## Infinitesmals

### Old-school Calculus

Back in the good old days before Herr Cantor and Monsieur Cauchy came along with their limits and mathematical rigor and messed everything up, calculus was much more intuitive. People worked with objects called infinitesimals, which represented infinitely small (but non-zero) quantities. Then, instead of mucking around with limits, you might define the derivative as

$$ \dot{x}(t) = \frac{x(t + dt) - x(t)}{dt} $$

where $dt$ is an infinitesmal. For instance,

$$ \frac{(t + dt)^2 - t^2}{dt} = \frac{2tdt+dt^2}{dt} = \frac{2tdt}{dt} + dt = 2t + dt \approx 2t $$

After mathematicians stopped fangirling over limits, different ways of making this intuitive idea of infinitesimals rigorous started making the rounds. It turns out that there are several different ways of doing this, each with its own pros and cons. One of my favorite ways (which we will not be talking about today) uses Model Theory, another way uses weird things called ultrafilters. ^[which incidentally sounds like something Billy Mae would do a commercial on: "DO YOU HAVE A PROBLEM WITH SMELLY AIR? USE ULTRAFILTERS, ONLY $19.99 CALL NOW"] We are going to do a completely different approach.

### In synthetic differential geometry

The synthetic approach is to assume the existence of a special set of infinitesimals that we shall refer to as $D$, which is defined as the set of numbers whose square is 0. When we have a smooth function, we expect that near any point the function looks like a line. That is to say, we expect $f(a + dx) = f(a) + f'(a)dx$, where $f'(a)$ is the slope of the line. In synthetic differential geometry, we build things out of axioms, and our first axiom is that this is true. 

*Linearity Axiom*: For all functions $g : D \to \mathbb{R}$, there a unique number s such that $g(dx) = g(0) + s \cdot dx$.

We use this linearity axiom to take derivatives. For instance, to take the derivative of a function $f: \mathbb{R} \to \mathbb{R}$ at a point $a$, we can define $g : D \to \mathbb{R}$ by $g(dx) = f(a + dx)$ and then use the linearity axiom to get a number $s$ such that $f(a + dx) = f(a) + s \cdot dx$. Because this exists for any $a$, we can define $f'(a)$ to be this $s$ for any $a$. The careful reader will notice I did not put any conditions on the function in the linearity axiom. This seems problematic. For instance consider the function $g : D \to \mathbb{R}$ defined by

$$ g(dx) = \begin{cases} 1 \quad \text{if $dx \neq 0$} \\ 0 \quad \text{otherwise} \end{cases} $$

If we apply the linearity axiom to this, we get $g(dx) = s \cdot dx$ for some s. Now, for $dx \neq 0$, $s \cdot dx = 1$. However, we can multiply this by $dx$ on both sides to get $s \cdot dx^2 = dx$, so $s \cdot 0 = dx$ and $0 = dx$ for all $dx$, whence $D = \{0\}$. It seems like our theory has flopped before it could get off the ground. To salvage our theory, we have to question the foundations of mathematics.

## Intuitionism

### What went wrong before?

The killer of our fledgling theory was the function $g$. If we manage to remove $g$, then our theory might have a shot. But we have to not only eliminate $g$, we have to eliminate all piece-wise functions. In order to do this, let us examine the mechanism behind the construction of a piece-wise function. Whenever you have a piece-wise defined function, you are implicitly relying on the idea that given a condition, a number either satisfies this condition or it does not. This assumption is also know as the law of the excluded middle -- it states that there are no logical values for a statement other than true and false. We will abbreviate this to LEM. Anyways, practically, in a lot of cases it is infeasible to define functions based on LEM. For instance, try building a circuit that outputs 1V if you input a rational valued voltage into it and 0V if you input an irrational voltage. Asking this question doesn't even really make sense because voltages aren't that precise. There is a saying: when physics and logic disagree, change the logic. And that is exactly what we are going to do: we are going to throw out LEM. When people hear this, they immediately try to think of propositions that are neither true nor false, and, not being able to find one, conclude that this is bunk. This is because the correct interpretation is that given a proposition, it is often impossible or very difficult to tell whether it is true or false, so we are not going to assume that we always can when we define functions. It may be true that propositions are always true or false, but from a practical standpoint, it's infeasible to build things based on that assumption.

However, this is not how things work in standard mathematics. Therefore, we need a new mathematics. Essentially, the way that this new mathematics works is that we will promise to never invoke the law of the excluded middle, and in return all of our functions will be smooth. This is essentially the assumption that is made in every physics and engineering class, except they don't realize you have to throw away LEM so that stuff doesn't explode in your face. Most of the time they get away with it because they don't do much real math, they just cite things that have been proved by real mathematicians who have done the dirty work to make sure that their theorems are properly proved. As a mathematician we do our own dirty work, though, so, if we want to live life like a carefree physicist, assuming everything is as differentiable as our heart desires, we have to swear off LEM.

This is for the best, because to be perfectly honest, living an LEM-free life is better for the soul. When you write a proof without LEM you have to actually construct any objects that you want to use, you can't just say that if they didn't exist there would be a contradiction. Constructing your objects gives you a better intuition for what they look and feel like, which in turn makes you and your readers understand proofs better. 

### A Topos to Call Home

Topos is greek for "place". You can think of a topos like a country in mathematics. Most mathematicians live in **Set**, which is a topos made out of sets. But, sometimes to spice it up, we mathematicians like to visit other topoi, just like you might go with your family to Paris or Peru. Just like how different countries have different laws, different topoi have different laws. For instance, in Amsterdam you can get *real* high, but you might have a much more difficult time with that in the US. Just like that, in the (mumble mumble mumble) topos, you can play around with infinitesimals without a care in the world, but in **Set** you have to worry about limits and other nasty stuff.

I say (mumble mumble mumble) topos because I really don't know that much about the topos that you do synthetic geometry in, or that much topos theory in general. Luckily, just like you have been living in **Set** all your life without knowing any topos theory, you can work with the (mumble mumble mumble) topos without ever giving it much thought. In fact, the whole point of synthetic geometry is to free ourselves from having to work in a specific topos -- we just assume some laws and there are several suitable topoi that we might be in but we really don't care. We are multinational lawyers.

One of the *differences* between countries and topoi is that leaving a country is (normally) something discussed in the laws of a country, and normally countries trade with each other and have wars and other stuff, but topoi generally keep to themselves. In the case of the (mumble mumble mumble) topos, this means that as long as you follow the laws of the topos (which include not invoking LEM), you won't accidentally create an object that lives in another topos. It is *this* property of topoi that allows the linearity axiom to work without putting any preconditions on the function involved. We do background checks on functions that want to come into our topos, and they have to promise to uphold the linearity axiom so help them Gauss, and while they are in our topos as long as they follow the laws they won't accidentally create any functions that might violate the linearity axiom.

One thing that is important to mention is that for the sake of intuition I will be treating various mathematical objects that live in synthetic geometry topoi sort of like sets, when they are in fact NOT SETS. This is to increase intuition and familiarity, but in order to make the distinction clear I will be careful to call them objects. When you hear "object" think "sort of like a set, but maybe with some extra assumptions about it and maybe I can't do some of the things with it that I can do with sets".

So what are these laws I've been harping on about? I'll give a brief summary of differences between **Set** and a topos that synthetic geometry could live in.

- LEM is outlawed. Anybody using LEM will be KICKED OUT and will NOT be allowed to come back unless they bring chocolate.
- We can no longer divide with impunity in $\mathbb{R}$. (For those of you who have had some algebra:$\mathbb{R}$ has been downgraded from a field to a commutative ring with a unit element). There are still some numbers that are safe to divide by. For instance, you can always divide by rational numbers, because all of the rational numbers are in $\mathbb{R}$ and if $p/q$ is a rational number then $q/p$ is a rational number (as long as $p \neq 0$). Therefore, if we want to divide by $p/q$ we can just multiply by $q/p$ (and we can still always multiply real numbers). There are also other real numbers that you can divide by, it's just not all of them anymore. To emphasize this change, we will no longer use $\mathbb{R}$ to denote the real numbers, we will instead use just $R$, because in fact we might be talking about any one of a number of topoi, each of which have their own "real number object", and $\mathbb{R}$ normally denotes "the unique set of real numbers".
- Some members of $R$ square to 0, but are not themselves 0. We will call the object of all these numbers $D$.
- The linearity axiom is true for $D$ and $R$.
- Some other stuff that we'll get to when we get to.

# Calculus

## Derivatives

### Linearity Axiom Revisited

\begin{ax}[Linearity Axiom]
For all $f : D \to R$ there exists a unique $b \in R$ such that $f(d) = f(0) + b \cdot d$.
\end{ax}

Let's play around with infinitesimals a bit. One question we ought to ask is whether we can divide by infinitesimals. Remember, we can't divide by everything in $R$, but we can divide by somethings, so it is reasonable to ask whether infinitesimals are one of the things we can divide by. I claim that we cannot.

\begin{prop}
Infinitesimals do not have inverses.
\end{prop}
\begin{proof}
Fix $d \in D$. Suppose that there exists some $d' \in R$ such that $d \cdot d' = 1$.

\begin{align*}
  d \cdot d &= 0 \\
  d' \cdot d \cdot d &= 0 \\
  1 \cdot d &= 0 \\
  d &= 0
\end{align*}

As $D \neq \{0\}$, this is a contradiction, thus we cannot divide by any $d \in D$.
\end{proof}

<!---

If you are scared by the title of this section and don't know what the words mean, don't worry! You as the reader have two options.

1. If you are going to be scared and confused by terminology that you don't understand quite yet, you can just stop reading! I promise I won't get mad at you.
1. You can see words that you don't understand and *be OK* with that. Just roll with it. You'll get there eventually. But I am going to be picking up the mathematical pace from now on, and it will not be easy. I am saying this to scare you but to say that you are not alone in being confused, and you should not assume that I am assuming readers will get this at first read, and there are dragons under the surface of this subject that I will not be confronting that are very tough cookies, so some of this will not at all be possible to understand in its entirety just from this document. It's important to become comfortable in a state of partial understanding.

Are you still with me? Good! Let's get going again!


Another way of putting it is that U is the largest subset of $R$ such that the following diagram is commutative.

\begin{figure}
\centering
\begin{tikzcd}
  R \arrow[r, "x \mapsto x^2", shift left] \arrow[r, "x \mapsto 0"', shift right] & R
\end{tikzcd}
\end{figure}
-->
