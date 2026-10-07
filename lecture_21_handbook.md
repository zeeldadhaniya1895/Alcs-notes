# Advanced Logic Handbook: Lecture 21

# Lecture 21: Modal Frames and Formulas (frame correspondence)

**What this lecture covers:** which **formulas are valid on which frames**. For each formula we find a **frame condition** C such that *𝔉 validates the formula iff 𝔉 satisfies C*: reflexive, transitive, symmetric, serial, the Geach family ga_{klmn}, n-transitive, dense, Euclidean, (strongly) directed, strongly connected.

**How to read each section.** Every topic has three layers:
1. **Math:** the precise statement and proof (what you write in exams).
2. **Room-and-light picture:** the building-with-doors story (for intuition).
3. **Normal explanation:** the same idea in ordinary words.

Section 1 is a **recipe** for finding and proving a correspondence. Use it for every formula; this is where the mistakes usually happen.

**Quick recap.**
- **𝔉 validates φ** (𝔉 ⊨ φ) means φ is true at **every point under every valuation** V on 𝔉.
- To **show a formula is NOT valid** on 𝔉, you need **one** valuation and **one** point where it is false.
- To **show it IS valid**, you must handle **all** valuations.
- xRⁿy means a walk of **exactly n** steps; xR⁰y means x = y. ◇ᵏ and □ˡ mean k diamonds and l boxes in a row (k = 0 means none).
- Names used on the board: **re** = □p → p, **tra** = □p → □□p.

**Notation notes and what is (not) on the board.**
- Page 2 states "validates tra iff transitive" but does **not** prove it; I supply the proof.
- Page 5 states "validates ser iff serial". The board proves one direction (page 4); I supply the other.
- The conjunction in **tra_n** has an index that reads **i = 1** (small handwriting). I checked that i = 1 matches the board's definition of n-transitive; with i = 0 it would not (see Section 7).
- The words **"strongly directed"** and **"strongly connected"** are used but **not defined** on these pages. I give the conditions derived from the formulas and **verified them** (Sections 7 and 8).
- The proofs for Euclidean, strongly directed, directed and SC are not on the board; they are mine.
- The board writes the family as **ga_{klmn}**. I read it as the **Geach family** (the board later calls ◇□p → □◇p "the Geach formula").

---

## 1. THE RECIPE: how to find and prove a frame condition

**Goal:** given a formula φ, find a condition C on R such that **𝔉 ⊨ φ iff 𝔉 satisfies C**.

### Part A: guess C by imagining a counter-model
1. **Assume a counter-model:** a model on 𝔉 and a point x where **φ is false**: the premise (left of →) is true at x and the conclusion is false at x.
2. **Unpack with the truth definition.** □ψ false at x gives a **successor** where ψ is false. ◇ψ true at x gives a **successor** where ψ is true. This creates **witnesses** y, z, … and facts such as "y ⊨ □ˡp" or "z ⊭ p".
3. **Find the relational facts these force**, usually of the type "¬yRx" or "there is no u with …". Typical trick: if y ⊨ □p and z ⊭ p, then ¬yRz.
4. The **configuration** you found (witnesses with their forced facts) must exist in any frame refuting φ. Its **negation is C.**

### Part B: prove "C ⇒ valid"
5. Assume 𝔉 satisfies C and suppose, for contradiction, a counter-model. Run step 2 again to get the witnesses and **apply C** to them. It gives a contradiction. (This is Part A read backwards.)

### Part C: prove "not C ⇒ not valid" (build a counter-valuation)
6. Assume C **fails**: take the **bad witnesses** x, y, z, … that violate C.
7. **Define V cleverly (the minimal valuation).** Make the premise true using the **smallest sets** possible. Rules of thumb:

| Situation | Choose V(p) = … |
|---|---|
| premise needs p true at x only | **{x}** |
| premise is □p and p must fail at one specific point z | **W ∖ {z}** |
| premise is ◇ᵏ□ˡp, witnessed at y | **{u : yRˡu}** (so □ˡp holds at y, and nowhere else more than needed) |
| two variables, each tied to a different witness | one set per witness (for example V(p) = {u : yRu}, V(q) = {u : zRu}) |

8. **Verify** by evaluating φ at x: the premise is true, the conclusion false. Check **each** step (witnesses y, z really are successors, the false conclusion really fails).

### Part D: sanity check
9. Test C and φ on 2 to 3 tiny frames (Section 9 has ready-made ones).

**Why this works.** "All valuations" is a ∀ over sets. Step 7 turns that ∀ into one concrete set, and the truth definition then gives a first-order statement about R.

---

## 2. re: □p → p  ⟺  reflexive

### Math
**Proposition.** A frame 𝔉 validates □p → p **iff 𝔉 is reflexive.**

**Proof.**
- (**not reflexive ⇒ not valid**) If 𝔉 = ⟨W,R⟩ is not reflexive, then ¬xRx for some x ∈ W. Let **V(p) = W ∖ {x}**. Then **x ⊨ □p** (every successor of x differs from x, so it lies in V(p)) and **x ⊭ p**. So x ⊭ □p → p.
- (**reflexive ⇒ valid**) If 𝔉 is reflexive and the formula were false at x under some model, then x ⊨ □p and x ⊭ p. But xRx and x ⊨ □p give x ⊨ p. Contradiction. ∎

> **Room-and-light picture:** a room has a door to itself. "All my doors lead to lit rooms" then includes the door to myself, so I must be lit too. If a room has no self-door, switch off only that room: all its doors lead to lit rooms, but the room itself is dark.

> **Normal explanation:** □p → p says "necessarily p implies p", i.e. the actual world is among the possible ones. That is exactly xRx. (This is axiom T from your revision table.)

---

## 3. tra: □p → □□p  ⟺  transitive

### Math
**Proposition.** 𝔉 validates □p → □□p **iff 𝔉 is transitive.** *(Stated on the board; proof mine.)*

**Proof.**
- (**not transitive ⇒ not valid**) Let xRy, yRz, ¬xRz. Take **V(p) = W ∖ {z}**. Then x ⊨ □p (no successor of x is z). But y is a successor of x with y ⊭ □p (since yRz and z ⊭ p), so x ⊭ □□p.
- (**transitive ⇒ valid**) Suppose x ⊨ □p and xRy, yRz. Then xRz, so z ⊨ p. Hence x ⊨ □□p. ∎

> **Room-and-light picture:** if every door from x leads to a lit room, and you walk two doors x → y → z, the room z must also be lit. That is guaranteed only if there is a **shortcut door x → z**.

> **Normal explanation:** transitivity means a step of a step is a step. Then "p in all next states" automatically passes along two steps. (Axiom 4.)

---

## 4. sym: p → □◇p  ⟺  symmetric

### Math
**Necessary condition (board, pages 2 to 3).** Suppose a counter-model on 𝔉 = ⟨W,R⟩. Then x ⊨ p and x ⊭ □◇p for some x. So there is a successor y (xRy) with y ⊭ ◇p. Since x ⊨ p, we must have **¬yRx** (otherwise y would have a successor satisfying p). So a counter-model forces **∃x,y (xRy ∧ ¬yRx)**.

Hence a **sufficient condition for validity** is **∀x,y (xRy → yRx)**. A frame satisfying it is called **symmetric**.

**Proposition.** 𝔉 validates **sym = p → □◇p iff 𝔉 is symmetric.**

**Proof (not symmetric ⇒ not valid, board).** There are x, y with xRy and ¬yRx. Define **V(p) = {x}**. Then x ⊨ p. Also y ⊭ ◇p (y's successors do not include x, and p holds only at x). So x ⊭ □◇p. Hence x ⊭ p → □◇p. The other direction is the necessary-condition argument above. ∎

> **Room-and-light picture:** I am lit. If every door of mine has a **way back**, then from each neighbour I can see a lit room (me): "◇p holds at each neighbour". If a neighbour y has no door back to me, y sees nothing lit.

> **Normal explanation:** "if p then necessarily possibly p": whatever else is reachable from here can come back to here. This is axiom B. Notice that V(p) = {x} is the **minimal** valuation: p is true only where the premise needs it.

---

## 5. ser: □p → ◇p  ⟺  serial

### Math
**Necessary condition (board, page 4).** Suppose a counter-model: x ⊨ □p and x ⊭ ◇p for some x. Then **x is a dead end**: if xRy for some y, then y ⊨ p (from □p) and y ⊭ p (from ¬◇p), a contradiction. So a counter-model forces **∃x ∀y ¬xRy**.

Hence a **sufficient condition** for 𝔉 ⊨ □p → ◇p is **seriality: ∀x ∃y xRy**.

**Proposition.** 𝔉 validates **ser = □p → ◇p iff 𝔉 is serial.**
*(Converse, mine:)* if x is a dead end, then x ⊨ □p (vacuous) and x ⊭ ◇p under **any** valuation, so the formula is false at x. ∎

> **Room-and-light picture:** a room with **no door at all**: "all doors lead to lit rooms" is vacuously true, but "some door leads to a lit room" is false. Every room needs at least one door out.

> **Normal explanation:** □p → ◇p says "if p must hold next, then p can hold next". That is only reliable when a next state exists (seriality). This is axiom D.

---

## 6. The Geach family ga_{klmn} = ◇ᵏ□ˡp → □ᵐ◇ⁿp

### Math
Consider the **family** of formulas

> **ga_{klmn} = ◇ᵏ □ˡ p → □ᵐ ◇ⁿ p,**  where k, l, m, n are arbitrary natural numbers, possibly 0.

**Proposition.** 𝔉 = ⟨W,R⟩ validates ga_{klmn} **iff**

> **∀x,y,z ( xRᵏy ∧ xRᵐz → ∃u ( yRˡu ∧ zRⁿu ) ).**

**Proof.**
- (**condition ⇒ valid**, board page 5). Suppose a counter-model: x ⊨ ◇ᵏ□ˡp and x ⊭ □ᵐ◇ⁿp. Then there are y, z with **xRᵏy, y ⊨ □ˡp** and **xRᵐz, z ⊭ ◇ⁿp**. If some u had yRˡu and zRⁿu, then u ⊨ p (from y ⊨ □ˡp), so z ⊨ ◇ⁿp, a contradiction. So **no u** with yRˡu and zRⁿu exists. This violates the condition at (x,y,z). So if the condition holds, there is no counter-model.
- (**not condition ⇒ not valid**, board page 6). Suppose the condition fails: there are x, y, z with xRᵏy, xRᵐz, and for every u, **¬yRˡu or ¬zRⁿu**. Define **V(p) = { u ∈ W : yRˡu }**. Then y ⊨ □ˡp, so **x ⊨ ◇ᵏ□ˡp**. There is no u with zRⁿu and u ∈ V(p) (that would give yRˡu and zRⁿu), so z ⊭ ◇ⁿp and **x ⊭ □ᵐ◇ⁿp**. So ga_{klmn} is false at x. ∎

### Special cases (my computation from the condition)
| Formula | (k,l,m,n) | Condition becomes | Name |
|---|---|---|---|
| □p → p | (0,1,0,0) | xRx | reflexive |
| □p → □□p | (0,1,2,0) | xR²z → xRz | transitive |
| p → □◇p | (0,0,1,1) | xRz → zRx | symmetric |
| □p → ◇p | (0,1,0,1) | ∃u xRu | serial |
| ◇□p → □p | (1,1,1,0) | xRy ∧ xRz → yRz | Euclidean |
| ◇□p → □◇p | (1,1,1,1) | xRy ∧ xRz → ∃u(yRu ∧ zRu) | strongly directed |
| □ⁿ⁺¹p → □ⁿp | (0,n+1,n,0) | xRⁿz → xRⁿ⁺¹z | n-dense |
| p → □p | (0,0,1,0) | xRz → z = x | R inside identity |
| ◇p → □p | (1,0,1,0) | xRy ∧ xRz → y = z | R functional |
| ◇p → □◇p | (1,0,1,1) | xRy ∧ xRz → zRy | Euclidean |

*(For k = 0 or m = 0, "xR⁰y" just means x = y, so the variables collapse.)*

> **Room-and-light picture:** the formula says "if from x I can walk k doors to a room y from which all l-door walks are lit, then from x, after m doors to any z, I can reach a lit room in n doors". The condition says: from y (l steps) and from z (n steps) you can **always reach a common room u**. Then a lit room reachable from y must also be reachable from z.

> **Normal explanation:** the family is a template. One proof handles all of T, 4, B, D, 5-style, confluence and density at once. In the literature these are the **Geach (Lemmon–Scott)** formulas, and they are special cases of **Sahlqvist** formulas (my remark, from your revision notes). The key idea is the minimal valuation V(p) = {u : yRˡu}.

---

## 7. n-transitive, dense, n-dense, Euclidean

### n-transitive (board, page 7)
**Definition.** 𝔉 is **n-transitive** if **∀x,y ( xRⁿ⁺¹y → xRy ∨ xR²y ∨ … ∨ xRⁿy )**.

**Corollary.** 𝔉 validates **tra_n = ⋀_{i=1}^{n} □ⁱp → □ⁿ⁺¹p** iff 𝔉 is n-transitive.

**Proof (mine).**
- (n-transitive ⇒ valid) Let x ⊨ □ⁱp for i = 1..n and xRⁿ⁺¹z. Then xRⁱz for some i ≤ n, so z ⊨ p. Hence x ⊨ □ⁿ⁺¹p.
- (not n-transitive ⇒ not valid) Take xRⁿ⁺¹z with ¬xRⁱz for all i = 1..n. Let **V(p) = W ∖ {z}**. Then x ⊨ □ⁱp for i = 1..n (z is not reachable in i steps), but z is reachable in n+1 steps and z ⊭ p, so x ⊭ □ⁿ⁺¹p. ∎

**n = 1** gives □p → □□p and "transitive".
*(Check on the index:)* with i starting at **0** the formula would be p ∧ □p → □□p, which is valid on the **2-cycle** {a,b} with R = {(a,b),(b,a)}, a frame that is **not** transitive (aRb, bRa, ¬aRa). So i = 1 is the right reading.

### Dense and n-dense (board, page 7)
**Definition.** **Dense:** ∀x,y (xRy → xR²y). **n-dense:** ∀x,y (xRⁿy → xRⁿ⁺¹y).
**Corollary.** 𝔉 validates **den_n = □ⁿ⁺¹p → □ⁿp** iff 𝔉 is n-dense. *(An instance of ga_{0,n+1,n,0}.)*
**n = 0:** xR⁰y → xR¹y, i.e. x = y → xRx, which is **reflexive** (and □p → p). **n = 1:** □□p → □p ⟺ dense.

### Euclidean (board, page 8)
**Definition.** **Euclidean:** ∀x,y,z (xRy ∧ xRz → yRz). (Two successors of the same point see each other, in that direction.)
**Corollary.** 𝔉 validates **euc = ◇□p → □p** iff 𝔉 is Euclidean.

**Proof (mine, same pattern).**
- (Euclidean ⇒ valid) If x ⊨ ◇□p, pick y with xRy, y ⊨ □p. For any z with xRz, Euclidean gives yRz, so z ⊨ p. So x ⊨ □p.
- (not Euclidean ⇒ not valid) Take xRy, xRz, ¬yRz. Let **V(p) = {u : yRu}**. Then y ⊨ □p, so x ⊨ ◇□p. But z ∉ V(p) (as ¬yRz), so x ⊭ □p. ∎

> **Room-and-light picture:** **n-transitive:** a walk of n+1 doors can be replaced by a walk of at most n doors from the same start. **Dense:** every door x → y can be **split** into two doors x → z → y (you can squeeze a room in between). **Euclidean:** if x has doors to y and to z, then **y has a door to z** (siblings see each other).

> **Normal explanation:** these are variations on the same theme: "paths can be shortened" (n-transitive), "paths can be lengthened" (dense), "two successors of one point are related" (Euclidean). In each case the proof is the same: counter-model gives witnesses, and the minimal valuation shows the converse.

---

## 8. Directedness and strong connectedness

### Strongly directed (board, page 8)
**Corollary.** 𝔉 ⊨ **◇□p → □◇p** iff 𝔉 is **strongly directed**, i.e.

> **∀x,y,z ( xRy ∧ xRz → ∃u ( yRu ∧ zRu ) ).**

*(The board does not write this out; it is the ga_{1,1,1,1} condition, and the board calls this formula "the Geach formula".)*

### Directed (board, page 8)
**Directedness condition:** **∀x,y,z ( xRy ∧ xRz ∧ y ≠ z → ∃u ( yRu ∧ zRu ) ).**
**Proposition.** 𝔉 ⊨ **dir = ◇(□p ∧ q) → □(◇p ∨ q)** iff 𝔉 is **directed**.

**Proof (mine).**
- (directed ⇒ valid) Suppose a counter-model at x. Then some successor y has □p ∧ q, and some successor z has ¬◇p ∧ ¬q. Since q holds at y and fails at z, **y ≠ z**. By directedness there is u with yRu and zRu. Then u ⊨ p (from y ⊨ □p), so z ⊨ ◇p, a contradiction.
- (not directed ⇒ not valid) Take xRy, xRz, y ≠ z with no common successor. Let **V(p) = {u : yRu}** and **V(q) = {y}**. Then y ⊨ □p ∧ q, so x ⊨ ◇(□p ∧ q). Point z has q false (z ≠ y) and no successor in V(p) (no common successor), so z ⊭ ◇p ∨ q and x ⊭ □(◇p ∨ q). ∎

**Difference:** *strongly* directed also applies to the case **y = z**, so it requires every successor y of x to have **a successor** (take z = y: ∃u yRu). *Directed* does not.

### Strongly connected (board, page 9)
**Proposition.** 𝔉 validates **SC = □(□p → q) ∨ □(□q → p)** iff 𝔉 is **strongly connected**, i.e. *(derived and verified, not written on the board)*:

> **∀x,y,z ( xRy ∧ xRz → yRz ∨ zRy ).**

**Proof (mine).**
- (condition ⇒ valid) Suppose SC is false at x. Then there are successors y, z with y ⊨ □p, y ⊭ q, and z ⊨ □q, z ⊭ p. By the condition yRz or zRy. If yRz, then y ⊨ □p gives z ⊨ p, a contradiction. If zRy, then z ⊨ □q gives y ⊨ q, a contradiction.
- (condition fails ⇒ not valid) Take xRy, xRz, ¬yRz, ¬zRy. Let **V(p) = {u : yRu}** and **V(q) = {u : zRu}**. Then y ⊨ □p and y ⊭ q (as ¬zRy), so x ⊭ □(□p → q). Also z ⊨ □q and z ⊭ p (as ¬yRz), so x ⊭ □(□q → p). Hence x ⊭ SC. ∎

**Note the case y = z.** The condition then says **yRy**: every successor of x must see itself. That is exactly why the **merged model of Lecture 20** (t₀ → t, with t irreflexive) refutes SC.

> **Room-and-light picture:** **Directed:** two different rooms reachable from x can always **meet again** in a common room. **Strongly connected:** any two rooms behind doors of x (the same room twice included) are connected by a door one way or the other. A "fork" (x with two rooms y, z that do not see each other) breaks both.

> **Normal explanation:** these are the conditions behind **confluence/.2** and **linearity/.3** axioms (my remark: S4.2 and S4.3 in the literature). Both refuse "forks": branches must reconverge (directed) or be comparable (strongly connected).

---

## 9. Overview tables

### 9.1 Correspondences
| Formula | Name | Frame condition | Source |
|---|---|---|---|
| □p → p | re (T) | reflexive | board |
| □p → □□p | tra (4) | transitive | board (stated), proof mine |
| p → □◇p | sym (B) | symmetric | board |
| □p → ◇p | ser (D) | serial | board |
| ◇ᵏ□ˡp → □ᵐ◇ⁿp | Geach family | xRᵏy ∧ xRᵐz → ∃u(yRˡu ∧ zRⁿu) | board |
| ⋀_{i=1}^{n}□ⁱp → □ⁿ⁺¹p | tra_n | n-transitive | board, proof mine |
| □ⁿ⁺¹p → □ⁿp | den_n | n-dense | board |
| ◇□p → □p | euc | Euclidean | board, proof mine |
| ◇□p → □◇p | Geach (.2) | strongly directed | board |
| ◇(□p∧q) → □(◇p∨q) | dir | directed | board, proof mine |
| □(□p→q) ∨ □(□q→p) | SC | strongly connected | board, proof mine |

### 9.2 Frame test (use it to check your understanding)
Frames: **F1** = a → b. **F2** = one reflexive point. **F3** = two points, universal relation. **F4** = (ℕ, <). **F5** = fork a → b, a → c. **C2** = 2-cycle a ⇄ b (no loops).

| Property | F1 | F2 | F3 | F4 | F5 | C2 |
|---|---|---|---|---|---|---|
| reflexive | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ |
| transitive | ✓ | ✓ | ✓ | ✓ | ✓ | ✗ |
| symmetric | ✗ | ✓ | ✓ | ✗ | ✗ | ✓ |
| serial | ✗ | ✓ | ✓ | ✓ | ✗ | ✓ |
| Euclidean | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ |
| dense | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ |
| strongly directed | ✗ | ✓ | ✓ | ✓ | ✗ | ✓ |
| directed (y ≠ z) | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ |
| strongly connected | ✗ | ✓ | ✓ | ✗ | ✗ | ✗ |

*(Also: C2 is 2-transitive but not transitive.)*

**Facts relating the conditions (mine, checked).**
- **Reflexive + Euclidean ⇒ symmetric.** (xRy and xRx give yRx by Euclid.)
- **Symmetric + Euclidean ⇒ transitive.** (xRy, yRz: yRx by symmetry, then Euclid at y gives xRz.)
- So **reflexive + Euclidean ⇒ equivalence relation** (the S5 case from your revision).

---

## 10. Worked examples (using the recipe)

### Example 1: find the condition for **p → □p**
- **Part A.** Counter-model: x ⊨ p and x ⊭ □p, so some successor y has y ⊭ p. Since x ⊨ p, **y ≠ x**. Forced configuration: **xRy with y ≠ x**. So C = **∀x,y (xRy → y = x)** (R ⊆ identity).
- **Part B.** Under C, any successor of x is x itself; but x ⊨ p, so □p holds. No counter-model. ✓
- **Part C.** If xRy with y ≠ x: **V(p) = {x}**. Then x ⊨ p, y ⊭ p, so x ⊭ □p. The formula is false at x. ✓
- *(Check with the table: it is the ga_{0,0,1,0} case.)*

### Example 2: find the condition for **◇p → □p**
- **Part A.** Counter-model: x ⊨ ◇p gives a successor y ⊨ p; x ⊭ □p gives a successor z ⊭ p. So **y ≠ z**. Forced configuration: **xRy, xRz, y ≠ z**. C = **∀x,y,z (xRy ∧ xRz → y = z)** (R is functional: at most one successor).
- **Part C.** If xRy, xRz, y ≠ z: **V(p) = {y}**. Then x ⊨ ◇p, z ⊭ p, so x ⊭ □p. ✓

### Example 3: use the Geach condition for **□p → ◇◇p**
Here **□p = ◇⁰□¹p** (k=0, l=1) and **◇◇p = □⁰◇²p** (m=0, n=2), so (0,1,0,2). The condition: xR⁰y ∧ xR⁰z → ∃u (yR¹u ∧ zR²u). Since y = z = x: **∀x ∃u (xRu ∧ xR²u)** (every point has a successor that is also a 2-step successor).
**Direct check of Part C:** if this fails at x, set **V(p) = x↑**. Then x ⊨ □p. A point u with xR²u and u ⊨ p would be in x↑ ∩ x↑², which is empty. So x ⊭ ◇◇p. ✓

### Example 4: evaluate on frames (using the table)
**Which of the formulas re, tra, sym, ser are valid on F1 (a → b)?**
From the table: transitive ✓ ⇒ tra valid. Not reflexive, not symmetric, not serial ⇒ re, sym, ser **not** valid.
*Refute sym on F1 explicitly:* **V(p) = {a}**: a ⊨ p, b is a dead end so b ⊭ ◇p, hence a ⊭ □◇p and a ⊭ p → □◇p. ✓

### Example 5: tie-in with Lecture 20
The **fork F5** (a → b, a → c) is the frame of Lecture 20's first counter-model for SC. In terms of Section 8, it violates strong connectedness (b and c do not see each other) and also directedness. *Refute dir on F5 explicitly:* x = a, y = b, z = c. **V(p) = {u : bRu} = ∅, V(q) = {b}.** Then b ⊨ □p (dead end) and q, so a ⊨ ◇(□p ∧ q). At c: ◇p is false (no successors) and q is false, so c ⊭ ◇p ∨ q, hence a ⊭ □(◇p ∨ q). ✓

---

## 11. Common mistakes (check this list every time)

1. **Mixing "validates" and "true in a model".** Validity needs **all valuations**. A single model where the formula is true proves nothing about validity.
2. **Choosing V arbitrarily.** To refute validity, choose the **minimal valuation** from the table in Section 1 and **verify** both the premise and the failed conclusion.
3. **Forgetting the case y = z** (or y = x) in conditions: strong connectedness requires yRy, and "strongly directed" requires every successor to have a successor. *Directed* excludes y = z; *strongly directed* does not.
4. **Confusing the conditions:** T → reflexive, D → serial, 4 → transitive, B → symmetric, ◇□p → □p → Euclidean, ◇□p → □◇p → strongly directed. Check by running Part A once.
5. **Treating xRⁿy as "within n steps".** It means **exactly n steps** (and xR⁰y means x = y). That is why n-transitive and n-dense have the shapes they have.
6. **Reading the n-transitive axiom with i = 0.** That gives a different (weaker) formula (see the 2-cycle in Section 7).
7. **Proving only one direction.** Each correspondence is an "iff": show C ⇒ valid **and** not C ⇒ not valid.
8. **Confusing necessary and sufficient.** A counter-model *forces* a configuration (necessary for failure). Its negation is therefore *sufficient* for validity. The converse needs Part C.
9. **Wrong witness bookkeeping.** □ψ false gives *one* successor where ψ fails. ◇ψ true gives *one* successor where ψ holds. Never "all".
10. **Assuming transitivity when drawing frames.** Draw all arrows explicitly when testing conditions such as Euclidean or n-transitive.

---

## 12. Exercises (try first, then read the solutions)

1. Use the recipe to find the frame condition of **◇p → □◇p**. Compare with Euclidean.
2. Show that the **2-cycle C2** validates □□□p ∧ □□p ∧ □p → □⁴... no: show that C2 is **2-transitive** and state which formula it therefore validates.
3. Give a valuation refuting **□p → □□p** on the frame **a → b → c** with **R = {(a,b),(b,c)}** (not transitive), at the point a.
4. Is **□p → ◇p** valid on **F5** (the fork)? Give a refutation if not.
5. On which of F1 to F5, C2 is **□□p → □p** valid? (Use the table.)
6. Prove that **p → □p** is valid on F2 (one reflexive point) and refute it on **F3** (two points, universal relation).

**Solutions**

1. ◇p → □◇p = ga_{1,0,1,1}. **Part A:** counter-model: x ⊨ ◇p gives y ⊨ p with xRy; x ⊭ □◇p gives z with xRz and z ⊭ ◇p. Then **¬zRy** (else z would have a successor satisfying p). Forced: xRy, xRz, ¬zRy. **C = ∀x,y,z (xRy ∧ xRz → zRy)**, which is **Euclidean** (rename y ↔ z). **Part C:** if xRy, xRz, ¬zRy, set **V(p) = {y}**: x ⊨ ◇p, and z ⊭ ◇p (its successors do not include y), so x ⊭ □◇p. ✓

2. C2 has R = {(a,b),(b,a)}, so R³ = R (odd lengths go to the other point) and R² = {(a,a),(b,b)}. Check 2-transitivity: xR³y → xRy ∨ xR²y: if aR³b then aRb ✓; if bR³a then bRa ✓. So **C2 is 2-transitive** and therefore validates **tra₂ = □p ∧ □²p → □³p**. It is **not** transitive (aRb, bRa, ¬aRa), so it does **not** validate □p → □□p. *(Refutation: V(p) = {b}... take x = a, y = b, z = a... check: a ⊨ □p (only successor b ∈ V(p)), and a ⊭ □□p since b's successor a ∉ V(p). ✓)*

3. Take **V(p) = {b}**... careful: a ⊨ □p needs all successors of a to satisfy p: b ∈ V(p) ✓. □□p at a needs □p at b: b's successor is c; with c ∉ V(p), b ⊭ □p. So a ⊭ □□p. **V(p) = {b}** works (equivalently W ∖ {c} = {a,b}, also works). ✓

4. **No, it is not valid.** F5 is not serial (b and c are dead ends). At b: □p is vacuously true and ◇p is false for any V, so **b ⊭ □p → ◇p** (even for V = ∅). ✓

5. □□p → □p is valid iff the frame is **dense**. From the table: **F2 and F3 only** (dense ✓). It is not valid on F1, F4, F5 or C2. *(E.g. F4: 0 < 1 but 0R²1 fails; set V(p) = W ∖ {1}: 0 ⊨ □□p (the points two steps away are 2,3,… which satisfy p) while 0 ⊭ □p since 1 ∉ V(p).)*

6. **F2** (aRa only): R ⊆ identity, so the condition of Example 1 holds, hence valid. Direct: if a ⊨ p then a ⊨ □p, since the only successor is a. **F3** (points a₁, a₂, universal): a₁R a₂ with a₂ ≠ a₁. **V(p) = {a₁}**: a₁ ⊨ p but a₂ ⊭ p, so a₁ ⊭ □p. ✓

---

## One-page summary

- **Frame validity = truth under all valuations.** Refute with **one** minimal valuation, prove with all.
- **Recipe:** (A) assume a counter-model, unpack into witnesses, read off the forced configuration, negate it to get C. (B) C ⇒ valid by running A backwards. (C) not C ⇒ build V (minimal valuation) and verify. (D) sanity-check on small frames.
- **Key correspondences:** □p→p reflexive; □p→□□p transitive; p→□◇p symmetric; □p→◇p serial; ◇□p→□p (and ◇p→□◇p) Euclidean; ◇□p→□◇p strongly directed; □ⁿ⁺¹p→□ⁿp n-dense; ⋀_{i=1}^{n}□ⁱp→□ⁿ⁺¹p n-transitive; □(□p→q)∨□(□q→p) strongly connected; ◇(□p∧q)→□(◇p∨q) directed.
- **Geach family:** ◇ᵏ□ˡp → □ᵐ◇ⁿp ⟺ ∀x,y,z (xRᵏy ∧ xRᵐz → ∃u (yRˡu ∧ zRⁿu)), with minimal valuation V(p) = {u : yRˡu}.
- **Watch:** y = z cases, "exactly n steps", both directions of each iff.
- **Links:** Lecture 20's SC counter-models (fork, and the merged irreflexive point) are exactly frames violating strong connectedness.

---

*(Next lecture goes below this line.)*
