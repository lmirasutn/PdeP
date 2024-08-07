# Intro Lógico.

* A diferencia de funcional, no solo hay un camino de ida, y tampoco existe el concepto de unicidad.
* Es extremadamente declarativo.
## Ejemplo
```pl

humano(socrates).
mortal(Alguien) :- humano(Alguien).
```
## 
```pl
humano(socrates).
```  
Es un hecho.
```pl 
mortal(Alguien):- humano(Alguien)
```
Es una regla que significa: "**Alguien** es mortal si dicho **Alguien** es humano".
## 
* **socrates**, con minuscula, es un individuo(atomo).
* **Alguien**, con mayuscula, es una variable.

```pl 
humano(platon).
humano(aristoteles).
humano(socrates).

mortal(Alguien:- humano(Alguien)).
mortal(elGalloDeAsclepio).

maestro(socrates,platon).
maestro(platon, aristoteles).

groso(Alguien):-
maestro(Alguien, Uno),
maestro(Alguien, Otro),
Uno \= Otro.
```
* ¿Cuando alguien es **humano**? Cuando es **platon**,**aristoteles** o **socrates**.
* el O logico seria declarar varias sentencias para el mismo predicado. Como en este caso con **humano**.
```pl
mortal(Alguien:- humano(Alguien)).
mortal(elGalloDeAsclepio).

```
En este caso, no solamente aclaro que **Alguien** es mortal si es **humano**, sino que aparte estoy declarando que **elGalloDeAsclepio** es mortal, sin necesidad de aportar un dato más.

```pl
groso(Alguien):-
maestro(Alguien, Uno),
maestro(Alguien, Otro),
Uno \= Otro.
```
Por otro lado, en este predicado, digo que **Alguien** es **groso** si tiene por lo menos, dos **alumnos**.
* Como dijimos antes, para el 'o' podemos crear varias sentencias. En cambio cuando necesitamos varias condiciones a la vez ('y'), tenemos que separarlas con coma, como en este caso.
* Entonces, **Alguien** es **groso** si es maestro de **Uno**, es maestro de **Otro** y **Uno** es distinto de **Otro**.

## Consulta individual
**Prolog trabaja con la idea de universo cerrado, es decir, todo lo que NO CONOCE, es falso. por ende si nosotros escribimos en la **CONSOLA** la sentencia:**
```pl
?-mortal(zeus).
```
esto arrojaría falso, puesto que en ningún momento, declaramos a zeus.

## Consulta existencial
**Si en cambio, le preguntaramos sobre una variable:**
```pl
?-mortal(Alguien).
```
**Esto arrojaría los elementos que cumplen con "mortal", en este caso: aristoteles,socrates,platon,elGalloDeAsclepio.**

## Otras consultas
* ?- maestro(platon, aristoteles).  --------> ¿Platon es maestro de Aristoteles?
* ?- maestro(platon, Discipulo). -----------> ¿Quién es discipulo de Platon?
* ?- maestro(Maestro, aristoteles) ---------> ¿Quién es maestro de Aristoteles?
* ?- maestro(Maestro, Discipulo) -----------> ¿Quién es maestro, y de quien? (devuelve todos los pares maestro-discipulo)
* ?- maestro(Maestro, _). ------------------> ¿Quienes son maestros?
* ?- maestro(platon, Alguien)---------------> ¿Platón es maestro de alguien?

# Inversibilidad.
Es la capacidad de ligar una variable.

Hay varias causas que rompen la inversibilidad de nuestro código. Una es la siguiente: 
```pl
odia(platon,diogenes).
odia(diogenes,_).
```
* ?- odia(diogenes, platon).
  
 *True*
* ?- odia(Alguien, platon).
  
 *diogenes*.

  sin embargo, si consulto:
* ?-odia(diogenes, Alguien). **aunque yo espero que me de una larga lista de lo que odia, porque diogenes odia a todo el mundo, la respuesta es:**

 True.

* Esto se debe a que por el principio de universo cerrado, si pongo odia (diogenes,_). estoy asumiendo que odia a cualquier cosa, absolutamente a todo, lo cual si bien puede decirme "Si, diogenes odia bañarse" no puede darme una lista con todas las cosas que odia, porque el universo es *CERRADO*.
* Un predicado es completamente inversible cuando es inversible para todos sus parametros.
