## Historia
El termino backtrack fue acuñado por D. H. Lehmer en los 1950s. Trabajos tempranos que estudiaron el proceso fueron R. J Walker, quien dió una cuenta algoritmica del mismo, en 1960. Además S. Golomb y L.Baumert presentaron una descripción muy general del algoritmo y diversas aplicaciones.

## Metodo General

En muchas aplicaciones del metodo de backtrack, la solución deseada es expresable en una tupla de n elementos (x<sub>1</sub>, ...,x<sub>n</sub> ), donde los x<sub>i</sub> son elegidos de algún set infinito S<sub>i</sub>. Imaginando que algún x<sub>i</sub> es la solución deseada el enfoque de fuerza bruta sería comprobar la satisfacción del algoritmo para todos los elementos de S<sub>i</sub>.
El algoritmo **backtracking** tiene la virtud de resolver el problema en menos de n pruebas, esto lo hace probando si las soluciones, que tienen ciertas caracteristicas, tienen algúna chance de éxito. Esto lo hace discriminando las soluciones posibles de las imposibles a través de las **podas**.

## Bibliografía
[Computer Algorithms by Ellis Horowitz](https://kailash392.wordpress.com/wp-content/uploads/2019/02/fundamentalsof-computer-algorithms-by-ellis-horowitz.pdf) - Chapter 7
