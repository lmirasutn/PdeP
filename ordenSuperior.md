# Orden superior.

## Negacion.

un predicado de orden superior es aquel que recibe otro predicado.


```pl
terrestre(Animal):-
not(habitat(Animal, mar)).
```
* ?- terrestre(jirafa).

*True*.

* ?-terrestre(Animal).

*false*.

Esto es porque la variable animal esta llegando sin ligar.

* Not no es inversible.

* para que sea inversible, ligamos una variable antes:
```pl
terrestre(Animal):-
animal(Animal),
not(habitat(Animal, mar)).
```
## Cuantificador Universal

Ejemplo: imaginen si tuviesemos
```pl
habitat(foca, tundra)
habitat(foca, costa)
```
y quisieramos crear friolento, podríamos pensar en hacer esto:
```pl
friolento(Animal):-
habitat(Animal, Bioma), templado(Bioma). 
```
pero esto es incorrecto, ya que ahí estaríamos diciendo que la foca es friolenta, por vivir en la costa, cuando no lo es, ya que puede vivir en la tundra. para resolver esto hay que hacer uso del *forall*.

### Forall
forall(Universo, Condicion).

ambas consultas deben compartir una variable, por ejemplo
```pl
friolento(Animal):-
forall(habitat(Animal, Bioma), templado(Bioma)).
```
basicamente estoy generando el universo de biomas donde habita 
dicho animal, y luego me aseguro que todos esos sean templados.
ahora la consulta **?-friolento(foca)** devolvería **false**.

Forall no es inversible, si no le paso ligada la variable Animal, el universo que estoy generando no tiene la forma de una lista de animales.
entonces la forma correcta en definitiva es: 

```pl
friolento(Animal):-
animal(Animal),
forall(habitat(Animal, Bioma), templado(Bioma)).
```

### Not vs Forall

si yo digo **"para todos los x de un conjunto, se cumple P"** es lo mismo que decir **"No existe ningun x  de un conjunto que NO cumpla P"**
ej: es lo mismo decir "Todos los animales son friolentos" 
que decir: "No existe animal que no sea friolento".
entonces podría traducirse esto a:

"Todos los animales son friolentos":
```pl
forall(animal(X),friolento(X))
```

esto es igual a decir:
"No existe animal que no sea friolento":
```pl
not((animal(X), not(friolento(x)))).
```

también, en caso de querer expresar "No todos los animales son friolentos", es lo mismo que decir "Existen animales que no son friolentos".

"No todos los animales son friolentos": 
```pl
not(forall(animal(x), friolento(x))).
```

"Existen animales que no son friolentos" : 

```pl
animal(X), not(friolento(x)).
```

como se puede observar, es recomendable el correcto uso de ambas, ya que hay veces donde una de las dos opciones, es más sencilla de implementar que otras.
