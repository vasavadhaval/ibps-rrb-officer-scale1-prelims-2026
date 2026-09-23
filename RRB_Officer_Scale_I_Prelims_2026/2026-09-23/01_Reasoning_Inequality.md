# Reasoning - Inequality: Complete Study Material

## 1. What this topic tests

Inequality questions give relationships between variables and ask which conclusions must be true. Your job is not to find numerical values. You only compare positions in a chain.

This is normally a fast-scoring topic. Aim to solve a standard five-question set accurately in about three to four minutes after practice.

## 2. Symbols and meanings

| Symbol | Meaning | Example |
|---|---|---|
| `A > B` | A is strictly greater than B | A cannot equal B |
| `A < B` | A is strictly smaller than B | B is greater than A |
| `A >= B` | A is greater than or equal to B | Equality is possible |
| `A <= B` | A is smaller than or equal to B | Equality is possible |
| `A = B` | A and B are equal | They can replace each other in a chain |

## 3. Reverse-direction rule

When reading a relationship backwards, reverse the sign:

```text
A > B  becomes  B < A
A >= B becomes  B <= A
A = B  remains  B = A
```

Never reverse only the letters while keeping the original sign.

## 4. Combining relationships

Relationships can be combined when they point consistently in one direction.

```text
A > B >= C > D
```

Definite results include:

```text
A > C
A > D
B > D
D < A
```

But `B > C` is not definite because `B >= C` allows equality.

### Strength rule

If at least one link in a connected same-direction chain is strict, the end relationship is strict.

```text
A >= B > C
Therefore A > C
```

If every link is non-strict, only a non-strict conclusion is guaranteed.

```text
A >= B >= C
Therefore A >= C
```

## 5. When no relationship can be determined

Consider:

```text
A > B < C
```

Both A and C are greater than B, but A and C cannot be compared. A may be greater than, smaller than or equal to C.

The same problem occurs with:

```text
A < B > C
```

Do not force a relationship between disconnected branches.

## 6. Testing conclusions

Use this process for every conclusion:

1. Find both variables in the statement.
2. Connect them through the shortest valid chain.
3. Read the chain in the direction used by the conclusion.
4. Check whether the conclusion is guaranteed, not merely possible.
5. If equality remains possible, reject a strict `>` or `<` conclusion.

## 7. Either-or conclusions

An either-or pair covers all possibilities between the same two variables. Common complementary pairs are:

```text
A > B  OR  A <= B
A < B  OR  A >= B
```

Exactly one statement from each pair must be true. Do not use the either-or rule when the conclusions compare different variable pairs or are not complementary.

## 8. Coded inequalities

A coded question replaces signs with symbols. Decode every symbol before solving.

Example code:

```text
P @ Q means P >= Q
P # Q means P < Q
P $ Q means P = Q
```

Statement:

```text
A @ B # C
```

Decoded form:

```text
A >= B < C
```

A and C cannot be compared because the directions break at B.

## 9. Worked examples

### Example 1

```text
Statement: A > B >= C = D
Conclusion I: A > C
Conclusion II: D < B
```

I follows because `A > B >= C` gives `A > C`.

II does not definitely follow because `B >= C = D` allows `B = D`.

**Answer: Only Conclusion I follows.**

### Example 2

```text
Statement: P <= Q < R = S
Conclusion I: P < R
Conclusion II: S > Q
```

Both follow. The strict `Q < R` link makes both end relationships strict.

### Example 3

```text
Statement: M > N < O
Conclusion I: M > O
Conclusion II: M <= O
```

M and O cannot be directly compared. The conclusions are complementary, so exactly one must be true.

**Answer: Either Conclusion I or II follows.**

### Example 4

```text
Statement: H = I >= J > K
Conclusion I: H > K
Conclusion II: K < I
```

Both follow because the connected chain contains the strict relationship `J > K`.

### Example 5

```text
Statement: X >= Y >= Z
Conclusion: X > Z
```

The conclusion does not follow. X, Y and Z could all be equal. Only `X >= Z` is guaranteed.

## 10. Practice set

For Questions 1-10, use these answer choices:

```text
A. Only Conclusion I follows
B. Only Conclusion II follows
C. Both conclusions follow
D. Neither conclusion follows
E. Either Conclusion I or II follows
```

### Question 1

```text
Statement: A > B >= C = D
I. A > D
II. B > D
```

### Question 2

```text
Statement: P <= Q < R <= S
I. P < R
II. S > Q
```

### Question 3

```text
Statement: M = N >= O > P
I. M > P
II. O < M
```

### Question 4

```text
Statement: X < Y <= Z
I. Z > X
II. X = Z
```

### Question 5

```text
Statement: A >= B >= C
I. A >= C
II. C > A
```

### Question 6

```text
Statement: J < K = L <= M
I. J < L
II. M >= K
```

### Question 7

```text
Statement: R > S; T >= R
I. T > S
II. S < T
```

### Question 8

```text
Statement: U <= V; W < V
I. U < W
II. U >= W
```

### Question 9

```text
Statement: H = I < J <= K
I. H < K
II. K > I
```

### Question 10

```text
Statement: A > B; C > B
I. A > C
II. C > A
```

## 11. Answers and short explanations

1. **A** - A is strictly greater than D; B may equal D.
2. **C** - The strict Q-R link makes both conclusions definite.
3. **A** - M is greater than P; O may equal M.
4. **A** - Z is definitely greater than X; equality is impossible.
5. **A** - A is at least C; C cannot be greater than A.
6. **C** - J is below L, and M is at least K.
7. **C** - Both conclusions express the same definite relationship.
8. **E** - U and W cannot be compared, but the two conclusions are complementary.
9. **C** - Both conclusions express the same strict relationship.
10. **D** - A and C are on separate branches above B and cannot be compared; equality also remains possible, so I and II are not an exhaustive pair.

## 12. Common mistakes

- Treating `>=` as strictly greater than.
- Assuming two variables are related simply because both connect to a third variable.
- Reversing the variables without reversing the sign.
- Accepting a conclusion that is only possible rather than guaranteed.
- Applying either-or to conclusions that are not complementary.

## 13. Completion target

- Read the lesson once.
- Solve the ten written questions without seeing the answers.
- Import and take the JSON topic test.
- Target at least 17 correct out of 20 in the JSON test.
- Redo every incorrect question tomorrow without reading its explanation first.
