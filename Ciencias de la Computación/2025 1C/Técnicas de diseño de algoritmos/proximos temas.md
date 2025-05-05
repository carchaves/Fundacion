
# Greedy - Cormen 16.1 16.2
# BFS - Cormen 22.2
# Dijkstra - 24


## Greedy
se aplican en tipos de problema parecidos a pd. subproblemas blah blah blah, la idea es ademas obtener soluciones locales.
La idea es construir una solución

Solucion -> localmente (lo mejor)
	    ->prueba una sola cosa
		->nunca revisa lo que propuso antes porque lo que prueba es la mas optima
		-> requiere una función de selección

Cuando algo funciona con greedy no hace falta hacer pd porque lo hace mas rápido
De un arbol de soluciones nos quedamos con una rama

-Problema de la mochila (mochila fraccionaria)
tenemos una mochila con 
una capacidad $C\in \mathbf{R}_+$     = 100
una cantidad $C\in \mathbf{N}$
Peso $P_i \in \mathbf{R}_+$ para cada objeto
Beneficio $b_i \in \mathbf{R}$ para cada objeto

	1  2  3  4  5
P      10 20 30 40 50
G      20 30 66 40 60
p/g   2   15  22 10 15

Basicamente en vez de ir probando hasta encontrar la solución más optima, calcula el resultado mas óptimo en cada caso. Funciona para ciertos problemas, para el problema de la mochila sin fraccionar no funciona.

```
Def DarCambio(Cambio):
	Suma = 0
	Monedas = []
	While suma < cambio:
		Moneda = masGrande(cambio-suma) #funcion de selección
		Monedas += [Moneda]
		Suma = Suma + Moneda
	Return Monedas
```



## BFS

Visita a lo ancho
Q=FIFO

BFS (G,s)
	For each vertex $u\in G.v-{s}$
		U.color = blanco
		U.d = $\infty$ 
		U.prev = NULL
	S. color = gris
	S.u = 0
	S.prev = NULL
	Q = $\emptyset$
	encolar(s)
	While Q!=$\emptyset$
		U= Desencolar(Q)
		For  each $v\in vecinos(u)$
			If v.color == blanco:
				v.color = Gris
				v.d = u.d +1
				v.prev = u
				encolar(v)
			u.color= negro

## Dijkstra

Dijkstra (G, w, s)
	