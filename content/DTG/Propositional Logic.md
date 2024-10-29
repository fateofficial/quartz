## Connectives

In propositional logic generally we use five connectives which are −

- OR (∨)
 ![[Pasted image 20240923080226.png]]
- AND (∧)
![[Pasted image 20240923080244.png]]
- Negation/ NOT (¬)
 ![[Pasted image 20240923080251.png]]
- Implication / if-then (→)
![[Pasted image 20240923080303.png]]
- If and only if (⇔).

## Tautologies

A Tautology is a formula which is always true for every value of its propositional variables.

**Example** − Prove [(A→B)∧A]→B[(A→B)∧A]→B is a tautology

The truth table is as follows −
![[Pasted image 20240923080423.png]]


## Contradictions

A Contradiction is a formula which is always false for every value of its propositional variables.

**Example** − Prove (A∨B)∧[(¬A)∧(¬B)](A∨B)∧[(¬A)∧(¬B)] is a contradiction

The truth table is as follows −
![[Pasted image 20240923080358.png]]


## Contingency

A Contingency is a formula which has both some true and some false values for every value of its propositional variables.

**Example** − Prove (A∨B)∧(¬A)(A∨B)∧(¬A) a contingency

The truth table is as follows −
![[Pasted image 20240923080347.png]]

## Inverse, Converse, and Contra-positive

Implication / if-then (→)(→) is also called a conditional statement. It has two parts −

- Hypothesis, p
- Conclusion, q

As mentioned earlier, it is denoted as p→qp→q.

**Example of Conditional Statement** − “If you do your homework, you will not be punished.” Here, "you do your homework" is the hypothesis, p, and "you will not be punished" is the conclusion, q.

**Inverse** − An inverse of the conditional statement is the negation of both the hypothesis and the conclusion. If the statement is “If p, then q”, the inverse will be “If not p, then not q”. Thus the inverse of p→qp→q is ¬p→¬q¬p→¬q.

**Example** − The inverse of “If you do your homework, you will not be punished” is “If you do not do your homework, you will be punished.”

**Converse** − The converse of the conditional statement is computed by interchanging the hypothesis and the conclusion. If the statement is “If p, then q”, the converse will be “If q, then p”. The converse of p→qp→q is q→pq→p.

**Example** − The converse of "If you do your homework, you will not be punished" is "If you will not be punished, you do your homework”.

**Contra-positive** − The contra-positive of the conditional is computed by interchanging the hypothesis and the conclusion of the inverse statement. If the statement is “If p, then q”, the contra-positive will be “If not q, then not p”. The contra-positive of p→qp→q is ¬q→¬p¬q→¬p.

**Example** − The Contra-positive of " If you do your homework, you will not be punished” is "If you are punished, you did not do your homework”.


### Duality for Laws in Propositional Logic:

In **propositional logic**, the **Duality Principle** allows you to create a dual statement by swapping logical operators and truth values. Specifically, in this context:

1. **AND (∧)** is swapped with **OR (∨)**.
2. **TRUE (T)** is swapped with **FALSE (F)**.

Here’s how some common logical laws look when the duality principle is applied:

1. **Identity Laws**:
    
    - P∧T=PP \wedge T = PP∧T=P becomes P∨F=PP \vee F = PP∨F=P.
2. **Domination Laws**:
    
    - P∨T=TP \vee T = TP∨T=T becomes P∧F=FP \wedge F = FP∧F=F.
3. **Idempotent Laws**:
    
    - P∧P=PP \wedge P = PP∧P=P becomes P∨P=PP \vee P = PP∨P=P.
4. **Distributive Laws**:
    
    - P∧(Q∨R)=(P∧Q)∨(P∧R)P \wedge (Q \vee R) = (P \wedge Q) \vee (P \wedge R)P∧(Q∨R)=(P∧Q)∨(P∧R) becomes P∨(Q∧R)=(P∨Q)∧(P∨R)P \vee (Q \wedge R) = (P \vee Q) \wedge (P \vee R)P∨(Q∧R)=(P∨Q)∧(P∨R).

### De Morgan's Laws (as an example of duality):

¬(P∧Q)=¬P∨¬Q\neg (P \wedge Q) = \neg P \vee \neg Q¬(P∧Q)=¬P∨¬Q ¬(P∨Q)=¬P∧¬Q\neg (P \vee Q) = \neg P \wedge \neg Q¬(P∨Q)=¬P∧¬Q