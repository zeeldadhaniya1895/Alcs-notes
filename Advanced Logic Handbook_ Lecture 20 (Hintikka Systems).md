# Advanced Logic Handbook: Lecture 20

# Lecture 20: Hintikka Systems (building counter-models step by step)

**What this lecture covers:** (1) tableaux, saturated and disjoint tableaux, (2) Hintikka systems, (3) when a tableau is realizable, (4) the bound of 2^|Σ| tableaux, (5) finite counter-models for every non-theorem of K, (6) **how to actually use the method**, with many worked examples.

> **Name check:** the method on the board is **Hintikka** (not Henkin). Henkin's method builds one huge canonical model out of all maximal consistent sets. Hintikka's method builds a **small counter-model for one given formula**, by hand, step by step. This lecture is the second one.

**How to read each section.** Every definition has three layers:

1. **Math:** the precise definition (what you write in exams).
2. **Room-and-light picture:** the building story (for intuition).
3. **Normal explanation:** the same idea in ordinary words.

The practical part (Sections 5 to 8) is a **procedure** with a rule table, a checklist, fully worked examples and exercises, since that is where mistakes happen.

**Quick recap.**

- The language has ∧, ∨, →, ⊥, □. **¬A := A → ⊥** and **◇A := ¬□¬A**.
- Truth at a point is written (𝔐,x) ⊨ ψ. As on your earlier board pages: **true formulas go on the left, false formulas on the right.**
- **K** = the formulas valid on all frames. A formula φ is **not in K** exactly when some model has a point where φ is false (a **counter-model**).

**Notation notes and what is (not) on the board.**

- The board refers to saturation conditions **(S1) to (S6)** but they are **not written on the pages I have**. I list the standard six in Section 1 (they are the six propositional rules for ∧, ∨, → on the true and false sides).
- **Page 3** (reflexive Grz) is incomplete: the table is cut off and the picture shows only three points. I completed it in Example 3 and **checked the final model by hand**.
- **Page 11** is blank.
- The truth lemma, and the derivations of the two corollaries, are **not on the board**. They are my fillings, marked as such.

---

## 1. Tableaux

### Math

A **tableau** in the language ML is any pair **t = (Γ, Δ)** of subsets of Form_ML.

- Γ = formulas we want **true** (left column). Δ = formulas we want **false** (right column).

A tableau is **saturated** if conditions (S1) to (S6) hold. *(Standard list; the board only refers to them.)*

|  | If this is in … | Then … |
| --- | --- | --- |
| (S1) | A ∧ B ∈ Γ | A ∈ Γ **and** B ∈ Γ |
| (S2) | A ∧ B ∈ Δ | A ∈ Δ **or** B ∈ Δ |
| (S3) | A ∨ B ∈ Γ | A ∈ Γ **or** B ∈ Γ |
| (S4) | A ∨ B ∈ Δ | A ∈ Δ **and** B ∈ Δ |
| (S5) | A → B ∈ Γ | A ∈ Δ **or** B ∈ Γ |
| (S6) | A → B ∈ Δ | A ∈ Γ **and** B ∈ Δ |

A tableau t is **disjoint** if **Γ ∩ Δ = ∅ and ⊥ ∉ Γ**. (Nothing is both true and false, and ⊥ is never required to be true.)

**Order on tableaux:** t ⊆ t′ means Γ ⊆ Γ′ and Δ ⊆ Δ′.

> **Room-and-light picture:** a tableau is a **note about one room**: a list of lights we need ON (Γ) and a list we need OFF (Δ). The note is *saturated* if it has been worked out fully (if it says "A and B must be lit", then it also says "A lit, B lit"). It is *disjoint* if it does not demand that some light is both on and off.

> **Normal explanation:** a tableau is a **partial description of one possible situation**. Saturation says that every requirement has been unpacked into requirements about its parts. Disjointness is consistency: a contradictory note describes nothing, so that branch of the search is dead (it is "closed").

---

## 2. Hintikka systems

### Math

A **Hintikka system in K** is a pair **𝔥 = ⟨T, S⟩** where **T** is a non-empty set of **disjoint saturated tableaux** and **S** is a binary relation on T satisfying:

- **(HS_m1)** if t = (Γ,Δ), t′ = (Γ′,Δ′) and **t S t′**, then **ψ ∈ Γ′ for every □ψ ∈ Γ.**
- **(HS_m2)** if t = (Γ,Δ) and **□ψ ∈ Δ**, then there is **t′ = (Γ′,Δ′) in T with t S t′ and ψ ∈ Δ′.**

**Further definitions.**

- 𝔥 is a **Hintikka system for a tableau t** if **t ⊆ t′ for some t′ ∈ T**.
- A tableau (Γ,Δ) is **realized** in (a point x of) a model 𝔐 if **(𝔐,x) ⊨ ψ for every ψ ∈ Γ** and **(𝔐,x) ⊭ ψ for every ψ ∈ Δ**.
- A tableau is **realizable in K** if it is realized in some model.

> **Room-and-light picture:** a Hintikka system is a **whole building drawn as notes**: one note per room, plus doors between notes. Two rules make it a genuine building. (HS_m1, **push true boxes through doors**) If room t says "□ψ must be true", then every room behind a door from t must say "ψ must be lit". (HS_m2, **false boxes need a witness door**) If room t says "□ψ must be false", there must be **at least one** door from t to a room that says "ψ must be off".

> **Normal explanation:** HS_m1 and HS_m2 are exactly the truth conditions of □ read in two directions: □ψ true needs ψ true at **all** successors, and □ψ false needs ψ false at **some** successor. The set T plays the role of the worlds and S the role of the accessibility relation.

---

## 3. Why Hintikka systems work

### 3.1 From a Hintikka system to a counter-model

**Proposition.** A tableau t is realizable in K **iff** there is a Hintikka system for t.

**Proposition.** If 𝔥 is a Hintikka system for **(∅, {φ})**, then **𝔥 ⊭ φ** (φ is refuted in the model built from 𝔥, so φ ∉ K).

**Proof of the "system ⇒ model" direction (my filling in, standard).** Turn 𝔥 into a model: the points are the tableaux, the arrows are S, and **V(p) = { (Γ,Δ) ∈ T : p ∈ Γ }**. **Truth lemma:** for every tableau t = (Γ,Δ) ∈ T and every formula ψ,

> **ψ ∈ Γ ⇒ (𝔥,t) ⊨ ψ and ψ ∈ Δ ⇒ (𝔥,t) ⊭ ψ.**

By induction on ψ.

- *Variable p:* p ∈ Γ means t ∈ V(p). If p ∈ Δ then p ∉ Γ (disjoint), so t ∉ V(p).
- *⊥:* ⊥ ∉ Γ (disjoint), so only ⊥ ∈ Δ can occur, and ⊥ is false.
- *∧, ∨, →:* by (S1) to (S6) and induction. For example, A → B ∈ Γ gives A ∈ Δ (so A false) or B ∈ Γ (so B true), and either makes A → B true.
- *□ψ ∈ Γ:* for every t S t′, (HS_m1) gives ψ ∈ Γ′, which is true at t′ by induction. So □ψ is true at t.
- *□ψ ∈ Δ:* (HS_m2) gives t′ with t S t′ and ψ ∈ Δ′, which is false at t′. So □ψ is false at t. ∎

Applying it to t₀ with φ ∈ Δ gives (𝔥,t₀) ⊭ φ.

> **Room-and-light picture:** if the notes obey the four checks (saturated, disjoint, HS_m1, HS_m2), you can **build the real building from the notes**: rooms = notes, doors = S, a light p is on exactly in the notes that list p as ON. Every room then behaves exactly as its note says.

> **Normal explanation:** the construction is **sound**: you never need to verify the counter-model separately, since correctness is built into the four conditions. (Still, checking the final model by hand is the best way to catch your own slips.)

### 3.2 The size bound

**Theorem.** A tableau t is realizable in K **iff** there is a Hintikka system for t containing **at most 2^|Σ| tableaux**, where **Σ** is the set of all subformulas of the formulas in t.

**Proof ("⇒" direction, from the board).** Suppose t is realized in 𝔐 = ⟨𝔉,V⟩, 𝔉 = ⟨W,R⟩. For every x ∈ W define the tableau **t_x = (Γ_x, Δ_x)** with

> Γ_x = { ψ ∈ Σ : x ⊨ ψ }, Δ_x = { ψ ∈ Σ : x ⊭ ψ }.

Let **𝔥 = ⟨T,S⟩** with **T = { t_x : x ∈ W }** and, for t_x, t_y:

> **t_x S t_y iff (□ψ ∈ Γ_x implies ψ ∈ Γ_y) for all □ψ ∈ Σ.**

- **HS_m1** holds by the definition of S.
- **HS_m2:** let □ψ ∈ Δ_x. Then x ⊭ □ψ, so there is y with xRy and y ⊭ ψ. Then t_x S t_y, because if □χ ∈ Γ_x then x ⊨ □χ, so χ is true at y (as xRy), i.e. χ ∈ Γ_y. Also ψ ∈ Δ_y.
- The t_x are disjoint and saturated, because they come from real truth values.
- If t is realized at x₀, then t ⊆ t\_{x₀}. So 𝔥 is a Hintikka system for t.

**Counting.** T is a **set** of tableaux and each t_x is determined by Γ_x ⊆ Σ (Δ_x is the rest of Σ). So **|T| ≤ number of subsets of Σ = 2^|Σ|**. The "⇐" direction is the previous proposition. ∎

> **Room-and-light picture:** take a real building and write one note per room, listing for each subformula in Σ whether it is ON or OFF there. **Rooms with identical notes collapse into one**, so at most 2^|Σ| notes exist, no matter how huge the building was. Doors between notes: allow a door from note A to note B whenever B contains everything that A's true boxes demand.

> **Normal explanation:** this is a **finite model property** argument (compare filtration): only the truth values of the finitely many formulas in Σ matter, so a counter-model never needs more than 2^|Σ| points. In practice this means the search for a counter-model **terminates**, so K is decidable (my remark; the lecture states the bound).

---

## 4. Corollaries: finite counter-models

**Corollary (i).** For every formula **φ ∉ K** there is a **rooted frame refuting φ with at most 2^|Sub φ| points.** *Why:* apply the theorem to t = (∅,{φ}), so Σ = Sub φ. The Hintikka system gives a frame with at most 2^|Sub φ| points refuting φ at some point. By the generation theorem (Lecture 19), the subframe generated by that point still refutes φ, and it is rooted.

**Corollary (ii).** **Every φ ∉ K is refuted in some finite intransitive tree.** *Why (my derivation, not on the board):* take the finite rooted counter-model from (i), unravel it into a tree (Lecture 19: a reduction preserves truth), then **cut the tree at depth md(φ)**, which keeps the truth of φ at the root (the locality theorem of Lecture 17). The result is a finite tree because the frame is finite and the depth is bounded.

**Corollary.** **K = { φ ∈ Form_ML : 𝔉 ⊨ φ for all finite intransitive trees 𝔉 }.**

> **Normal explanation:** K can be tested on **small, tree-shaped, finite** frames. If a formula survives every finite intransitive tree, it is in K. This is the basis of the practical method below.

---

## 5. HOW TO USE THE METHOD: step by step

**Goal:** given a formula φ, either **build a counter-model** (so φ ∉ K), or show that **no counter-model exists** (so φ ∈ K).

### Step 0: Prepare the formula

Rewrite ¬ and ◇ using the basic connectives, **or** use the derived rules in the table below.

- ¬A is A → ⊥.
- ◇A is ¬□¬A, i.e. (□(A → ⊥)) → ⊥.

### Step 1: Start tableau t₀

Put **φ on the right (false side)**. So **t₀ = (∅, {φ})**. Draw a two-column table:

| t₀ | TRUE (Γ) | FALSE (Δ) |
| --- | --- | --- |
|  | *(empty)* | φ |

*Memory aid:* we are trying to make φ **false**, so it goes in Δ.

### Step 2: Saturate the tableau with the propositional rules

Work on **one tableau at a time** and keep applying these until nothing new can be added.

| Rule | If you see … | Do this | Branching? |
| --- | --- | --- | --- |
| (S1) | A ∧ B in Γ | add A, B to Γ | no |
| (S2) | A ∧ B in Δ | add A to Δ **or** B to Δ | **yes** |
| (S3) | A ∨ B in Γ | add A to Γ **or** B to Γ | **yes** |
| (S4) | A ∨ B in Δ | add A, B to Δ | no |
| (S5) | A → B in Γ | add A to Δ **or** B to Γ | **yes** |
| (S6) | A → B in Δ | add A to Γ **and** B to Δ | no |
| (¬Γ) | ¬A in Γ | add A to Δ | no |
| (¬Δ) | ¬A in Δ | add A to Γ | no |

**Tip:** do all the **non-branching** rules first, and use the branching ones last. Before branching, check whether the tableau already satisfies the "or" (for instance, if B is already in Γ, then (S5) is already satisfied and you do not branch).

### Step 3: Check for a clash (the closing test)

A tableau **clashes** if some formula is in **both** Γ and Δ, **or** ⊥ is in Γ. A clash **kills that branch**.

- If you were in the middle of a **branching choice**, go back and try the **other** option.
- If **every** choice at **every** branching point clashes, then **no counter-model exists**: **φ ∈ K (valid)**. Stop.

### Step 4: Create witnesses for false boxes (HS_m2)

For **each □A in Δ** of a tableau t: create a **new successor tableau t′** with **A in its Δ′**. Draw an arrow t → t′.

- **One witness per false box is enough.** (A false box needs *some* successor, not all.)
- Different false boxes can get different successors, or they can share one **if** the shared tableau stays disjoint (merging is optional, see Example 1).

### Step 5: Push true boxes through all doors (HS_m1)

For **each □A in Γ** of a tableau t and **each arrow t → t′** (including successors created later): add **A to Γ′** of t′.

### Step 6: Repeat on the new tableaux

Go back to Step 2 for every tableau that received new formulas (the new successors and anything you pushed into). Then Steps 3 to 5 again. Stop when **nothing changes**: no clash, every false box has its witness, every true box has been pushed through every arrow.

### Step 7: Read off the counter-model

- **Points** = the tableaux (t₀, t₁, …).
- **Arrows** = the arrows you drew. **No extra arrows**, not even "shortcuts": in this method arrows are listed explicitly.
- **V(p) = the set of tableaux with p in Γ.** If an atom is in neither Γ nor Δ of a tableau, make it **false** (any choice works).

### Step 8: Verify by hand (always do this)

Evaluate φ at t₀ in your model using the truth definition. It must be **false**. If it is not, you missed a push (Step 5) or a witness (Step 4).

### Summary of the correspondence

| Step | Hintikka condition |
| --- | --- |
| 2 | saturation (S1 to S6) |
| 3 | disjointness (Γ ∩ Δ = ∅, ⊥ ∉ Γ) |
| 4 | HS_m2 |
| 5 | HS_m1 |

### Extra rules for **reflexive** counter-models (as used on page 3)

If the question asks for a **reflexive** counter-model:

- **(T-rule)** if **□A ∈ Γ**, then also add **A to Γ of the same tableau.**
- **Add a loop** t → t for every tableau, and make sure HS_m1 holds for the loop (this is exactly the T-rule).
- Everything else stays the same. **Do not make the frame transitive**: the arrows are exactly the ones you drew plus the loops.

### Derived rules for ◇ (if you prefer not to rewrite)

*(Derived from ◇A := (□(A → ⊥)) → ⊥ with S5, S6, HS_m1, HS_m2; checked.)*

- **◇A ∈ Γ:** create a **new successor** with **A in its Γ′**. (Some successor makes A true.)
- **◇A ∈ Δ:** add **A to Δ′ for every successor** t′, including later ones. (No successor makes A true.)

---

## 6. Worked examples

### Example 1 (board, page 1): refute **SC = □(□p → q) ∨ □(□q → p)**

*(A form of the "linearity" formula, my note.)*

| Step | Action | Result |
| --- | --- | --- |
| 0 | start | t₀: Γ = ∅, Δ = {SC} |
| 1 | (S4) on SC ∈ Δ | Δ₀ gets □(□p→q) and □(□q→p) |
| 2 | witness for □(□p→q) ∈ Δ₀ | new t₁ with (□p→q) ∈ Δ₁ |
| 3 | witness for □(□q→p) ∈ Δ₀ | new t₂ with (□q→p) ∈ Δ₂ |
| 4 | push true boxes of t₀ | Γ₀ = ∅, nothing to push |
| 5 | (S6) in t₁ | □p ∈ Γ₁, q ∈ Δ₁ |
| 6 | (S6) in t₂ | □q ∈ Γ₂, p ∈ Δ₂ |
| 7 | clash check | none |

Tableaux: **t₀** (∅ | SC, □(□p→q), □(□q→p)); **t₁** (□p | □p→q, q); **t₂** (□q | □q→p, p).

**Model:** t₀ → t₁ and t₀ → t₂, with p, q false everywhere (V = ∅). **Verify:** t₁ is a dead end, so □p is true at t₁ while q is false, so □p → q is false at t₁. Hence □(□p→q) is false at t₀. The same at t₂ for the second disjunct. So **SC is false at t₀** ✓.

**Merged model (page 2).** Join t₁ and t₂ into one tableau t = (□p, □q | q, p, □p→q, □q→p). It is disjoint and still dead-ended, so t₀ → t is a **2-point counter-model** as well. (Merging is allowed only when the merged tableau is still disjoint.)

### Example 2 (board, page 2): refute **Grz = □(□(p → □p) → p) → p** in K

Write A := □(□(p→□p)→p). So Grz = A → p.

- (S6): **A ∈ Γ₀, p ∈ Δ₀.**
- Δ₀ = {Grz, p} contains **no box**, so **no witness is needed**.
- No successors, so nothing to push. No clash.

**Model:** a **single irreflexive point t₀** with p false. **Verify:** A is true at a dead end (vacuous), and p is false, so A → p is false ✓. *(Grz is therefore not in K.)*

### Example 3 (board, page 3): a **reflexive** counter-model for Grz

Notation: **A = □(□(p→□p)→p)**, **B = □(p→□p) → p**.

| Step | Action | Result |
| --- | --- | --- |
| 0 | start | t₀: Δ₀ = {Grz} |
| 1 | (S6) | A ∈ Γ₀, p ∈ Δ₀ |
| 2 | **T-rule**: A ∈ Γ₀ | **B ∈ Γ₀** |
| 3 | (S5) on B ∈ Γ₀: either □(p→□p) ∈ Δ₀ or p ∈ Γ₀ | p ∈ Γ₀ **clashes** with p ∈ Δ₀, so take **□(p→□p) ∈ Δ₀** |
| 4 | witness for □(p→□p) ∈ Δ₀ | new t₁ with **(p→□p) ∈ Δ₁** |
| 5 | push A ∈ Γ₀ into t₁ | **B ∈ Γ₁** |
| 6 | (S6) on (p→□p) ∈ Δ₁ | **p ∈ Γ₁, □p ∈ Δ₁** |
| 7 | (S5) on B ∈ Γ₁: p ∈ Γ₁ already holds | no branching needed |
| 8 | witness for □p ∈ Δ₁ | new t₂ with **p ∈ Δ₂** |
| 9 | push true boxes of t₁ | Γ₁ = {p, B} has no top-level box, nothing to push |
| 10 | loops | t₀, t₁, t₂ reflexive. HS_m1 for the loop at t₀ holds (B ∈ Γ₀) |

Tableaux: **t₀** (A, B | Grz, p, □(p→□p)); **t₁** (p, B | p→□p, □p); **t₂** (∅ | p).

**Model:** all points reflexive, arrows **t₀ → t₁ → t₂**, **V(p) = {t₁}** (p false at t₀ and t₂, true at t₁). *The frame is **not transitive**: there is no arrow t₀ → t₂.* **Verify:** at t₁, □p is false (t₂ has no p), so p → □p is false at t₁, so □(p→□p) is false at t₀ (t₁ is a successor), so B is true at t₀. At t₁, p is true, so B is true. So A is true at t₀ (successors are t₀ and t₁). But p is false at t₀. So **Grz is false at t₀** ✓.

⚠ **Why transitivity must not be assumed:** if you add the arrow t₀ → t₂, then B must hold at t₂. But p is false at t₂ and □(p→□p) is true there (t₂'s only successor is itself, where p→□p holds because p is false). So B fails at t₂ and A becomes false at t₀, and the model stops being a counter-model.

### Example 4 (mine): refute **□(p ∨ q) → □p ∨ □q** (a **branching** rule)

| Step | Action | Result |
| --- | --- | --- |
| 0 | start | Δ₀ = {φ} |
| 1 | (S6) | **□(p∨q) ∈ Γ₀**, (□p ∨ □q) ∈ Δ₀ |
| 2 | (S4) | □p, □q ∈ Δ₀ |
| 3 | witness for □p ∈ Δ₀ | t₁ with **p ∈ Δ₁** |
| 4 | witness for □q ∈ Δ₀ | t₂ with **q ∈ Δ₂** |
| 5 | push □(p∨q) | **(p∨q) ∈ Γ₁** and **(p∨q) ∈ Γ₂** |
| 6 | (S3) at t₁: p ∈ Γ₁ or q ∈ Γ₁ | p ∈ Γ₁ **clashes** with p ∈ Δ₁, so **q ∈ Γ₁** |
| 7 | (S3) at t₂: p ∈ Γ₂ or q ∈ Γ₂ | q ∈ Γ₂ **clashes**, so **p ∈ Γ₂** |

**Model:** t₀ → t₁, t₀ → t₂. V(q) = {t₁}, V(p) = {t₂}. **Verify:** p ∨ q is true at both successors, so □(p∨q) is true at t₀. p is false at t₁ and q is false at t₂, so □p and □q are both false. So φ is false at t₀ ✓.

**Lesson:** one of the two options of a branching rule often clashes; just take the other. You only declare "valid" if **both** options clash.

### Example 5 (mine): a **valid** formula, so every branch closes: **□(p → q) → (□p → □q)** (axiom K)

| Step | Action | Result |
| --- | --- | --- |
| 0 | start | Δ₀ = {φ} |
| 1 | (S6) | □(p→q) ∈ Γ₀, (□p→□q) ∈ Δ₀ |
| 2 | (S6) again | □p ∈ Γ₀, □q ∈ Δ₀ |
| 3 | witness for □q ∈ Δ₀ | t₁ with **q ∈ Δ₁** |
| 4 | push both true boxes | **(p→q) ∈ Γ₁** and **p ∈ Γ₁** |
| 5 | (S5) on (p→q) ∈ Γ₁: p ∈ Δ₁ or q ∈ Γ₁ | p ∈ Δ₁ **clashes** with p ∈ Γ₁; q ∈ Γ₁ **clashes** with q ∈ Δ₁ |

**Both options clash, and every earlier step was forced**, so **no counter-model exists** and **φ ∈ K** ✓. (Extra successors cannot help: the false box □q ∈ Δ₀ forces at least this witness, which already clashes.)

### Example 6 (mine): refute axiom 4, **□p → □□p**, in a **reflexive** model

| Step | Action | Result |
| --- | --- | --- |
| 0 | start | Δ₀ = {□p→□□p} |
| 1 | (S6) | □p ∈ Γ₀, □□p ∈ Δ₀ |
| 2 | T-rule on □p ∈ Γ₀ | **p ∈ Γ₀** |
| 3 | witness for □□p ∈ Δ₀ | t₁ with **□p ∈ Δ₁** |
| 4 | push □p from Γ₀ | **p ∈ Γ₁** |
| 5 | witness for □p ∈ Δ₁ | t₂ with **p ∈ Δ₂** |
| 6 | push from Γ₁ = {p} | nothing |

**Model:** reflexive points, arrows t₀ → t₁ → t₂ (**no** t₀ → t₂). V(p) = {t₀, t₁}. **Verify:** □p at t₀: successors t₀, t₁ both have p ✓. □□p at t₀: □p at t₁ needs p at t₂, which fails, so □p is false at t₁ and □□p is false at t₀. So φ is false at t₀ ✓. *(It shows axiom 4 is not valid on all reflexive frames, in line with 4 needing transitivity.)*

### Example 7 (mine): using the ◇ rules, refute **◇p → □p**

| Step | Action | Result |
| --- | --- | --- |
| 0 | start | Δ₀ = {◇p → □p} |
| 1 | (S6) | **◇p ∈ Γ₀**, **□p ∈ Δ₀** |
| 2 | ◇p ∈ Γ₀: new successor | t₁ with **p ∈ Γ₁** |
| 3 | □p ∈ Δ₀: new successor | t₂ with **p ∈ Δ₂** |

**Model:** t₀ → t₁, t₀ → t₂, V(p) = {t₁}. **Verify:** ◇p is true at t₀ (t₁), □p is false at t₀ (t₂), so the implication is false ✓. *(t₁ and t₂ cannot be merged, because p would be in both Γ and Δ.)*

---

## 7. Common mistakes (check this list every time)

1. **Starting on the wrong side.** The formula to refute goes in **Δ (false)**, not Γ.
2. **Handling an implication wrongly.** A → B in **Δ** gives **A in Γ and B in Δ** (both things). A → B in **Γ** gives a **choice** (A in Δ or B in Γ).
3. **Forgetting to push true boxes (HS_m1) into every successor**, including successors that you create **later**. This is the most common error. After creating a new successor, always re-push all □A from the parent's Γ.
4. **Treating a false box like a true box.** □A ∈ Δ needs **one** successor with A in its Δ′. It does **not** apply to all successors.
5. **Giving up at the first clash on a branching rule.** A clash only kills that **option**. Try the other. "Valid" is correct only if **all** options clash.
6. **Not checking disjointness after every step.** Check Γ ∩ Δ = ∅ and ⊥ ∉ Γ in each tableau after you add formulas.
7. **Adding arrows you did not create** (for example reading the picture as transitive). Arrows are exactly the ones drawn (plus loops in the reflexive case). See the warning in Example 3.
8. **Forgetting the T-rule in reflexive questions**, or applying the T-rule in plain K questions. (Compare Exercise 5.)
9. **Merging successors blindly.** Merge only if the result stays disjoint (Example 7 cannot merge).
10. **Reading the final model wrongly.** V(p) = tableaux with p in **Γ**. Atoms in Δ, or in neither, are false.
11. **Skipping the final check.** Always evaluate φ at t₀ in your model.
12. **Not converting ◇ and ¬**, or converting them wrongly. Use the derived ◇ rules above or rewrite ◇A = ¬□¬A.

---

## 8. Exercises (try first, then read the solutions)

1. Decide: is **□(p ∧ q) → □p** in K? If not, give a counter-model.
2. Refute **□p ∨ □¬p** in K.
3. Decide: is **□(p → q) → (◇p → ◇q)** in K?
4. Refute **◇p ∧ ◇q → ◇(p ∧ q)** in K.
5. Treat **□p → p**: (a) refute it in K, (b) try to refute it with the reflexive rule.
6. Give a **reflexive** counter-model for **p → □p**.

**Solutions**

1. **t₀:** (S6) gives □(p∧q) ∈ Γ₀ and □p ∈ Δ₀. Witness t₁ with p ∈ Δ₁. Push: (p∧q) ∈ Γ₁, then (S1): p, q ∈ Γ₁. **Clash** with p ∈ Δ₁, and there was no choice. So it is **in K**.
2. **t₀:** Δ₀ = {□p ∨ □¬p}. (S4): □p, □¬p ∈ Δ₀. Witness t₁: p ∈ Δ₁. Witness t₂: ¬p ∈ Δ₂, so (¬Δ) p ∈ Γ₂. **Model:** t₀ → t₁ (p false), t₀ → t₂ (p true). Check: □p fails at t₁, □¬p fails at t₂ ✓.
3. **t₀:** (S6): □(p→q) ∈ Γ₀, (◇p→◇q) ∈ Δ₀; (S6) again: **◇p ∈ Γ₀, ◇q ∈ Δ₀**. ◇p ∈ Γ₀: new t₁ with p ∈ Γ₁. ◇q ∈ Δ₀: **q ∈ Δ for every successor**, so q ∈ Δ₁. Push □(p→q): (p→q) ∈ Γ₁. (S5): p ∈ Δ₁ (clash with p ∈ Γ₁) or q ∈ Γ₁ (clash with q ∈ Δ₁). **Both clash, so it is in K.**
4. **t₀:** Γ₀ ∋ ◇p ∧ ◇q, Δ₀ ∋ ◇(p∧q). (S1): ◇p, ◇q ∈ Γ₀. Witness t₁: p ∈ Γ₁. Witness t₂: q ∈ Γ₂. ◇(p∧q) ∈ Δ₀ pushes (p∧q) ∈ Δ into **every** successor. (S2) at t₁: p ∈ Δ₁ (clash) or **q ∈ Δ₁** ✓. (S2) at t₂: **p ∈ Δ₂** ✓. **Model:** t₀ → t₁ (p true, q false), t₀ → t₂ (q true, p false). Check: ◇p, ◇q true; p∧q false at both successors, so ◇(p∧q) false ✓. (A single successor with p, q ∈ Γ would put p∧q in both Γ and Δ, which is why two successors are needed.)
5. (a) In K: Γ₀ ∋ □p, Δ₀ ∋ p. Δ₀ has no box, so there is no witness. **Model:** one dead-end point with p false (□p vacuously true). (b) With the T-rule: □p ∈ Γ₀ forces **p ∈ Γ₀**, which clashes with p ∈ Δ₀, with no choice. **No reflexive counter-model: □p → p is valid on reflexive frames.**
6. t₀: p ∈ Γ₀, □p ∈ Δ₀. Witness t₁: p ∈ Δ₁. T-rule: Γ₀ has no box, so nothing. **Model:** t₀ (p true) → t₁ (p false), both reflexive. Check: □p at t₀ fails (t₁), and p true at t₀, so p → □p is false ✓.

---

## One-page cheat card

- **Tableau** t = (Γ, Δ): Γ = must be **true**, Δ = must be **false**. Start: **t₀ = (∅, {φ})**.
- **Saturate** with S1 to S6. **Branching rules:** A∧B in Δ, A∨B in Γ, A→B in Γ.
- **Clash** if Γ ∩ Δ ≠ ∅ or ⊥ ∈ Γ → that branch dies. **All branches die ⇒ φ ∈ K.**
- **□A in Δ:** make a **new successor** with A in Δ′ (one witness is enough).
- **□A in Γ:** put A into Γ′ of **every** successor (existing and future).
- **Reflexive:** □A ∈ Γ ⇒ A ∈ Γ (same tableau), add loops. Do **not** add transitivity arrows.
- **◇A in Γ:** new successor with A in Γ′. **◇A in Δ:** A in Δ′ of every successor.
- **Read model:** points = tableaux, arrows as drawn, V(p) = tableaux with p ∈ Γ. **Always verify φ is false at t₀.**
- **Theory:** Hintikka system for (∅,{φ}) ⇒ φ refuted. Realizable ⇔ Hintikka system with ≤ 2^|Σ| tableaux. So counter-models can be **finite** (≤ 2^|Sub φ| points, rooted), even **finite intransitive trees**, and K = formulas valid on all finite intransitive trees.

---

*(Next lecture goes below this line.)*