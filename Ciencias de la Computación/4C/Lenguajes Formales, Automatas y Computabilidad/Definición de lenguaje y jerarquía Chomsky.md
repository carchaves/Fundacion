## Jerarquía Chomsky

![[Pasted image 20250430002529.png#center|300]]


## Alfabetos y Lenguaje

**Alfabeto**: conjunto finito, no vacío, de símbolos.
Consideramos la concatenación de símbolos.

**Palabra**: Una palabra sobre el alfabeto Σ es la concatenación de los elementos de una secuencia finita de símbolos. Tambien la llamamos cadena o string.

**λ**: Palabra nula, no tiene símbolos.

Ejemplos: Estas son algunas palabras sobre Σ = {a, j, r}, λ, a, j, r, aa, aj, ar, ja, jj, aaj, rja, raja, jarra, etc.

## Conjunto de todas las palabras sobre un alfabeto
Dado alfabeto Σ, escribimos: 
$\Sigma^0$ = {λ}
$\Sigma^1$= $\Sigma$ 
$\Sigma^2$= $\Sigma\Sigma$ = {ab : a ∈ $\Sigma$, b ∈ $\Sigma$}
$\Sigma^3$= $\Sigma\Sigma\Sigma$ = {abc : a ∈ $\Sigma$, b ∈ $\Sigma$, c ∈ $\Sigma$}
### Clausura Kleene del alfabeto $\Sigma$
$$\displaystyle \Sigma^* = \bigcup_{i \geq 0} \Sigma^i$$


