# Diseño
La utilización del display se realiza en el módulo `user_interface.cpp`, funciones `userInterfaceDisplayInit()` y `userInterfaceDisplayUpdate()`

El módulo Display implementa la interfaz paralelo de 8 o 4 bits. Para la interfaz de 8 bits utiliza las salidas digitales:

```cpp
    DigitalOut displayD0( D0 );
    DigitalOut displayD1( D1 );
    DigitalOut displayD2( D2 );
    DigitalOut displayD3( D3 );
    DigitalOut displayD4( D4 );
    DigitalOut displayD5( D5 );
    DigitalOut displayD6( D6 );
    DigitalOut displayD7( D7 );
    DigitalOut displayRs( D8 );
    DigitalOut displayEn( D9 );
```

Para la interfaz de 4 bits solo utiliza las salidas digitales:

```cpp
    DigitalOut displayD4( D4 );
    DigitalOut displayD5( D5 );
    DigitalOut displayD6( D6 );
    DigitalOut displayD7( D7 );
    DigitalOut displayRs( D8 );
    DigitalOut displayEn( D9 );
```

En la función `userInterfaceDisplayInit()` del archivo `user_interface.cpp` se establece la interfaz paralelo de 4 bits para la comunicación con el display de caracteres.

# Impresión por consola
Para la impresión por consola se implementan las funciones:

- `clearVirtualDisplay`: Borra la memoria del display virtual.
- `printVirtualDisplay`: Imprime la memoria del display virtual.

En las funciones `displayCharPositionWrite` y `displayStringWrite` se agrega la funcionalidad para imprimir simultáneamente en el display virtual.

# Árbol de funciones

<picture>
    <img src="img/dependency-tree.png">
</picture>

# Captura de mensaje

Se conecta el analizador lógico a los pines correspondientes a las salidas digitales de la interfaz de 4 bits (ver arriba).