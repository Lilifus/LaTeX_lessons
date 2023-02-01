
---
title: Algorithmique et programmation distribuée
author: Zakaria EJJED
documentclass: article
header-includes:
    - \usepackage{algorithm}
    - \usepackage{algpseudocode}
    - \usepackage{tikz}
toc: true
...


# Wednesday February 1st 2023

Un graphe: G(V,E) $\to$ (ensemble sommet, ensembles arêtes)

V=1,2,3,4 | E=[(1,2),(2,3),(3,4)(2,4)}

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {1};
\node[main] (2) [right of=1] {2}; 
\node[main] (3) [below of=2] {3}; 
\node[main] (4) [right of=3] {4}; 
\foreach \from/\to in {1/2,2/3,3/4,2/4}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}

degré d'un sommet x $\in$ V

d(x)=nombre  de ses voisins dans le graphe

exemple: d(2)=3

soit un graphe à n sommets

G=(V,E), |V|=4 (ordre du graphe), max:n-1 min:0

**Exercice: Modelisation d'un problème**

Montrer que dans un groupe de personnes (___n noeuds___), il y a toujours 2 personnes 
qui connaissent (___arêtes___) le même nombre de membres d'un groupe.

Par l'absurde, opposons que les n noeuds ont tous un degré différent

$\to$ contradiction: un noeuds doit avoir un degré n-1

$\to$ Un noeud doit avoir un degré 0 ou il y a n noeuds et n degrés différents possibles
or ces 2 noeuds sont pas connecté.


**Graphe orienté:**Un graphe dans lequel les arêtes (_arc_) ont une direction.

G=(V,A) $\to$ (sommets,arcs)


\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {1};
\node[main] (2) [right of=1] {2}; 
\node[main] (3) [below of=2] {3}; 
\node[main] (4) [above left of=2] {4}; 
\foreach \from/\to in {2/1,3/2,4/2}
    \draw[->] (\from) -- (\to);
\end{tikzpicture} 
\end{center}

V=1,2,3,4 | A =(2,1) (3,2) (4,2) $\to$ (_origine_,_extremité_)

Pour le somemt x

degré entrant: nombre d'arcs dans lequel x extremité

degré sortant: nombre d'arcs dans lequel x origine

d$^+$(x) | d$^-$(x)

**Exemple de graphes:**

* ___graphe complet___: toutes les arêtes sont presentes
$$\text{nombres d'arête }=\frac{n(n-1}{2}$$ 

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {1};
\node[main] (2) [right of=1] {2}; 
\node[main] (3) [below of=2] {3}; 
\node[main] (4) [left of=3] {4}; 
\foreach \from/\to in {1/2,2/3,3/4,4/1,1/3,2/4}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}

* ___graphe biparti___:

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {1};
\node[main] (2) [right of=1] {2}; 
\node[main] (3) [below of=1] {3}; 
\node[main] (4) [below of=2] {4}; 
\node[main] (5) [below of=3] {5}; 
\node[main] (6) [below of=4] {6}; 
\node[main] (7) [below of=5] {7}; 
\node[main] (8) [below of=6] {8}; 
\foreach \from/\to in {1/2,2/3,3/4,4/1,4/7,5/8,3/6}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}

* ___Arbres___: graphe qui n'a pas de cycles.\
cycle:\
\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {1};
\node[main] (2) [right of=1] {2}; 
\node[main] (3) [below of=2] {3}; 
\node[main] (4) [left of=3] {4}; 
\foreach \from/\to in {1/2,2/3,3/4,4/1}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}\
Nombre d'arêtes dans un arbre, sans sommet de degré 0: n-1\
\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {1};
\node[main] (2) [below left of=1] {2}; 
\node[main] (3) [below right of=1] {3}; 
\node[main] (4) [below right of=2] {4}; 
\node[main] (5) [below left of=2] {5}; 
\node[main] (6) [below right of=3] {6}; 
\foreach \from/\to in {1/2,1/3,2/4,2/5,3/6}
    \draw[->] (\from) -- (\to);
\end{tikzpicture} 
\end{center}

* ___arbres enracinés___: Arbres don orienté dans lequel on distingue un noeud racine.

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {R};
\node[main] (2) [below left of=1] {2}; 
\node[main] (3) [below right of=1] {3}; 
\node[main] (4) [below right of=2] {4}; 
\node[main] (5) [below left of=2] {5}; 
\node[main] (6) [below right of=3] {6}; 
\foreach \from/\to in {1/2,1/3,2/4,2/5,3/6}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}\
Feuille d'un arbre: sommets de degré 1 qui n'est pas la racine.

Chemin: ensemble de sommets $x_1,x_2,x_3,...,x_{n-1},x_n$

tel que ($x_1,x_2,x_3,...,x_{n-1},x_n$) sont des arêtes

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (3) {3}; 
\node[main] (1) [above left of=3] {1};
\node[main] (2) [above right of=3] {2}; 
\node[main] (4) [below of=3] {4}; 
\foreach \from/\to in {1/2,1/3,3/2,3/4}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}

longueur chemin: nombre de ses arêtes

père d'un noeud x: soit h(x) sa hauteur, Son père est son voisin dont la hauteur vaut 
h(x)-1

fils d'un noeuf: comme le père mais h(x)+1

___mini exo:___

Soit un arbre à n noeuds\
$\to$hauteur max $\Rightarrow$ n-1 (arbre chemin)\
$\to$hauteur min $\Rightarrow$ 1 (n feuilles)\
$\to$hauteur quand un noeud a exactement 2 fils $\Rightarrow 2^{h-1} \leq n \leq 2^h$


Soit un graphe avec n sommets, $s_1,s_2,...,s_n$

Montrer que $\sum_{i=1}^{n} d(s_i)$ est paire.

Dans la $\sum$ des degrés: chaque arête est compté 2 fois, une fois pour chaque extremité.

**Exercice:** Montrer que le nombre de sommets de degré impaire est paire.

On sait que la somme des degrés est paire, donc pour chaque sommet de degré impaire,
il doit y avoir un second sommet de degrés impaire.

Dans le cas où on aurait un nombre impaire de sommet de degré impaire, la somme des degrés 
serait elle aussi impaire.


Montrer que dans un arbre avec + de 2 sommet, il y a au moins deux sommets de degré 1.

$\to$ En supposant n $\geq$ 2 et un noeud de degré 1.
$$\sum_{i=1}^n d(s_i) \geq 2\times (n-1)+1$$


* ___Complexité - notion :___\
Notation de Landeau: $O(f(x))=g(x)$

* ___informel:___\
à partir d'un certain x, la valeur $g(x)$ sera inférieur à $f(x)$

//COURBE

* ___formellement:___\
on écrit 
$$\begin{array}{lll}
f(x)&=&O(g(x))\\
f(x)&\in &O(g(x))
\end{array}$$\
$$\text{Ssi: }\forall x \geq x_0, \exists k \in N \text{ tel que }|f(x)|\leq k|g(x)|$$\
Exemple:
$$\begin{array}{lll}
f(x)&=&x\\
g(x)&=&x^x
\end{array}$$

//COURBE 4

$$x_0=1 \quad k=1 \quad f(x)=O(g(x))$$

Lors d'une compétition il y a 13 joueurs, est-ce qu'il est possible que chaque joueur
participe à exactement 3 matchs.


* ___système distribué:___ un ensemble de noeuds de calculs, autonomes interconnecté et
pouvant communiquer

* ___représenté par un graphe:___ 
\begin{align*}\text{1 noeud de calcul }&\text{= 1 sommet}\\ \text{1 lien de com }&
\text{= 1 arête}\end{align*}

* 1 noeud n'a accès en lecture/écriture qu'à sa propre mémoire. Tout le reste lui est
envoyé sous forme de message. Un noeud a une vision locale du réseau. Il faut souvent
résoudre des problèmes globaux.

* ___objectif:___ résoudre problèmes globaux à l'aide d'algos locaux\
$\to$ Les noeuds vont devoir communiquer entre eux par passage de message.\
$\hookrightarrow$ 1 noeud peut recevoir 1 message (on sait qui nous l'a envoyé).
$\hookrightarrow$ 1 noeud peut envoyer 1 message à son voisin/

___mini exemple:___

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {$x_1$}; 
\node[main] (2) [right of=3] {$x_2$}; 
\foreach \from/\to in {1/2}
    \draw (\from) -- (\to);
\end{tikzpicture} 
\end{center}

On veut un algo: à la fin de l'execution chaque noeud connait la valeur var max dans le
réseau.

chaque noeud e*nvoie son* var à son voisin

calcul: sur réception de var faire le calcul de max (var $x_1$, var $x_2$)



