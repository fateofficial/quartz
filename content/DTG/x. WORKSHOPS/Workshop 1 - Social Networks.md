![[Pasted image 20241202101809.png]]

A = {Abe, Bob, Cem, Dee, Eve, Fey, Gil}.
As a starting point it is set up such that you can follow other users (similar to e.g. Instagram or Twitter). This introduces a relation S on the set of users given by (a, b) ∈ S if person a follows person b. Figure 1 shows which users are following whom at this point (as a starting point, everyone is following themselves, since you can see your own posts).
___
# Exercise 1

## 1.
Write down the relation S given in figure 1 as a set.
Subset of the cartesian product of A x A
S= (A,A),(B,B),(C,C),(D,D),(E,E),(F,F),(G,G),(B,C),(C,D),(D,E),(D,A),(E,A),(F,A),(F,D),(F,G)
S* = (A,A),(B,A),(B,B),(B,C),(B,D),(B,E),(C,A),(C,C),(C,D),(C,E),(D,A),(D,D),(D,E),(E,A),(E,E),(F,A),(F,D),(F,E),(F,F),(F,G),(G,G)
___
## 2.
What is the cardinality of the relation?
The cardinality can be found by counting the amount of relations, which is:
|S| = 15;
___
## 3.
The relation can be described as a subset of a cartesian product. Which cartesian product does this refer to here and what is its cardinality?

It can be described as a subset of the cartesian product of A, which is A x A.
Set a contains 7 elements. $7*7 = 49$ so the cardinality of A x A is 49.

___
## 4.
Decide whether the relation above is reflexive, symmetric, transitive, or antisymmetric. Explain why it has or does not have these properties. Consider what it means for a social network to have these properties.
It is reflexive because it has the pair $\forall a \in A, (a,a) \in R$
As seen in matrix

It is not symmetric because for it to be symmetric it has to be $\forall a,b \in A,(a,b) \in R \implies (b,a)\in R$ 
As seen in the matrix  there is a B,C but no C,B.

It is not transitive because transitive means $\forall a, b, c \in A, \; \big((a, b) \in R \text{ and } (b, c) \in R\big) \implies (a, c) \in R$
Because we have (B,C) and (C,D) but no (B,D)

A relation is antisymmetric if $(a,b) \in R~and~(b,a)∈R  ⟹  a=b$
No pair $(a, b)$ exists where both (a, b) and $(b, a)$ are in R unless  $a = b$
Relation is antisymmetric

|     | A   | B     | C     | D     | E   | F   | G   |
| --- | --- | ----- | ----- | ----- | --- | --- | --- |
| A   | 1   | 0     | 0     | 0     | 0   | 0   | 0   |
| B   | 0   | 1     | 1 (a) | 0 (t) | 0   | 0   | 0   |
| C   | 0   | 0 (s) | 1     | 1     | 0   | 0   | 0   |
| D   | 1   | 0     | 0     | 1     | 1   | 0   | 0   |
| E   | 1   | 0     | 0     | 0     | 1   | 0   | 0   |
| F   | 1   | 0     | 0     | 1     | 0   | 1   | 1   |
| G   | 0   | 0     | 0     | 0     | 0   | 0   | 1   |
___
# Exercise 2
One topic for discussion for the social media app is the idea that if someone publishes a post, it is re-published by everyone who follows them (a form of automatic retweet). The makers of the app can not decide whether this should 

a) only happen with immediate followers
or
b) generate a chain reaction

For option b) this means that if $x_1 \leq x_2$, $x_2 \leq x_3$, $\dots$, $x_{n-1} \leq x_n$ then $x_1, x_2, \dots, x_{n-1}$ will also see all posts by $x_n$ and in effect also follow them. While in option a) posts by $x_n$ are only visible to $x_{n-1}$ and $x_{n-2}$.

Explain the two options in terms of relations. The second option is related to a closure operation, which one?
___
## 1.
Option a)
each person can see the posts of their direct followers, but also the posts of those whom their followers are connected to (so long as they follow them directly). This can be thought of as the relation R allowing visibility through one step of propagation. Essentially, the relation defines immediate connections but allows you to trace a path through a follower to see their posts.
In terms of relations, we can define this as a direct relation between the nodes (users) in the graph, where each directed edge represents a "following" relationship (i.e., one node follows another, and thus can see their posts).
This means if u take the composite of the relation on the relation $R \circ R$  that u will see who is indirectly followed just by association.


Option b is related to the transitive closure operation

Option b) applies the transitive closure of the relation, ensuring that:
1. If there’s a sequence of relationships connecting $x_1$​ to  $x_n$​, then $x_1$​ is treated as directly related to $x_n$​​.
2. As a result, all posts or information from $x_n$​ "propagate" backwards through the chain to $x_1, x_2, \dots, x_{n-1}$

So, when it says "in effect also follow them," it means that by seeing posts through the chain of relationships, the person (or element) is treated as if they are directly connected or following the end of the chain.
___
## 2.
![[Pasted image 20241203104429.png]]
$S* = (A,A),(B,A),(B,B),(B,C),(B,D),(B,E),(C,A),(C,C),(C,D),(C,E),(D,A),(D,D),(D,E),(E,A),(E,E),(F,A),(F,D),(F,E),(F,F),(F,G),(G,G)$
___
# Exercise 3

$F_{Abe} = \{a \in A \mid (a, Abe) \in S^* \}$

$F_{Eve} = \{a \in A \mid (a, Abe) \in S^* \}$

What do these sets describe? Which elements are in the sets $F_{Abe}$, $F_{Eve}$ and $F_{Abe} \cap F_{Eve}$.
They describe a list that is defined from a, which is in A so that any element in the transitive closure of S and connected to Abe is in the relation.
## 1.
$S = (A,A),(B,B),(C,C),(D,D),(E,E),(F,F),(G,G),(B,C),(C,D),(D,E),(D,A),(E,A),(F,A),(F,D),(F,G)$
$S* = (A,A),(B,A),(B,B),(B,C),(B,D),(B,E),(C,A),(C,C),(C,D),(C,E),(D,A),(D,D),(D,E),(E,A),(E,E),(F,A),(F,D),(F,E),(F,F),(F,G),(G,G)$

This means that for $F_{Abe}$ 
We have to find every directed edge towards Abe in the transitive closure.
$$F_{Abe} = (A,A)~(B,A)~(C,A)~(D,A)~(E,A)~(F,A)$$

This means that for $F_{Eve}$ 
We have to find every directed edge toward Eve
$$F_{Eve} = (B,E)~(C,E)~(D,E)~(E,E)~(F,E)$$ 

Looking at the sets, there are no pairs shared between $F_{Abe}$​ and $F_{Eve}$​, because the second element of each pair ($A~in~F_{Abe}~and~E~in~F_{Eve}$) is always different.
$$F_{Abe} \cap F_{Eve} = \emptyset$$
___
## 2. 
**Let $b \in G_{Abe}$​.** By the definition of $G_{Abe}$​, there exists a directed path from $b$ to "Abe" in the relation $S^*$, i.e., $(b, Abe) \in S^*$.
#problem 
Let $B \subseteq A$ and consider $G_{Abe} = \{ b \in B \mid (b, Abe) \in S^* \}.$
Show that = $G_{Abe} \subseteq F_{Abe}$
$F_{Abe} = \{a \in A \mid (a, Abe) \in S^* \}$

#proof
 Let $b \in G_{Abe}$. By the definition of $G_{Abe}$, there exists a directed path from $b$ to "Abe" in the relation $S^∗$, i.e., $(b, Abe) \in S^*$.
 
Since $b \in B$ and $B \subseteq A$, we know that b is an element of A as well.

Since $(b, Abe) \in S^*$ and $(b, Abe) \in S^*$ by the definition of $(b, Abe) \in S^*$​, b must be in $(b, Abe) \in S^*$​. In other words, $b \in F_{Abe}$​.

**Conclusion:** Since $b \in G_{Abe}$​ implies $b \in F_{Abe}$, we have shown that $G_{Abe} \subseteq F_{Abe}$.
___
# Exercise 4

## 1.
Consider the relation R on $A = {w, x, y, z}$ given by $R = {(w, w),(w, x),(x, y),(z, y)}$. Draw the directed graph that represents this relation and write down its matrix representation.

![[Pasted image 20241203121251.png]]

 $R = {(w, w),(w, x),(x, y),(z, y)}$

|     | w   | x   | y   | x   |
| --- | --- | --- | --- | --- |
| w   | 1   | 1   | 0   | 0   |
| x   | 0   | 0   | 1   | 0   |
| y   | 0   | 0   | 0   | 0   |
| z   | 0   | 0   | 1   | 0   |
___
## 2.
2. Find the reflexive closure R˜ of R.
To find the reflexive closure of R we just input every possible self directed edge.

$R = {(w, w),(w, x),(x, y),(z, y)}$
$R^˜ = {(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z)}$

|     | w   | x         | y         | z         |
| --- | --- | --------- | --------- | --------- |
| w   | 1   | 1         | 0         | 0         |
| x   | 0   | ==**1**== | 1         | 0         |
| y   | 0   | 0         | ==**1**== | 0         |
| z   | 0   | 0         | 1         | ==**1**== |
___
## 3. 
Symmetric closure of $R^˜ = {(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z)}$

If there is a 1 on the other side of the diagonal make sure its mirrored.

|     | w   | x   | y   | z   |
| --- | --- | --- | --- | --- |
| w   | 1   | 1   | 0   | 0   |
| x   | 0   | 1   | 1   | 0   |
| y   | 0   | 0   | 1   | 0   |
| z   | 0   | 0   | 1   | 1   |

|     | w         | x         | y   | z         |
| --- | --------- | --------- | --- | --------- |
| w   | 1         | 1         | 0   | 0         |
| x   | ==**1**== | 1         | 1   | 0         |
| y   | 0         | ==**1**== | 1   | ==**1**== |
| z   | 0         | 0         | 1   | 1         |

So added x,w y,x and y,z
The symmetric closure of $R^˜ = {(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z)}$
Is:  $S=(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z),(x,w),(y,x),(y,z)$


Construct the transitive closure $S^∗$ of $S$

![[Pasted image 20241203122908.png]]

|     | w         | x         | y         | z         |
| --- | --------- | --------- | --------- | --------- |
| w   | 1         | 1         | ==**1**== | ==**1**== |
| x   | 1         | 1         | 1         | ==**1**== |
| y   | ==**1**== | 1         | 1         | 1         |
| z   | ==**1**== | ==**1**== | 1         | 1         |

$S^*=(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z),(x,w),(y,x),(y,z),(w,y),(w,z),(x,z),(y,w),(z,w),(z,x)$
So the transitive closure of S which is S* is a complete graph, where all possible edges are added.
___
## 4.
Now begin by constructing the transitive closure $T$ of the reflexive closure $\tilde{R}$. You may use whichever representation of the relation you prefer.

![[Pasted image 20241203124409.png]]
Only one added edge which is w,y therefore the transitive closure of the reflexice closure of R = $\tilde{R} = {(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z)}$
And transitive closure is
$T = {(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z),(w,y)}$


Next construct the symmetric closure $T^\prime$ of $T$

$T = {(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z),(w,y)}$

|     | w   | x   | y   | z   |
| --- | --- | --- | --- | --- |
| w   | 1   | 1   | 1   | 0   |
| x   | 0   | 1   | 1   | 0   |
| y   | 0   | 0   | 1   | 0   |
| z   | 0   | 0   | 1   | 1   |

|     | w         | x         | y   | z         |
| --- | --------- | --------- | --- | --------- |
| w   | 1         | 1         | 1   | 0         |
| x   | ==**1**== | 1         | 1   | 0         |
| y   | ==**1**== | ==**1**== | 1   | ==**1**== |
| z   | 0         | 0         | 1   | 1         |
$T^\prime = {(w, w),(w, x),(x,x),(x, y),(y,y),(z,y),(z,z),(w,y),(x,w),(y,w),(y,x),(y,z)}$


$S^*=(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z),(x,w),(y,x),(y,z),(w,y),(w,z),(x,z),(y,w),(z,w),(z,x)$

Compare the results from the two previous tasks. Which of the two final relations S ∗ and T 0 is an equivalence relation?

## 5.
$S^*=(w, w),(w, x),(x,x),(x, y),(y,y),(z, y),(z,z),(x,w),(y,x),(y,z),(w,y),(w,z),(x,z),(y,w),(z,w),(z,x)$
$T^\prime = {(w, w),(w, x),(x,x),(x, y),(y,y),(z,y),(z,z),(w,y),(x,w),(y,w),(y,x),(y,z)}$

For it to be an equivalence relation it has to be symmetric, reflexive and transitive

| $S^*$ | w         | x         | y         | z         |
| ----- | --------- | --------- | --------- | --------- |
| w     | 1         | 1         | ==**1**== | ==**1**== |
| x     | 1         | 1         | 1         | ==**1**== |
| y     | ==**1**== | 1         | 1         | 1         |
| z     | ==**1**== | ==**1**== | 1         | 1         |
It is symmetric, reflexive and transitive, therefore $S^*$ is an equivalence relation.



| $T^\prime$ | w         | x         | y   | z         |
| ---------- | --------- | --------- | --- | --------- |
| w          | 1         | 1         | 1   | 0         |
| x          | ==**1**== | 1         | 1   | 0         |
| y          | ==**1**== | ==**1**== | 1   | ==**1**== |
| z          | 0         | 0         | 1   | 1         |
It is symmetric, reflexive however not transitive therefore $T^\prime$ is not an equivalence relation