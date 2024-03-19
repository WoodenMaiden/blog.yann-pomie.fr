## Définition 

Un **mot** est une séquence de longueur positive de **lettres/symboles**, inscrits   dans un **alphabet** noté $\Sigma$ qui lui définit un **langage**.

### Significations 
- $\epsilon$ le mot vide
- $\Sigma = \{a,b,c\}$ Un alphabet avec les lettres a, b et c
- $|m|$ Est la longueur d'un mot
- $m(i)$ $i$-ème lettre du mot $m$

> [!IMPORTANT]
> L'égalité entre deux mots se fait sur leur contenu pas seulement leur longueur

### Opérations et propriétés 

- La concaténation (aka produit, concaténation): Soit un mot $u.v$, il est définit par 
$$|u.v| = |u| + |v|$$
$$\forall i \in [1,|u|]: u.v(i) = u(i)$$
$$\forall i \in [1,|v|]: u.v(|u| + i) = v(i)$$
Par exemple si $u = ab, v = cd$ -> $u.v = ab.cd = abcd$

- Associatif: $u.(v.w) = (u.v).w$
- $u.\epsilon = \epsilon.u = u$

### Préfixes, suffixes et facteurs 

Tout comme en Français un mot $m$ peut avoir des suffixes et des préfixes, c'est a dires des mots placés en produit au début ou à la fin de $m$. 

Un Facteur est le mot qui se trouve entre le préfixe et le suffixe.

Un mot $m$ admet des sous mots $x$ qui sont constitués de lettres extraites de $m$ mais dont on à gardé l'ordre.   

![[Pasted image 20240208001402.png|center]] 