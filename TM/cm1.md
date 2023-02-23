
---
title: Technique de modélisation
author: Zakaria EJJED
documentclass: article
header-includes:
    - \usepackage{algorithm}
    - \usepackage{algpseudocode}
    - \usepackage{tikz}
    - \usepackage{fancyhdr}
toc: true
geometry:
    - margin=2cm
...

\pagestyle{fancy}
\newcommand{\deer}{\includegraphics[scale=0.5]{/home/zakaria/Pictures/deer_sig.png}}
\fancyfoot[RE,RO]{\deer}


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
Dans le cas contraire on parle d'EDO ou d'EDP non homogène. * Une distinction importante est de savoir si une EDO ou EDP est linéaire ou non linéaire.
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

# Tuesday February 21st 2023 Exercises

## Exercise 2

* Correction manquante

## Exercice 3

* 1. \
$$\left\{\begin{array}{lll}
\frac{\partial u}{\partial t} + 2x\frac{\partial u}{\partial x} &=& 0  
\qquad x\in \mathbb{R}, t > 0,\\
u(x,0)&=&e^{-x^2}
\end{array}\right.$$\
$$\frac{\partial u}{\partial t}+\frac{\partial x(t)}{\partial t}
\frac{\partial u}{\partial x}=0$$
Courbe caractéristique:
$\left\{\begin{array}{lll}
\frac{\partial x(t)}{\partial t}=2x\\
x(t=0)=x_0
\end{array}\right.$\
$$\begin{array}{llll}
&x(t)&=&Ke^{2t}\\
&x(t)&=&x_0e^{2t}\\
\Rightarrow & x_0 & = & xe^{-2t}
\end{array}$$\
Sur la courbe caractéristique:\
$$\begin{array}{lll}
\frac{\partial u}{\partial t}&=&\frac{\partial x}{\partial t}\frac{\partial u}{\partial x}+
\frac{\partial t}{\partial t}\frac{\partial u}{\partial t}\\
&=&2x\frac{\partial u}{\partial x}+\frac{\partial u}{\partial t}=0
\end{array}$$\
$\int^t_0 \frac{\partial u}{\partial t} = \int^t_0 0 = 0 = u(x,t) - u(x_0,0)$\
$$\begin{array}{lll}
\Rightarrow u(x,t)&=&u(x_0,0)\\
&=&\phi(x_0)\\
&=&e^{-x_0^2}\\
&=&e^{-(xe^{-2t})^2}
\end{array}$$


* 2. \
$$\left\{\begin{array}{lll}
\frac{\partial u}{\partial t} - x\frac{\partial u}{\partial x} &=& 0  
\qquad x\in \mathbb{R}, t > 0,\\
u(x,0)&=&sin(87x)
\end{array}\right.$$\
$$\frac{\partial u}{\partial t}+\frac{\partial x(t)}{\partial t}
\frac{\partial u}{\partial x}=0$$
Courbe caractéristique:
$\left\{\begin{array}{lll}
\frac{\partial x(t)}{\partial t}=-x\\
x(t=0)=x_0
\end{array}\right.$\
$$\begin{array}{llll}
&x(t)&=&Ke^{-t}\\
&x(t)&=&x_0e^{-t}\\
\Rightarrow & x_0 & = & xe^{t}
\end{array}$$\
Sur la courbe caractéristique:\
$$\begin{array}{lll}
\frac{\partial u}{\partial t}&=&\frac{\partial x}{\partial t}\frac{\partial u}{\partial x}+
\frac{\partial t}{\partial t}\frac{\partial u}{\partial t}\\
&=&-x\frac{\partial u}{\partial x}+\frac{\partial u}{\partial t}=0
\end{array}$$\
$\int^t_0 \frac{\partial u}{\partial t} = \int^t_0 0 = 0 = u(x,t) - u(x_0,0)$\
$$\begin{array}{lll}
\Rightarrow u(x,t)&=&u(x_0,0)\\
&=&\phi(x_0)\\
&=&sin(87x_0)\\
&=&sin(87xe^t)
\end{array}$$

* 3.\
$$\left\{\begin{array}{lll}
\frac{\partial u}{\partial t} + x\frac{\partial u}{\partial x} &=& x  \qquad x\in \mathbb{R}, t > 0,\\
u(x,0)=x_0
\end{array}\right.$$\
Courbe caractéristique:
$\left\{\begin{array}{lll}
\frac{\partial x(t)}{\partial t}=x(t) (\leftarrow a(x,t) )\\
x(0)=x_0
\end{array}\right.$\
Donc $x(t) = Ke^t$ avec $K \in \mathbb{R}$\
Or, $x(0)=x_0=Kxe^0$ donc $x(t) = x_0e^t$\
Si $u$ est solution alors: 
$$\begin{array}{lll}
\frac{\partial u(x(t),t)}{\partial t}&=& 
\frac{\partial u}{\partial x} \frac{\partial x(t)}{\partial t} +
\frac{\partial u}{\partial t} \frac{\partial t}{\partial t} \\
&&(\frac{\partial x(t)}{\partial t}
=x(t)\text{ car u est le long d'une courbe caractéristique})\quad\&\quad(\frac{\partial t}{\partial t}= 1)\\
&=& \frac{\partial u}{\partial t} + 
x\frac{\partial u}{\partial x}\\&=& x
\end{array}$$\
$$\begin{array}{lll}
\int^t_0 \frac{\partial u(x(\tau),\tau)}{\partial t} \partial\tau &=& \int^t_0 x(\tau) 
\partial \tau\\
\text{donc } u(x(t),t) - u(x(0),0) &= &[x_0e^\tau]^t_0\\
\text{donc } u(x(t),t) &=& cos(90x_0) + x_0e^t -x_0 
\end{array}$$

$$\begin{array}{lll}
u(x,t)&=&cos(90xe^{-t}+x-xe^{-t} \\
u(x,t)&=&cos(90xe^{-t}+x(1-e^{-t}) \\
x_0&=&xe^{-t}
\end{array}$$

* 4.\
$$\left\{\begin{array}{lll}
\frac{\partial u}{\partial t} + x\frac{\partial u}{\partial x} &=& x^2  \qquad x\in \mathbb{R}, t > 0,\\
u(x,0)=sin(87x)cos(90x)
\end{array}\right.$$\
Courbe caractéristique:
$\left\{\begin{array}{lll}
\frac{\partial x(t)}{\partial t}=x(t) (\leftarrow a(x,t) )\\
x(0)=x_0
\end{array}\right.$\
Donc $x(t) = Ke^t$ avec $K \in \mathbb{R}$\
$$\begin{array}{llll}
&x(t)&=&Ke^{t}\\
&x(t)&=&x_0e^{t}\\
\Rightarrow & x_0 & = & xe^{-t}
\end{array}$$\
SUITE....


## Exercice 4


$$\left\{\begin{array}{llll}
\frac{\partial u}{\partial t} + \frac{\partial u}{\partial x} &=& u  
\quad& x\in \mathbb{R}, t > 0,\\
u(x,0)&=&\phi(x) \quad& x\in \mathbb{R}
\end{array}\right.$$

$$\frac{\partial u}{\partial t}+\frac{\partial x(t)}{\partial t}
\frac{\partial u}{\partial x}=u$$

Courbe caractéristique:
$\left\{\begin{array}{lll}
\frac{\partial x(t)}{\partial t}=1\\
x(t=0)=x_0
\end{array}\right.$

$$\begin{array}{llll}
&x(t)&=&t+cst\\
&x(t)&=&t+x_0\\
\Rightarrow & x_0 & = & x(t)-t
\end{array}$$

$$\begin{array}{lll}
u(x(t),t)&=&Ke^t\\
u(x(0),0)&=&K=\phi(x(0))
\end{array}$$

# Tuesday February 21st 2023 Course

## b - Changement de variables
### Equations des ondes :

$u_{tt}(x,t)=u_{xx}(x,t)$  
$u(x,0) = \phi (x)$  
$u_t(x,0) = \psi (x)$  
On pose  
$\xi = x+t$  
$\eta = x-t$  
$u(x,t) = v(\xi ,\eta)$  
$u_x(x,t) = \frac{\partial v(\xi ,\eta)}{\partial x} = \frac{\partial v}{\partial \xi}\frac{\partial \xi}{\partial x}+\frac{\partial v}{\partial \eta}\frac{\partial \eta}{\partial x}$  
$= \partial_\xi v + \partial_\eta v$  
$u_{xx}(x,t)=\partial x(\partial_\xi v) + \partial x(\partial_\eta v)$  
$=\partial \xi(\partial x v) + \partial \eta(\partial x v)$  
$=\partial \xi (\partial \xi v + \partial \eta v) + \partial \eta (\partial \xi v+ \partial \eta v)$  
$= \partial^2_{\xi \xi} v + \partial^2_{\eta \xi} v + \partial^2_{\xi \eta}v + \partial^2_{\eta \eta} v$  
$u_{xx}= \partial^2_{\xi \xi} v + 2\partial^2_{\eta \xi} v+ \partial^2_{\eta \eta} v$  
$u_t = \frac{\partial v}{\partial t} = \frac{\partial \xi}{\partial t}\frac{\partial v }{\partial \xi}+
\frac{\partial \eta}{\partial t}\frac{\partial v}{\partial \eta}$
$=\partial_{\xi} v - \partial_{\eta}v$  


$u_{tt}=\partial t(\partial_\xi v) - \partial t(\partial_\eta v)$  
$=\partial \xi(\partial t v) - \partial \eta(\partial t v)$  
$=\partial \xi (\partial \xi v - \partial \eta v) - \partial \eta (\partial \xi v- \partial \eta v)$  
$= \partial^2_{\xi \xi} v - \partial^2_{\eta \xi} v - \partial^2_{\xi \eta}v + \partial^2_{\eta \eta} v$  
$u_{tt}= \partial^2_{\xi \xi} v - 2\partial^2_{\eta \xi} v+ \partial^2_{\eta \eta} v$  
$4\partial^2_{\eta \xi}v=0$  
$\partial^2_{\eta \xi}v=0$  
$\partial_{\eta} v = f_1(\eta)$  
$v = \int f1(\eta) + c^k$ peut dÃ©pendre de $\xi$  
$v(\xi , \eta) = f(\eta) + g(\xi)$  
$u(x, t) = v(x+t, n-t) = f(x-t) + g(x+t)$  
$u(x,t)=f(x-t)+g(x+t)$  
$$u(x,0)=f(x)+g(x) = \phi (x)$$  
$$u_t(x,0)=-f'(x)+g'(x) = \psi(x)$$  
$g'(x)=\frac{\phi '(x)+\psi (x)}2$  
$f'(x)=\frac{\phi '(x)-\psi (x)}2$  
$g(x)=c_1 + \frac{\phi (x)}2 + \frac12\int \psi x$  
$f(x)=c_2 + \frac{\phi (x)}2 - \frac12\int \psi x$  
$f+g = c_1 + c_2 + \phi (x)$  
$u(x,t)=\frac{\phi(x-t)}2 - \frac12 \int^{x-t}_0 \psi(z)\partial z+
\frac{\phi(x+t)}2 + \frac12 \int^{x+t}_0 \psi(z)\partial z$
$u(x,t)=\frac{\phi(x-t)+\phi(x+t)}2 + \frac12 \int_{x-t}^0 \psi(z)\partial z+
\frac12 \int^{x+t}_0 \psi(z)\partial z$
$u(x,t)=\frac{\phi(x-t)+\phi(x+t)}2 + \frac12 \int_{x-t}^{x+t} \psi(z)\partial z$

# Tuesday February 21st Exercises (suite)

## Exercice 1

* 1.\
$\partial_x f - \partial_y f = a$, avec $u=x+y$ et $v=x-y$\
$$\left\{\begin{array}{lll}
\partial_x f - \partial_y f &=& a,\quad a\quad cst \in \mathbb{R}\\
u&=&x+y\\
v&=&x-y
\end{array}\right.$$\
$$\begin{array}{lll}
f(x,y)&=&W(u,v)\\\\
f_x(x,y)&=&\frac{\partial W(u,v)}{\partial x}\\
&=&\frac{\partial W}{\partial u}\frac{\partial u}{\partial x}+
\frac{\partial W}{\partial v}\frac{\partial v}{\partial x}\\
&=&\frac{\partial W}{\partial u}+\frac{\partial W}{\partial v}\\\\
f_y(x,y)&=&\frac{\partial W(u,v)}{\partial y}\\
&=&\frac{\partial W}{\partial u}\frac{\partial u}{\partial y}+
\frac{\partial W}{\partial v}\frac{\partial v}{\partial y}\\
&=&\frac{\partial W}{\partial u}-\frac{\partial W}{\partial v}
\end{array}$$\

$$f_x(x,y)-f_y(x,y)=a$$

$\Rightarrow (\frac{\partial W}{\partial v} - (- \frac{\partial W}{\partial v})=a$
$\Rightarrow 2 \frac{\partial W}{\partial v}=a$
$\Rightarrow \int \frac{2 \partial W}{\partial v}=\int a$
$\Rightarrow 2W= av + cst(u)$
$\Rightarrow W= \frac{av + cst(u)}2 = \frac{a}2 v + g(u)$


* 2.\
$x\partial_x f = y\partial_y f$, avec $u=xy$ et $v=\frac{x}{y}$\
$$\left\{\begin{array}{lll}
x\partial_x f &=& y\partial_y f\\
u&=&xy\\
v&=&\frac{x}{y}
\end{array}\right.$$\
$$\begin{array}{lll}
f(x,y)&=&W(u,v)\\\\
f_x(x,y)&=&\frac{\partial W(u,v)}{\partial x}\\
&=&\frac{\partial W}{\partial u}\frac{\partial u}{\partial x}+
\frac{\partial W}{\partial v}\frac{\partial v}{\partial x}\\
&=&\frac{y\partial W}{\partial u}+\frac{\partial W}{y\partial v}\\\\
f_y(x,y)&=&\frac{\partial W(u,v)}{\partial y}\\
&=&\frac{\partial W}{\partial u}\frac{\partial u}{\partial y}+
\frac{\partial W}{\partial v}\frac{\partial v}{\partial y}\\
&=&\frac{x\partial W}{\partial u}+\frac{\partial W}{\partial v}\frac{-x}{y^2}
\end{array}$$  
$$xf_x(x,y)=yf_y(x,y)$$  
$\Rightarrow xy \frac{\partial W}{\partial u} + \frac{x}{y}\frac{\partial W}{\partial v}=
xy \frac{\partial W}{\partial u} + \frac{-x}{y}\frac{\partial W}{\partial v}$  
$\Rightarrow u \frac{\partial W}{\partial u} + v \frac{\partial W}{\partial v}=
u \frac{\partial W}{\partial u} -v \frac{\partial W}{\partial v}$  
$\Rightarrow 2v\frac{\partial W}{\partial v} = 0$
$\Rightarrow \frac{\partial W}{\partial v} = 0$ $v=0$ ou 
$\frac{\partial W}{\partial v}=0$  
$\hookrightarrow W_v=0$  
$\exists g \in C^1$ tq $W(u,v)=g(u)$  
$\exists g \in C^1 / f(x,y)=g(xy)$

# Thursday February 23rd 2023 Cours
## c - Méthode de séparation de variables

* Considérons l'équation de la chaleur:  
$$(Y)\left\{\begin{array}{lll}
\forall (x,t) \in ]0,L[ \times \mathbb{R}^{t \alpha} & u_t(x,t) = \beta u_{xx}(x,t) & 
\beta > 0\\
u(0,t)=u(t,t)=0 & \forall t > 0&\\
u(x,0)=f(x)&&
\end{array}\right.$$  
On suppose que la solution de cette équation peut s'écrire sous la forme 
$u(x,t) = X(x)T(t)$ (séparation de variable) pour tout (x,t) $\in ]0,L[ \times
\mathbb{R}^{t\alpha}$  
En injectant dans (Y) on obtient:  
$$\partial_t(X(x)T(t))=\beta \partial_{xx}(X(x)T(t)$$
$$X.T'=\beta T.X''$$
$$\frac{X}{X''} = \frac{\beta T}{T'} \text{ ou } \frac{X''}{X}=\frac{T'}{\beta T}$$
$$\frac{X''}{X}\to \text{ ne dépend que de "x" } \to \text{ forcément constant } \gets
\text{ ne dépends que de "t" } \gets \frac{T'}{\beta T}$$  
$\exists \lambda \in \mathbb{R}$ tq $\frac{X''}{X}=\frac{T'}{\beta T} = - \lambda$  
soit $X''=-\lambda X$ et $T' = - \lambda \beta T$  

$$\forall t \in \mathbb{R}^{+*}\left|\begin{array}{lll}
u(0,t)=&X(0)T(t)&=0\\
u(L,t)=&X(L)T(t)&=0
\end{array}\right\}  
\Rightarrow
\begin{array}{l}
X(0)=0\\
X(L)=0
\end{array}$$

Si on veut autre chose que la solution triviale $u=0$  
On doit donc résoudre:  
$$\left\{\begin{array}{lllll}
X''&+&\lambda X&=&0\\
X(0)&=&X(L)&=&0
\end{array}\right.$$  
Polynôme caractéristique associé à $X''+ \lambda X = 0$ est  
$$r^2+\lambda=0$$  
$$r^2=-\lambda$$

**Remarque:**  
$$\begin{array}{llll}
&ay''+by'+cy&=&0\\
\hookrightarrow & ar^2+br+c&=&0
\end{array}$$  
___cas 1:___ 2 solutions réelles $r_1,r_2$  
$$y(z)=\alpha_1 e^{r_1 Z} + \alpha_2 e^{r_2 z} \quad
(\alpha_1, \alpha_2) \in \mathbb{R}^2$$

___cas 2:___ 2 solutions complexes $c_1,c_2$  
$$y(z)=\alpha_1 e^{c_1 Z} + \alpha_2 e^{c_2 z} \quad
(\alpha_1, \alpha_2) \in \mathbb{R}^2$$
$$ = \gamma_1 cos(\omega z) + \gamma_2 sin(\omega z)$$
$$ \omega = \sqrt{|b^2-4ac|}$$

___cas 3:___ 1 solutions double $d_1$  
$$y(z)=\delta_1 ze^{d_1 z}+\delta_2 ze^{d_2 z}$$  
$$=\delta_1 z +\delta_2 = e^{d_1 z}$$  

**$$r^2 = -\lambda$$**
**cas 1** :$-\lambda > 0$  
$r_1 = \sqrt{- \lambda} \quad r_2 = -\sqrt{- \lambda}$  
$X(x) = \alpha_1 e^{\sqrt{-\lambda}x} + \alpha_2 e^{-\sqrt{-\lambda}x}$  
$$
\begin{array}{ll}
  X(0) = 0 = \alpha_1 + \alpha_2 &\\
  X(L) = 0 = \alpha_1 e^{\sqrt{-\lambda}L}+\alpha_2 e^{- \sqrt{-\lambda}L} & \\
  \Leftrightarrow & \alpha_2 = - \alpha_1 \\
  & \alpha_1 e^{\sqrt{-\lambda}L} - \alpha_1 e^{-\sqrt{-\lambda}L} = 0\\
  & \alpha_1(e^{\sqrt{-\lambda}L} -e^{-\sqrt{-\lambda}L})\\
  & \alpha_1 = 0 \quad e^{\sqrt{-\lambda}L} - e^{-\sqrt{-\lambda}L} = 0\\
  & \alpha_1 = 0 \implies \alpha_2 = 0\\
  & \implies X = 0 \implies u = 0
\end{array}
$$

___cas 3:___ $-\lambda < 0$  
$$X(x)=c_1 cos(\sqrt{\lambda} x ) + c_2 sin(\sqrt{\lambda}x)$$
$$\left.\begin{array}{lll}
X(0)&=&c_1 cos(0) + c_2 sin(0)\\
&=&c_1\\
&=&0
\end{array}\right\}\Rightarrow c_1=0$$
$$X(L) = c_1 cos (\sqrt{\lambda} L) + c_2 sin(\sqrt{\lambda} L) = 0$$
$$c_2 sin(\sqrt{\lambda}L)=0 \Rightarrow c_2=0 \text{ ou } sin(\sqrt{\lambda}L)=0$$

___si___ $c_2 = 0, c_2 = c_1 = 0 \Rightarrow X=0 \Rightarrow c_1 = 0$
$$sin(\sqrt{\lambda}L)=0$$
$$\begin{array}{llll}
\sqrt{\lambda}L&=&k\pi&\quad k \in \mathbb{Z}^*\\
\lambda&=&(\frac{k\pi}L)^2&\quad k \in \mathbb{Z}^*
\end{array}$$

Si l'on veut une solution non-triviale il faut que 
$$ \lambda=(\frac{k\pi}L)^2 \quad k \in \mathbb{Z}^*$$

### Principe de superposition

Pour des EDP linéaire homogènes, si u et v sont solution de cette EDP alors toute 
combinaison linéaire de ces solutions est encore solution de l'EDP.

On introduit $X_k$ qui va être la solution de
$$X''_k+ (\frac{2\pi}L)^2 X_k=0$$
$$X_k=a_k sin(\frac{k\pi}L x)$$

On introduit $T_k$ solution de l'équation:
$$\begin{array}{ll}
T'_k = &- \beta (\frac{k\pi}L)^2 T_k\\
T(t)=& b_k e^{- \beta (\frac{k\pi}L)^2 t}
\end{array}$$

$$u_k(x,t)=T_k(t)X_k(x)=a_kb_ke^{- \beta (\frac{k\pi}L)^2 t} sin(\frac{k\pi}L x)$$
$$u_k(x,t)=x_ke^{- \beta (\frac{k\pi}L)^2 t}sin(\frac{k\pi}L x)$$
$$u(x,t)=\sum^{+\infty}_{k=1} c_ke^{- \beta (\frac{k\pi}L)^2 t} sin(\frac{k\pi}L x)$$ 

$$\begin{array}{lll}
u(x,0)&=&f(x)\\
&=&\sum^{+\infty}_{k=1} c_k sin(\frac{k\pi}L x)
\end{array}$$

On calcule la série de fourrier de de "$f$" et par unicité de ce développement on 
identifie les coefficients "$c_k$" ou coefficients "$\alpha_k$" de $f$.  
Si $f(x) = \sum^{+\infty}_{k=1} \alpha_k sin(\frac{k\pi}L x)$ alors  
$\forall k \in \mathbb{N}^* \quad c_k =\alpha_k$
$$u(x,t)=\sum^{+\infty}_{k=1} \alpha_ke^{- \beta (\frac{k\pi}L)^2 t} sin(\frac{k\pi}L x)$$ 

**Calcul des $\alpha_k$:**  
Le père de Fourier en "$sinus$" sur $]0,L[$ de $f$ est:  
$\sum^{\infty}_{k=1} \alpha_k sin(\frac{k\pi}L$ avec  
$\alpha_k \frac2L \int^L_0 f(x)sin(\frac{k\pi}L x) dx$  
De même la série de Fourier en "$cosinus$" sur $[0,L]$ de $f$ est:
$f(x) = \frac{\gamma_0}2 + \sum^{+\infty}_{k=1} \gamma_k cos(\frac{k\pi}L x)$  
avec $\gamma_k = \frac2L \int^L_0 f(x) cos(\frac{k\pi}L x) dx$

**Exemple:**
On considère ($Y$) avec $L=\pi \quad \beta=7$ et  
$f(x)=3sin(2x) - 6sin(5x)$  
$$\begin{array}{lll}
u(x,t)&=&\sum^{+\infty}_{k=1} \alpha_ke^{-7 (\frac{k\pi}{\pi})^2 t} 
sin(\frac{k\pi}{\pi} x)\\
&=&\sum^{+\infty}_{k=1} \alpha_k e^{-7k^2t} sin (kx)\\\\
u(x,0)&=&\sum^{+\infty}_{k=1} \alpha_k sin(k,x)
\end{array}$$

on a $f(x)=3sin(2x)-6sin(5x) \to$ (c'est déjà le développement en série de Fourier.

on a donc:
$$\begin{array}{lll}
\alpha_2&=&3\\
\alpha_5&=&-6
\end{array}$$

$\forall k \in \mathbb{N}^* \ \{2,5\} \quad \alpha_k=0$  
$u(x,t)=3e^{-7\times 2^2 \times t} sin(2x) - 6e^{-7\times 2^2 \times t} sin(5x)$  
$u(x,t)=3e^{-28t} sin(2x) - 6e^{-175t} sin(5x)$

