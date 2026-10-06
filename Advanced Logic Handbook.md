# Advanced Logic for Computer Science: Handbook

*Built lecture by lecture. Each lecture is one self-contained section; new lectures get appended at the bottom.*

**Contents**

- [Lecture 16: Modal Logic, Language, Frames, Models, Truth](#lecture-16)
- *(Lecture 17 goes here)*

---

# Lecture 16: Modal Logic, Language, Frames, Models, Truth

**What this lecture covers:** (1) why modal logic exists, (2) its language, (3) Kripke frames, (4) valuations and models, (5) the truth relation, (6) modal degree, (7) n-step accessibility and properties of R, and (8) a supplement from the reference book.

**Notation note:** I read this from handwritten board pages. Where a symbol was ambiguous I say so.

---

## The big picture (read this first)

Think of a **building with rooms and one-way doors**.

- **Rooms** are the *worlds*: possible situations, or program states.
- **Doors** are the relation **R**: a door from room x to room y means "y is a situation you can move to from x".
- **Lights**: for each simple statement like *p*, some rooms have the light on (p is true there) and some are dark.
- **□p** (box) at a room means: **every door leading out of this room goes to a lit room.** (p is *forced*.)
- **◇p** (diamond) at a room means: **at least one door leading out goes to a lit room.** (p is *possible*.)

Everything in this lecture is a precise version of that picture. Whenever a section feels abstract, come back to the rooms.

| Math word | Plain meaning |
| --- | --- |
| World / point | A room (one possible situation) |
| R, xRy | A one-way door from room x to room y |
| Frame ⟨W,R⟩ | The floor plan: rooms and doors only, no lights |
| Valuation V | The list of which rooms have which lights on |
| Model ⟨𝔉,V⟩ | Floor plan plus lights |
| (𝔐,x) ⊨ ψ | "ψ is true when you stand in room x" |
| □ψ | ψ is true in **all** rooms one door away |
| ◇ψ | ψ is true in **some** room one door away |
| md(ψ) | How many doors deep the formula looks |
| xRⁿy | You can walk from x to y using exactly n doors |

---

## 1. Motivation: necessary vs. possible

> **In plain words:** ordinary logic only answers "true or false?". Modal logic lets you say **"must be true"** or **"might be true"**. "7 is prime" is true no matter where or when you ask, so it is *necessary*. "It is raining" is true in some places and times and false in others, so it is only *possible*. Modal logic gives a clean way to talk about all those different places and times at once.

Propositional logic only says whether a statement is true or false. **Modal logic** adds the ability to talk about *how* it is true: **necessarily** or **possibly**.

| Statement | Status | Modal form |
| --- | --- | --- |
| "7 is a prime number" (call it *p*) | Necessarily true: true everywhere, always | **□p** |
| "It is raining now" (call it *q*) | Possibly true: true in some situations, not others | **◇q** |

The lecture's key remark: **truth values change from place to place and from time to time.** "It is raining now" is true in one city and false in another, true at 3pm and false at 5pm. Modal logic handles this by talking about a *collection of situations* (worlds) and asking what holds in all of them or in at least one.

**Symbols**

- Propositional logic: ¬, ∧, ∨, →, ↔
- Modal logic: all of those, **plus □ ("box": necessarily) and ◇ ("diamond": possibly)**

**CS reading:** worlds = program states, accessibility = "can step to". Then □φ means "φ holds after every possible next step", and ◇φ means "φ holds after some possible next step".

---

## 2. The modal language

> **In plain words:** you take ordinary logic (and, or, not, if-then) and add **one new symbol, □**, which you can put in front of any formula to say "this is necessarily so". That's it. ◇ ("possibly") is not a new idea: "possibly p" just means "it is *not* necessary that p fails", which is ¬□¬p. The precedence rule means □ grabs only the thing right next to it, like a minus sign. So □p → □q ∨ □r reads: "*if* p is necessary, *then* either q is necessary or r is necessary."

Let **L** be the language of propositional logic. The **propositional modal language ML** is L enriched with:

- one new **unary** connective **□**
- one new formula formation rule: **if φ is an ML-formula, then (□φ) is also an ML-formula.**

Notation:

- **Form_ML** = the set of all ML-formulas
- **Var_ML** = the set of all propositional variables in ML

### Precedence convention

□ binds **stronger** than ∧, ∨, →, ↔ (like unary minus binds tighter than +). So

> □p → □q ∨ □r is an abbreviation for **(□p) → ((□q) ∨ (□r))**

and **not** for □(p → □(q ∨ □r)).

Compare: **¬□p** (it is not necessary that p) vs **□¬p** (it is necessary that not-p). These are different. Example: "it is not necessary that it rains" is very different from "necessarily it does not rain".

### ◇ is defined, not primitive

> **◇φ := ¬□¬φ**

Reading: "φ is possible" means "it is *not* necessary that φ fails." So ◇ is just shorthand; the only new primitive symbol is □.

---

## 3. Kripke frames

> **In plain words:** a frame is just the **floor plan**: a non-empty set of rooms and some one-way doors. "Arbitrary" means the architect can draw any doors at all, including none, doors back to the same room, or doors in both directions. "y is accessible from x" simply means "there is a door from x to y". **x↑** is the list of rooms you can walk into from x. **y↓** is the list of rooms that have a door into y. The frame says nothing about what is true in the rooms.

A **(modal Kripke) frame** is a pair **𝔉 = ⟨W, R⟩** where:

- **W** is a **non-empty** set of **worlds** (also called **points**)
- **R** is an **arbitrary binary relation on W** (R ⊆ W × W). *Arbitrary* means no conditions are imposed (it need not be reflexive, transitive, etc.).

Terminology:

- If **xRy**, then **y is accessible from x**.
- **y ∈ x↑** means y is a successor of x (accessible from x). **x ∈ y↓** means x is a predecessor of y. These say the same thing as xRy.
- Proper/immediate successors and predecessors are defined **exactly as in the intuitionistic case** (earlier lectures). *Intuition: "immediate" = no other world lies strictly between them.*

A frame is only a **graph**: dots (worlds) and arrows (R). It says nothing yet about which facts are true where.

---

## 4. Valuations and models

> **In plain words:** now we switch the lights on. For each statement p, the valuation gives the list of rooms where p is true. The floor plan together with these lights is a **model**. The one rule difference from intuitionistic logic: there, once something became true it had to stay true in every room you could reach. Here there is **no such rule**. A room can have the rain light on while the next room has it off, which is exactly what we need for "raining now, not raining later".

Fix a modal language ML.

- A **valuation** in a frame 𝔉 = ⟨W, R⟩ is a map **V : Var_ML → 2^W** (2^W = the power set of W, i.e. all subsets of W).
- So V sends each variable p to a set **V(p) ⊆ W**, read as **"the set of worlds at which p is true."**
- A **Kripke model** is a pair **𝔐 = ⟨𝔉, V⟩** where 𝔉 is a frame and V is a valuation in 𝔉.

> **Model = frame + valuation.** Frame = the shape. Valuation = which atomic facts hold at which point.

**Difference from intuitionistic logic:** there, V(p) had to be an *upset* (once true, true forever upward). In modal logic **V(p) can be any subset** of W, with no persistence requirement. This is why modal logic can say "raining now, not raining later".

---

## 5. The truth relation

> **In plain words:** to check a formula, **stand in a room** and apply these rules.
> 
> 1. For a plain statement like p: look at the light in *this* room.
> 2. For and, or, not, if-then: use ordinary logic, looking **only at this room**.
> 3. For □ψ: list all doors out of this room, walk through each one, and check ψ in the room you land in. **All** must pass.
> 4. For ◇ψ: same, but **at least one** must pass.
> 
> Nested formulas just repeat the walk. For □◇p: go through every door, and in each landing room check that *some* further door leads to a lit room.
> 
> **Dead-end room (no doors):** □ is automatically true, because "every door leads to a lit room" has no counterexample. ◇ is automatically false, because there is no door to find. Think of "every student in an empty classroom passed": technically true, since nobody failed.

Let x be a point of 𝔉. We define **(𝔐, x) ⊨ ψ**, read "**ψ is true at world x in model 𝔐**", by induction on ψ:

| Formula | Truth condition |
| --- | --- |
| p (variable) | (𝔐,x) ⊨ p **iff** x ∈ V(p) |
| ψ ∧ χ | (𝔐,x) ⊨ ψ **and** (𝔐,x) ⊨ χ |
| ψ ∨ χ | (𝔐,x) ⊨ ψ **or** (𝔐,x) ⊨ χ |
| ψ → χ | (𝔐,x) ⊨ ψ **implies** (𝔐,x) ⊨ χ (i.e. ψ fails at x, or χ holds at x) |
| ⊥ | **never**: (𝔐,x) ⊭ ⊥ |
| ¬ψ | (𝔐,x) ⊨ ¬ψ **iff** (𝔐,x) ⊭ ψ |
| **□ψ** | (𝔐,**y**) ⊨ ψ **for all y ∈ W such that xRy** |
| **◇ψ** | (𝔐,**y**) ⊨ ψ **for some y ∈ W such that xRy** |

**Critical difference from intuitionistic logic:** in intuitionistic logic, → and ¬ look at *all future points*. In modal logic, → and ¬ are **classical and local**: they look **only at the current world x**. Only □ and ◇ look at *other* worlds, and only at those **directly accessible** (one step) from x.

### Edge case: dead ends

If x has **no successors**, then:

- □ψ is **true** at x for every ψ (vacuous truth: "all zero successors satisfy ψ")
- ◇ψ is **false** at x for every ψ (no witness exists)

This is consistent with ◇ψ = ¬□¬ψ: □¬ψ is vacuously true, so ¬□¬ψ is false.

### Shorthand

- "(𝔐,x) ⊭ ψ" means **ψ is false at x in 𝔐**.
- When the model is clear from context, write **x ⊨ ψ** and **x ⊭ ψ**.
- The **truth set** of ψ in 𝔐 is the set of worlds where ψ holds: **V̄(ψ) = { x ∈ W : (𝔐,x) ⊨ ψ }**. *(The board writes this as V with a bar over it, and it extends V from variables to all formulas.)*

### Other semantic notions

**Satisfiability, truth, refutability, validity** (in models and frames) and **isomorphism** between frames and models are defined **the same as in intuitionistic logic**. The board also states that **Propositions 2.2 and 2.3 (from the earlier lectures) also hold in modal logic.**

> These numbers refer to the lecturer's own earlier material (the intuitionistic chapter), which is not in either upload. **They are not the same as Proposition 2.2/2.3 in the reference book** (there, 2.3 is about disjoint unions; see Section 8). So I don't state their content as fact. If you send that earlier lecture, I'll add them exactly.

For reference, the standard modal versions of the definitions:

- ψ is **satisfiable** if true at some world of some model.
- ψ is **true in a model** if true at every world of it.
- ψ is **refutable** in a model if false at some world of it.
- ψ is **valid in a frame** if true in every model on that frame (every valuation).

---

## 6. Modal degree

> **In plain words:** modal degree counts **how many doors deep** a formula looks. Plain statements look at no doors (degree 0). Each □ or ◇ stacked on top lets the formula look one door further. For □◇p: go through one door (□), then through another (◇), so it looks 2 doors deep. When two parts are joined by and/or/if-then, the formula is only as deep as its deepest part. A formula of degree 2 can never be affected by anything more than 2 doors away.

The **modal degree md(ψ)** is the **maximum nesting depth of modal operators** in ψ. Defined by induction:

- **md(ψ) = 0** for every atom ψ
- **md(ψ ⊙ χ) = max{ md(ψ), md(χ) }** for ⊙ ∈ {∧, ∨, →}
- **md(□ψ) = md(◇ψ) = md(ψ) + 1**

(⊥ counts as an atom, so md = 0. ¬ψ is ψ → ⊥, so md(¬ψ) = md(ψ).)

### Iterated modalities

- **□ⁿψ** = □□…□ψ (n boxes), **◇ⁿψ** = ◇◇…◇ψ (n diamonds)
- **□⁰ψ = ◇⁰ψ = ψ**
- If ψ has **no** modal operators, then **md(□ⁿψ) = md(◇ⁿψ) = n**

### Worked examples

| Formula | Computation | md |
| --- | --- | --- |
| p ∧ q | max(0,0) | **0** |
| ◇p ∨ □□q | max(1, 2) | **2** |
| □(p ∧ ◇q) → r | md(◇q)=1, so md(p∧◇q)=1, so md(□(…))=2, then max(2,0) | **2** |
| □³p | 3 boxes on a modal-free formula | **3** |

**Intuition (not from the board, but why this matters):** md(ψ) measures how far from x the truth of ψ can "see". A formula of degree n at x depends only on worlds reachable within n steps of x.

---

## 7. n-step accessibility

> **In plain words:** xRⁿy means "you can get from x to y by walking exactly n doors" (rooms may repeat, so you can pass through the same room twice). Walking 0 doors means you haven't moved, so xR⁰y just means x is y. Then the shape words:
> 
> - **Transitive:** whenever you can go x → y → z, there is also a **shortcut door** straight from x to z.
> - **Reflexive:** every room has a door that leads back to itself.
> - **Irreflexive:** **no** room has such a door.
> - **Intransitive:** the opposite of transitive. Whenever you can go x → y → z, a straight door x → z is **forbidden**.
> 
> **Why the four facts are true, in words:**
> 
> 1. *Transitive means long walks can be shortened:* with shortcuts, you can fold a 5-door walk into a 4-door walk, then 3, and so on, until one door is left.
> 2. *Transitive and reflexive means you can also stretch:* if every room has a door to itself, you can "stall" in a room as many times as you like, so a single door x → y can be padded into a walk of any length.
> 3. *A room with a self-door can be left and re-entered forever:* just loop around n times.
> 4. *Intransitive frames have no self-doors:* suppose room x has a door to itself. Then x → x → x is a two-step walk, and the intransitive rule would then forbid the door x → x. But it exists. Contradiction.
> 
> **Careful:** *irreflexive* means **no** room loops back. *Not reflexive* only means **some** room fails to.

Let 𝔉 = ⟨W, R⟩ be a frame and x, y ∈ W.

**y is accessible from x in n > 0 steps**, written **xRⁿy**, or **y ∈ x↑ⁿ**, or **x ∈ y↓ⁿ**, if there exist points z₁, …, z\_{n−1} ∈ W (**not necessarily distinct**) such that

> **xRz₁, z₁Rz₂, …, z\_{n−1}Ry**

(a path of n arrows). For **n = 0**: **xR⁰y** (also y ∈ x↑⁰, x ∈ y↓⁰) **means x = y** (zero steps = stay put).

**Connection to □ⁿ:** (𝔐,x) ⊨ □ⁿψ iff ψ holds at every y with xRⁿy. Likewise ◇ⁿψ holds iff some y with xRⁿy satisfies ψ.

### Properties of R

| Property | Definition |
| --- | --- |
| **Transitive** | xRy ∧ yRz → xRz |
| **Reflexive point** | a point x with xRx |
| **Reflexive frame** | every point is reflexive |
| **Irreflexive frame** | no point is reflexive (never xRx) |
| **Intransitive frame** | ∀x,y,z ( xRy ∧ yRz → \*\*¬\*\*xRz ) |

**Facts from the lecture**

1. **If R is transitive, then xRⁿy ⇒ xRy** (for n ≥ 1). *Why:* a path x→z₁→…→y can be shortened by transitivity, merging two steps into one at a time until a single step xRy remains.
2. **If R is transitive and reflexive, the converse also holds:** xRy ⇒ xRⁿy for every n ≥ 1. *Why:* pad the path with reflexive loops: x R x R … R x R y gives n steps. So for reflexive+transitive R: **xRy ⇔ xRⁿy** (all n ≥ 1).
3. **If x is a reflexive point, then xRⁿx for every n ≥ 0.** Loop on x n times.
4. **An intransitive frame is irreflexive.** *Proof:* suppose xRx. Taking y = z = x gives xRx ∧ xRx → ¬xRx, so ¬xRx. Contradiction. So no xRx exists.

**Warning:** *irreflexive* ≠ *not reflexive*. "Not reflexive" means *some* point lacks a loop. "Irreflexive" means *no* point has a loop.

---

## Full worked example

> **Walk-through in words:** three rooms **a, b, c**. Room a has one door to b. Room b has one door to c. Room c has one door **back to itself**. The *p* light is on in b and c. The *q* light is on only in c.
> 
> - From a, the only door goes to b, and b has p lit. So **□p is true** (all doors lead to lit rooms) and **◇p is true** (some door does).
> - But b has no q light. So **□q is false** at a, and **◇q is false** too, since the only door leads to a dark-for-q room.
> - Two doors from a you reach c (a→b→c), and c has q. So **□□q is true** at a.
> - Room c loops to itself and has q, so q stays true however many steps you take from c.
> - Not transitive: you can go a→b→c but there is no shortcut door a→c.

**Model:** W = {a, b, c}, R = {(a,b), (b,c), (c,c)}, V(p) = {b, c}, V(q) = {c}.

```
a ──► b ──► c ⟲
```

| Question | Answer | Reason |
| --- | --- | --- |
| a ⊨ □p ? | **Yes** | only successor of a is b, and b ∈ V(p) |
| a ⊨ ◇p ? | **Yes** | b is a successor with p |
| a ⊨ □q ? | **No** | b is the only successor and b ∉ V(q) |
| a ⊨ ◇q ? | **No** | the only successor b lacks q |
| a ⊨ □□q ? | **Yes** | a→b→c and c ∈ V(q); md = 2 |
| c ⊨ □ⁿq for all n ? | **Yes** | c loops to itself and q holds at c |
| a R² c ? | **Yes** | a→b→c |
| a R c ? | **No** | not in R |
| Transitive? | **No** | aRb, bRc but not aRc |
| Reflexive? | **No** | a has no loop |
| Irreflexive? | **No** | c has a loop |
| Is c a reflexive point? | **Yes** | cRc, hence cRⁿc for all n |

Note a ⊨ □p and a ⊨ ¬□q while a ⊨ ◇p and a ⊭ ◇q: all computed by looking **only at a's direct successors**.

---

## Common mistakes

1. **Treating → and ¬ like intuitionistic logic.** Here they are classical and local to the current world.
2. **Forgetting vacuous truth** at dead-end worlds (□ true, ◇ false).
3. **Confusing ¬□p with □¬p.**
4. **Reading □ as "all reachable worlds".** It means all **one-step** successors. Multi-step is □ⁿ or □□.
5. **Forgetting that V(p) can be any subset** of W (no persistence).
6. **Confusing irreflexive with non-reflexive.**
7. **Misreading precedence:** □p → □q ∨ □r is (□p) → ((□q) ∨ (□r)).

---

## 8. Supplement from the reference book

**Source:** Blackburn, de Rijke & Venema, *Modal Logic* (Cambridge Tracts in Theoretical Computer Science 53), Chapters 1 and 2.

**Notation difference:** the book takes **◇ as primitive** and defines **□ := ¬◇¬**. The lecture does the reverse (□ primitive, ◇ := ¬□¬). The two are equivalent, so everything transfers.

### 8.1 Same definitions as the lecture

> **In plain words:** the textbook says the same thing with slightly different notation, so you can read either one. The book's Definitions 1.19 to 1.21 give the same frame, model, satisfaction clauses (◇ is "some successor", □ is "all successors"), and "true in a model / valid on a frame". Its **degree** is defined as deg(p)=0, deg(⊥)=0, deg(¬φ)=deg(φ), deg(φ∨ψ)=max, deg(◇φ)=1+deg(φ), which matches the lecture's md. It also defines the iterated modality ◇ⁿ ("true somewhere n steps from here"), matching ◇ⁿ and xRⁿy above.

### 8.2 Isomorphism and why it is harmless

> **In plain words:** two buildings are *isomorphic* if they are the **same building with the rooms renamed**: same doors, same lights, only the labels differ. Obviously, renaming a room can't change what is true there. That is the whole result. It lets us say "these two models are the same" without worrying about names. An **isomorphism** f : 𝔐 → 𝔐′ is a **bijection** W → W′ such that

1. x and f(x) satisfy the **same variables**, and
2. **xRy iff f(x)R′f(y)** (arrows are preserved *and* reflected).

**Result:** if 𝔐 ≅ 𝔐′ then x and f(x) satisfy exactly the same modal formulas. *Proof idea:* induction on the formula. Variables use condition 1. Boolean steps are immediate. For ◇ψ, a successor y of x with ψ true corresponds to the successor f(y) of f(x) with ψ true (condition 2 gives both directions). *Meaning:* renaming worlds changes nothing, so we work with frames and models **up to isomorphism**. This is what the lecture means by "isomorphism is defined as in the intuitionistic case".

### 8.3 Disjoint unions

> **In plain words:** put two separate buildings side by side with **no doors between them**. If you stand in a room of building 1, you can still only walk through building 1's doors, so you see exactly what you saw before. The neighbouring building is invisible. So what is true at a room doesn't change when other buildings are placed next to it. The **disjoint union** of models 𝔐ᵢ (with disjoint world sets) takes the union of the worlds, the union of the relations, and V(p) = union of the Vᵢ(p). No arrows are added between components.

**Result (book's Prop. 2.3):** for every world x of 𝔐ᵢ and every formula φ, **𝔐ᵢ, x ⊨ φ iff (⊎ⱼ𝔐ⱼ), x ⊨ φ.** *Why:* ◇ and □ only look at one-step successors, and every successor of x lies in x's own component. Gluing other models alongside cannot change what x sees.

### 8.4 Finitely many formulas of each degree

> **In plain words:** if you only have a few lights (statements) and you are only allowed to look a few doors deep, then there are only so many genuinely different things you can say. Many formulas that look different just say the same thing. So limiting the depth limits how much you can express. If there are only **finitely many variables**, then for every n there are only **finitely many formulas of degree ≤ n up to logical equivalence** (book's Prop. 2.29). *Why:* degree 0 gives Boolean combinations of finitely many letters, so finitely many up to equivalence. A degree n+1 formula is a Boolean combination of letters and formulas ◇ψ with deg ψ ≤ n, and there are finitely many such ψ up to equivalence. *Meaning:* this is why md is a useful size measure: bounded depth means bounded expressive power.

### 8.5 Local vs global

> **In plain words:** □ and ◇ only see the **neighbouring rooms through doors**. They cannot say "somewhere in the whole building". That would need a separate tool, the *global modality*. And since a modal formula can't see the building next door (8.3), it cannot talk about "everywhere" at all. □ and ◇ are **local** (one step from the current world). The **global modality** E ("true at some world of the model") and its dual A ("true at all worlds") are **not** definable in the basic language. The disjoint-union result shows why: adding a new component can change Eφ at x but can never change basic modal truth at x.

---

## Self-test (answers below)

1. Is □(p → q) → (□p → □q) true at a dead-end world? What about ◇⊤?
2. Compute md( □◇p → ◇(q ∧ □r) ).
3. In the worked-example model, does b ⊨ □□q? Does b ⊨ ◇¬q?
4. Give a frame that is intransitive and show it is irreflexive.
5. If R is transitive but not reflexive, give an example where xRy but not xR²y.

**Answers**

1. The implication is true at a dead end, since □(p→q) is vacuously true and so is the consequent □p→□q (both □'s hold). ◇⊤ is **false** (no successor exists).
2. md(□◇p) = 2; md(◇(q∧□r)) = 1 + max(0,1) = 2. So md = **2**.
3. b's only successor is c, and c's only successor is c, with q true at c, so b ⊨ □□q is **true**. For ◇¬q, c ⊨ q so ¬q fails at c, so b ⊭ ◇¬q: **false**.
4. W = {1,2}, R = {(1,2)}. Check: 1R2, but 2 has no successor, so the premise xRy ∧ yRz never fires and the condition holds trivially. No xRx exists, so the frame is irreflexive.
5. W = {1,2}, R = {(1,2)}. R is transitive (the chain 1R2 cannot be extended, so there is nothing to check) and 1R2 holds. But 1R²2 would need a z with 1Rz and zR2, and no such z exists, so **not 1R²2**. Transitivity gives xRⁿy ⇒ xRy, but without reflexivity the converse xRy ⇒ xR²y fails.

---

## One-page summary

- **□ = necessarily, ◇ = possibly (= ¬□¬).** □ binds tighter than ∧, ∨, →, ↔.
- **Frame ⟨W,R⟩** = worlds + arbitrary accessibility. **Model = frame + V**, with V(p) ⊆ W any subset.
- **Truth:** atoms by V; ∧, ∨, →, ¬, ⊥ classical and local; **□ = all successors, ◇ = some successor.**
- **Dead end:** □ true, ◇ false.
- **md:** atoms 0; binary connectives take max; □/◇ add 1.
- **xRⁿy = path of n arrows; xR⁰y = (x = y).**
- **Transitive ⇒ xRⁿy → xRy. Transitive + reflexive ⇒ equivalence in both directions. Intransitive ⇒ irreflexive.**

---

*(Next lecture goes below this line.)*