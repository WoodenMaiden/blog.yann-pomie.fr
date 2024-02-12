# Définition

Les automates à piles sont un type d'[[Automates#Déterminisme|automates non-déterministes]] qui vont lire une entrée tout en remplissant et vidant une [pile (ou _stack_)](https://fr.wikipedia.org/wiki/Pile_(informatique))avec des symboles, et c'est un lisant ces symboles que l'automate devient déterministe.

Chaque transition va avoir cette notation: 

```
a,b -> c
--------->
```

Soit: 
- `a`: le symbole qui complétera l'[[Automates#Définitions|étiquette]], peut être une [[Automates#Epsilon Transitions|epsilon transition]]
- `b`: le symbole qui est censé être au sommet de la pile et qui va être consommé, **la transition est à emprunter si on retrouve ce symbole au sommet de la pile**, si c'est le symbole de fin de stack on ne lit et pop rien. 
- `c`: le symbole à mettre au sommet de la pile, si c'est $\epsilon$ on n'y envoie rien

> [!INFO]
> En général on a un symbole dans la stack pour symboliser le fond de celle ci, très souvent un dollar.

Quand nous allons changer d'état dans cet automate on va donc regarder ce qui y à au dessus de la stack et faire les actions ci dessus.

--- 

<iframe title="Lecture 20/65: PDAs: Pushdown Automata" src="https://www.youtube.com/embed/s5cB_xg9NGg?start=275&amp;feature=oembed" height="150" width="200" allowfullscreen="" allow="fullscreen" style="aspect-ratio: 1.33333 / 1; width: 100%; height: 100%;"></iframe>