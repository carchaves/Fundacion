La búsqueda en un grafo significa seguir las aristas sistemáticamente para visitar los vértices.
## Representación de grafos (22.1)
Es posible elegir dos formas de representar un grafo $G = (V, E)$, como:
- Una colección de listas adyacentes
- Una matriz de adyacencia

### Listas adyacentes
![[Pasted image 20250419142023.png]]
Dado a que la representación es mucho más compacta, para grafos con conexiones esparcidas (|E| mucho menor a |V<sup>2</sup>|) es el método más común.

La representación por lista de adyacencia de un grafo $G = (V, E)$, consiste en un array de listas de longitud igual a la cantidad de vertices (|V|). De forma que para dicho array llamado por ejemplo *Adj*, para cada *u ∈ V*, la lista de adyacencia *Adj[u]* contiene todos los vertices *v* tal que hay una arista *(u, v) ∈ E*. Entonces *Adj[u]* cosiste de todas las vertices adyacentes a *u* en G. (Alternativamente, puede contener punteros a esos vertices)

Si G es un grafo dirigido la suma de las longitudes de todas las listas de adyacencia es |E|, dado que una arista es de la forma *(u, v)* es representada teniendo *v* en *Adj[u]*.

SI G es no dirigido, la suma de longitudes de todas las listas de adyacencia es 2|E|, dado que si *(u, v)* es una arista no dirigida, entonces *u* aparece en la lista de adyacencia de *v* y viceversa.

Para ambos casos de grafos dirigidos o no dirigidos la cantidad de memoria necesaria es de Θ(V + E).

Se puede adaptar grafos con peso, grafos que tienen aristas asociadas con un peso. Simplemente guardando el peso de la arista *(u, v)* con el vertice *v* en la lista de adyacencia de *u*.

Una potencial desventaja de la representación por listas de adyacencia, es que no provee una forma rápida de determinar si una determinada arista esta presente en el gráfico. Esta desventaja se remedia a través de una representación de una matriz de adyacencia.
### Matriz de adyacencia
![[Pasted image 20250419142215.png]]
Se puede preferir una matriz de adyacencia cuando el grafo es muy denso ((|E| se acerca a |V<sup>2</sup>|)) o cuando se necesita una forma de determinar si una arista conecta dos vertices rapidamente.

Para la representacion por matriz de adyacencia de un grafo $G = (V, E)$, asumimos que los vertices tienen un orden 1,2,..,|V| arbitrario. Luego la representación consiste de una matriz de |V| x |V|  de forma que para todo elemento en la matriz es 1 si existe una conexión entre los vertices a las que las coordenadas corresponden y 0 si no existe dicha conexión.
![[Pasted image 20250419171458.png]]
La matriz de adyacencia de un grafo requiere Θ(V<sup>2</sup>) de memoria, independiente del numero de aristas.
Es posible guardar el peso de una arista, guardandolo en la posición correspondiente a dicha arista.

## 
## Bibliografía
[Introduction to Algorithms (Third Edition) - Thomas H. Cormen](https://enos.itcollege.ee/~japoia/algorithms/GT/Introduction_to_algorithms-3rd%20Edition.pdf) - Chapter VI (~~22.1~~,22.3,22.4; 24.1, 24.2; 25.2)