# Advanced Logic Handbook: Lecture 17

# Lecture 17: n-step Truth, Submodels, Locality, Diagrams, Transitive Frames

**What this lecture covers:** (1) truth of □ⁿ and ◇ⁿ, and dead ends, (2) subframes and submodels, (3) the locality theorem (a formula of degree n only sees n steps), (4) drawing conventions for frames and models, (5) worked examples, including a failing Löb-type formula, (6) a persistence result for transitive frames.

**How to read each section.** Every topic has three layers:

1. **Math:** the precise statement or proof (what you write in exams).
2. **Room-and-light picture:** the building-with-doors story (for intuition).
3. **Normal explanation:** the same idea in ordinary words, without the room picture.

**Quick recap from Lecture 16:** x↑ = points one step from x, x↑ⁿ = points reachable in exactly n steps (x↑⁰ = {x}), md(φ) = modal degree, □ⁿ/◇ⁿ = n boxes/diamonds. Room picture: rooms = worlds, one-way doors = R, lights = where p is true; □ = all doors lead to lit rooms, ◇ = some door does.

**Notation note:** this is read from handwritten board pages. Where the board is ambiguous or incomplete I say so.

---

## 1. Truth of □ⁿ and ◇ⁿ, and dead ends

### Math

**Proposition.** For every n ≥ 0:

- (𝔐,x) ⊨ □ⁿψ **iff** (𝔐,y) ⊨ ψ **for all y ∈ x↑ⁿ**
- (𝔐,x) ⊨ ◇ⁿψ **iff** (𝔐,y) ⊨ ψ **for some y ∈ x↑ⁿ**

(The n = 1 case is just the truth definition of □ and ◇ from Lecture 16.)

**Empty case.** If xRⁿy holds for **no** y, i.e. **x↑ⁿ = ∅**, then for **every formula ψ**:

> (𝔐,x) ⊨ □ⁿψ **and** (𝔐,x) ⊭ ◇ⁿψ.

*(The board writes the frame 𝔉 here, but truth needs a model, so read it as: in any model on that frame.)*

**Dead end.** A point x with **no successor** (there is no y with xRy) is called a **dead end**. For a dead end, x↑ = ∅, which is the case n = 1 above.

**Proof idea of the proposition.** Induction on n. □⁰ψ = ψ and x↑⁰ = {x}, so n = 0 is trivial. For n+1: □ⁿ⁺¹ψ = □(□ⁿψ), which says "□ⁿψ holds at every one-step successor y", and by induction that says "ψ holds at every z ∈ y↑ⁿ". The points z reachable this way are exactly those in x↑ⁿ⁺¹. ◇ is the same with "some" in place of "all".

> **Room-and-light picture:** □ⁿp at room x: take every possible walk of exactly n doors from x; **every** room where a walk ends must have the p light on. ◇ⁿp: **at least one** such walk must end in a lit room. If there is **no walk of n doors at all**, then there are no end rooms to check: "all end rooms are lit" is automatically true, and "some end room is lit" is automatically false. A **dead end** is a room with no door out, so it has no walk even of length 1.

> **Normal explanation:** the proposition just says that "n boxes in a row" means "for all points exactly n steps away". It is a quantifier statement over the set x↑ⁿ. When that set is empty, we get the standard logical facts: a "for all" over an empty set is **true**, and a "there exists" over an empty set is **false**. This holds for **every** ψ, even ψ = ⊥. Note that x does not have to be a dead end: if a is a point with a single successor b which is itself a dead end, then a↑² = ∅, so a ⊨ □²⊥ even though a has a successor.

---

## 2. Subframes and submodels

### Math

These are defined **as in intuitionistic logic**. The standard definition: for a frame 𝔉 = ⟨W,R⟩ and a **non-empty** set X ⊆ W:

- the **subframe induced by X** is ⟨X, R ∩ (X × X)⟩ (keep the points in X and only the arrows between them)
- the **submodel induced by X** is that subframe with valuation V′(p) = V(p) ∩ X (keep only the facts at points of X)

**Key point from the board:** each non-empty set X of points determines, **in a unique way**, the subframe and the submodel with set of worlds X. There is no choice involved. These are called **the subframe and the submodel induced by X**.

> **Room-and-light picture:** pick some rooms and **demolish all the others**. Keep every door that connects two surviving rooms, and keep the lights as they were in the surviving rooms. The result is fully determined by which rooms you chose.

> **Normal explanation:** a submodel is "the model restricted to a chosen set of points". Nothing is invented: the relation is the old relation restricted to X, and each variable is true exactly where it was true before, within X. That is why the choice of X alone determines everything. Submodels matter because the next theorem compares truth in a model with truth in a well-chosen submodel.

---

## 3. The locality theorem

### Math

**Proposition.** Let 𝔐 be a model, x a point in 𝔐, n ≥ 0, and 𝔑 the **submodel of 𝔐 induced by the set**

> x↑⁰ ∪ x↑¹ ∪ … ∪ x↑ⁿ (all points within n steps of x).

Then for **every formula φ with md(φ) ≤ n**:

> **(𝔐,x) ⊨ φ iff (𝔑,x) ⊨ φ.**

**Proof.** By induction on the construction of φ (with md(φ) ≤ n; the hypothesis is assumed for all points, all models and all smaller bounds).

- **Basis and φ = ψ ⊙ χ** (⊙ ∈ {∧, ∨, →}): trivial. A variable or Boolean combination looks only at x itself, and x belongs to both models, with the same facts.
- **φ = □ψ.** Since md(□ψ) ≤ n, we have n ≥ 1 and **md(ψ) ≤ n − 1**. We show (𝔐,x) ⊭ □ψ iff (𝔑,x) ⊭ □ψ.
  - (𝔐,x) ⊭ □ψ iff there is **y ∈ x↑ with (𝔐,y) ⊭ ψ**.
  - Take the submodel 𝔑′ of 𝔐 induced by **y↑⁰ ∪ … ∪ y↑ⁿ⁻¹**. Every point within n−1 steps of y is within n steps of x (go x → y first), so 𝔑′ lives inside 𝔑.
  - Since md(ψ) ≤ n − 1, the induction hypothesis gives (𝔐,y) ⊭ ψ **iff** (𝔑′,y) ⊭ ψ **iff** (𝔑,y) ⊭ ψ.
  - Also, every y ∈ x↑ is in 𝔑 and the arrow x → y is kept, so x↑ is the same in 𝔐 and 𝔑.
  - Hence there is a y ∈ x↑ falsifying ψ in 𝔐 iff there is one in 𝔑, i.e. **(𝔐,x) ⊭ □ψ iff (𝔑,x) ⊭ □ψ**, which is the claim.
- **φ = ◇ψ:** the board only does □. The case ◇ follows because ◇ψ ≡ ¬□¬ψ and md(¬ψ) = md(ψ); it can also be proved the same way with "some" in place of "all".

> **Room-and-light picture:** a formula of degree n is like a person who can only **peek n doors ahead** from where they stand. Everything farther away is invisible to them. So you can **demolish every room more than n doors from x**, and the person's answer at x does not change.

> **Normal explanation:** this is a **locality** result. Whether a formula of modal degree n is true at x depends only on the points within n steps of x. The proof is natural: each modal operator moves the "viewpoint" one step further out, and the degree counts how many such moves can happen. The inductive step for □ψ reduces to a smaller problem: it passes from x with budget n to a successor y with budget n − 1, which is exactly why the induction runs on the formula and why n decreases. This is the formal reason that md was introduced in Lecture 16.

---

## 4. Drawing conventions for frames and models

### Math / convention

- A point that is **irreflexive** (not xRx) is drawn as a **bullet •**. A **reflexive** point (xRx) is drawn as a **circle ∘**.
- Draw an **arrow from x to y** only if **x ≠ y and xRy**. (Self-loops are shown by the circle, not by an arrow.)
- Frames drawn this way are **assumed transitive**: **do not draw** an arrow x → z if you already draw x → y and y → z. The missing arrow is understood.
- In **non-transitive** frames, **all arrows are shown explicitly**.
- When drawing **models**: write **next to each point the formulas true there on its left, and the formulas false there on its right.**

> **Room-and-light picture:** a bullet is a room with **no door back into itself**; a circle is a room with a **self-door**. For a building with shortcut doors, the plan only shows the "step by step" doors, and you mentally add the shortcuts. For buildings without that property, every door is on the plan.

> **Normal explanation:** these are conventions for readability, not mathematics, but you must read them correctly. Two traps: a missing arrow in a drawn frame does **not** mean "no accessibility" (transitivity is assumed unless told otherwise), and a formula written on the **right** of a point is **false** there, which is the opposite of what a label like "p" next to a point might suggest.

---

## 5. Worked examples

### 5.1 A single irreflexive point (dead end)

**Math.** W = {a}, R = ∅, V(p) = ∅.

- a ⊨ □p, vacuously (a ⊨ □p iff ∀y (aRy ⇒ y ⊨ p), and there is no y).
- a ⊭ p. So **a ⊭ □p → p**.
- a ⊭ ◇p (iff ∃y (aRy and y ⊨ p), and there is no y). With a ⊨ □p, we get **a ⊭ □p → ◇p**.

> **Room-and-light picture:** one room, no doors at all, light off. "All doors lead to lit rooms" is true (no doors), but the room itself is dark, so □p → p fails. And "some door leads to a lit room" is false, so □p → ◇p fails.

> **Normal explanation:** these two formulas are the axioms **T** (□p → p) and **D** (□p → ◇p) from your revision table. This example is a tiny model refuting both, because a dead end makes □ vacuously true. It explains why T needs reflexivity and D needs seriality (every point has a successor).

### 5.2 A single reflexive point, and a failing Löb-type formula

**Math.** W = {a}, R = {⟨a,a⟩}, V(p) = ∅.

- a ⊭ p, and the only successor of a is a itself, so **a ⊭ □p** and **a ⊭ ◇p**.
- So **a ⊨ □p → p** and **a ⊨ □p → ◇p** (the premise □p is false).
- Next, **a ⊨ □(□p → p)**: the only successor is a, and a ⊨ □p → p.
- But a ⊭ □p. Therefore

> **a ⊭ □(□p → p) → □p.**

> **Room-and-light picture:** one room with a door back to itself, light off. Every door leads to the same dark room, so □p is false and p is false, which makes "□p → p" true. Since that holds in every room you can reach, the premise "□(□p → p)" is true, but the conclusion □p is false.

> **Normal explanation:** the formula □(□p → p) → □p is **Löb's formula** (the axiom of the logic **GL** from your revision notes; the lecture does not name it here). This example shows it is **not valid** on every frame. For GL the relevant frames must have no endless forward paths. A single reflexive point is exactly an endless path (a → a → a → …).

### 5.3 An infinite chain (transitive model)

**Math.** Take points a, b, c, … with a R b R c R …, closed under transitivity, drawn as a vertical chain, with **V(p) = ∅**. *(On the board p is written to the right of each point; by the convention in Section 4 that means p is **false** everywhere.)*

- At every point x: p is false, and x has a successor lacking p, so □p is false.
- So □p → p is **true** at every point. Hence **□(□p → p) is true** at every point (all successors satisfy □p → p).
- But □p is false at every point. Therefore

> **□(□p → p) → □p is false at every point of this transitive model.**

> **Room-and-light picture:** an endless corridor of dark rooms, each with a door to the next. Everywhere, "all doors lead to lit rooms" is false, because there is always a next dark room. So □p → p is true everywhere (false premise), the premise □(□p → p) is true everywhere, but □p is false everywhere.

> **Normal explanation:** this repeats Example 5.2 but now the frame is **transitive and irreflexive**, so the failure is not due to a loop or non-transitivity. The culprit is the **infinite ascending chain**. This is the conversely-well-foundedness condition of GL from your revision: Löb's formula is valid on a transitive frame only if there are no infinite chains a R b R c R …

### 5.4 An intransitive frame where □p → □□p fails

**Math.** W = {a, b, c}, R = {⟨a,b⟩, ⟨b,c⟩}, V(p) = {a, b}. (Drawn: a bullet chain a → b → c, with all arrows shown since the frame is non-transitive.)

- a ⊨ □p: the only successor of a is b, and b ∈ V(p).
- a ⊭ □□p: a → b → c and c ∉ V(p).
- So **a ⊭ □p → □□p.**

**Variant (add self-loops).** R = {⟨a,b⟩, ⟨b,c⟩, ⟨a,a⟩, ⟨b,b⟩, ⟨c,c⟩}, same V. (Drawn with **circles** instead of bullets.)

- Successors of a are {a, b}, both in V(p), so a ⊨ □p.
- Successors of b are {b, c}, and c ∉ V(p), so b ⊭ □p.
- Since b is a successor of a, a ⊭ □□p. So again **a ⊭ □p → □□p.**

> **Room-and-light picture:** a is lit and b is lit, c is dark. From a you only see b (lit), so □p holds at a. But one more door takes you from b to the dark room c, so "two doors ahead everything is lit" fails. There is no shortcut door a → c to warn you, because the building has no shortcuts.

> **Normal explanation:** □p → □□p is axiom **4**, which corresponds to **transitivity**. Both frames here are **not transitive** (aRb and bRc but not aRc), and axiom 4 fails in both, even after adding reflexivity. This shows that reflexivity alone does not rescue it, and it motivates the next result.

---

## 6. Transitive frames: □ moves forward, ◇ moves backward

### Math

**Proposition.** Let 𝔐 be a model on a **transitive** frame. Then for every point x and every formula ψ:

1. **(𝔐,x) ⊨ □ψ ⇒ (𝔐,y) ⊨ □ψ for every y ∈ x↑** (every successor of x)
2. **(𝔐,x) ⊨ ◇ψ ⇒ (𝔐,y) ⊨ ◇ψ for every y ∈ x↓** (every predecessor of x)

**Proof.**

1. Contrapositive. Suppose (𝔐,y) ⊭ □ψ for some y ∈ x↑. Then there is z ∈ y↑ with (𝔐,z) ⊭ ψ. We have xRy and yRz, so by **transitivity xRz**, i.e. z ∈ x↑. So x has a successor falsifying ψ, hence **(𝔐,x) ⊭ □ψ**.
2. Similar. Suppose (𝔐,x) ⊨ ◇ψ and y ∈ x↓ (so yRx). There is z with xRz and z ⊨ ψ. Now yRx and xRz give **yRz** by transitivity, so y has a successor satisfying ψ, hence **(𝔐,y) ⊨ ◇ψ**.

> **Room-and-light picture:** the building has shortcut doors. (1) If **every door out of x** leads to a lit room, and y is a room x can enter, then any room y can reach is **also directly reachable from x** by a shortcut, so it is lit too. So "all doors lit" holds at y as well: the property travels **forward**. (2) If x has a door to a lit room, then any room y with a door into x also has a **shortcut** straight to that lit room, so "some door is lit" travels **backward**.

> **Normal explanation:** transitivity says "a step of a step is a step", so the set of points reachable from y is **contained** in the set reachable from x whenever xRy. A "for all" statement over a bigger set (x's successors) implies the same statement over the smaller set (y's successors). That is (1). A "there exists" statement transfers the other way, to anything that can reach x. That is (2). This is the semantic reason behind axiom **4** (□p → □□p) holding on transitive frames, and it is analogous to **persistence** in intuitionistic logic. It also explains Example 5.4: without transitivity, □p at a does not carry over to b.

---

## Common mistakes

1. **Treating □ⁿ as a single step.** □ⁿψ talks about points exactly n steps away (x↑ⁿ), not "within n".
2. **Forgetting vacuous truth for every ψ.** If x↑ⁿ = ∅, then □ⁿψ is true and ◇ⁿψ is false even for ψ = ⊥, and x need not be a dead end.
3. **Using the locality theorem with md(φ) > n.** A formula deeper than n can see outside the n-step submodel.
4. **Misreading diagrams.** A missing arrow in a transitive diagram is a shortcut you must add mentally. Formulas on the **right** of a point are **false**.
5. **Drawing arrows for self-loops.** Reflexive points are circles, and arrows are drawn only for x ≠ y.
6. **Concluding from one example.** Examples 5.2 to 5.4 show formulas **failing in a given model**. Validity needs all models, but one counter-model is enough to show a formula is **not valid**.

---

## Self-test (answers below)

1. Frame W = {a,b}, R = {(a,b)}. Which of □²ψ and ◇²ψ is true at a? Is a a dead end?
2. A formula φ has md(φ) = 2. Which set of points of 𝔐 is enough to decide (𝔐,x) ⊨ φ?
3. On the frame W = {a,b}, R = {(a,b)}, show that □(□p → p) → □p is true at every point for **every** valuation V.
4. In Example 5.4 (first frame), verify that part (1) of Section 6 fails.
5. How is the frame W = {a,b,c}, R = {(a,b),(b,c),(a,c)} drawn under our conventions?

**Answers**

1. a↑² = ∅ (a → b, but b has no successor). So **a ⊨ □²ψ** for every ψ (even ⊥) and **a ⊭ ◇²ψ** for every ψ. a is **not** a dead end (it has successor b); b is the dead end.
2. The submodel induced by **x↑⁰ ∪ x↑¹ ∪ x↑²**, i.e. all points within 2 steps of x.
3. At b (a dead end): □p is true and □(□p → p) is vacuously true. The formula holds at b exactly when □p does, and □p is true, so the implication is true. At a: if a ⊨ □(□p → p), then b ⊨ □p → p. Since b ⊨ □p (dead end), b ⊨ p. So a ⊨ □p. Hence the implication holds at a. No assumption about V was used.
4. In the first frame, a ⊨ □p (b ∈ V(p)) and b ∈ a↑, but b ⊭ □p because b's successor c ∉ V(p). So □p does not persist to b, as the frame is not transitive.
5. As a **chain a → b → c with bullets and no arrow a → c**, because the frame is transitive (aRb and bRc) and all points are irreflexive. The arrow a → c is the shortcut that transitivity supplies.

---

## One-page summary

- **□ⁿψ at x:** ψ at **all** points of x↑ⁿ. **◇ⁿψ:** ψ at **some** point of x↑ⁿ. If x↑ⁿ = ∅: □ⁿψ true, ◇ⁿψ false, for every ψ.
- **Dead end:** a point with no successor.
- **Submodel induced by X:** keep points X, restrict R to X, restrict V to X.
- **Locality:** if md(φ) ≤ n, truth of φ at x is decided by the submodel on x↑⁰ ∪ … ∪ x↑ⁿ. Proof: induction, with □ψ passing from budget n at x to budget n−1 at a successor.
- **Drawing:** bullet = irreflexive, circle = reflexive; arrow only for x ≠ y; transitive diagrams omit shortcut arrows; true formulas left of a point, false formulas right.
- **Examples:** a dead end refutes □p → p and □p → ◇p; a reflexive point and an infinite transitive chain both refute **Löb's formula** □(□p → p) → □p; an intransitive frame refutes □p → □□p.
- **Transitive frames:** □ψ at x passes **forward** to every successor; ◇ψ at x passes **backward** to every predecessor.

---

*(Next lecture goes below this line.)*