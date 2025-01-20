# Workshop: Analyzing Conditions for an IF Statement

In this workshop, we will analyze some conditions for an IF statement. In the accompanying file, you can see the code and the IF statement in question. We are looking for a big natural number $x$ that fulfills certain conditions. To describe these conditions, we introduce the following propositional functions:

- $P(x)$: $x$ is a prime
- $Q(x)$: $\gcd(x, 2) = 1$
- $R(x)$: $9x - 2 \mod 5 = 2$

We are looking for numbers $x$ for which the following proposition is true:

$$
(P(x) \land \neg R(x)) \lor \neg(P(x) \lor \neg Q(x) \lor R(x)) \lor (\neg P(x) \land \neg Q(x) \land R(x))
$$

For now, we only know that $2$ fulfills this condition. Since $P(2)$ is true, 2 is a prime, and $Q(2)$ is false, since $\gcd(2, 2) = 2 \neq 1$, and $R(2)$ is false, because

$$
9 \times 2 - 2 \mod 5 = 7 \mod 5 = 4.
$$

Hence we get:

$$
(P(2) \land \neg R(2)) \lor \neg(P(2) \lor \neg Q(2) \lor R(2)) \lor (\neg P(2) \land \neg Q(2) \land R(2))
$$

$$
\equiv (T \land \neg F) \lor \neg (T \lor \neg F \lor F) \lor (\neg T \land \neg F \land F)
$$

$$
\equiv (T \land T) \lor \neg (T \lor T \lor F) \lor (F \land T \land F)
$$

$$
\equiv T \lor \neg T \lor F
$$

$$
\equiv T.
$$

Assume we are interested in finding large numbers for which the condition is true. More precisely, we would like to find three numbers $\{x, y, z\}$, where $100000 < x, y, z \leq 1000000$ that all fulfill the given condition.

# Exercise 1

## 1)
How many ways can we choose $\{x, y, z\}$, where $100000 < x, y, z \leq 1000000$?
(a) If we do not require them to be necessarily all different?

First step is to find how many numbers are strictly between 100000 and 1000001.
In the case of there only being mixed inequalities u can use 
$b-a$
$1000000-100000=900000$ different numbers.

In this case it means that each of the variables can have the same number, so all 3 variables can contain the value 100001 for example.

This means that there is $900000^3$ permutations of values where they dont have to be distinct.

(b) If we want them to be pairwise different?
If pairwise different needed to be 900000 options for the first variable, then 900000-1 for the next and so on.

$900000*899999*899998$

## 2)
Complete the accompanying code by adding the functions isPrime, is2mod5, and isGcd1 so they check the corresponding condition.

Hint for isGcd1:
The function does not need to compute the gcd but can simply check possible divisors.

Hint for is2mod5:  
Find a way to apply the modulus throughout the calculations. Otherwise, you will get much too big numbers very quickly when calculating $9^x$.

```
int isPrime(int x) {  
    if (x <= 1) return 0;  // Numbers less than or equal to 1 are not prime  
    for (int i = 2; i < x; i++) {  
        if (x % i == 0) {  
            return 0;  // If divisible by any number other than 1 and itself, not prime  
        }  
    }  
    return 1;  // No divisors found, so n is prime  
}  
  
/* This function should return 1 if gcd(x,2)=1 and 0 otherwise */  
int isGcd1(int a) {  
    if (a % 2 == 0) {  
        return 0;  // If a is even, gcd(a, 2) = 2  
    }  
    return 1;  // If a is odd, gcd(a, 2) = 1  
}  
  
/* This function should return 1 if 9^x-2 mod 5 = 2 and 0 otherwise */  
int is2mod5(int x) {  
    int result = 1;  
  
    for (int i = 0; i < x; i++) {  
        result = (result * 9) % 5;  // Multiply and take modulus 5 at each step  
    }  
    return (result - 2) % 5 == 2 ? 1 : 0;  // Check if 9^x - 2 mod 5 equals 2  
}
```

## 3)
Try (ten) different values of x and see if you can find one that fulfills all conditions. Can you find one that makes (1) true?'

```
for (int i = 0;i<10;i++) {  
    checkConditions(i);  
}
```

output,
```
You have found a valid x
x was 2
```


# Exercise 2


$$
\begin{array}{|c|c|}
\hline
\textbf{Law} & \textbf{Boolean Expression} \\
\hline
\text{Identity Law} & A \land 1 = A, \quad A \lor 0 = A \\
\hline
\text{Null Law} & A \land 0 = 0, \quad A \lor 1 = 1 \\
\hline
\text{Domination Law} & A \land 0 = 0, \quad A \lor 1 = 1 \\
\hline
\text{Idempotent Law} & A \land A = A, \quad A \lor A = A \\
\hline
\text{Complement Law} & A \land \neg A = 0, \quad A \lor \neg A = 1 \\
\hline
\text{Double Negation Law} & \neg(\neg A) = A \\
\hline
\text{Commutative Law} & A \land B = B \land A, \quad A \lor B = B \lor A \\
\hline
\text{Associative Law} & (A \land B) \land C = A \land (B \land C), \quad (A \lor B) \lor C = A \lor (B \lor C) \\
\hline
\text{Distributive Law} & A \land (B \lor C) = (A \land B) \lor (A \land C), \quad A \lor (B \land C) = (A \lor B) \land (A \lor C) \\
\hline
\text{Absorption Law} & A \land (A \lor B) = A, \quad A \lor (A \land B) = A \\
\hline
\text{De Morgan's Law} & \neg(A \land B) = \neg A \lor \neg B, \quad \neg(A \lor B) = \neg A \land \neg B \\
\hline
\text{Involution Law} & \neg(\neg A) = A \\
\hline
\text{Redundancy Law} & A \land (A \lor B) = A, \quad A \lor (A \land B) = A \\
\hline
\end{array}
$$


## 1)
Rewrite the condition in (1) into PDNF.

$$
(P(x) \land \neg R(x)) \lor \neg (P(x) \lor \neg Q(x) \lor R(x)) \lor (\neg P(x) \land \neg Q(x) \land R(x))
$$
The steps are usually
1. In this step, we will replace → with their equivalent formula, which is used to have ¬, ∧, and ∨.
2. Now, we will apply negation on the variables with the help of De Morgan's laws, which will follow the distributive law.
3. Now we will drop those elementary products, which are a contradiction. After this, we can get minterms in disjunction with the help of introducing the missing factors. If there are some identical minterms in the disjunction, then we will delete them.


No implications are used so skipping step:
Second minterm however contains disjunctions, therefore de morgans law is needed.

$\neg (P(x) \lor \neg Q(x) \lor R(x))$

De morgans laws
$\neg(A \land B) = \neg A \lor \neg B, \quad \neg(A \lor B) = \neg A \land \neg B$

That means we end up with 

$(\neg P(x) \land \neg(\neg Q(x)) \land \neg R(x))$

Simplify double negation

$(\neg P(x) \land Q(x) \land \neg R(x))$

Replace in the full version, now we have:

$(P(x) \land \neg R(x)) \lor (\neg P(x) \land Q(x) \land \neg R(x)) \lor (\neg P(x) \land \neg Q(x) \land R(x))$

However to make it PDNF a term is missing from the first minterm which is Q(x), this can be added of taking into consideration both options of Q(x).

$(P(x) \land \neg R(x)) = (P(x) \land \neg R(x) \land Q(x)) \lor (P(x) \land \neg R(x) \land \neg Q(x))$

That means the PDNF is $(P(x) \land \neg R(x) \land Q(x)) \lor (P(x) \land \neg R(x) \land \neg Q(x)) \lor (\neg P(x) \land Q(x) \land \neg R(x)) \lor (\neg P(x) \land \neg Q(x) \land R(x))$
## 2)
How many minterms does the normalform contain? What does this mean for the corresponding truth table? 
Each  minterm represents a unique combination of the variables that results in a true (1 output.

Each variable adds $2^x$ different boolean values so $2*2*2=8$ so 4 our of 8 values that correspond to cases where the output is 1. This means that the Boolean function has 4 minterms in its disjunctive normal form (PDNF), as each minterm represents a specific combination of inputs that make the function true.

# Exercise 3

## 1)
Prove the following theorem: Let $x$ be a positive integer. It holds that $gcd(x, 2) = 1$ if and only if x is odd.

Theorem: 
Let $x$ be a positive integer. It holds that: $$\gcd(x, 2) = 1 \iff x \text{ is odd.}$$We will prove this theorem by contraposition. Let: $p$ be the statement $\gcd(x, 2) = 1$, - $q$ be the statement $x$ is odd. The original implication is: $$p \rightarrow q.$$ The contrapositive is: $$\neg q \rightarrow \neg p,$$ where: $\neg q$ means $x$ is even, and 
$\neg p$ means $\gcd(x, 2) \neq 1$. 
We now proceed to prove the contrapositive. 
Proof: 
1. Assume $x$ is even. By definition, an even number can be written as: $$x = 2k, \quad \text{where } k \text{ is a positive integer.}$$
2. Compute $\gcd(x, 2)$: Since $x = 2k$, $x$ is divisible by 2. Therefore, we have: $$\gcd(x, 2) = 2.$$
3. Since $\gcd(x, 2) = 2$, it follows that $\gcd(x, 2) \neq 1$. 

Since the contrapositive is true, the original statement is also true. Therefore, we have proven that: $$\gcd(x, 2) = 1 \iff x \text{ is odd.}$$


## 2)
Prove the following theorem: Let x be a positive integer. It holds that $9^x − 2 ~mod~ 5 = 2$ is equivalent to $x$ being odd.

Theorem:
Let $x$ be a positive integer.  
$9^x - 2 \mod 5 \equiv 2$ is equivalent to $x$ being odd.

#Proof

Because mod 5 is just a function it can be discarded.
$9^x - 2 \equiv 2$

Add 2 to both sides
$9^x  \equiv 4$

Because of the nature of orders of units in modular arithmetic $9^x \mod 5$  has a cyclic behaviour. This means that the same last digit is seen multiple times when varying x.

$9^1 \mod 5 \equiv 4$
$9^2 \mod 5 \equiv 1$
$9^3 \mod 5 \equiv 4$
$9^4 \mod 5 \equiv 1$

Here it is seen that it cycles between 4 and 1.

This means that when x is:
even it returns 1.
odd it returns 4.

The equation:
$9^x - 2 \equiv 2 \pmod{5}$ is satisfied if and only if $x$ is odd.
Therefore the theorem is true.


## 3)
Explain why the previous theorems show that $Q(x)$ and $R(x)$ are the same function. Hence we can replace $R(x)$ with $Q(x)$ in (1) and show that it is equivalent to $$(P(x) \land \neg Q(x)) \lor \neg (P(x) \lor \neg Q(x) \lor Q(x)) \lor (\neg P(x) \land \neg Q(x) \land Q(x))$$ $$\equiv (P(x) \land \neg Q(x)) \lor \neg (P(x) \lor T) \lor (\neg P(x) \land F)$$ $$\equiv P(x) \land \neg Q(x)$$
The theorems show that $Q(x)$ and $R(x)$ are the same because 

$$9^x - 2 \equiv 2 \pmod{5} \iff \text{ x is odd.}$$
$$\gcd(x, 2) = 1 \iff x \text{ is odd.}$$
That means they are both true for the same x value, or if it is odd. They are logically equivalent.


$$(P(x) \land \neg R(x)) \lor \neg (P(x) \lor \neg Q(x) \lor R(x)) \lor (\neg P(x) \land \neg Q(x) \land R(x))$$
Now that $Q(x)$ and $R(x)$ are proven to logically equivalent it can be replaced in the formula. 
 Replace $Q(x)$ with $R(x)$
 
$$(P(x) \land \neg R(x)) \lor \neg (P(x) \lor \neg R(x) \lor R(x)) \lor (\neg P(x) \land \neg R(x) \land R(x))$$

Remove negation from second term using de morgans

$$(P(x) \land \neg R(x)) \lor (\neg P(x) \land R(x) \land \neg R(x)) \lor (\neg P(x) \land \neg R(x) \land R(x))$$

R(x) and R(x) is a contradiction therefore it can be replaced with F

$$(P(x) \land \neg R(x)) \lor (\neg P(x) \land F) \lor (\neg P(x) \land F)$$
Since any minterm with false in it is a contradiction the minterms can be discarded.

$$P(x) \land \neg R(x)$$
Replace R(x) with Q(x)

$$(P(x) \land \neg Q(x) \equiv P(x) \land \neg Q(x)$$

Thus it shown that it is logically equivalent.

## 3) 
Check if (2) is in CNF, DNF, PCNF and PDNF.

$$P(x) \land \neg Q(x)$$

CNF:
- Visual: $(P(x) \lor \text{False}) \land (\neg Q(x) \lor \text{False})$
- Explanation: A conjunction of disjunctions of literals.

DNF:
- Visual: $(P(x) \land \neg Q(x)) \lor \text{False}$
- Explanation: This satisfies DNF because it is a **disjunction** of **conjunctions** (in this case, just one conjunction).

### PDNF:
- Visual: $(P(x) \land \neg Q(x))$
- Explanation: It is in PDNF because it represents conjunctions of minterm.

### PCNF:
- Explanation: It is not in PCNF because there are no maxterms (no disjunction of literals).












