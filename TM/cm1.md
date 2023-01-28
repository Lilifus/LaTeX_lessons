
---
title: Technique de modélisation
documentclass: article
toc: true
...

//pandoc user guide pour la doc

# Wednesday January 25 2023 Course
## I - Equations differentielles
### 1. Définitions
Une équation differentielle est une équation qui relie une fonction à ses dérivées.
La solution recherchée n'est donc pas un nombre mais une fonction.

\textbf{Exemple:} $u'(t)=u(t)$

* On distingue les équations différentielle ordinaires(EDO) des équations aux dérivées partielles (EDP).
Les EDO concernent les fonctions à une variable et les dérivées par rapport à cette variable
Les EDP concernent les fonctions à plusieurs variables et les dérivées partielles par rapport aux différentes variables.
* On appelle ordre d'une EDO ouu d'une EDP l'ordre de dérivation le plus elevé de l'équation.
On dit qu'une équation est à coefficient constant si les coefficients devant la fonction et ses dérivées sont constants.
Dans le cas contraire on parle d'EDO ou d'EDP à coefficients variables.
* On dit qu'une EDP ou une EDO est homogène si tous ses termes dépendent de la fonction inconuue.
Dans le cas contraire on parle d'EDO ou d'EDP non homogène.
* Une distinction importante est de savoir si une EDO ou EDP est linéaire ou non linéaire.
Pour répondre à cette question on va transformer notre equation sous la forme: $L(u)=f$
On dira que l'équation est linéaire si l'opérateur associé $L$ est linéaire.
Dans le cas contraire, elle sera non linéaire.

### 2. Notion de problème bien posé
On dit qu'un problème (i.e. EDO+Condition initiale, ou EDP+Condition initale+Condition initiales/aux bords) est bien posé s'il vérifie les points suivants:
    - il existe une solution
    - cette solution est unique
    - La solution dépend continument des conditions initiales ou aux limites.

\textbf{Exemple:}
$$
\begin{cases}
u'(t) = -u(t) \text{ et } v'(t) = -v(t)\\
u(0) = u_0\quad\quad\quad v(0) = v_0+\epsilon
\end{cases}$$

$$
\text{(1)}
\left.\begin{array}{lll}
u(t)&=&Ke^{-t}\\
u(0)&=&K = u_0
\end{array}\right\}
\rightarrow u(t)=u_0e^{-t}$$

$$
\text{(2)}
\left.\begin{array}{lll}
v(t)&=&Ke^{-t}\\
v(0)&=&u_0 + \epsilon = K
\end{array}\right\}
\rightarrow v(t)=(u_0+\epsilon)e^{-t}$$

$$|v(t)-u(t)|=|(u_0+\epsilon)e^{-t}-v_0e^{-t} = |\epsilon|e^{-t}\Rightarrow \text{"erreur controlée"}$$


\textbf{Exemple 2:}
$$
\left\{\begin{array}{lll}
u'(t)&=&t u(t)(u(t)-2)\\
u(0)&=&u_0
\end{array}\right.
$$

\textbf{Solution:}
$$
\begin{array}{lll}
u(t)&=&\frac{2u_0}{u_0+(2-u_0)e^{t^2})}\\
u&=&2\\
u(t)&=&\frac{2(2+\epsilon)}{2+\epsilon e - \epsilon e^{t^2}}
\end{array}
$$

$$
\begin{array}{lll}
2+\epsilon - \epsilon e^{t^2}&=&0\\
e^{t^2}&=&\frac{2+\epsilon}{\epsilon}\\
t_0&=&\sqrt{ln(\frac{2+\epsilon}{\epsilon}}
\end{array}
$$

* $v_0=2-\epsilon$
pour $\epsilon << 1 \quad 2-\epsilon + \epsilon e^{t^2} >0$
$u(t) = \frac{2(2-\epsilon)}{2-\epsilon + \epsilon e^{t^2}}$


//INSERER COURBE


### 3 - Quelque solutions analytiques
### a - Méthode des caractéristique

On appelle problème de Cauchy, une équation différentielle sur $\mathbb{R}$ avec une condition initiale.

Considéroons le problème suivant:
$$ \begin{cases}
u_t(x,t) + a(x,t) u_x(x,t) = 0 \forall x \in \mathbb{R}, t > 0\\
u(x,0) = \Phi(x) \forall x \in \mathbb{R}
\end{cases}$$
et a et $\Phi$ sont des fonctions régulières

Equation caractéristiques:
$$\begin{cases}
\frac{\partial x^t}{\partial t} = a(x(t),t)\\
x(0)=x_0
\end{cases}$$
//INSERER COURBE 2

$$ 
\begin{array}{ll}
\frac{\partial u(x(t),t)}{\partial t}&= u_x(x(t),t)\frac{\partial x}{\partial t} + u_t(x(t),t) \frac{\partial t}{\partial t}\\
 &=u_x(x(t),t) a(x(t),t) + u_t(x(t),t)\\
 &= 0\\
\end{array}$$

 $$ u(x(t),t) = const = u(x_0,0) = \Phi(x_0)$$

\textbf{Exemple:}
$$
\begin{cases}
u_t + au_x = 0 \quad a = c^k\\
u(x,0) = \Phi(x)
\end{cases}$$

$$ \begin{cases}
\frac{\partial x}{\partial t} = a\\
x(0) = x_0
\end{cases}
\begin{matrix}\to\\\\\end{matrix}
\begin{matrix}
x(t)=at+c^k\\
x(t)=at+x_0
\end{matrix}$$
$$\begin{array}{lll}
u(x(t),t)&=&\Phi(x_0)\\
x&=&at+x_0 \to x_0=x-at\\
u(x,t)&=&\Phi(x-at)
\end{array}$$//encadrer

Le long d'une caractéristique analytique:
$$ \frac{\partial u(x(t),t)}{ \partial t} = u_t a(x,t)u_x =b(x(t),t) $$

$$\begin{array}{lll}
\int^t_0 \frac{\partial u_x(x(\tau),\tau)}{\partial \tau} d \tau &=& \int^t_0 b(x(\tau),\tau)d\tau\\
 u(x(\tau),\tau)-u(x(0),0) &=& \int_0^tb(n(\tau),\tau)+\tau
 \end{array}$$

 $$\begin{cases}
 u_e+u_x=x x \in \mathbb{R}, t > 0\\
 u(x,0)=\Phi(x)
 \end{cases}$$

 $$\left.\begin{array}{ll}
 \frac{\partial x}{\partial t} = 1\\
 x(t=0)=x_0
 \end{array}\right\}
 \to x(t)=t+x_0\Rightarrow x_0=x-t$$

 $$
 \begin{array}{lll}
 u(x(t),t)&=&\Phi(x_0)+\int^t_0(x_0+\tau)d\tau\\
  &=& \Phi(x-t)+ \int^t_0(x_0+\tau)d\tau\\
  &=& \Phi(x-t) + [x_0\tau+\frac{\tau^2}{2})^t_0\\
  &=& \Phi(x-t) + (x_0t+\frac{t^2}{2})
  \end{array}$$

$$
\begin{array}{lll}
u(x,t)&=&\Phi(x-t)+(x-t)t+\frac{t^2}{2}\\
 &=& \Phi(x-t)+xt-\frac{t^2}{2}
 \end{array}$$
  
\pagebreak

# Wednesday January 25 2023 Exercises
## TD 1
### Exercice 1

Une EDO (Equation Différentielle Ordianaire) possède \textbf{ UNE variable}.

Une EDP (Equation aux Dérivées Partielles) possède \textbf{ PLUSIEURS variable}.

Une équation est homogène si tout dépends de la fonction inconnue.

\underline{Espace vectoriel}: stabilité par l'addition et la multiplication par une constante, càd l'addition de 2 valeurs $\in$ ensemble.

1. $u'(t)=e^tu(t)$

La seule variable est $t$, l'équation est donc une \textbf{EDO}.

2. $u''(t)=u(x)\sqrt{x}$

Les variables sont $x$ et $t$, l'équation est donc une \textbf{EDP}.

3. $u_{xx}(x,y) + u_{yy}(x,y)e^{\sin{x}}=1$

Les variables sont $x$ et $y$, l'équation est donc une \textbf{EDP}.

4. $u_{t}(x,t) + u_{x}(x,t)=u_{xx}(x,t)+u^{2}(x,t)$

Les variables sont $x$ et $t$, l'équation est donc une \textbf{EDP}.

5. $(u(t))^{(2)}+u(t)=e^t$

La seule variable est $t$, l'équation est donc une \textbf{EDO}.

