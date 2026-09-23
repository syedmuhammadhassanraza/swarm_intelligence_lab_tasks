# Swarm Intelligence Labs

This repo holds my lab work for the Swarm Intelligence course (BS-AI 7A, Bahria University, H-11 Campus). Each lab builds on the last one, starting from plain random search and working up to actual swarm-based optimization algorithms.

**Name:** S. M. Hassan Raza
**Enrollment:** 01-136232-080

All notebooks use my roll number as the random seed, so the numbers you see in the outputs are specific to my run and won't match anyone else's exactly that's intentional, it's how the instructor set the assignment up.

---

## Lab 1 — Random Search

**File:** `Lab1_SwarmIntelligence.ipynb`

This one lays the groundwork before getting into actual swarm algorithms. I defined three classic benchmark functions — Sphere, Rastrigin, and Ackley — plotted their landscapes as contour maps, then wrote a basic random search algorithm and ran it against all three.

The point here was to see how a "dumb" search strategy (just picking random points and keeping the best one) performs depending on how tricky the landscape is. Sphere is a smooth single bowl, so random search does fine on it. Rastrigin and Ackley are covered in local dips and bumps, so random guessing struggles a lot more — which sets up the motivation for the smarter algorithms in the next labs.

## Lab 2 — Ant Colony Optimization (ACO)

**File:** `Swarm-Intelligence-Lab2-ACO-09092026-033158pm.pptx` (lab handout) + completed notebook

This lab simulates a colony of ants choosing between four paths from nest to food, each with a different length. Ants pick a path based on pheromone levels, deposit more pheromone on shorter paths, and old pheromone evaporates over time. Run it enough times and the colony converges on the shortest path without any ant actually "knowing" the answer — it just emerges from the pheromone feedback loop.

Key parts of the code:
- `pheromone` dict tracking scent level per path, starting equal for all
- `evaporation_rate` controlling how fast old trails fade
- `Q` controlling how big a pheromone boost a path gets when chosen (shorter paths get a bigger boost since it's `Q / length`)
- A loop over iterations and ants per iteration that updates pheromone and finally prints the path the colony converged on

## Lab 3 — Particle Swarm Optimization (PSO)

**File:** `SWARM_INTELLIGENCE__LAB_3 (1).ipynb`

This lab moves from a discrete path-choosing problem to continuous function minimization. The goal is to minimize `f(x) = (x - 7)² + 4` using a swarm of particles that adjust their velocity based on:
- their own personal best position found so far,
- the swarm's global best position,
- and some inertia from their previous velocity.

Over 40 iterations, the particles converge on `x ≈ 7`, which is the actual minimum of the function. The parameters `w` (inertia), `c1` (how much a particle trusts its own best), and `c2` (how much it trusts the swarm's best) control how fast and how accurately the swarm converges.

---

## Notes

- All notebooks were run in Google Colab.
- Random search (Lab 1) has no memory of past results, which is why it struggles on bumpy landscapes like Rastrigin — that weakness is basically the reason ACO and PSO exist.
- ACO and PSO both solve the same underlying problem (finding good solutions without brute-forcing every possibility) but represent it differently: ACO works over discrete paths, PSO works over continuous space.