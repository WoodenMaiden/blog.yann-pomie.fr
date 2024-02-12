# Définitions

Un automate permet de savoir si un mot appartient à un [[Langages formels|langage]], $L(A)$ représente les mots d'un langage $L$ reconnus par un automate $A$

![[Screenshot from 2024-02-10 18-07-15_cleanup.png]]
![[Pasted image 20240210180956.png|center]]


Un chemin est une séquence d'États reliés par des transitions, l'ensemble des transitions forment une étiquette 

![[Screenshot from 2024-02-10 18-18-34_cleanup.png|center]]

> [!IMPORTANT]
>  - $m \in \Sigma*$ est reconnu par un automate A ssi il l'est l'étiquette d'un chemin qui commence par in état initial et qui finit sur un état final.
>  - Deux automates sont équivalents si ils reconnaissent le même langage $L$ et seulement L, pas plus pas moins

# Fonction de transition

On peut utiliser une fonction $\zeta(e, m)$ qui prend en paramètre un état $e$ et un **mot** $m$ de $\Sigma*$ (donc pas forcément reconnu par l'automate) et retourne tous les états que l'on atteint en partant de $e$ avec l'etiquette $m$.

![[Pasted image 20240210183735.png|center]]
![[Pasted image 20240210183819.png|center]] 

> [!INFO]
> Si le mot $a$ est de longueur 1 on a donc les voisins directs accessibles avec a


**Exemple:**
![[Pasted image 20240210184035.png|center]]


> [!TIP]
> On peut reformuler la reconnaisance d'un mot ainsi
>$$ m \in \Sigma*\, est \, reconnu\, par\, A\, ssi$$
>$$\exists e \in I,f, \in F\, tq$$
>$$f\in\zeta(e,m)$$
>
>Donc si il existe un état initial $e$ tq $\zeta(e,m)$ contient un etat final

> [!NOTE]- Notes
> - Si $\exists e \in E \cap F$ alors on a $L(A)= \{\epsilon\}$
> - Si $A$ n'a pas de circuit alors $L(A)$ est fini 

# Déterminisme

## Définition

Un automate fini est déterministe (_AFD_) si il admet un seul état initial, et si tous les états ont au plus une transition d'une lettre donnée.
$$|I| = 1$$
$$\forall e \in E,\, \forall a \in \Sigma, |\zeta(e,a)| \le 1$$
![[Pasted image 20240211001418.png|center]]

Ici l'automate n'est pas déterministe car l'état 1 à deux transitions avec le mot $a$. Un AFD est en général plus rapide

## Epsilon Transitions

Il est possible d'avoir des epsilon transitions, c'est a dire d'avoir des transitions avec epsilon (ou le mot vide) comme lettre. C'est notamment utile quand on veut joindre deux automates pour le produit de deux alphabets 

> [!NOTE]
> $e \in \zeta(e,\epsilon)$ car avec epsilon on ne nous demande pas forcément de bouger donc e est une réponse valide

## Déterminisation d'un automate

On peut déterminiser un automate avec cet algorithme on a donc une complexité exponentielle $\mathcal{O}(2^n*|\Sigma|)$

![[Pasted image 20240211005128.png]]

Concrètement avec cet algorithme on démarre depuis l'état initial pour chaque lettre $l$ du langage on note l'ensemble états sur lesquels on atterrit avec $l$ puis on répète l'opération pour chaque état de l'ensemble obtenu. Après tout cela on crée des états pour chaque état/ensemble d'état créés, on les relie et on marque les groups qui ont des états finaux en eux comme tel.    

![[Pasted image 20240211010158.png]]

# Complémentaire


Un automate **peut admettre** un complémentaire, càd pour $A$ un automate sur un alphabet $\Sigma$ qui reconnait un langage $L$ on admet $A'$ qui reconnait des mots sur l'alphabet $\Sigma$, qui ne sont pas de $L$ (qu'on appelle $\overline{L}$)
![[Pasted image 20240211011011.png|center]]

On peut faire ceci en intervertissant les états finaux et les états non-finaux **si et seulement si l'automate est déterministe et complet**. 

Un automate est complet si $\forall e \in E,\forall m \in \Sigma,\, |\zeta(e, m)| >= 1$ càd **si pour tout état $e$ et pour toute lettre $m$ de I'alphabet $\Sigma$ il existe une transition étiquetée $m$ qui part de $e$**

Pour compléter un automate on va créer un état puis qui va recevoir toutes les transitions manquantes. 

![[Pasted image 20240211012017.png]]![[Pasted image 20240211012034.png]]

>[!Important]
>Pour Avoir la complémentaire d'un automate on va donc faire ces étapes dans l'ordre
>1. Le déterminiser
>2. Le compléter
>3. Inverser ses états finaux et non-finaux

# L'union de deux langages

Pour créer un automate $A^3$ qui reconnait le langage de $A^1$ et de $A^2$ Il suffit de les prendre un à côté de l'autre. On a donc à un **automate fini non déterministe** car il garde les mêmes états finaux et initiaux on a donc $|I| = 2$ 
![[Pasted image 20240211012655.png|center]]

# L'intersection de deux langages

Pour créer un automate $A^3$ qui reconnait les mots communs à $A^1$ et à $A^2$, on utiise là loi de Morgan: $A^1 \cap A^2 = \overline{\overline{A^1} \cup \overline{A^2}}$.

On va donc 
1. [[#Complémentaire|Complémenter]] $A^1$ et $A^2$
2. Faire [[#L'union de deux langages|l'union]] de ces compléments 
3. [[#Complémentaire|Complémenter]] cette même union
