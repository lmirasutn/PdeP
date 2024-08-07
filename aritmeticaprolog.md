# Aritmetica.

```pl
% siguiente(Anterior, Siguiente)
siguiente( N, N+1).
```
cuando consultamos:
*?- siguiente(41, Siguiente).
* Siguiente = 41 + 1.
 
¿Como resuelvo esto? 

```pl
siguiente(N, S):- S is N+1.
```

y finalmente, al consultar, dara 42.

ahora: 
*siguiente(Anterior, 42).
**ERROR** 

esto se debe a que la suma, y "is" no son totalmente inversibles. por lo cual no puede pasarse una variable.
para hacerlo inversible, entonces, hay que ligarlo a una variable de la siguientee manera:

```pl
siguiente(N, 42):-
numero(N),
42 is N + 1.
```
con esto, prolog va a ir consultando uno por uno hasta dar con el valor que cumpla, hasta llegar a 41 + 1 y llegar al 42.