
---
title: Optimisation et Recherche Operationnelle
author: Zakaria EJJED
documentclass: article
header-includes:
    - \usepackage{algorithm}
    - \usepackage{algpseudocode}
    - \usepackage{tikz}
toc: true
...


# Thursday January 26 2023 Course

\textbf{Optimisation:}

$\to$ on cherhce le point $x*$ où l'optimisation (minimum ou maximum selon le cas) de la
fonction f est réalisé.

\textbf{Recherche opérationnelle:}
$\to$ on se trouve dans un contexte industriel dans lequel on cherche à résoudre un 
problème concret, problèmes que l'on peut représenter comme des problème d'optimisation.

$\Rightarrow$ \underline{modélisation}: travail de représentation mathématique/informatique
d'un problème concret qui est posé.
$\to$ abstraction/simplification.


\textbf{Exemple:} Gestion de stocks.

* **Entrepot:**
Chaque jour, q=100 unités sortant; une unité en stock coûte a=0,16€/jour; le coût d'une passation de commande est b=50€, et le réapprovisionnement à lui automatiquement dès que le stock est vide; une commande ne peux axcéder c=400 unités.\
On cherche le volume optimal O$^\text{R}$ d'une commande.\
$\to$ modélisation: on cherche à minimiser le coût de gestion de l'entrepôt.

* **Coût de gestion:**\

$$
\begin{array}{llll}
&\text{coût de stock}&=&0,16\text{€/jour/unité}\\
+ &\text{coût de commande}&=&50\text{€}
\end{array}$$
$\to$ On expime tout en euros par jour.

* **Coût de stock:** \
\quad On cherche le nombre moyen d'unités dans le stock: on suppose que le stock se vide à un rythme régulier, et de façon continue.\
//1
Le stock moyen est le stock moyen sur un période
$\frac{Q}{2}$ .

$$\int^T_0 Q(1 -\frac{t}{T}) dT = \frac{Q}{2} $$

Le coût quotidien de gestion de stock est a.$\frac{Q}{2}$€/j.\
coût de commande:\
$\frac{Q}{100}$ est le temps (en jour) entre deux commandes: on fait une commande, coûte b=50€, tous les $\frac{Q}{100}$ jours, et le coût quotidient moyen de commande est des:
$$\frac{b}{a/q}=\frac{50}{Q/100}=\frac{5000}{Q}$$

Le coût quotidien moyen de gestion de l'entrepôt est de:

$$\begin{array}{l}
f(Q)=0,08Q+\frac{5000}{Q}\\
D=[0,400]\quad Q\leq 400 \quad Q\geq 0\\
\text{min }\{f(Q)/Q\in D\}\\
\text{min }\{0,08Q+\frac{5000}{Q}/0\leq 400\} 
\end{array}$$

On détermine le table de variation de f:

$$\begin{array}{lll}
\forall Q\in ]O,400],&&\\
f'(Q)&=&0,08-\frac{5000}{Q^2}\\
f'(Q) & = & 0\\\\
\Leftrightarrow 0,08-\frac{5000}{Q^2}&=&0\\
\Leftrightarrow \frac{5000}{Q^2}&=&0,08\\
\Leftrightarrow \frac{Q^2}{5000}&=&\frac{1}{0,08}\\
\Leftrightarrow Q^2&=&\frac{5000}{0,08}=\frac{500000}{8}=62500\\
\Leftrightarrow Q&=&\sqrt{62500}\simeq 250\text{car Q>0}
\end{array}$$ 

$$\text{si } \sqrt{\frac{2bq}{Q}}$$
...

//TABLEAU DE VARIATION

La minimisation de f est atteinte à 250: le volume optimal de commande est Q*=250, pour un coût quotidien de f(Q*)=40.

Si on généralise à des a, b, c, q, quelconques:

$$\begin{array}{lll}
\forall Q\in ]O,0],&&\\
f(Q)&=&a\times\frac{Q}{Q^2}+\frac{bq}{Q}\\
f'(Q) & = & \frac{a}{2}-\frac{bq}{Q^2}\\\\
f'(Q) & = & 0\\\\
\Leftrightarrow \frac{a}{2}-\frac{bq}{Q^2}&=&0\\
\Leftrightarrow \frac{bq}{Q^2}&=&\frac{a}{2}\\
\Leftrightarrow \frac{Q^2}{5000}&=&\frac{1}{0,08}\\
\Leftrightarrow Q&=&sqrt{\frac{2bq}{a}}\text{ car } Q > 0\\
\end{array}$$ 

//TABLEAU DE VARIATIONS

\begin{algorithm}
\caption{Algo Stock opti (a,b,c,q:réels > 0)$\to$Q$^*$:réel>0}\label{alg:cap}
\begin{algorithmic}
    \If{$\sqrt{\frac{2bq}{a}}\leq c$}
        \State$Q^* \gets \frac{2bq}{a}$
    \Else
        \State$Q^* \gets c$
    \EndIf
\end{algorithmic}
\end{algorithm}

## I - Problème d'ordonnancement
On cherche à déterminer l'ordre dans le quel effectuer des tâches, définies par leurs 
durées, et par des relations de précedence: certaines tâches ne peuvent être effectuées 
qu'après que d'autres aient été accomplies.

On cherche à déterminer le planning permettant de terminer au plus vite le projet.

On a une série de tâche {$t_i/i=1,...,u$}, A chaque tâche est associée une durée, ainsi 
qu'une liste de tâches {$p_{ij}/j=1,...,k_i$} qui doivent être terminée avant que la tâche
$t_i$ ne puisse commencer.

La fonction objective est la durée du projet, que l'on cherche à minimiser; les
contraintes sont les contraintes de précendence; les variables de décision décrivent
l'ordre dans lequel on effectue les tâches: c'est le planning de ces tâches, c'est à
dire la date de début de chacune des tâches.

La durée totale du projet, fonction objective, est la durée entre le début de la premiète
tâche ($\to t=0$) et la fin de la dernière.

$t_f=$

la tâche $t_i$ se termine au temps $a_i\text{(date de début de la tâche)} + d_i\text{(durée de la tâche)}$

Le projet se termine en même temps que la dernière tâche, au temps:\
max\{ $a_i+d_i/i=1,...,u$ \}.

On cherche donc à minimiser max\{ $a_i+d_i/i=1,...,u$ \}.

On a de plus les contraintes suivantes:
$$\begin{array}{lll}
\forall i=1,...,u\\
a_i &\geq & 0\\
\forall i=1,...,u && \forall k \in P_i,\\
a_k+d_ka&\leq & a a_i
\end{array}$$

Au final, le problème consiste à trouver des $a_i$ réalisant:

min\{max\{$a_i+d_i/i=1,...,u$\}/
$\forall i, a_i \geq 0;\quad \forall k \in P_i,$
$a_i\geq a_k+d_k\}\text{ contraintes}$

On peut également modéliser ce problème sous la forme de graphes. Dans la 
méthode des **potentiels**, chaque tâche est représentée par un sommet et
les relations de précédences par des arcs. Un arc joint $j$ à $i$ si $j \in P_i$

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {$j$};
\node[main] (2) [right of=1] {$i$}; 
\draw[->] (1) -- node[midway, above, sloped] {$d_j$}(2);
\end{tikzpicture} 
\end{center}

A chaque arc, on associe la durée de la tâche dont il est issu.
La longueur d'un chemin représente la durée de tâches qui doivent être executés consécutivement: la durée du projet est donc plus grande que la longueure et n'importe quel chemin dans ce graphe.

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {A};
\node[main] (2) [right of=1] {B}; 
\node[main] (3) [below right of=1] {C}; 
\node[main] (4) [right of=3] {D}; 
\node[main] (5) [right of=4] {E}; 
\node[main] (6) [right of=5] {fin}; 
\foreach \from/\to in {1/2,1/3,2/4,4/2,3/4,4/5}
    \draw[->] (\from) -- (\to);
\draw[->] (5) -- node[midway, above, sloped] {1}(6);
\end{tikzpicture} 
\end{center}

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {A};
\node[main] (2) [above right of=1] {B}; 
\node[main] (3) [below right of=1] {C}; 
\node[main] (4) [right of=2] {D}; 
\node[main] (5) [below right of=4] {E}; 
\node[main] (6) [above right of=5] {fin}; 
\node[main] (7) [above right of=2] {F}; 
\draw[->] (1) -- node[midway, above, sloped] {3}(2);
\draw[->] (1) -- node[midway, above, sloped] {3}(3);
\draw[->] (2) -- node[midway, above, sloped] {4}(4);
\draw[->] (3) -- node[midway, above, sloped] {2}(4);
\draw[->] (4) -- node[midway, above, sloped] {2}(5);
\draw[->] (5) -- node[midway, above, sloped] {1}(6);
\draw[->] (4) -- node[midway, above, sloped] {2}(6);
\draw[->] (2) -- node[midway, above, sloped] {4}(7);
\draw[->] (7) -- node[midway, above, sloped] {5}(4);
\end{tikzpicture} 
\end{center}

Recherche d'un plus long chemin dans un graphe (problème de maximisation):
max\{$f$\} = -min\{$-f$\}

//COURBE

L'algo de Dijkstra ne peut s'appliquer car il nécessite des valuations positives.
$\Rightarrow$ algo de **Bellman-Ford**.

La durée totale du projet est donc minorée par la longueure du plus long chemin dans ce 
graphe; en fait, on peut la rendre égale à cette longueuer.

$\to$ recherche d'un plus long chemin dans un graphe.

$\hookrightarrow$ revient à chercher le plus court chemin dans ce graphe dans lequel on a 
remplacé chaque valuation par son opposé.

Le problème du plus court chemin n'a pas de solution en présence d'un cycle de poids <0;

\begin{center}
\begin{tikzpicture}[node distance={15mm},main/.style = {draw, circle}] 
\node[main] (1) {d};
\node[main] (2) [right of=1] {b}; 
\node[main] (3) [right of=2] {a}; 
\foreach \from/\val/\to in {1/l/2,2/l'/3}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);
    \draw[->] (2) to [looseness=5]  node[midway, above, sloped] {l''}(2);
\end{tikzpicture} 
\end{center}
$$l+l' > l+l'+l'' > l+ l' + 2l'' > ... > l + l' + kl'' \quad \forall k$$

$\to$ pas de plus court chemin, parce qu'une fois qu'on en a un, on peut toujours en 
construire un encore plus court.

**DAG**: directed acyclic graph, graphe orienté acyclique.

$\Rightarrow$ algo de **Ford**  
On prend les noeuds dans un ordre garantissant qu'in noeud est traité après
tous ses prédécesseurs (cet ordre existe sinon le graphe contiendrait un cycle) traiter 
les noeud i consiste à fixer sa date à 
$max\{a_j + d_j / j \in P\}$

**Par exemple:**

Tâche|Description|Durée|Précédence
---|---|---|---
A|teinture|1|E,G
B|confection|1|A,D
C|étude de marché|5|-
D|commande fermeture éclaire|7|E
E|commande tissu|6|-
F|impression catalogue|6|G,H
G|choix coloris|4|C
H|contact imprimeur|7|-

\begin{center}
\begin{tikzpicture}[node distance={20mm},main/.style = {draw, circle}] 
\node[main] (1) {A};
\node[main] (2) [below right of=1] {B}; 
\node[main] (3) [left of=1] {G}; 
\node[main] (4) [left of=2] {D}; 
\node[main] (5) [left of=4] {E}; 
\node[main] (6) [left of=3] {C}; 
\node[main] (7) [above right of=3] {F}; 
\node[main] (8) [left of=7] {H}; 
\node[main] (9) [right of=1] {fin}; 
\foreach \from/\val/\to in {8/7/7,7/6/9,6/5/3,3/4/7,3/4/1,5/6/1,5/6/4,4/7/2,2/1/9,1/1/2}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);
\end{tikzpicture} 
\end{center}
\begin{center} \textbf{Graphe des potentiels} \end{center}

max\{$a_j+d_j/j\ in P$\}

$\qquad\qquad\qquad\searrow$

Tâche|Date au plus tôt|Date au plus tard|Marge totale|Marge libre
---|---|---|:---:|:---:
C|0|min\{5-5\}=0|0|0
E|0|min\{13-6,7-6\}=1|1|0
H|0|min\{5-7\}=2|2|2
D|max\{0+6\}=6|min\{14-7\}=7|1|0
G|max\{0+5\}=5|min\{13-4,9-4\}=5|0|0
A|max\{5+4,0+6\}=9|min\{14-1\}=13|4|3
F|max\{5+4,0+7\}=9|min\{15-6\}=9|0|0
B|max\{9+1,6+7\}=13|min\{15-1\}=14|1|1
fin|max\{5+6,13+2\}=15|=15|0|0
\begin{center}
$\downarrow$

Planning optimal
\end{center}

Les tâches C,G et F doivent être exécutées consécutivement, et elles prennent à elles 3 
15j: le projet ne peut pas durer moins, et comme le planning trouvé prend 15j, 
il est optimal.

On appelle date au plus tard la date avant laquelle une tâche doit commencer au risque de
mettre tout le projet en retard.

Une tâche ayant une marge totale de 0 est dite critique: il existe un chemin partant d'un 
sommet sans prédécesseur et allant au noeud "___fin___" en ne passant que par des 
tâches critiques.

La marge libre est le retard que peut prendre une tâche tout en permettant aux tâches 
suivantes de commencer à leur date au plus tôt (=conserver leur marge).

### Quelques formules:

$$\begin{array}{lll}
\text{tôt}_i &=& \text{max\{tôt}_j+d_j/j \in P_i\}\\
&&\text{(avec max }\varnothing=0)\\
\text{tard}_i&=&\text{min\{tard}_j-d_i/i \in P_j\}\\
\text{marge}_i&=&\text{tard}_i - \text{tôt}_i\\
\text{libre}_i&=&\text{min\{tôt}_j-d_i-\text{tôt}_i/i \in P_j\}
\end{array}$$


# Thursday January 26 2023 Exercises

## Exercice 1

Tâche|Durée|Antériorité
---|---|---
A|30|-
B|12|A+15j
C|8|A+20j
D|5|A et C
E|7|C et D
F|15|B et D
G|20|E
H|4|F et G
I|14|H
J|7|I+3j
K|6|I et J

\begin{center}
\begin{tikzpicture}[node distance={20mm},main/.style = {draw, circle}] 
\node[main] (1) {A};
\node[main] (2) [left of=1] {B}; 
\node[main] (3) [right of=1] {C}; 
\node[main] (4) [below of=1] {D}; 
\node[main] (5) [below of=3] {E}; 
\node[main] (6) [below of=2] {F}; 
\node[main] (7) [below of=5] {G}; 
\node[main] (8) [below of=6] {H}; 
\node[main] (9) [below of=8] {I}; 
\node[main] (10) [below left of=9] {J}; 
\node[main] (11) [below right of=9] {K}; 
\node[main] (12) [right of=11] {fin}; 
\foreach \from/\val/\to in {1/15/2,1/20/3,1/30/4,3/8/4,3/8/5,4/5/5,2/12/6,4/5/6,5/7/7,
6/15/8,7/20/8,8/4/9,9/3/10,9/14/11,10/7/11,11/6/12}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);
\end{tikzpicture} 
\end{center}


Tâche|Date au plus tôt|Date au plus tard|Marge totale|Marge libre
:---:|:---:|:---:|:---:|:---:
A|0|0|0|0
B|15|35|20|8
C|20|22|2|2
D|30|30|0|0
E|35|35|0|0
F|35|47|12|12
G|42|42|0|0
H|62|62|0|0
I|66|66|0|0
J|69|73|4|0
K|80|80|0|0
fin|86|86|0|0

## Exercice 2


Tâche|Durée|Antériorité
---|---|---
A|30|-
B|25|-
C|20|5j après début
D|5|A
E|15|B
F|10|B,D
G|25|C
H|12|G
I|7|E,F
J|5|G
K|10|I,J


\begin{center}
\begin{tikzpicture}[node distance={20mm},main/.style = {draw, circle}] 
\node[main] (1) {Début};
\node[main] (2) [above of=1] {A};
\node[main] (4) [right of=1] {C}; 
\node[main] (5) [left of=1] {D}; 
\node[main] (7) [below of=5] {F}; 
\node[main] (3) [below of=1] {B}; 
\node[main] (8) [below of=4] {G}; 
\node[main] (6) [below of=3] {E}; 
\node[main] (9) [right of=8] {H}; 
\node[main] (10) [below of=7] {I}; 
\node[main] (11) [below of=8] {J}; 
\node[main] (12) [below left of=11] {K}; 
\node[main] (13) [below of=12] {fin}; 
\foreach \from/\val/\to in {1/0/2,1/0/3,1/5/4,2/30/5,3/25/6,3/25/7,5/5/7,4/20/8,8/25/9,6/15/10,
7/10/10,8/25/11,10/7/12,11/5/12,12/10/13}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);
\end{tikzpicture} 
\end{center}


Tâche|Date au plus tôt|Date au plus tard|Marge totale|Marge libre
:---:|:---:|:---:|:---:|:---:
Début|0|0|0|0
A|0|0|0|0
B|0|0|0|0
C|5|5|0|0
D|30|33|3|0
E|25|33|8|5
F|35|38|3|0
G|25|25|0|0
H|50|50|0|0
I|45|48|3|3
J|50|50|0|0
K|55|55|0|0
fin|65|65|0|0


\pagebreak
# Thursday February 2nd 2023 Course

La méthode ___PERT___ est une autre méthode pour calculer un ordonnancement optimal. 
Dans cette méthode, on dessine un graphe dont les arcs (et non plus les noeuds ) 
représentent les tâches du problème d'ordonnancement.

Les noeuds représentent alors des "étapes" de la réalisation du projet, étapes auxquelles
un certain nombre de tâches ont été réalisées, permettant de démarrer de nouvelles tâches.

Dans des situations où deux tâches n'ont pas les mêmes antécédents, mais en partagent
certains, pour placer leur étape de départ, on peut être obligé de recourir à des tâches
fictives, de durées nulles, et allant d'une étape correspondant à la réalisation d'un 
ensemble de ses tâches vers une étape correspondant à un ensemble de tâches.

\begin{center}
\begin{tikzpicture}[node distance={20mm},main/.style = {draw, circle}] 
\node[main] (1) {$\frac{\_\_}{|}$};
\node (2) [above right of=1] {ensemble de tâches terminées correspondant à 
l'antécedence des tâches qui en sortent.};
\node (3) [below right of=1] {date au plus tard}; 
\node (4) [below left of=1] {date au plus tôt}; 
    \draw[->] (1) -- (2);
    \draw[->] (1) -- (3);
    \draw[->] (1) -- (4);
\end{tikzpicture} 
\end{center}

\pagebreak

**1.**

Tâche|durée|antécédant
---|---|---
A|6|-
B|5|-
C|7|-
D|4|B
E|1|A,D
F|6|C,D
G|7|A
H|2|E,G


\begin{center}
  \begin{tikzpicture}
    [scale=.8,node/.style={draw, circle}]
    \node[node] (0) at (0,0) {$\frac{Début}{0|0}$};
    \node[node] (1) at (2,-4) {$\frac{A}{6|6}$};
    \node[node] (2) at (2,0) {$\frac{B}{5|5}$};
    \node[node] (3) at (4,4) {$\frac{C,D}{9|8}$};
    \node[node] (4) at (4,0) {$\frac{D}{9|9}$};
    \node[node] (5) at (6,-4) {$\frac{E,G}{13|13}$};
    \node[node] (10)at (4,-2) {$\frac{A,D}{9|12}$};
    \node[node] (9) at (8,0) {$\frac{FIN}{15|15}$};

    \foreach \from/\val/\to in {0/A\,6/1, 0/C\,7/3, 0/B\,5/2, 2/D\,4/4, 1/G\,7/5, 10/E\,1/5, 5/H\,2/9, 3/f\,6/9}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);

    \foreach \from/\to in {4/3, 4/10, 1/10}
    \draw[dashed,->] (\from) -- node[midway, above, sloped] {$\phi$\,0}(\to);
     
  \end{tikzpicture}
\end{center}

Tâche|date au plus tôt|date au plus tard|marge totale|marge libre
---|---|---|---|---
A|0|0|0|0
B|0|0|0|0
C|0|2|2|2
D|5|5|0|0
E|9|9|0|0
F|9|9|0|0
G|6|6|0|0
H|13|13|0|0

**2.**

Tâche|durée|antécédant
---|---|---
A|4|-
B|2|-
C|7|-
D|4|B
E|4|A
F|5|D
G|3|E,F
H|3|D
I|4|C,H
J|1|I,G

\begin{center}
  \begin{tikzpicture}
    [scale=.8,node/.style={draw, circle}]
    \node[node] (0) at (0,0) {$\frac{Début}{0|0}$};
    \node[node] (1) at (2,-4) {$\frac{A}{4|7}$};
    \node[node] (2) at (2,0) {$\frac{B}{2|2}$};
    \node[node] (3) at (4,4) {$\frac{C,H}{9|10}$};
    \node[node] (4) at (4,0) {$\frac{D}{6|6}$};
    \node[node] (5) at (6,-4) {$\frac{E,F}{11|11}$};
    \node[node] (10)at (8,0) {$\frac{I,G}{14|14}$};
    \node[node] (9) at (10,0) {$\frac{FIN}{15|15}$};

    \foreach \from/\val/\to in {0/A\,4/1, 0/B\,2/2, 2/D\,4/4, 1/E\,4/5, 
    4/F\,5/5, 5/G\,3/10, 4/H\,3/3, 3/I\,4/10, 10/J\,1/9, 0/C\,7/3}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);

  \end{tikzpicture}
\end{center}

Tâche|date au plus tôt|date au plus tard|marge totale|marge libre
---|---|---|---|---
A|0|3|3|0
B|0|0|0|0
C|0|3|3|2
D|2|2|0|0
E|4|7|3|3
F|6|6|0|0
G|11|11|0|0
H|6|7|1|0
I|9|10|1|1
J|14|14|0|0

**3.**

Tâche|durée|antécédant
---|---|---
A|5|-
B|1|-
C|7|-
D|3|B
E|3|B
F|3|A,D
G|4|A,C
H|4|A
I|3|H
J|5|I,F,G
K|2|L
L|3|H

\begin{center}
  \begin{tikzpicture}
    [scale=.8,node/.style={draw, circle}]
    \node[node] (0) at (0,0) {$\frac{Début}{0|0}$};
    \node[node] (1) at (2,-4) {$\frac{A}{5|5}$};
    \node[node] (2) at (4,2) {$\frac{B}{1|6}$};
    \node[node] (3) at (4,4) {$\frac{A,C}{7|8}$};
    \node[node] (5) at (4,-2) {$\frac{A,D}{5|9}$};
    \node[node] (9) at (8,-4) {$\frac{H}{9|9}$};
    \node[node] (10)at (7,0) {$\frac{I,F,G}{12|12}$};
    \node[node] (11)at (10,0) {$\frac{L}{12|15}$};
    \node[node] (12)at (8,4) {$\frac{FIN}{17|17}$};

    \foreach \from/\val/\to in {0/A\,5/1, 0/B\,1/2, 0/C\,7/3, 2/E\,3/12, 
    2/D\,3/5, 3/G\,4/10, 1/H\,4/9, 9/L\,3/11, 11/K\,2/12, 9/I\,3/10, 5/F\,3/10, 10/J\,5/12}
    \draw[->] (\from) -- node[midway, above, sloped] {\val}(\to);

    \foreach \from/\to in {1/3,1/5}
    \draw[dashed,->] (\from) -- node[midway, above, sloped] {$\phi,0$}(\to);
  \end{tikzpicture}
\end{center}

Tâche|date au plus tôt|date au plus tard|marge totale|marge libre
---|---|---|---|---
A|0|0|0|0
B|0|5|5|0
C|0|1|1|0
D|1|6|5|1
E|1|14|13|13
F|5|9|4|4
G|7|8|1|1
H|5|5|0|0
I|9|9|0|0
J|12|12|0|0
K|12|15|3|3
L|9|12|3|0
## II - Programmation linéaire

Un programme linéaire est un problème d'optimisation dans lequel la fonction objective
est linéaire et les contraintes sont affines.

max/min $\{\sum_{i=1}^n c_i x_i / \forall j, \sum_{j=}^n a_{ij} x_i \{\leq , \geq , 
\text{ ou } = \} b_j\}$ 

C'est une catégorie particulière, mais importante de problèmes d'optimisation.

* Imaginer une entreprise fabriquant des compotes.\
$\to$compote pommes/fraises PF\
$\to$compote pommes P\
$\to$compote pommes F

* Pour produire 1kg de compotes\
\makebox[0.5cm]{PF}$\to$ 2kg pommes, 1kg fraises\
\makebox[0.5cm]{P}$\to$ 3kg pommes\
\makebox[0.5cm]{F}$\to$ 1kg pommes, 2kg fraises

Chaque jour, l'usine reçoit, 3t de pommes et 5t de fraises.

* La préparation d'une tonne de compote nécessite:\
$\to$ 40h pour PF\
$\to$ 30h pour F\
$\to$ 40h pour P\
L'entreprise dispose de 80h de travail/j.

L'entreprise ne peut pas produire plus de 4t de compote par jour (limite de stockage est 
expédition).

* Le bénéfice de l'entreprise est de:\
$\to$ 60€ par tonne de PF\
$\to$ 70€ par tonne de F\
$\to$ 20€ par tonne de P

* Les variables de décision sont ici les nombres de tonne de chaque compote produits 
chaque jour:\
$\to x_1$ est le nombre de tonnes de PF produit chaque jour.\
$\to x_2$ est le nombre de tonnes de F produit chaque jour.\
$\to x_3$ est le nombre de tonnes de P produit chaque jour.\
$(x_1,x_2,x_3)$ représente un plan de production.

* Ce plan de production doit vérifier des contraintes:
  * stockage:\
 $x_1+x_2+x_3 \leq 4$

  * travail:\
  $40x_1+30x_2+40x_3 \leq 80$

  * approvisionnement:\
  $2x_1+x_2+3x_3 \leq 3$\
$\qquad \qquad \uparrow$\
_quantité de pommes (en t)\
nécessaire pour produire\
la quantité de PF du plan\
de produit._\
$$x_1+2x_2 \leq 5$$

   * positivité:\
  $x_1 \geq 0$\
  $x_2 \geq 0$\
  $x_3 \geq 0$

On cherche à maximiser les bénéfices quotidiens:\
$$60x_1+70x_2+20x_3$$

Au final, le problème peut s'écrire:
$$\text{max} \{60x_1+70x_2+20x_3\}\
s.c
\left\{\begin{array}{lll}
x_1+x_2+x_3& \leq & 4\\
40x_1+30x_2+40x_3& \leq & 80\\
2x_1+x_2+3x_3& \leq & 3\\
x_1+2x_2 & \leq & 5\\
x_1,x_2,x_3& \leq & 0\\
\end{array}\right.$$

On appelle solution (réalisable) d'un problème d'optimisation un plan de production $x$
véridiant les contraintes. La solution optimale $x^*$ est la solution
réalisable optimisant la fonction objective.

\begin{tikzpicture}
\draw (0,0) -- (0,1) -- (-1,0.25) -- (-0.5,-1) -- (1,-1) -- (1.5,0) -- (0,0);
\draw (-0.175,0.65) -- (0.75,-0.25);
\end{tikzpicture}

_pas convexe_


* L'ensemble des contraintes définit polyèdre:\
$\to$ c'est l'intersection des sous-espaces définis par chaque contrainte,\
$\to$ chaque contrainte $\sum a_{ij} x_i \leq b_j$ définit un demi-espace limité par
l'hyperplan $\sum a_{ij} x_i = b_j$\
La fonction objective est linéaire. Donc son gradient est constant.\
Donc son gradient est constant. De plus les lignes de niveau associée à cette fonction
sont des hyperplans.\
\begin{tikzpicture}
\draw (-1.75,0) -- (-1,1.25) -- (1,1.25) -- (1.75,0) -- (1,-1.25) -- (-1,-1.25) -- (-1.75,0);
\draw[->] (-0.125,0) -- (0.125,0.125);
\end{tikzpicture}\
Si on prend un point à l'intérieur du polyèdre, le gradient en ce point est non-nul, et
on peut prendre un point $x_0 + \epsilon \triangledown f(x_0)$ avec $\epsilon > 0$ 
suffisement petit, point qui sera meilleur que $x_0$ et toujours dans le polyèdre.\
La solution optimale est forcément sur la frontière ("au bord") de polyèdre.

//COURBE ORO 1

Une solution optimale est donc nécessairement un sommet du ployèdre.
Il suffit donc de parcourir les sommets du polyèdre.
De plus le polyèdre est convexe.

\begin{center}\begin{tikzpicture}
\draw (0,0) -- (0.5,-0.5) -- (1,1) -- (1.2,-0.6) -- (0.8,-1) -- (0.5,-1.7) -- (0.5, -1.25) -- (0,-1.25) -- (0,0);
\end{tikzpicture}\end{center}

La convexité garantit que si un sommet a une valeur meilleur que celle des sommets
adjacents, il est un optimum global.

On peut donc parcourir les sommets de façon à examiner des sommets avec une valeur toujours meilleure, jusqu'à trouver l'optimum.

gradient: 

$$\triangledown f(y) =
\begin{pmatrix}
\frac{\partial f}{\partial x_1} (y)\\
\frac{\partial f}{\partial x_2} (y)\\
\frac{\partial f}{\partial x_3} (y)\\
\end{pmatrix}$$

courbe de niveau:
$$\{x:f(x)=\alpha\}$$

En tout point $x_0$ , le gradient $\vec{\triangledown} f(x_0)$ est normale à la courbe 
de niveau $$\{x/f(x)=f(x_0)\}$$

# Thursday February 2nd 2023 Exercises

## Exercice 1

max \{ $15x_1 +8x_2 - 6HS - 1,5MP - PUB_1 - PUB_2$ \}


$$\text{sc}\left\{\begin{array}{ll}
MP &\leq 400\\
2x_1+x_2 &\leq MP\\
0,75x_1+0,5x_2 &\leq 160 + HS\\
x_1 &\leq 50 + 10PUB_1\\
x_2 &\leq 60 + 15PUB_2\\
PUB_1 + PUB_2 &\leq 100\\
x_1,x_2,MP,HS,PUB_1,PUB_2 &\geq 0
\end{array}\right.$$

## Exercice 2 (annule et remplace !)

On considère un problème d'ordonnancement,

tâche|durée|antécédents
---|---|---
$i$|$d_i$|$P_i$

Modéliser le sous forme de PL.

Notons $x_i$ la date de début de la tâche i (en u.t.) contraintes:
$$\begin{array}{ll}
\forall i, \forall j \in P_i , x_i &\geq x_j + d_j\\
\forall i, x_i &\geq 0
\end{array}$$

fonction objective:\
\begin{center}min\{max\{$x_i+d_i$\}\}\end{center}

Cette fonction objective n'est pas linéaire.

On ajoute une variable de décision, $x_f$, représentant la date de fin du projet.

$$\forall, x_f \geq x_i + d_i$$

$\qquad\qquad\qquad\qquad\qquad\qquad\quad\text{min}\{x_f\}$
$$\text{sc}\left\{\begin{array}{l}
\forall i, \forall j \in P_i, x_i \geq x_j + d_j\\
\forall i, x_i \geq 0\\
\forall i, x_f \geq x_i + d_i
\end{array}\right.$$

$x_f$ représente une date plus grande que le max\{$x_i+d_i\}, mais que les contraintes autorisent à lui être égale; puisqu'on cherche à le minimiser, on a la garanti que, dans la solution optimale, il vaudra ce max.

### Algo du simplexe
## III - Séparation et Evaluation
