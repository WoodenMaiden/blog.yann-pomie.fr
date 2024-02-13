# Définition

Soit un [[Alphabets et mots|alphabet]] $\Sigma$ on exprime $\Sigma *$ l'ensemble des mots sur $\Sigma$. Un langage formel $L$ est un ensemble de mots sur $\Sigma$ càd $L \subseteq \Sigma *$

> [!IMPORTANT]
> $\Sigma *$ inclut $\epsilon$

## Définir un langage formel

Langages définis en extension.
$$
L_a = \{ \epsilon, a, aa, aaa \}
$$
$$
L_i = \{ a, b, aaa, aba \}
$$
Langages définis en intention.
$$
L^\prime_a = \{ mots\, dont\, toutes\, les\, lettres\, sont\, des\, a \}
$$
$$
L^\prime_i = \{ u \in \Sigma * tel\, que\, \exists n \in \mathbb{N}, |u| = 2n + 1 \}
$$

## Opérations sur les langages

| Opération | Signification |
| ---- | ---- |
| Union | Mots appartenant $L_1$ ou $L_2$ |
| Intersection | Mots appartenant $L_1$ et $L_2$ |
| Produit | $\{ u =v.w\; tel\, que\, v\, dans\, L_1\, w\, dans\, L_2 \}$ |
| Complément | $\Sigma* \setminus L$ ou $\Sigma* - L$ |
| Exponentiation | Soit $n \in \mathbb{N}$ <br>$L^0= \{\epsilon\}$<br>$L^1=L$<br>$L^2=L.L$ |

### Propriétés

- le produit et l'union sont associatif
- le produit est asymétrique: $L_1.L_2 \ne L_2.l_1$, mais l'union l'est
- $L.\emptyset = \emptyset$  et $L\cup\emptyset = L$  
- ![[Pasted image 20240209232439.png]]

![[Pasted image 20240209234722.png|center]]

![[Pasted image 20240209234739.png|center]]

Il existe de 3 outils pour les langages

- [[Automates|Les automates]]
- [[Expressions régulières|Les expressions régulières]]
- [[Grammaires|Les grammaires]]

![[Pasted image 20240210180315.png|center]]
