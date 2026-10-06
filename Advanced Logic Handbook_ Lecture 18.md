# Advanced Logic Handbook: Lecture 18

# Lecture 18: Clusters, Quotient Frames, Skeletons, Generated Subframes

**What this lecture covers:** (1) clusters in transitive frames, (2) points in a cluster agree on □φ and ◇φ, (3) quotient frame and skeleton, (4) quasi-orders and the three types of cluster, (5) an example refuting the McKinsey formula, (6) a preview of truth-preserving operations, (7) closure notation X↑ω, X⇑, (8) generated subframes, roots, final/last points, covers.

**How to read each section.** Every topic has three layers:

1. **Math:** the precise definition or proof (what you write in exams).
2. **Room-and-light picture:** the building-with-doors story (for intuition).
3. **Normal explanation:** the same idea in ordinary words, without the room picture.

**Quick recap:** x↑ = successors of x (one step), x↑ⁿ = points reachable in exactly n steps, x↓ = predecessors. From Lecture 17: on a transitive frame, □ψ at x passes forward to every successor of x, and ◇ψ at x passes backward to every predecessor. Room picture: rooms = worlds, one-way doors = R, lights = where p is true.

**Notation notes (read from handwriting).**

- The board draws some arrows with an **extra bar**. I write these as **x⇑** and **x⇓** (see Section 7).
- The skeleton is written ρ𝔉 = ⟨ρW, ρR⟩ (the board's letter looks like ρ).
- Where the board is incomplete or illegible I say so, and I do not guess.

---

## 1. Clusters

### Math

Let 𝔉 = ⟨W,R⟩ be a **transitive** frame. Define a relation **∼** on W by

> **x ∼ y iff x = y, or (xRy and yRx).**

Then ∼ is an **equivalence relation** (proof in the self-test). Its equivalence classes are called **clusters**. The cluster containing x is denoted **C(x)**.

> **Room-and-light picture:** two rooms are "mates" if they are the same room, or if you can walk from each to the other by a single door. A **cluster** is a **lounge**: a group of rooms where you can get from any room to any other (and back) in one step. Every room belongs to exactly one lounge (possibly a lounge of just itself).

> **Normal explanation:** ∼ groups together points that **see each other mutually**. Transitivity of R is what makes this grouping consistent (if x and y see each other and y and z see each other, then x and z see each other). Every point belongs to exactly one cluster, so the clusters partition W. Clusters turn a possibly messy transitive frame into something much simpler: a collection of blobs.

---

## 2. Points of one cluster agree on □φ and ◇φ

### Math

**Proposition.** Let x be a point in a model 𝔐 built on a **transitive** frame, and φ an arbitrary formula. Then for **every y ∈ C(x)**:

> (𝔐,x) ⊨ □φ **iff** (𝔐,y) ⊨ □φ, (𝔐,x) ⊨ ◇φ **iff** (𝔐,y) ⊨ ◇φ.

**Proof.** Let y ∈ C(x). If y = x there is nothing to prove. Otherwise xRy and yRx, so y ∈ x↑ and x ∈ y↑.

- By the Lecture 17 result (transitive frames), (𝔐,x) ⊨ □φ implies (𝔐,y) ⊨ □φ for every y ∈ x↑. Since also x ∈ y↑, the same result gives the converse. So □φ holds at x iff it holds at y.
- For ◇: the Lecture 17 result says (𝔐,x) ⊨ ◇φ implies (𝔐,y) ⊨ ◇φ for every y ∈ x↓. Since xRy and yRx, we have y ∈ x↓ and x ∈ y↓, so the implication goes both ways. ∎

> **Room-and-light picture:** inside a lounge, every room sees the same set of "outside rooms through doors", because doors to anything one lounge-mate reaches are also available (via shortcuts) to the others. So "all doors lead to lit rooms" has the **same answer in every room of the lounge**, and "some door leads to a lit room" too.

> **Normal explanation:** the successors of x and of any y in its cluster are essentially the same set (by transitivity and mutual access). Since □ and ◇ only look at successors, they cannot tell cluster-mates apart. **Warning:** this says nothing about the formula φ itself. Cluster-mates can disagree on a plain variable p. Only formulas that **begin with □ or ◇** are guaranteed to agree.

---

## 3. Quotient frame and skeleton

### Math

Let 𝔉 be a transitive frame. The **quotient frame of 𝔉 with respect to ∼** is ⟨W/∼, R/∼⟩ where

- **W/∼ = { C(x) : x ∈ W }** (the set of clusters)
- **C(x) (R/∼) C(y) iff xRy**

It is called the **skeleton** of 𝔉 and is denoted **ρ𝔉 = ⟨ρW, ρR⟩**.

**Facts.**

1. The definition does not depend on which representatives x, y are chosen. (If x ∼ x′, y ∼ y′ and xRy, then x′Rx, xRy, yRy′ give x′Ry′ by transitivity, or one of the pairs is equal.)
2. **The skeleton ρ𝔉 is antisymmetric:** if C(x) ρR C(y) and C(y) ρR C(x), then xRy and yRx, so x ∼ y, so C(x) = C(y).
3. **If R is reflexive, then ρ𝔉 is partially ordered by ρR** (reflexive, transitive, antisymmetric).

*(The board says "every frame", but the construction is stated for transitive frames, so I read it that way.)*

> **Room-and-light picture:** **collapse each lounge into one big room** and keep a door between two big rooms whenever there was a door between rooms of the two lounges. The result is the skeleton: the same building, but with every lounge shrunk to a single node. In the skeleton you can never walk from a big room to a different big room and back again (that is antisymmetry), because then they would have been the same lounge.

> **Normal explanation:** the skeleton is the **quotient of the frame by the cluster relation**, exactly like quotienting a set by an equivalence relation. It removes the "mutual access" detail and keeps only the one-directional structure between clusters. That is why it is antisymmetric: all two-way connections have been absorbed inside clusters. If R was already reflexive (a quasi-order, see next section), the skeleton becomes a genuine **partial order**.

---

## 4. Quasi-orders and the three types of cluster

### Math

A **reflexive and transitive** binary relation is called a **quasi-order** (or **preorder**).

In a transitive frame there are **three types of cluster**:

1. **Degenerate cluster:** consists of a **single irreflexive point**.
2. **Simple cluster:** consists of a **single reflexive point**.
3. **Proper cluster:** contains **at least two (reflexive) points**.

A proper cluster with n points is drawn as a **circled n**, written ⓝ.

**Why proper clusters consist of reflexive points:** if x ∼ y with x ≠ y, then xRy and yRx, so xRx by transitivity (and likewise yRy).

*(The board also has two small sketches under this: a bullet at the bottom with two arrows going up to cluster or point symbols. The labels are not legible, so I don't interpret them.)*

> **Room-and-light picture:** the three kinds of room-groups: (1) a **corridor room**: a lone room with no door to itself; (2) a **one-room lounge**: a lone room with a self-door; (3) a **real lounge** of two or more rooms, all with doors to each other and to themselves. A real lounge is drawn as one circle with its size written inside.

> **Normal explanation:** every cluster has exactly one of these three shapes. The only way a point can be irreflexive in a transitive frame is to be alone in its cluster. As soon as two points see each other, both automatically see themselves. This three-way classification is a useful tool because later arguments about transitive frames can be done cluster by cluster.

---

## 5. Example: the McKinsey formula on a 2-point cluster

### Math

**Example.** Frame 𝔉 = ⟨W,R⟩ with W = {a₁, a₂}, R = {⟨aᵢ,aⱼ⟩ : i, j = 1, 2} (every point sees every point, including itself), and valuation V(p) = {a₁}. This is a **proper 2-point cluster ②**.

The formula **□◇p → ◇□p** (known as the **McKinsey formula**; the board's name for it is hard to read) is **false at both a₁ and a₂**:

- ◇p is true at a₁ and at a₂ (each sees a₁, where p holds).
- So □◇p is true at both (all successors satisfy ◇p).
- □p is false at both, since a₂ ⊭ p and each point sees a₂.
- So ◇□p is false at both (no successor satisfies □p).
- Hence □◇p → ◇□p is **false at a₁ and at a₂**.

**Definition (end of the page).** Let **K_ML = { φ ∈ Form_ML : 𝔉 ⊨ φ for all frames 𝔉 }**, the set of formulas valid on **every frame** (this is the logic **K** from your revision). Since the example refutes □◇p → ◇□p on a frame, **□◇p → ◇□p ∉ K_ML**.

> **Room-and-light picture:** two rooms with doors between them and back to themselves. The p light is on in room 1 only. From either room you can reach a lit room, so "some door is lit" holds everywhere and "all rooms can see a lit room" holds everywhere. But there is **no room from which all doors lead to lit rooms**, because room 2 is dark and both rooms can walk into it. So the formula fails.

> **Normal explanation:** the example also illustrates Section 2: a₁ and a₂ **agree on □p, ◇p, □◇p, ◇□p** (all four are false or true at both), yet they **disagree on p**. The formula is not valid even on this very simple frame (an equivalence relation), which shows how much stronger "valid on all frames" is than "true in one model". One counter-model on one frame is enough to show a formula is not in K_ML.

---

## 6. Preview: truth-preserving operations

The next topic, which the board only names at this point, is **truth-preserving operations**, i.e. ways of building new frames or models from old ones without changing which formulas are true:

- **generating subframes** (keep only what is reachable from some points),
- **reduction**,
- **disjoint union** (Lecture 16 reference supplement, Section 8.3).

> **Room-and-light picture:** three ways to change the building without changing the truth: (1) **demolish everything you cannot reach** from where you stand, (2) **merge look-alike rooms** (reduction), (3) **put buildings side by side** with no doors between them.

> **Normal explanation:** these operations are the tools for comparing frames. Generated subframes are developed in the rest of this lecture. In other textbooks, "reduction" appears as a **p-morphism** (bounded morphism); the lecture only names it here, so I do not state its definition. It will come in a later lecture.

---

## 7. Closure notation: X↑ⁿ, X↑ω, X⇑

### Math

For a frame 𝔉 = ⟨W,R⟩ and **X ⊆ W**:

- **X↑ⁿ** = the set of points y with xRⁿy **for some x ∈ X** (n-step successors of X); **X↓ⁿ** = the same backwards. *(The board's line for X↓ⁿ is blank; this is the symmetric version.)*
- **X↑ω = ⋃\_{n ≥ 1} X↑ⁿ** (everything reachable in **one or more** steps)
- **X↓ω = ⋃\_{n ≥ 1} X↓ⁿ** (everything from which X is reachable in one or more steps)
- **Reflexive versions** (arrow drawn with a bar; I write ⇑ and ⇓): **X⇑ξ = X ∪ X↑ξ** and **X⇓ξ = X ∪ X↓ξ**, for 1 ≤ ξ ≤ ω. In particular **X⇑ = X ∪ X↑ω** (zero or more steps).

**Example (board).** Non-transitive frame W = {a,b,c}, R = {(a,b),(b,c)}.

- a↑ = {b} (one step only)
- **upward closure of a** = a⇑ = {a} ∪ a↑ω = **{a,b,c}**
- a↓ = ∅

> **Room-and-light picture:** x↑ = rooms behind the doors out of x. x↑ω = rooms you can reach by walking **any positive number of doors**. x⇑ = the same plus x itself (**walking zero doors is allowed**). X⇑ for a set of rooms: everything you can reach starting from any of them.

> **Normal explanation:** this is the **reachability closure**. X↑ω is the transitive closure applied to X, and X⇑ is the reflexive-transitive closure. Distinguish three things: **x↑** (one step), **x↑ω** (one or more steps, may not contain x), and **x⇑** (zero or more steps, always contains x). In the example, the single-step set {b} is much smaller than the closure {a,b,c}.

---

## 8. Generated subframes, roots, final and last points, covers

### Math

- The **upward closed set generated by X in 𝔉** is **X⇑** (= X ∪ X↑ω). It is "upward closed": once you are in it, every successor is also in it.
- The **subframe generated by X** is the subframe induced by X⇑ (standard definition; the board states it only for a point x).
- A point x is a **root** of 𝔉 if **the subframe of 𝔉 generated by x is 𝔉 itself**, i.e. **x⇑ = W** (every point is reachable from x or equals x). A frame with a root is called **rooted**.
- The **cluster generated by a point x** is

> **C(x) = x⇑ ∩ x⇓**

(points reachable from x, or x itself, **and** from which x is reachable, or x itself).

- If 𝔉 is transitive: **x is a final point and C(x) a final cluster in X** if

> **x⇑ ∩ X = C(x) ∩ X**

i.e. inside X nothing lies strictly above x outside its own cluster.

- **x is a last point and C(x) the last cluster in X** if **X ⊆ x⇓** (every point of X is below or equal to x).
- A set **X ⊆ W is a cover for Y ⊆ W** if **Y ⊆ X⇓** (every point of Y can reach some point of X, or is in X).

**Board example (partly legible).** A **non-transitive** frame drawn as several vertical chains (some start with a 2-point cluster, some are infinite, some have n, n−1, …, 1 labelled along them). The text says the frame is **generated by a as well as by b**, so **𝔉 is rooted with a and b both roots**. The labels of the individual diagrams are not legible, so I don't interpret them. What I can derive: if both a and b are roots, then b ∈ a⇑ and a ∈ b⇑. So there is a walk from a to b and a walk from b to a (or a = b).

> **Room-and-light picture:** the **generated subframe** of x is the part of the building you can **reach by walking from x**; demolish the rest. A **root** is a room from which you can reach **every** room of the building (so the building is just "the part reachable from x"). The **cluster generated by x** is x's lounge: rooms you can walk to **and** that can walk back to you. A **final point** is a "top floor" room: within the chosen rooms X, nothing is strictly above it. A **last point** is a room such that **all** rooms of X can reach it (it is below-or-equal by everything). A **cover** for Y is a set of rooms X such that every room of Y can reach some room of X.

> **Normal explanation:** these are all **order-theoretic words** for talking about reachability. Final = **maximal** (nothing strictly above in X), last = **greatest** (everything in X is below it); a final point need not be last, and there can be several final clusters. Generated subframes are the main tool of the next lectures: by the locality idea of Lecture 17, truth at x only depends on what x can reach, so cutting the frame down to x⇑ should not change the truth of modal formulas at x. (The lecture sets this up here; it states the preservation result next.)

---

## Worked example: clusters, skeleton, roots (my own)

**Frame.** W = {a, b, c, d}, R = { aRa, aRb, bRa, bRb, aRc, bRc, aRd, bRd, dRd }. Drawn: a proper 2-cluster ② = {a,b} at the bottom, with arrows up to c (a bullet) and d (a circle).

- **Transitive?** Yes: whatever a or b reach (a, b, c, d) is reached from both, and dRd ∧ dRd gives dRd.
- **Clusters:** a ∼ b (aRb and bRa). C(a) = C(b) = {a,b} is **proper** (a and b are reflexive). C(c) = {c} is **degenerate** (c has no self-loop). C(d) = {d} is **simple** (dRd).
- **Skeleton ρ𝔉:** nodes A = {a,b}, C, D. Arrows: A ρR A, A ρR C, A ρR D, D ρR D. C has no arrows. It is **antisymmetric**, but **not a partial order** since C is not reflexive (R was not reflexive).
- **Roots:** a⇑ = {a} ∪ a↑ω = {a,b,c,d} = W, so **a is a root**; so is b. c and d are not roots.
- **Final points in W:** c⇑ = {c} = C(c), so c is final; d⇑ = {d} = C(d), so d is final. a is not final because a⇑ = W ≠ C(a) = {a,b}.
- **Last point in W?** None: c⇓ = {c,a,b} does not contain d, and d⇓ = {d,a,b} does not contain c.
- **Cover:** {c,d} covers W, since {c,d}⇓ = {c,d,a,b} = W. {a} does not cover W, since {a}⇓ = {a,b}.

---

## Common mistakes

1. **Believing cluster-mates satisfy the same formulas.** Only □φ and ◇φ are guaranteed to agree. Plain variables (and anything else) can differ (Example 5).
2. **Thinking x ∼ y only needs xRy.** For x ≠ y you need **both** xRy and yRx.
3. **Putting an irreflexive point inside a proper cluster.** All points of a proper cluster are reflexive.
4. **Confusing x↑ with x↑ω with x⇑.** One step, one or more steps, zero or more steps.
5. **Confusing final and last.** Final (maximal): nothing strictly above in X. Last (greatest): every point of X is below it.
6. **Calling the skeleton a partial order always.** It is a partial order only when R is reflexive; otherwise irreflexive clusters appear as irreflexive nodes.
7. **Concluding "valid" from one model.** The McKinsey example shows a formula is **not in K_ML**. Validity needs every frame.

---

## Self-test (answers below)

1. Show that ∼ is an equivalence relation on a transitive frame.
2. Why must every point of a proper cluster be reflexive?
3. In the 2-point cluster model of Section 5 (V(p) = {a₁}), do a₁ and a₂ agree on p? On □p? On ◇□p?
4. For the chain frame W = {a,b,c}, R = {(a,b),(b,c)} compute {b}⇑. Is b a root? Which point is a root?
5. In the worked example, which clusters are final, and is there a last cluster?

**Answers**

1. **Reflexive:** x = x, so x ∼ x. **Symmetric:** the definition "x = y, or (xRy and yRx)" is symmetric in x and y. **Transitive:** let x ∼ y and y ∼ z. If any two of x, y, z are equal, it is immediate. Otherwise xRy, yRx, yRz, zRy. Then xRz (xRy, yRz) and zRx (zRy, yRx) by transitivity, so x ∼ z.
2. If x ∼ y with x ≠ y, then xRy and yRx. By transitivity xRy ∧ yRx gives xRx, and symmetrically yRy. So both are reflexive.
3. They **disagree on p** (a₁ ⊨ p, a₂ ⊭ p). They **agree on □p** (false at both) and on **◇□p** (false at both), as Section 2 predicts for formulas beginning with □ or ◇.
4. {b}⇑ = {b} ∪ {c} = **{b,c}**. Since {b,c} ≠ W, b is **not** a root. The root is **a**, since a⇑ = {a,b,c} = W. (The frame is not transitive, so these are plain reachability closures.)
5. Final clusters: **{c}** (degenerate) and **{d}** (simple). There is **no last cluster**: a last point x needs W ⊆ x⇓, but c⇓ = {c,a,b} misses d, d⇓ = {d,a,b} misses c, and a⇓ = b⇓ = {a,b} misses both.

---

## One-page summary

- **Cluster:** for a transitive frame, x ∼ y iff x = y or (xRy and yRx). Clusters are the ∼-classes, C(x) the class of x.
- **Same-cluster points agree on □φ and ◇φ** (via the Lecture 17 persistence result), but not necessarily on φ.
- **Quotient / skeleton ρ𝔉:** nodes = clusters, C(x) ρR C(y) iff xRy. **Antisymmetric**; a **partial order** if R is reflexive.
- **Quasi-order = reflexive + transitive.** **Three cluster types:** degenerate (one irreflexive point), simple (one reflexive point), proper (≥ 2 reflexive points, drawn ⓝ).
- **McKinsey □◇p → ◇□p** fails on the 2-point cluster with V(p) = {a₁}, so it is **not in K_ML** (the set of formulas valid on all frames).
- **Truth-preserving operations:** generated subframes, reduction, disjoint union.
- **Notation:** X↑ω (one or more steps), X⇑ = X ∪ X↑ω (zero or more). **Generated subframe** = induced by X⇑. **Root:** x⇑ = W. **C(x) = x⇑ ∩ x⇓.**
- **Final** (nothing strictly above in X), **last** (X ⊆ x⇓), **cover** (Y ⊆ X⇓).

---

*(Next lecture goes below this line.)*