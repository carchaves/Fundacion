- 🖋 ¿Qué entienden por convención de llamada? ¿Cómo está definida en la ABI de System V para 64 y 32 bits?
- 🖋 ¿Quién toma la responsabilidad de asegurar que se cumple la convención de llamada en `C`? ¿Quién toma la responsabilidad de asegurar que se cumple la convención de llamada en `ASM`?
- 🖋 ¿Qué es un stack frame? ¿A qué se le suele decir **prólogo y epílogo**?
- 🖋 ¿Cuál es el mecanismo utilizado para almacenar **variables temporales**?
- 🖋 ¿A cuántos bytes es necesario alinear la pila si utilizamos funciones de `libc`? ¿Si la pila está alienada a 16 bytes al realizarse una llamada función, cuál va a ser su alineamiento al ejecutar la primera instrucción de la función llamada?
- 🖋 Una actualización de bibliotecas realiza los siguientes cambios a distintas funciones. ¿Cómo se ven impactados los programas ya compilados? _Sugerencia:_ Describan la convención de llamada de cada una (en su versión antes y después del cambio).
    - Una biblioteca de procesamiento cambia la estructura `pixel_t`:
        - Antes era `struct { uint8_t r, g, b, a; }`
        - Ahora es `struct { uint8_t a, r, g, b; }` ¿Cómo afecta esto a la función `void a_escala_de_grises(uint32_t ancho, uint32_t alto, pixel_t* data)`?
    - Se reordenan los parámetros (i.e. intercambian su posición) de la función `float sumar_floats(float* array, uint64_t tamano)`.
    - La función `uint16_t registrar_usuario(char* nombre, char* contraseña)` registra un usuario y devuelve su ID. Para soportar más usuarios se cambia el tipo de retorno por `uint64_t`.
    - La función `void cambiar_nombre(uint16_t user_id, char* nuevo_nombre)` también recibe la misma actualización. ¿Qué sucede ahora?
    - Se reordenan los parámetros de `int32_t multiplicar(float a, int32_t b)`.

Una vez analizados los casos específicos describan la situación general:

- 🖋 ¿Qué sucede si una función externa utilizada por nuestro programa _(Es decir, que vive en una **biblioteca compartida**)_ cambia su interfaz (parámetros o tipo devuelto) luego de una actualización?