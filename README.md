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
    <img src=img/dependecy-tree.png>
</picture>

# Captura de mensaje

Se conecta el analizador lógico a los pines correspondientes a las salidas digitales de la interfaz de 4 bits (ver arriba) para capturar la trama correspondiente a  a la impresión al display de la línea

```cpp
    displayStringWrite( "'C" );
```

En la siguiente tabla se muestran los códigos de los caracteres en el display.

<picture>
    <img src=img/table-6.1.png>
</picture>

A continuación se muestra la captura de la trama utilizando el software saleae. Notar que la transmisión de los nibbles se encuentra sincronizada con el bit de EN y que RS se establece en 1.

<picture>
    <img src=img/4-bits-parallel.png>
</picture>

Los bytes se envían por nibbles:

    D7 D6 D5 D4

#1:  0  0  1  0

#2:  0  1  1  1

#3:  0  1  0  0

#4:  0  0  1  1

Los nibbles #1 y #2 forman el valor decimal 39 (correspondiente al ', ver tabla).
Los nibbles #3 y #4 forman el valor decimal 67 (correspondiente a la letra C, ver tabla).