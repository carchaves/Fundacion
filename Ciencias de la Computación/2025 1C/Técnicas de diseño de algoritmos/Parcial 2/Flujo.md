Al igual que puedes modelar un mapa de carreteras como un grafo dirigido para encontrar la ruta más corta entre dos puntos, también puedes interpretar un grafo dirigido como una **"red de flujo"** y usarlo para responder preguntas sobre flujos de materiales. Imagina un material que circula por un sistema desde una **fuente** (donde se produce) hasta un **sumidero** (donde se consume). La fuente produce el material a una tasa constante, y el sumidero lo consume a la misma tasa. El **"flujo"** del material en cualquier punto del sistema se entiende intuitivamente como la velocidad a la que este se mueve.
El objetivo del **problema de flujo máximo** es calcular la tasa más alta posible de envío de material desde la **fuente** hasta el **sumidero**, sin violar ninguna de las **restricciones de capacidad**.
# Redes de Flujo
Una **_red de flujo_** G=(V,E) es un **grafo dirigido** en el que cada arista (u,v)∈E tiene una **_capacidad_** no negativa c(u,v)≥0. Además, se exige que si E contiene una arista (u,v), no exista una arista (v,u) en dirección inversa (más adelante veremos cómo evitar esta restricción). Si (u,v)∉E, por convención se define c(u,v)=0, y no se permiten **bucles** (aristas que unan un vértice consigo mismo).

Toda red de flujo incluye dos vértices distinguidos:
- Una **_fuente_** s.
- Un **_sumidero_** t.

Por simplicidad, se asume que cada vértice v∈V pertenece a algún camino desde s hasta t, es decir, existe una trayectoria s∼>v∼>​​t. Dado que todo vértice (excepto s) tiene al menos una arista entrante, se cumple ∣E∣≥∣V∣−1.
![[Pasted image 20250601200701.png]]

Un **_flujo_** en G es una función con valores reales f:V×V→R que satisface las siguientes dos propiedades:

**Restricción de capacidad:** Para todo par de vértices \(u,v \in V\), se debe cumplir:

 $0 \leq f(u,v) \leq c(u,v)$

El flujo entre dos vértices debe ser no negativo y no puede exceder la capacidad asignada a la arista.

**Conservación del flujo:** Para todo vértice \(u \in V - \{s,t\}\), se requiere:

$\sum_{v \in V} f(v,u) = \sum_{v \in V} f(u,v)$

Esto significa que el flujo total que entra a un vértice (que no sea la fuente ni el sumidero) debe ser igual al flujo total que sale de él. En términos coloquiales: "el flujo que entra es igual al flujo que sale".

Cuando no existe una arista $(u,v) \notin E$, el flujo de \(u\) a \(v\) es nulo, es decir, $f(u,v) = 0$.

Definimos el valor no negativo $f(u,v)$ como el flujo del vértice $u$ al vértice $v$. El _valor_ $|f|$ de un flujo $f$ se define como:

$|f| = \sum_{v \in V} f(s,v) - \sum_{v \in V} f(v,s)$

Es decir, el flujo total que sale de la fuente menos el flujo que entra a la fuente. (Aquí, la notación $|\cdot|$ denota el valor del flujo, no valor absoluto ni cardinalidad.) 

Normalmente, una red de flujo no tiene aristas entrantes a la fuente $s$, por lo que el flujo entrante $\sum_{v \in V} f(v,s)$ es $0$. Sin embargo, incluimos este término porque, cuando introduzcamos las **redes residuales** más adelante en este capítulo, el flujo hacia la fuente podría ser positivo.

En el **problema de flujo máximo**, la entrada es:
- Una red de flujo $G$
- Una fuente $s$
- Un sumidero $t$

Y el objetivo es encontrar un flujo $f$ con **valor máximo** $|f|$.
# Ford-Fulkerson método

## Método de Ford-Fulkerson
El método de Ford-Fulkerson incrementa **iterativamente** el valor del flujo. Comienza con $f(u,v) = 0$ para todo $u,v \in V$ (flujo inicial de valor $0$). En cada iteración:
1. **Red residual** $G_f$: Se busca un **camino de aumento** (*augmenting path*).
2. **Actualización del flujo**: Las aristas de este camino indican cómo modificar el flujo en $G$ para aumentar su valor.

**Observaciones clave**:
- El flujo en una arista específica puede **aumentar o disminuir** (aunque parezca contraintuitivo, esto permite optimizar el flujo global).
- El método termina cuando $G_f$ no tiene más caminos de aumento.
- El **teorema flujo máximo-corte mínimo** garantiza que el resultado es óptimo.

---

### Algoritmo: `Ford-Fulkerson-Method`$(G,s,t)$
```pseudocode
1  inicializar flujo f a 0
2  mientras exista un camino de aumento p en la red residual G_f:
3      aumentar el flujo f a lo largo de p
4  devolver f
```


### Redes residuales
Intuitivamente, dada una red de flujo $G$ y un flujo $f$, la red residual $G_f$ consta de aristas cuyas capacidades representan cómo puede cambiar el flujo en las aristas de $G$. Una arista de la red de flujo puede admitir una cantidad adicional de flujo igual a la capacidad de la arista menos el flujo en esa arista. Si ese valor es positivo, la arista se incluye en $G_f$ con una 'capacidad residual' de $c_f(u,v) = c(u,v) - f(u,v)$. Las únicas aristas de $G$ que pertenecen a $G_f$ son aquellas que pueden admitir más flujo. Aquellas aristas $(u,v)$ cuyo flujo iguala su capacidad tienen $c_f(u,v) = 0$ y no pertenecen a $G_f$.

Podría sorprender que la red residual $G_f$ también pueda contener aristas que no están en $G$. Cuando un algoritmo manipula el flujo (con el objetivo de aumentar el flujo total), podría necesitar disminuir el flujo en una arista específica para aumentarlo en otra. Para representar una posible disminución del flujo positivo $f(u,v)$ en una arista de $G$, la red residual $G_f$ incluye una arista $(v,u)$ con capacidad residual $c_f(v,u) = f(u,v)$. Esta arista permite admitir flujo en dirección opuesta a $(u,v)$, cancelando como máximo el flujo en $(u,v)$. Estas aristas inversas en $G_f$ permiten a un algoritmo "devolver" flujo previamente enviado, lo que equivale a _reducir_ el flujo en una arista, operación necesaria en muchos algoritmos.

Formalmente, dada una red de flujo $G=(V,E)$ con fuente $s$, sumidero $t$ y flujo $f$, para todo par de vértices $u,v \in V$, definimos la _capacidad residual_ $c_f(u,v)$ como:

$$
c_f(u,v) = 
\begin{cases} 
c(u,v) - f(u,v) & \text{si } (u,v) \in E, \\
f(v,u) & \text{si } (v,u) \in E, \\
0 & \text{en otro caso.}
\end{cases}
$$

En una red de flujo, \((u,v) \in E\) implica que \((v,u) \notin E\), por lo que exactamente un caso de la ecuación (24.2) aplica para cada par ordenado de vértices.

Como ejemplo de la ecuación (24.2), si \(c(u,v) = 16\) y \(f(u,v) = 11\), entonces \(f(u,v)\) puede aumentar hasta \(c_f(u,v) = 5\) unidades sin exceder la restricción de capacidad de la arista \((u,v)\). Alternativamente, hasta 11 unidades de flujo pueden regresar de \(v\) a \(u\), por lo que \(c_f(v,u) = 11\).

Dada una red de flujo \(G = (V,E)\) y un flujo \(f\), la _red residual_ de \(G\) inducida por \(f\) es \(G_f = (V,E_f)\), donde $E_f = \{ (u,v) \in V \times V : c_f(u,v) > 0\}$.
# Match máximo bipartito

