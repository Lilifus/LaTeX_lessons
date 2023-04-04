
---
title: Technique de modélisation
author: Zakaria EJJED
documentclass: article
header-includes:
    - \usepackage{algorithm}
    - \usepackage{algpseudocode}
    - \usepackage{tikz}
    - \usepackage{cancel}
    - \usepackage{fancyhdr}
toc: true
geometry:
    - margin=2cm
...

\pagestyle{fancy}
\everymath{\displaystyle}
\newcommand{\deer}{\includegraphics[height=1.3cm]{/home/zakaria/Pictures/deer_sig.png}}
\renewcommand*{\frac}{\dfrac}
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

Considérons le problème suivant:
$$\begin{cases}
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
$$ \begin{cases}
u_t + au_x = 0 \quad a = c^k\\
u(x,0) = \Phi(x)
\end{cases}$$

$$\begin{cases}
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
$$\begin{array}{ll}
  X(0) = 0 = \alpha_1 + \alpha_2 &\\
  X(L) = 0 = \alpha_1 e^{\sqrt{-\lambda}L}+\alpha_2 e^{- \sqrt{-\lambda}L} & \\
  \Leftrightarrow & \alpha_2 = - \alpha_1 \\
  & \alpha_1 e^{\sqrt{-\lambda}L} - \alpha_1 e^{-\sqrt{-\lambda}L} = 0\\
  & \alpha_1(e^{\sqrt{-\lambda}L} -e^{-\sqrt{-\lambda}L})\\
  & \alpha_1 = 0 \quad e^{\sqrt{-\lambda}L} - e^{-\sqrt{-\lambda}L} = 0\\
  & \alpha_1 = 0 \implies \alpha_2 = 0\\
  & \implies X = 0 \implies u = 0
\end{array} $$

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

# Monday 27th March 2023 Exercises
## TD1 suite
### Exercice 2

Posons $u(x,t)=X(x)T(t)$  
$u_{tt}=X(x)T''(t)=c_0^2u_{xx}=c^2_0 X''(x)T(t)$
donc $c_0^2 \frac{X''(x)}{X(x)}= - \lambda \quad \lambda \in \mathbb{R}$  
Considérons
$$\left\{\begin{array}{ lll }
c^2_0 X''(x) &+ \lambda X (x) &= 0\\
X(0)&=X(L)&=0
\end{array}\right.$$
L'équation caractéristique associée est $c_0^2 r^2 + \lambda = 0$ (e)  
On cherche les racines de (e).  

* **cas 1:** "solution réelles" $\lambda < 0$  
$c_0^2 r^2 = -\lambda \Leftrightarrow r^2 = \frac{-\lambda}{c^2_0}$  
On a comme solutions $X(x)=\alpha_0 e^{r_1 x}+\alpha_1 e^{r_2 x}$
$$\left\{ \begin{array}{ lll }
X(0)=0 \Rightarrow \alpha_0 + \alpha_1 = 0 \text{ donc } \alpha_1=-\alpha_0\\
X(L)=0 \Rightarrow \alpha_0(e^{r_1L}-e^{r_2L}= 0 \text{ donc } \alpha_0=0 ou e^{r_1L}-
e^{r_2L}=0
\end{array}\right.$$  
On retombe sur la solution triviale  
$$u(x,t)=X(x)T(t)=0 \text{ car } X(x) = 0)$$

* **cas 2:* "solution double" $\lambda = 0$  
$c_0^2 r^2 = 0 \qquad r^2=0 donc r=0$  
$c_0^2 \frac{X''(x)}{X(x)}=0$ donc $c^2_0=0$ ou $X''(x)=0$
- $X''(x)=0 \Rightarrow X'(x)=c_0 \Rightarrow X(x)=c_0x+c_1$
$$\left\{ \begin{array}{ lll }
X(0)=0 \Rightarrow X'(x) = c_0 \Rightarrow X(x) = c_0x+c_1\\
X(L)=0 \Rightarrow c_0L=0 \Rightarrow c_0=0
\end{array}\right.$$  
- $c_0=0 \Rightarrow$ même chose. On retombe sur la solution triviale.

* **cas 3:** "solution imaginaires" $\lambda > 0$
$c_0^2 r^2 + \lambda = 0 \Leftrightarrow c_0^2r^2=-\lambda$  
donc $r=\pm i \sqrt{\frac{\lambda}{c_0^2}} =\pm i\omega$  
$X_n)=\alpha_0 cos(\omega x) + \alpha_1 sin(\omega x)$  
$$\left\{ \begin{array}{ lll }
X(0)=0 \Rightarrow X'(x) = c_0 &\Rightarrow \alpha_0&=0\\
X(L)=0 \Rightarrow c_0L=0 &\Rightarrow \alpha_1 sin(\omega L)&=\alpha_1 
sin(\frac{sqrt{\lambda}}{c_0}L=0\\
&\Rightarrow \frac{sqrt{\lambda}L}{c_0}&=k\pi\\
&\Rightarrow \lambda &=(\frac{k\pi c_0}{L})^2
\end{array}\right.$$  
On introduit pour $k \in \mathbb{N}\*$  
$X_k(x) solution de c_0^2 X_k''(x)+\lambda_k X(k)=0$ avec 
$\lambda_k=(\frac{k\pi c_0}{L})^2$  
$X_k(x)=a_k sin(x\frac{\sqrt{\lambda k}}{c_0}) \qquad \sqrt{\lambda k}=k c_0$  
$T_k(t) solution de T''_k(t)+\lambda_k T_k(t)=0$  
l'équation caractéristique associée est $r^2+\lambda_k=0$ comme $\lambda_k=(\frac{k\pi 
c_0}{L})^2>0$  
les racones sont $r=\pm i\sqrt{\lambda_k}$  
$$T_k(t)=b_k cos(\sqrt{\lambda_k} t) + c_k sin(\sqrt{\lambda_k t})$$
Par le théorème de superposition:  
$$\begin{array}{ ll }
u(x,t)&=\sum^\infty_{k=1} X_k(x)T_k(t)\\
&=\sum^\infty_{k=1} a_k sin (x\frac{\sqrt{\lambda_k}}{c_0})[b_k cos(\sqrt{\lambda_k t}) +
c_k sin(\sqrt{\lambda_k t})]
\end{array}$$  
$$\begin{array}{ ll }
u(x,0)&=\sum^\infty_{k=1} a_k b_k sin(\frac{sqrt{\lambda_k}}{c_0} x)\\
&= sin(3x)-4sin(10x)
\end{array}$$  
$u(x,t)=\sum^\infty_{k=1} a_k \frac{sqrt{\lambda_k}}{c_0}$  
$cos(\frac{x\sqrt{\lambda k}}{c_0}) [ b_k cos\sqrt{\lambda_k} t) + c_k sin(\sqrt{\lambda_k t})]$
$$\begin{array}{ ll }
u(x,0)&=\sum^\infty_{k=1} a_k b_k cos(\frac{x\sqrt{k}}{c_0})\\
&=\sum^\infty_{k=1} a_k b_k cos(kx)\\
&= 2sin(4x)+sin(6x)
\end{array}$$  

Par identification:
$-k=3$, 
$$a_3 b_3=1$$
$$a_10 b_10=-4$$
$$\forall k \notin {3,10}, a_k b_k = 0$$

# Course
## 4 - Solution numérique
Considérons le problème suivant:
$$(PC)\left\{\begin{array}{ll}
u'(t)=&f(u(v)) \quad \forall t \in ]0,+\infty[\\
u(0)=&u_0
\end{array}\right.$$

Supposons que u soit de class $C^2$, alors son développement de taylor à l'ordre 2 s'écrit:
$$u(t+\Delta t) = u(t)+u'(t)\Delta t + u''(t)\frac{\Delta t^2}{2!}+o(\Delta t^2)$$

$$u'(t)=\frac{(t+\Delta t)-u(t)}{\Delta t} + O(\Delta t)$$

Nous allons utiliser cette relation pour construire une solution numérique approchée.  
Pour cela on va discrétiser l'intervalle sur lequel on cherche la solution ($[0,T_0]$) en 
($n+1$) points $t_i,i=0,\dots,n$ avec $t_0=0$ et $t_n=T_0$.  
$\Delta t_i = t_{i+1}-t_i$ est le pas de discrétisation.
On le considère constant ici $\Delta t = \frac{T-0}{n}=\frac{T}{n}$  
On parle alors de discrétisation régulière.  
En appliquant l'approximation de la dérivée première entre $t_i$ et $t_{i+1}$ on peut 
écrire:  
$$u'(_i) \simeq \frac{u(t_{i+1} - u(t_i)}{\Delta t}$$
Si on note $u_i=u(t_i) \quad \forall i \in [\![0,n]\!]$

Le problème numérique approchée obtenu est:
$$\left\{\begin{array}{l}
\frac{u_{i+1}-u_i}{\Delta t} = f(u_i) \quad \forall  i \in [\![0,n-1]\!]\\
u_0
\end{array}\right.$$
$$u_{i+1}=u_i+\Delta t f(u_i)$$
$$\to \text{ schéma d'Euler explicite (E-E)}$$

**Exp:**  
$$f(u)=u$$
$$u(0)=1$$
$$PC\left\{\begin{array}{ll}
u'=&u\\
u(0)=&1
\end{array}\right.\to \text{solution analytique: }t\to e^t$$

**Schéma d'E-E**:
$$PC\left\{\begin{array}{ll}
u_{i+1}=&u_i+\Delta t u_i = (1+\Delta t)u_i\\
u_0=&1
\end{array}\right.$$
$$u_{i+1}=(1+\Delta t)^{i+1}u_0=(1+\Delta t)^{i+1}$$

# Exercise
## TD1
### Exercice 7 - Mini-Projet

1.  
$$\left\{\begin{array}{ll}
u'(t)=&-u(t)\\
u(0)=&1
\end{array}\right. u(t)=e^{-t}$$

2.  
En partant du schéma E-E
$$\begin{array}{lll}
u_{n+1}&=&u_n + \Delta t f(u_n)\\
u_{n+1}&=&u_n - \Delta t u_n\\
&=&(1-\Delta t)u_n\\
&=&(1-\Delta t) \times (1-\Delta t)u_{n-1}\\
&&\dots\\
&=&(1-\Delta t)^{n+1} u_0\\
\Rightarrow u_n &=& (1-\Delta t)^n
\end{array}$$

3.  
$u_n=(1-\Delta t)^n$

# Monday April 3rd 2023 Cours

## Méthode de différences finies

On va s'intéresser dans ce qui suit à l'équation de la chaleur
$$\mathcal{EC}\left\{\begin{array}{lll}
U_t(x,t)&=&U_{xx}(x,t) \quad \forall x \in ]0,1[ / \quad \forall t>0\\
U(0,t)&=&U(1,t)=0\\
U(x,0)&=&f(x)
\end{array}\right.$$

### 1 - Approximations des dérivées successives
Considérons une subdivision régulière de [a,b].

\begin{tikzpicture}
\draw (-4,0) -- (2,0);
\foreach \x/\y in {-4/a,-3/\cdots,-2/x_{i-1},-1/x_i,0/x_{i+1},1/\cdots,2/b} {
\draw (\x,0.1cm) -- (\x,-0.1cm) node[below] {$\y\phantom{-}\strut$};
}
\end{tikzpicture}

$x_{i+1} - x_i = h \forall i$  
L'idée est d'utiliser la formule de Taylor pour des fonctions réguilères

### différences divisées progressives d'ordre 1
$$u'(x_i)=\frac{u(x_i+h)-u(x_i)}{h} + O(h) \to u'(x_i)\simeq \frac{u(x_{i+1})-u(x_i)}{h}$$

### différences divisées régressives d'ordre 1
$$u'(x_i)=\frac{u(x_i)-u(x_i-h)}{h} + O(h) \to u'(x_i)
\simeq \frac{u(x_{i})-u(x_{i-1})}{h}$$

### différences divisées progressives d'ordre 2
$$u'(x_i)=\frac{-u(x_i+2h)+4u(x_i+h)-3u(x_i)}{2h} + O(h^2) \to u'(x_i)
\simeq \frac{-u(x_{i+2})+4u(x_{i+1})-3u(x_i)}{2h}$$

$$\begin{array}{llll}
(1)&u(x_i+h)&=&u(x_i)+hu'(x_i)+\frac{h^2}{2!}u''(x_i)+\frac{h^3}{3!}u'''(x_i)+O(h^3)\\
(2)&u(x_i+2h)&=&u(x_i)+2hu'(x_i)+\frac{(4h)^2}{2!}u''(x_i)+
\frac{(4h)^3}{3!}u'''(x_i)+O(h^3)\\
4\times(1)+(2)&4u(x_i-h)-u(x_i+2h)&=&3u(x_i)+2hu'(x_i)+O(h^3)\\
&u'(x_i)&=&\frac{-u(x_i)+2h)+4u(x_i+h)-3u(x_i)}{2h}-u'(x_i)| < Mh^2
\end{array}$$

### différences divisées regressives d'ordre 2
$$u'(x_i)=\frac{3u(x_i)-4u(x_i-h)+u(x_i-2h)}{2h} + O(h^2) \to u'(x_i)
\simeq \frac{3u(x_{i})-4u(x_{i-1})+u(x_{i-2})}{2h}$$

$$\begin{array}{llll}
(1)&u(x_i-h)&=&u(x_i)-hu'(x_i)+\frac{h^2}{2!}u''(x_i)-\frac{h^3}{3!}u'''(x_i)+O(h^3)\\
(2)&u(x_i-2h)&=&u(x_i)-2hu'(x_i)+\frac{(2h)^2}{2!}u''(x_i)-
\frac{(2h)^3}{3!}u'''(x_i)+O(h^3)\\
4\times(1)-(2)&4u(x_i-h)-u(x_i-2h)&=&3u(x_i)-2hu'(x_i)+\frac{4h^3}{3!}u'''(x_i)+O(h^3)
\end{array}$$

### différences divisées centrées d'ordre 2
$$u'(x_i)=\frac{u(x_i+h)-u(x_i-h)}{2h} + O(h^2) \to u'(x_i)
\simeq \frac{u(x_{i+1})-u(x_{i-1})}{2h}$$


$$\begin{array}{lll}
u(x_i+h)&=&u(x_i) + hu'(x_i) + O(h^2)\\
&=&u(x_i) + hu'(x_i)+\epsilon(h)
\end{array}$$  
$$O(h) \to \exists M>0 \quad tq \quad |\epsilon(h)| < Mh$$
$$\begin{array}{lll}
u(x_i+h)-u(x_i)&=&hu'(x_i)+O(h^2)\\
\frac{u(x_i+h)-u(x_i)}{h}&=&u'(x_i)+O(\frac{h^2}{h})\\
\frac{u(x_i+h)-u(x_i)}{h} - u'(x_i)&=&O(\frac{h^2}{h})
\end{array}$$

$$\begin{array}{llll}
(1)&u(x_i+h)&=&u(x_i)+hu'(x_i)+\frac{h^2}{2!} u''(x_i) + \frac{h^3}{3!} u'''(x_i)+O(h^3)\\
(2)&u(x_i-h)&=&u(x_i)-hu'(x_i)+\frac{h^2}{2!} u''(x_i) - \frac{h^3}{3!} u'''(x_i)+O(h^3)\\
(1)-(2)&u(x_i+h)-u(x_i-h)&=&2hu''(x_i)+\frac{2h^3}{3!}u''(x_i)+O(h^3)\\
(1)+(2)&u(x_i+h)+u(x_i-h)&=&2u(x_i)+h^2u''(x_i)+\frac{2h^4}{4!}u^{(4)}(x_i)+O(h^4)
\end{array}$$
$$\frac{u(x_i+h)+u(x_i-h)-2u(x_i)}{h^2}-u''(x_i)=O(h^2)$$

Pour les dérivées d'ordre supérieurs on procède de la façon suivante:  
$$\begin{array}{lll}
u''(x_i)&=&\frac{u'(x_i+\frac{h}2)-u'\left(x_i-\frac{h}2\right)}{h}+O(h^2)\\
&=&\frac{\frac{u(x_i+h)-u(x_i)}{h}-\frac{u(x_i)-u(x_i-h)}{h}+O(h^2)}{h}+O(h^2)\\
&=&\frac{u(x_i+h)-2u(x_i)+u(x_i-h}{h^2}+O(h)+\cancel{O(h^2)}
\end{array}$$

### Schéma explicite pour l'équation de la chaleur

$$\begin{array}{llll}
u_t(x,t)&=&\frac{u(x,t+\Delta t)-u(x,t)}{\Delta t} &+ O(\Delta t)\\
u_{xx}(x,t)&=&\frac{u(x+\Delta x,t)-2u(x,t)+u(x-\Delta x, t)}{\Delta x^2} &+ O(\Delta x^2)
\end{array}$$
où $\Delta t$ est la pas de discrétisation en temps et $\Delta x$ celui en espace.
$$\frac{u(x,t+\Delta t) - u(x,t)}{\Delta t} + O(\Delta t) =
\frac{u(x+\Delta x,t) - 2u(x,t)+u(x-\Delta x, t)}{\Delta x^2} + O(\Delta x^2)$$
$$\frac{(x,t+\Delta t) - u -x,t)}{\Delta t} \simeq \frac{u(x+\Delta x,t) - 2 u(x,t) +
u(x-\Delta x,t)}{\Delta x^2}$$

Si on note:
$u_j^m \simeq u(j\Delta x, m \Delta t)$ pour tout $j\in [\![1,m-1]\!]$ et pour tout $m\in
\mathbb{N}^*$  
$$\frac{u^{m+1}_j-u^m_j}{\Delta t} = \frac{u^m_{j+1}-2u^m_j+u^m_{j-1}}{\Delta x^2}$$  
$$u_j^{m+1}=u^m_j+\frac{\Delta t}{\Delta x^2}[u^m_{j+1} - 2u^m_j+u^m_{j-1}]$$
$$u^m+1_j=u^m_j+\frac{\Delta t}{\Delta x^2}[u^m_{j+1}-2u^m_j+u^m_{j-1}]$$
$$u^m+1_j=ru^m_{j+1}+(1-2r)u^m_j+ru^m{j-1}$$

Ce que je veux faire $u^{m+1} = Au^m$

$$u^{m+1}=\begin{pmatrix}
u_0^{m+1}\\
\vdots\\
u_1^{m+1}\\
\vdots\\
u_N^{m+1}\\
\end{pmatrix}=
\begin{pmatrix}
0\\
u_1^{m+1}\\
\vdots\\
u_j^{m+1}\\
\vdots\\
u^{m+1}_{N-1}\\
0\\
\end{pmatrix}\quad
u^m=\begin{pmatrix}
u_0^{m}\\
\vdots\\
u_1^{m}\\
\vdots\\
u_N^{m}\\
\end{pmatrix}=
\begin{pmatrix}
0\\
u_1^{m}\\
\vdots\\
u_j^{m}\\
\vdots\\
u^{m}_{N-1}\\
0\\
\end{pmatrix}$$

$$F=(f(x_j))=\begin{pmatrix}
f(0)\\
f(x_1)\\
\vdots\\
f(x_j)\\
\vdots\\
f(x_{N-1})\\
f(1)\\
\end{pmatrix}$$

$$\begin{pmatrix}
u^{m-1}_1\\
\vdots\\
u^{m+1}_j\\
\vdots\\
u^{m+1}_{N-1}
\end{pmatrix}=
\begin{pmatrix}
1&-&2r & r &0&\cdots&\cdots&0\\
r & 1&-&2r & r&\ddots&&\vdots\\
0&\ddots && \ddots && \ddots&\ddots&\vdots\\
\vdots&\ddots& r & 1&-&2r & r&0\\
\vdots&&\ddots& r & 1&-&2r & r\\
0&\cdots&\cdots&0& r & 1&-&2r
\end{pmatrix}
\begin{pmatrix}
u_1^m\\
\vdots\\
u^m_{j-1}\\
u_j^m\\
u_{j+1}^m\\
\vdots\\
u^m_{N-1}
\end{pmatrix}$$

Pour les schémas implicites il existe souvent une condition de stabilité qui lie les 
différents pas de dicrétisation simultanément "petits" ce qui induit une puissance de calcul
plus importante. On aimerait se passer de cette contrainte. Les schémas implicites peuvent
répondre à cette contrainte.  
En utilisant la même approche que pour le schéma explicite on obtient:
$$ u(x,t + \Delta t) \simeq \frac{u(x, t + \Delta t) - u(x,t)}{\Delta t}$$
$$ u_{xx}(x,t + \Delta t) \simeq \frac{u(x+\Delta x, t + \Delta t) - 2u(x, t) + \Delta t 
+ u(x - \Delta x ,t + \Delta t)}{\Delta x^2}$$

* On obtient le schéma suivant:
$\frac{u_j^{m+1}-u_j^m}{\Delta t}= \frac{u^{m+1}_{j+1}-2u^{m+1}_j+u^{m+1}_{j-1}}
{\Delta x^2}$
$u_j^{m+1}(1+\frac{2\Delta t}{\Delta x^2})-\frac{\Delta t}{\Delta x^2} u^{m+1}_{j+1} -
\frac{\Delta t}{\Delta x^2} u^{m+1}_{j+1}=u^m_j$
$-ru^{m+1}_{j-1}+(1+2r)u_j^{m+1} - r u_{j-1}^{m+1}=u_j^r$

$$\begin{pmatrix}
1&+&2r & -r &0&\cdots&\cdots&0\\
-r & 1&+&2r & -r&\ddots&&\vdots\\
0&\ddots && \ddots && \ddots&\ddots&\vdots\\
\vdots&\ddots& -r & 1&+&2r & -r&0\\
\vdots&&\ddots& -r & 1&+&2r & -r\\
0&\cdots&\cdots&0& -r & 1&+&2r
\end{pmatrix}$$

## Analyse de la stabilité de Von Neuman
On introduit la notation suivant:  
$u_j^m = (a_k)^m e^{ik\pi x_j}$ avec $i^2=-1$.  
$u^{m+m_0}_{j+j_0}=(a_k)^{m+m_0} e^{ik\pi x_{j+j_0}}$

On introduit cette notation dans le schéma numérique dont on veut étudier la stabilité. 
Par exemple, pour le schéma explicite de l'équation de la chaleur on obtient.

$$\frac{u^{m+1}_j - u_j^m}{\Delta t}=\frac{u_{j+1}^m - 2u^m_j + u^m_{j-1}}{\Delta x^2}$$
$$\frac{(a_k)^{m+1}e^{ik\pi x_{j}}-(a_k)^me^{ik\pi x_{j}}}{\Delta t} = \frac{(a_k)^m e^{ik\pi x_{j+1}} - 2(a_k)^m
e^{ik\pi x_{j}}+(a_k)^me^{ik\pi x_{j-1}}}{\Delta x^2}$$

$$e^{ik\pi x_{j+1}}=e^{ik\pi (x_{j}+\Delta x)}=\text{??? (voir photo 03/04/23 15:12)}$$

$$\begin{array}{rll}
\frac{a_k-1}{\Delta t} &=& \frac{e^{ik\pi \Delta x}-2+e^{-ik\pi \Delta x}}{\Delta x^2}\\
&=& \frac{e^{\frac{ik\pi \Delta x}{2}}-e^{\frac{-ik\pi \Delta x}{2}}}{\Delta x^2}\\
&=& \frac{2i sin(\frac{k\pi \Delta x}{2})}{\Delta x^2}\\
a_k &=& 1 - 4 \frac{\Delta t}{\Delta x^2} sin^2(\frac{k\pi \Delta x}2)
\end{array}$$
Pour que le schéma soit stable, il faut que $|a_k| \leq 1$

$$\begin{array}{llrll}
&&|1 - 4 \frac{\Delta t}{\Delta x^2} sin^2(\frac{k\pi \Delta x}2)| &\leq& 1\\
 -1 &\leq& 1 - 4 \frac{\Delta t}{\Delta x^2} sin^2(\frac{k\pi \Delta x}2) &\leq& 1\\
-2&\leq& - 4 \frac{\Delta t}{\Delta x^2} sin^2(\frac{k\pi \Delta x}2) &\leq& 0\\
&& 4 \frac{\Delta t}{\Delta x^2} sin^2(\frac{k\pi \Delta x}2) &\leq& 2\\
&&\frac{\Delta t}{\Delta x^2} sin^2(\frac{k\pi \Delta x}2) &\leq& \frac{1}2\\
&&\frac{\Delta t}{\Delta x^2} &\leq& \frac12
\end{array}$$

