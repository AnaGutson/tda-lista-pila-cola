
─────────────────────────────────────────────────────────────────────────Convenciones─────────────────────────────────────────────────────────────────────────

● Las convenciones que se utilizan en el trabajo son con base en qué me parece más legible, siempre respetando el uso del ​snake_case​.

● Con respecto al código, se separa en tres partes:

...{
	declaraciones​;

	código​;

	return​;
}

En caso de no haber una de las partes, se hace lo siguiente:

● Si no hay declaraciones:
...{
	código​;

	return​;
}

● Si no hay return:
...{
	declaraciones​;

	código​;
}

● Si solo hay código:
...{

	código​;
}

● Si solo hay return:
...{

	return;
}

La razón por la que se deja un enter arriba del código pero no debajo es debido a que cuando se minimiza el bloque, no resulta agradable que quede una línea en blanco, ya que si hubiera un enter abajo quedaría como:
...{​░░

}

Y es preferible que quede sin el espacio:
...{​░░
}

- esto es más entendible con colores y dibujos pero no se puede, para más información consultar por privado-

Añado: Dentro de bloques de código se suele seguir la misma regla, es decir, dentro de funciones de control por ejemplo.

● Y dentro de funciones, si la función recibe muchos parámetros, como se trata de respetar el uso de 80 caracteres máximo por línea, se procede de la siguiente manera:

void* funcion(int ..., char ..., double ..., size_t ..., const int ..., char* ...,
	void (*funcion)(int, int)){

	declaraciones​;

	código​;

	return​;
}

Es decir, se deja una línea de separación para que se entienda dónde comienzan las declaraciones.

● Se prefiere escribir sin corchetes si es posible, como

for(...)
    ...;

o

if(...)
    ...;

Tratando de respetar siempre que sea posible una acción por línea.

● Para escribir funciones de control, se escribe la función y al lado los paréntesis, sin dejar espacio, por ejemplo:

while(...){
    ...;
}

● Para escribir un booleano (ya sea función o variable) dentro de una condición, se prefiere sin el "==", sino que con el mero nombre alcanza, y en caso de querer negarlo, un "!" antes del mismo. Por ejemplo:

while(es_rojo(tateti_suerte_pa_mi) || !termino){
    ...;
}

● Para escribir varias condiciones, se trata de usar la siguiente convención:
En caso de no haber una de las partes, se hace lo siguiente:

● En caso de haber varias operaciones de comparación:
if((condicion_1 > 0) && (condicion_2 > 0))
-> se respetan las buenas prácticas de cada comparación -acción- en un paréntesis, además no se dejan espacios entre el primer y último paréntesis. 

● En caso de haber funciones booleanas y operaciones de comparación:
if(es_valido(condicion_1) && (condicion_2 > 0))
-> las funciones no se separan entre paréntesis, se respetan las buenas prácticas de cada comparación -acción- en un paréntesis, además no se dejan espacios entre el primer y último paréntesis. 

● En caso de haber funciones booleanas solamente:
if(es_valido(condicion_1) && es_valido(condicion_1))
-> las funciones no se separan entre paréntesis, además no se dejan espacios entre el primer y último paréntesis. 

● En caso de que haya punteros con campos:
if(((condicion_1->tata) > 0) && ...)
-> toda la variable se coloca entre paréntesis, para evitar confusiones.

● Para declarar punteros, se prefiere hacerlo así
nodo_t* nodo;

En vez de:
nodo_t *nodo;

● Se prefiere escribir de precondiciones razones por las que no se podría cumplir el cometido de una función. Por ejemplo, si la intención es hacer algo con una lista, y no hay lista, no se podrá hacer.
Entonces, el programa no se rompe si se manda NULL como lista, pero en las pre condiciones se prefiere aclarar que no hay que mandar lista == NULL.

● Se prefiere hacer un return en medio de una función solo si es debido a que no se cumplieron las pre condiciones. También, si surge un problema al pedir memoria dinámica. Sino, SOLO se realiza al final de todo, nunca se hacen varios return: gusto personal, y no cuesta nada hacerlo como gusta.

● Para el TDA se trató de reutilizar el código de otras funciones anteriores, menos las del iterador: era más gustoso recorrer las funciones a mano, tanto con el iterador interno como el externo.

● Los colores para mostrar las pruebas fueron elegidos con intención, y también con intención se decidió solo colorear el texto, no resaltarlo. Esto último no agrada visualmente.

● Se exhorta usar el programa en pantalla completa, sino no se podrá asegurar la correcta visualización del mismo.

● En "pruebas.c" y "lista.c" se prefiere agrupar las funciones por lo que devuelven, y de qué tratan.

● Las constantes se tienen alineadas en grupos, así resulta más fácil organizarse. Es decir, los valores de cada una se tienen a la misma altura solo si son del mismo grupo. Por ejemplo:

#define LEER 						"r"
#define ESCRIBIR 					"w"

#define TODO_OK		0
#define ERROR		-1

─────────────────────────────────────────────────────────────────────────Ejecución─────────────────────────────────────────────────────────────────────────

Objetivo:
	
	El objetivo de esta entrega es realizar un TDA de lista, pila, cola e iterador (para más información leer "¿Qué es un TDA?" y sus respectivos "¿Qué es una lista?", "¿Qué es una pila?", "¿Qué es una cola?", "¿Qué es un iterador?") y realizar las pruebas necesarias para saber que funcionan en todos los casos.

Descripción breve del funcionamiento de mi programa y cómo compilarlo:

    Para ver el funcionamiento de estas pruebas sobre el TDA hay que compilar todos los .c de la carpeta entregada (menos el lista_minipruebas.c) y ejecutar lo compilado.

    La línea de compilación recomendada es: gcc *.c -o lista_se -g -std=c99 -Wall -Wconversion -Wtype-limits -pedantic -Werror -O0
    Si dentro de la carpeta hay algún .c con un main (además de pruebas.c) se debe hacer: gcc pruebas.c lista.c -o lista_se -g -std=c99 -Wall -Wconversion -Wtype-limits -pedantic -Werror -O0
    Es decir, se quieren compilar todos los .c (o los que se indiquen) con todos los warnings posibles, leyendo estos como error, y mostrando todas las conversiones que pueden generar cambios en el valor de una variable, y que el ejecutable se llame "lista_se".

    Para usar el TDA, basta con hacer dentro de un .c un "#include "lista.h"" y ya se pueden usar las funciones.

    Para ver el uso de memoria, correr con valgrind. Se recomienda correr con: valgrind --leak-check=full --track-origins=yes --show-reachable=yes ./lista_se
    Antes de correr con valgrind, recordar que hay que tener el ejecutable creado (en este caso "lista_se").
    
    Sino, ejecutar normal: "./lista_se".

─────────────────────────────────────────────────────────────────────────Funciones del TDA─────────────────────────────────────────────────────────────────────────

Aclaración: El trabajo entero se realizó tratando de practicar las habilidades con punteros. Por más que no sea tan cómodo, se trató de usar punteros a funciones todas las veces posibles.

A continuación explicaré las funciones que contiene el TDA y el por qué se realizaron así:

	●	lista_t* lista_crear();

Lo que se hace es reservar memoria en el heap para una lista. Se hace en el heap porque así se puede tener la cantidad de nodos que quiera sin preocuparse por el espacio. Si se obtiene la memoria para la lista, se inicializa: se podría hacer creandola directamente inicializada, pero se prefiere hacerlo a mano para tenerlo a la vista. Se devuelve la lista: si no se pudo reservar memoria para la lista, se devuelve NULL.

	●	int lista_insertar(lista_t* lista, void* elemento);

Si no hay lista (no se leyeron las pre condiciones), se devuelve ERROR. Sino, se trata de reservar memoria dinámica para el nuevo nodo a insertar. Si no se logra hacerlo, se devuelve ERROR.
En caso de poder reservar memoria dinámica, si la lista está vacía, se inserta un nodo al comienzo de la misma. Sino, al final de todo. Se aumenta la cantidad de elementos en la lista.
Se retorna EXITO.

	●	int lista_insertar_en_posicion(lista_t* lista, void* elemento, size_t posicion);

Si no hay lista (no se leyeron las pre condiciones), se devuelve ERROR. Sino, se trata de reservar memoria dinámica para el nuevo nodo a insertar. Si no se logra hacerlo, se devuelve ERROR.
En caso de poder reservar memoria dinámica, si la lista está vacía, se inserta un nodo al comienzo de la misma. Sino, en la posicion requerida, recorriendo la lista hasta encontrarla. Se aumenta la cantidad de elementos en la lista.
Se retorna EXITO o ERROR.

	●	int lista_borrar(lista_t* lista);

Si no hay lista o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve ERROR. Si la lista tiene un elemento, se libera la memoria reservada para ese nodo. Sino, para el último nodo que haya.
Para borrar el último nodo de una lista de más de un elemento, se recorre la lista hasta el final.
Se retorna EXITO o ERROR.

	●	int lista_borrar_de_posicion(lista_t* lista, size_t posicion);

Si no hay lista o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve ERROR. Si la lista tiene un elemento se libera la memoria reservada para ese nodo. Si se quiere borrar el último nodo de la lista se tiene que recorrer hasta el final y ahí liberar la memoria ocupada por ese nodo. En caso de querer borrar cualquier otra posición, se debe recorrer la lista hasta esa posición y ahí borrar.
Se retorna EXITO o ERROR.

	●	void* lista_elemento_en_posicion(lista_t* lista, size_t posicion);

Si no hay lista, si hay pero está vacía o si la posición es inválida (no se leyeron las pre condiciones), se devuelve NULL. Sino, se recorre la lista hasta la posición pedida y se devuelve el elemento.
Si algo falló en el proceso, se devuelve NULL.

	●	void* lista_ultimo(lista_t* lista);

Si no hay lista o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve NULL. Sino, se devuelve el último elemento de la lista.

	●	bool lista_vacia(lista_t* lista);

Si no hay lista o si hay pero no tiene elementos, se devuelve true. Sino, se devuelve false.

	●	size_t lista_elementos(lista_t* lista);

Si no hay lista se devuelve 0. Sino, se devuelve la cantidad de elementos de la lista.

	●	int lista_apilar(lista_t* pila, void* elemento);

Se reutiliza la función int lista_insertar(lista_t* lista, void* elemento);
Si no hay pila (no se leyeron las pre condiciones), se devuelve ERROR. Sino, se trata de reservar memoria dinámica para el nuevo nodo a insertar. Si no se logra hacerlo, se devuelve ERROR.
En caso de poder reservar memoria dinámica, si la pila está vacía, se inserta un nodo al comienzo de la misma. Sino, al final de todo. Se aumenta la cantidad de elementos en la pila.
Se retorna EXITO.

	●	int lista_desapilar(lista_t* pila);

Se reutiliza la función int lista_borrar(lista_t* lista);
Si no hay pila o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve ERROR. Si la pila tiene un elemento, se libera la memoria reservada para ese nodo. Sino, para el último nodo que haya.
Para borrar el último nodo de una pila de más de un elemento, se recorre la pila hasta el final.
Se retorna EXITO o ERROR.

	●	void* lista_tope(lista_t* pila);

Se reutiliza la función void* lista_ultimo(lista_t* lista);
Si no hay pila o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve NULL. Sino, se devuelve el último elemento de la pila.

	●	int lista_encolar(lista_t* cola, void* elemento);

Se reutiliza la función int lista_borrar(lista_t* lista);
Si no hay cola o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve ERROR. Si la cola tiene un elemento, se libera la memoria reservada para ese nodo. Sino, para el último nodo que haya.
Para borrar el último nodo de una cola de más de un elemento, se recorre la cola hasta el final.
Se retorna EXITO o ERROR.

	●	int lista_desencolar(lista_t* cola);

Se reutiliza la función int lista_borrar_de_posicion(lista_t* lista, size_t posicion);
Si no hay cola o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve ERROR. Si la cola tiene un elemento se libera la memoria reservada para ese nodo. Sino se tiene que recorrer hasta el final y ahí liberar la memoria ocupada por ese nodo.
Se retorna EXITO o ERROR.

	●	void* lista_primero(lista_t* cola);

Se reutiliza la función void* lista_elemento_en_posicion(lista_t* lista, size_t posicion);
Si no hay cola o si hay pero está vacía (no se leyeron las pre condiciones), se devuelve NULL. Sino, se devuelve el primer elemento.

	●	void lista_destruir(lista_t* lista);

Si no hay lista (no se leyeron las pre condiciones), se termina la función. Si la lista tiene al menos un elemento, se la vacía borrando sus nodos desde el último al primero. Por último, siempre se libera la memoria reservada para la lista.

	●	lista_iterador_t* lista_iterador_crear(lista_t* lista);

Si no hay lista (no se leyeron las pre condiciones), se devuelve NULL. Sino, lo que se hace es reservar memoria en el heap para un iterador. Si se obtiene la memoria para el iterador, se inicializa. Se devuelve el iterador: si no se pudo reservar memoria para el iterador, se devuelve NULL.

	●	bool lista_iterador_tiene_siguiente(lista_iterador_t* iterador);

Se devuelve si el iterador es distinto de NULL y si iterador->corriente también lo es.

	●	bool lista_iterador_avanzar(lista_iterador_t* iterador);

Si el iterador e iterador->corriente son distintos de NULL, se actualiza el valor de iterador->corriente con iterador->corriente->siguiente. Se devuelve si iterador e iterador->corriente son distintos de NULL. 

	●	void* lista_iterador_elemento_actual(lista_iterador_t* iterador);

Si no hay iterador, o si el nodo actual es nulo, se devuelve NULL. Sino, se retorna el elemento actual.

	●	void lista_iterador_destruir(lista_iterador_t* iterador);

Si hay iterador, se libera la memoria reservada para el iterador.

	●	size_t lista_con_cada_elemento(lista_t* lista, bool (*funcion)(void*, void*), void *contexto);

Se valida si hay lista, función y la lista no está vacía: se verifica en este orden para asegurar que se realicen la menor cantidad de operaciones: 
Si se hiciera así: lista && lista_vacia(lista) && funcion -> en el caso de función = NULL, se tendría que haber recorrido una función entera primero (lista_vacia(lista));
Como se hace así: lista && funcion && lista_vacia(lista) -> se asegura recorrer lo menos posible para los peores casos.
Como estaba diciendo, si hay lista, función y la lista no está vacía, se entra a una función iterativa (do while) donde se incrementa el valor del contador y se entra a la función recibida por parámetro, hasta que se recorra todos los elementos de la lista o hasta que la función recibida por parámetro devuelva false.
Se retorno la cantidad de elementos recorridos.

─────────────────────────────────────────────────────────────────────────Funciones que reciben punteros a función en el TDA (privadas)─────────────────────────────────────────────────────────────────────────

 	●	int buscar_y_borrar(lista_t* lista, size_t tope, void* contexto, bool(*es_nodo_borrar)(void*, nodo_t*, size_t), void(*borrar)(lista_t*, nodo_t*, nodo_t*, int*));

Se recorre la lista hasta "tope", hasta que no haya un "nodo_actual" o hasta que haya un error.
Si se cumple la condición recibida por parámetro, se procede a borrar el elemento de la forma recibida por parámetro.
La condición recibe tres parámetros porque según lo que quiera hacer, usaré un parámetro diferente: es decir,
en caso 'a' necesito "contexto" y "nodo_actual".
en caso 'b' necesito "contexto" e "i". 
Por eso, mi es_nodo_borrar() recibe los tres parámetros.
Se devuelve EXITO o ERROR.

─────────────────────────────────────────────────────────────────────────Pruebas del TDA─────────────────────────────────────────────────────────────────────────

En este trabajo se entregan 165 pruebas: han sido pensadas tan minuciosamente que han generado que este TDA pase las 181 pruebas de Chanutron2021 (patente pendiente) de una.

Estas pruebas están pensadas por TDA: pruebas para lista, pruebas para pila y pruebas para cola.

Dentro de las pruebas para cada TDA, se valida que cada función del TDA funcione tal como corresponde: para esto, se ha decidido asumir que todas las funciones del TDA andan menos la que se está probando (previamente preguntado en clase si se podía proceder así).

Las pruebas están divididas (visualmente) en "categoria", "grupo" y "subgrupo": la categoría es el tipo de TDA a probar, el grupo es de qué van a ser las pruebas (información del TDA o operaciones en el mismo), y el subgrupo es sobre qué función del TDA se está probando.
Las pruebas principales empiezan con "Se puede" o "No se puede": es por gusto personal.
Para las pruebas relacionadas con una prueba anterior, se decidió ponerlo como "subprueba".
Para las pruebas que devuelven la misma información, se decidió poner el mismo texto.
Como:
"La cantidad de elementos de la lista es correcta"
"El valor del elemento insertado en la lista es correcto"
"El inicio y fin de la lista son correctos"

Es posible que dentro de cada prueba capaz se vuelva a validar lo mismo que lo anterior y algo más.
Al probar cada función se crea una estructura de tipo lista_t* y se destruye al final de la prueba.
Al inicio de cada función para probar una estructura (probar_lista(), probar_pila() y probar_cola()) se crea un vector de numeros para insertar en las respectivas estrcturas. Al final se libera la memoria.

A continuación se explicará qué hace cada una de mis pruebas (se quiere creer que se entienden solas, pero es mejor prevenir que curar):

1.	lista_crear():					debe devolver una lista no nula.
2.	lista_crear(): 					debe devolver una lista no nula y sus campos deben ser lista->nodo_inicio = lista->nodo_fin = NULL y lista->cantidad = 0.
3.	lista_insertar():				lista nula: debe devolver ERROR.
4.	lista_insertar():				lista válida y vacía, insertar 1 elemento: debe devolver EXITO.
5.	lista_insertar():				lista válida y vacía, insertar 1 elemento: debe devolver EXITO y lista->cantidad debe ser 0.
6.	lista_insertar():				lista válida y vacía, insertar 1 elemento: debe devolver EXITO y sus nodos deben corresponder a los elementos que están al principio y final de la lista.
7.	lista_insertar():				lista válida y vacía, insertar 1 elemento: debe devolver EXITO y sus nodos deben ser diferentes de null.
8.	lista_insertar():				lista válida y vacía, insertar CANT_INSERCION elementos: debe devolver EXITO.
9.	lista_insertar():				lista válida y vacía, insertar CANT_INSERCION elementos: debe devolver EXITO y lista->cantidad debe ser CANT_INSERCION.
10.	lista_insertar():				lista válida y vacía, insertar CANT_INSERCION elementos: debe devolver EXITO y los valores insertados deben estar acorde a lo esperado.
11.	lista_insertar_en_posicion():	lista nula, insertar CANT_INSERCION elementos, en diversas posiciones: debe devolver ERROR.
12.	lista_insertar_en_posicion():	lista válida y vacía, insertar 1 elemento, en posicion 0: debe devolver EXITO.
13.	lista_insertar_en_posicion():	lista válida y vacía, insertar 1 elemento, en posicion 0: debe devolver EXITO y lista->nodo_inicio->elemento = lista->nodo_fin->elemento = elemento.
14.	lista_insertar_en_posicion():	lista válida y vacía, insertar 1 elemento, en posicion 0: debe devolver EXITO y el primer elemento debe ser ese.
15.	lista_insertar_en_posicion():	lista con 1 elemento, insertar 1 elemento, en última posicion: debe devolver EXITO.
16.	lista_insertar_en_posicion():	lista con 1 elemento, insertar 1 elemento, en última posicion: debe devolver EXITO y lista->cantidad debe ser 2.
17.	lista_insertar_en_posicion():	lista con 1 elemento, insertar 1 elemento, en última posicion: debe devolver EXITO y el valor insertado debe ser el correcto.
18.	lista_insertar_en_posicion():	lista con 1 elemento, insertar 1 elemento, en última posicion: debe devolver EXITO y el final de la lista tiene que haberse actualizado.
19.	lista_insertar_en_posicion():	lista con 2 elementos, insertar 1 elemento, en posición inválida: debe devolver EXITO.
20.	lista_insertar_en_posicion():	lista con 2 elementos, insertar 1 elemento, en posición inválida: debe devolver EXITO y lista->cantidad debe ser 3.
21.	lista_insertar_en_posicion():	lista con 2 elementos, insertar 1 elemento, en posición inválida: debe devolver EXITO y el valor insertado debe ser el correcto.
22.	lista_insertar_en_posicion():	lista con 2 elementos, insertar 1 elemento, en posición inválida: debe devolver EXITO y el final de la lista tiene que haberse actualizado.
23.	lista_insertar_en_posicion():	lista con 2 elementos, insertar 1 elemento, en última posicion: debe devolver EXITO y el final de la lista tiene que haberse actualizado.
24.	lista_insertar_en_posicion():	lista con 3 elementos, insertar 1 elemento, en posición 1: debe devolver EXITO.
25.	lista_insertar_en_posicion():	lista con 3 elementos, insertar 1 elemento, en posición 1: debe devolver EXITO y lista->cantidad debe ser 4.
26.	lista_insertar_en_posicion():	lista con 3 elementos, insertar 1 elemento, en posición 1: debe devolver EXITO y el valor insertado debe ser el correcto.
27.	lista_insertar_en_posicion():	lista con 3 elementos, insertar 1 elemento, en posición 1: debe devolver EXITO y el final de la lista tiene que haberse actualizado.
28.	lista_borrar():					lista nula: debe devolver ERROR.
29.	lista_borrar():					lista válida y vacía: debe devolver ERROR.
30.	lista_borrar():					lista con 1 elemento, borrar 1 elemento: debe devolver EXITO.
31.	lista_borrar():					lista con 1 elemento, borrar 1 elemento: debe devolver EXITO y lista->cantidad debe ser 0.
32.	lista_borrar():					lista con 1 elemento, borrar 1 elemento: debe devolver EXITO y sus nodos deben ser NULL.
33.	lista_borrar():					lista con CANT_INSERCION elementos, borrar CANT_BORRAR (< a CANT_INSERCION) elementos: debe devolver EXITO.
34.	lista_borrar():					lista con CANT_INSERCION elementos, borrar CANT_BORRAR (< a CANT_INSERCION) elementos: debe devolver EXITO y tener la cantidad esperada de elementos.
35.	lista_borrar():					lista con CANT_INSERCION elementos, borrar CANT_BORRAR (< a CANT_INSERCION) elementos: debe devolver EXITO y que su primer elemento inicial sea igual al actual elemento inicial.
36.	lista_borrar():					lista con elementos, borrar todos sus elementos: debe devolver EXITO.
37.	lista_borrar():					lista con elementos, borrar todos sus elementos: debe devolver EXITO y estar vacía.
38.	lista_borrar_de_posicion():		lista nula, cualquier posición: debe devolver ERROR.
39.	lista_borrar_de_posicion():		lista válida y vacía, cualquier posición: debe devolver ERROR.
40.	lista_borrar_de_posicion():		lista con 1 elemento, borrar 1 elemento, posición 0: debe devolver EXITO.
41.	lista_borrar_de_posicion():		lista con 1 elemento, borrar 1 elemento, posición 0: debe devolver EXITO y la lista debe estar vacía.
42.	lista_borrar_de_posicion():		lista con 1 elemento, borrar 1 elemento, posición cualquiera: debe devolver EXITO.
43.	lista_borrar_de_posicion():		lista con 1 elemento, borrar 1 elemento, posición cualquiera: debe devolver EXITO y la lista debe estar vacía.
44.	lista_borrar_de_posicion():		lista con CANT_INSERCION elementos, borrar 1 elemento, última posicion: debe devolver EXITO.
45.	lista_borrar_de_posicion():		lista con CANT_INSERCION elementos, borrar 1 elemento, última posicion: debe devolver EXITO y la cantidad de elementos debe ser la esperada.
46.	lista_borrar_de_posicion():		lista con CANT_INSERCION elementos, borrar 1 elemento, última posicion: debe devolver EXITO y el inicio de la lista debe ser correcto.
47.	lista_borrar_de_posicion():		lista con CANT_INSERCION elementos, borrar 1 elemento, última posicion: debe devolver EXITO y la final de la lista debe ser correcto.
48.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 0: debe devolver EXITO.
49.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 0: debe devolver EXITO y la cantidad de elementos de la lista ser correcta.
50.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 0: debe devolver EXITO y el inicio de la lista ser correcto.
51.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 0: debe devolver EXITO y el fin de la lista ser correcto.
52.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 1: debe devolver EXITO.
53.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 1: debe devolver EXITO y la cantidad de elementos de la lista ser correcta.
54.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 1: debe devolver EXITO y el inicio de la lista ser correcto.
55.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 1: debe devolver EXITO y el elemento borrado no estar más.
56.	lista_borrar_de_posicion():		lista con varios elemento, borrar 1 elemento, posición 1: debe devolver EXITO y el fin de la lista ser correcto.
57. lista_elemento_en_posicion():	lista nula, cualquier posición: debe devolver ERROR.
58.	lista_elemento_en_posicion():	lista válida y vacía, cualquier posición: debe devolver ERROR.
59.	lista_elemento_en_posicion():	lista con 1 elemento, posición 0: debe devolver EXITO.
60.	lista_elemento_en_posicion():	lista con 1 elemento, posición 0: debe devolver EXITO y el elemento ser el esperado.
61.	lista_elemento_en_posicion():	lista con 1 elemento, posición 1: debe devolver ERROR.
62.	lista_elemento_en_posicion():	lista con CANT_INSERCION elementos, última posición: debe devolver EXITO.
63.	lista_elemento_en_posicion():	lista con CANT_INSERCION elementos, última posición: debe devolver EXITO y el elemento ser el esperado.
64.	lista_elemento_en_posicion():	lista con CANT_INSERCION elementos, posición 0: debe devolver EXITO.
65.	lista_elemento_en_posicion():	lista con CANT_INSERCION elementos, posición 0: debe devolver EXITO y el elemento ser el esperado.
66. lista_ultimo():					lista nula: debe devolver ERROR.
67. lista_ultimo():					lista válida y vacía: debe devolver ERROR.
68. lista_ultimo():					lista con 1 elemento: debe devolver EXITO.
69. lista_ultimo():					lista con 1 elemento: debe devolver EXITO y el elemento ser el esperado.
70. lista_ultimo():					lista con CANT_INSERCION elementos: debe devolver EXITO.
71. lista_ultimo():					lista con CANT_INSERCION elementos: debe devolver EXITO y el elemento ser el esperado.
72. lista_vacia():					lista nula: debe devolver true.
73. lista_vacia():					lista válida y vacía: debe devolver true.
74. lista_vacia():					lista con 1 elemento: debe devolver false.
75. lista_vacia():					lista con CANT_INSERCION elementos: debe devolver false.
76. lista_elementos():				lista nula: debe devolver 0.
77. lista_elementos():				lista válida y vacía: debe devolver 0.
78. lista_elementos():				lista con 1 elemento: debe devolver 1.
79. lista_elementos():				lista con CANT_INSERCION elementos: debe devolver CANT_INSERCION.
80. lista_con_cada_elemento():		lista nula, funcion "cantidad_elementos": debe devolver 0.
81. lista_con_cada_elemento():		lista vacía y válida, funcion nula: debe devolver 0.
82. lista_con_cada_elemento():		lista vacía y válida, funcion "cantidad_elementos": debe devolver 0.
83. lista_con_cada_elemento():		lista con un elemento, funcion "cantidad_elementos": debe devolver 1.
84. lista_con_cada_elemento():		lista con CANT_INSERCION elementos, funcion "cantidad_elementos": debe devolver CANT_INSERCION y el contexto ser el esperado.
85. lista_con_cada_elemento():		lista válida y vacía, funcion "cantidad_digitos_total": debe devolver 0.
86. lista_con_cada_elemento():		lista con CANT_INSERCION elementos, funcion "cantidad_digitos_total": debe devolver CANT_INSERCION y el contexto ser el esperado.
87. lista_con_cada_elemento():		lista vacía y válida, funcion "cantidad_posiciones_impares": debe devolver 0.
88. lista_con_cada_elemento():		lista con CANT_INSERCION elementos, funcion "cantidad_digitos_total": debe devolver CANT_INSERCION y el contexto ser el esperado.
89.	lista_apilar():					pila nula: debe devolver ERROR.
90.	lista_apilar():					pila válida y vacía, apilar 1 elemento: debe devolver EXITO.
91.	lista_apilar():					pila válida y vacía, apilar 1 elemento: debe devolver EXITO y pila->cantidad debe ser 0.
92.	lista_apilar():					pila válida y vacía, apilar 1 elemento: debe devolver EXITO y sus nodos deben ser diferentes de null.
93.	lista_apilar():					pila válida y vacía, apilar CANT_INSERCION elementos: debe devolver EXITO.
94.	lista_apilar():					pila válida y vacía, apilar CANT_INSERCION elementos: debe devolver EXITO y pila->cantidad debe ser CANT_INSERCION.
95.	lista_apilar():					pila válida y vacía, apilar CANT_INSERCION elementos: debe devolver EXITO y los valores insertados deben estar acorde a lo esperado.
96.	lista_desapilar():				pila nula: debe devolver ERROR.
97.	lista_desapilar():				pila válida y vacía: debe devolver ERROR.
98.	lista_desapilar():				pila con 1 elemento, desapilar 1 elemento: debe devolver EXITO.
99.	lista_desapilar():				pila con 1 elemento, desapilar 1 elemento: debe devolver EXITO y pila->cantidad debe ser 0.
100. lista_desapilar():				pila con 1 elemento, desapilar 1 elemento: debe devolver EXITO y sus nodos deben ser NULL.
101. lista_desapilar():				pila con CANT_INSERCION elementos, desapilar CANT_BORRAR (< a CANT_INSERCION) elementos: debe devolver EXITO.
102. lista_desapilar():				pila con CANT_INSERCION elementos, desapilar CANT_BORRAR (< a CANT_INSERCION) elementos: debe devolver EXITO y tener la cantidad esperada de elementos.
103. lista_desapilar():				pila con CANT_INSERCION elementos, desapilar CANT_BORRAR (< a CANT_INSERCION) elementos: debe devolver EXITO y su primer elemento inicial ser igual a pila->nodo_inicio.
104. lista_desapilar():				pila con elementos, desapilar todos sus elementos: debe devolver EXITO.
105. lista_desapilar():				pila con elementos, desapilar todos sus elementos: debe devolver EXITO y pila debe estar vacía.
106. lista_tope():					pila nula: debe devolver ERROR.
107. lista_tope():					pila válida y vacía: debe devolver ERROR.
108. lista_tope():					pila con 1 elemento: debe devolver EXITO.
109. lista_tope():					pila con 1 elemento: debe devolver EXITO y el elemento ser el esperado.
110. lista_tope():					pila con CANT_INSERCION elementos: debe devolver EXITO.
111. lista_tope():					pila con CANT_INSERCION elementos: debe devolver EXITO y el elemento ser el esperado.
112. lista_encolar():				cola nula: debe devolver ERROR.
113. lista_encolar():				cola válida y vacía, encolar 1 elemento: debe devolver EXITO.
114. lista_encolar():				cola válida y vacía, encolar 1 elemento: debe devolver EXITO y cola->cantidad debe ser 0.
115. lista_encolar():				cola válida y vacía, encolar 1 elemento: debe devolver EXITO y el elemento encolado es el correcto.
116. lista_encolar():				cola válida y vacía, encolar 1 elemento: debe devolver EXITO y sus nodos deben ser diferentes de null.
117. lista_encolar():				cola válida y vacía, encolar CANT_INSERCION elementos: debe devolver EXITO.
118. lista_encolar():				cola válida y vacía, encolar CANT_INSERCION elementos: debe devolver EXITO y pila->cantidad debe ser CANT_INSERCION.
119. lista_encolar():				cola válida y vacía, encolar CANT_INSERCION elementos: debe devolver EXITO y los valores insertados deben estar acorde a lo esperado.
120. lista_desencolar():			cola nula: debe devolver ERROR.
121. lista_desencolar():			cola válida y vacía: debe devolver ERROR.
122. lista_desencolar():			cola con 2 elementos, desencolar 1 elemento: debe devolver EXITO.
123. lista_desencolar():			cola con 2 elementos, desencolar 1 elemento: debe devolver EXITO y la cola debe tener 1 elemento.
124. lista_desencolar():			cola con 2 elementos, desencolar 1 elemento: debe devolver EXITO y la cola debe tener nodo_inicio = nodo_fin.
125. lista_desencolar():			cola con 1 elemento, desencolar 1 elemento: debe devolver EXITO.
126. lista_desencolar():			cola con 1 elemento, desencolar 1 elemento: debe devolver EXITO y la cola tener un elemento.
127. lista_desencolar():			cola con 1 elemento, desencolar 1 elemento: debe devolver EXITO y sus nodos son nulos.
128. lista_desencolar():			cola con muchos elementos, desencolar varios elementos: debe devolver EXITO.
129. lista_desencolar():			cola con muchos elementos, desencolar varios elementos: debe devolver EXITO y la cantidad de elementos debe ser la esperada.
130. lista_desencolar():			cola con muchos elementos, desencolar varios elementos: debe devolver EXITO y los nodos están como se espera.
131. lista_desencolar():			cola con muchos elementos, desencolar todos los elementos: debe devolver EXITO.
132. lista_desencolar():			cola con muchos elementos, desencolar todos los elementos: debe devolver EXITO y la cola estar vacía.
133. lista_primero():				cola nula: debe devolver ERROR.
134. lista_primero():				cola válida y vacía: debe devolver ERROR.
135. lista_primero():				cola con 1 elemento: debe devolver EXITO.
136. lista_primero():				cola con 1 elemento: debe devolver EXITO y el elemento ser el esperado.
137. lista_primero():				cola con CANT_INSERCION elementos: debe devolver EXITO.
138. lista_primero():				cola con CANT_INSERCION elementos: debe devolver EXITO y el elemento ser el esperado.
139. lista_crear_iterador():		lista nula: debe devolver NULL.
140. lista_crear_iterador(): 		lista válida y vacía: debe devolver un iterador.
141. lista_crear_iterador(): 		lista válida y vacía: debe devolver un iterador con sus campos válidos.
142. lista_crear_iterador(): 		lista con 1 elemento: debe devolver un iterador.
143. lista_crear_iterador(): 		lista con 1 elemento: debe devolver un iterador con sus campos válidos.
144. lista_crear_iterador(): 		lista con CANT_INSERCION elementos: debe devolver un iterador.
145. lista_crear_iterador(): 		lista con CANT_INSERCION elementos: debe devolver un iterador con sus campos válidos.
146. lista_iterador_avanzar():		iterador nulo: debe devolver false.
147. lista_iterador_avanzar():		iterador con lista válida y vacía: debe devolver false.
148. lista_iterador_avanzar():		iterador con lista con 1 elemento: debe devolver false.
149. lista_iterador_avanzar():		iterador con lista con 2 elementos: debe devolver true en el primer llamado.
150. lista_iterador_avanzar():		iterador con lista con 2 elementos: debe devolver false en el segundo llamado.
151. lista_iterador_avanzar():		iterador con lista con CANT_INSERCION elementos: debe devolver true en los primeros CANT_INSERCION - 1 llamados.
152. lista_iterador_avanzar():		iterador con lista con CANT_INSERCION elementos: debe devolver false en el CANT_INSERCION llamado.
153. lista_iterador_tiene_siguiente():	iterador nulo: debe devolver false.
154. lista_iterador_tiene_siguiente():	iterador con lista válida y vacía: debe devolver false.
155. lista_iterador_tiene_siguiente():	iterador con lista con 1 elemento: debe devolver true.
156. lista_iterador_tiene_siguiente():	iterador con lista con CANT_INSERCION elementos: debe devolver true.
157: lista_iterador_elemento_actual():	iterador nulo: debe devolver NULL.
158. lista_iterador_elemento_actual():	iterador con lista válida y vacía: debe devolver NULL.
159. lista_iterador_elemento_actual():	iterador con lista con 1 elemento: debe devolver un elemento válido.
160. lista_iterador_elemento_actual():	iterador con lista con 1 elemento: debe devolver un elemento válido y ser el esperado.
161. lista_iterador_elemento_actual():	iterador con lista con CANT_INSERCION elementos: debe devolver un elemento válido.
162. lista_iterador_elemento_actual():	iterador con lista con CANT_INSERCION elementos: debe devolver un elemento válido y ser el esperado.
163. lista_iterador_elemento_actual():	iterador con lista con CANT_INSERCION elementos, se avanzó CANT_INSERCION - 1 veces: debe devolver un elemento válido.
164. lista_iterador_elemento_actual():	iterador con lista con CANT_INSERCION elementos, se avanzó CANT_INSERCION - 1 veces: debe devolver un elemento válido y ser el esperado.
165. lista_iterador_elemento_actual():	iterador con lista con CANT_INSERCION elementos, se avanzó CANT_INSERCION veces: debe devolver NULL.

─────────────────────────────────────────────────────────────────────────Funciones que reciben punteros a función en las pruebas─────────────────────────────────────────────────────────────────────────

 	●	bool se_inserto_bien(lista_t* lista, int* valor, size_t cant_elementos, size_t posicion_insertada, bool(*se_puede_seguir)(lista_t*, size_t, size_t, bool), bool(*es_valor)(void*, size_t, size_t, void*));

El objetivo es saber si se insertó los valores esperados.
Si no hay lista, se devuelve false.
Se itera mientras se cumpla la condición "se_puede_seguir()" recibida por parámetro. Si para cada iteración no se cumple la condición "es_valor()" recibida por parámetro, se devuelve false.

 	●	int borrar_muchos(lista_t* lista, int(*eliminar)(lista_t*));

El objetivo es borrar la cantidad de elementos recibida por parámetro hasta que ocurra un error o se termine de borrar.
Mientras se pueda, se eliminan los elementos mediante la función "eliminar()" recibida por parámetro. Se espera poder desencolar, desapilar y borrar.
Se devuelve si se pudo realizar la eliminación correctamente o no.

 	●	int insertar_elementos_lista(int* valor, lista_t* lista, int cant_elementos, int(*funcion_insertar)(lista_t*, void*));

El objetivo es insertar la cantidad de elementos recibida por parámetro hasta que ocurra un error o se termine de insertar.
Mientras se pueda, se insertan los elementos mediante la función "insertar()" recibida por parámetro. Se espera poder encolar, apilar e insertar.
Se devuelve si se pudo realizar la inserción correctamente o no.

 	●	int accion_invalida_elementos_lista(lista_t* lista, int* valor, int cant_elementos, int(*accion)(lista_t*, void*, size_t))

El objetivo es realizar una acción la cantidad de veces recibida por parámetro hasta que ocurra un error o se realice esa cantidad de veces.
Mientras se pueda, se realiza la acción mediante la función "accion()" recibida por parámetro. Se espera poder insertar y eliminar elementos.
Se devuelve si se pudo realizar lo pedido correctamente o no.

 	●	void reiniciar_lista(lista_t* lista, int(*eliminar)(lista_t*));

El objetivo es vaciar la memoria reservada para un elemento de tipo lista_t.
Mientras queden elementos en la estructura, se seguirá eliminando con la función "eliminar()" recibida por parámetro. Se espera poder desencolar, desapilar y eliminar elementos.

─────────────────────────────────────────────────────────────────────────TEORÍA─────────────────────────────────────────────────────────────────────────

─────────────────────────────────────────────────────────────────────────¿Qué es un TDA?

TDA hace referencia a Tipo de Dato Abstracto. Un Tipo de Dato Abstracto en programación se le considera al modelo que define valores y operaciones que se pueden realizar sobre él. Se crea una biblioteca con una o varias estructuras relacionadas a este tipo de dato, buscando que quien lo utilice no necesite conocer internamente cómo funciona: necesita saber qué hace, no cómo se hace. A este concepto se lo conoce como "caja blanca".

Se le llama abstracto ya que se busca concentrarse solo en lo que se necesita e importa a la hora de implementarlo.

El objetivo de usar un TDA es poder proveer de mayor flexibilización a la hora de programar: si una parte cambia, las demás no se ven afectadas. Esto nos lo brinda la abstracción.

Además, algo muy importante, al menos para mi, es que el usuario al no tener acceso al código, no puede romperlo, sabemos que la parte interna del mismo estará bien en todo momento, los casos bordes solo pueden ser generados por los parámetros recibidos en cada función.

En esta entrega, están "lista.c" junto a "lista.h", los cuales nos brindan las funciones necesarias para poder usar una lista, cola o pila. Lo ideal es que el usuario reciba el .h y un .o para utilizarlo, sin nada más.

Pila, cola y lista son tipos de TDA.

─────────────────────────────────────────────────────────────────────────¿Qué es una lista?

Una lista es un concepto que hace referencia al conjunto de varios elementos agrupados. Cada elemento tiene su posición. Si no hay elementos, la lista está vacía. Nosotros con una lista podemos hacer varias cosas, como insertar elementos, borrar elementos, buscar elementos. Podemos además, crear la lista y luego hacerla bolita y destruirla.

En programación, en C, es muy parecido: nosotros definimos las operaciones de lista, a partir del tipo de lista que tengamos. Además, los elementos de la lista no tienen que estar contiguos, pueden estar dispersos, cada uno conteniendo información de la ubicación del siguiente elemento.

Una lista tiene varias desventajas:
● No podemos acceder a una posición random de la lista sin recorrerla primero.
● Se trabaja con punteros y memoria dinámica, lo cual incrementa la dificultad de programarlas.

Existen varios tipos de listas:
● Listas simplemente enlazadas.
● Listas doblemente enlazadas.
● Listas circulares.

Una lista enlazada consiste en una secuencia de nodos, en los que se guardan campos de datos arbitrarios y una o dos referencias o punteros para ubicar al nodo anterior o siguiente. El gran beneficio es que los nodos no deben estar contiguos: pueden estar totalmente dispersos.

La lista simplemente enlazada se caracteriza por tener un enlace por nodo: nos da información de cómo ubicar al siguiente nodo: puede ser que contenga la dirección del siguiente nodo o NULL, entre otras.
El gran inconveniente es que no podemos volver al nodo anterior: debemos volver a recorrer la lista entera, ya que sabemos que en una lista no existe el acceso aleatorio.

La lista doblemente enlazada, por lo contrario, se caracteriza por tener dos enlaces por nodo: nos habla sobre la ubicación del nodo anterior y del siguiente. Resuelve el inconveniente del caso anterior, al poder acceder a nodos anteriores al actual. Entonces, se puede recorrer la lista desde el final hasta el inicio, y al revés.

El TDA entregado es de una lista simplemente enlazada.

Las operaciones de una lista son:
● Creación.
● Inserción (en cualquier lugar).
● Eliminación (en cualquier lugar).
● Búsqueda.
● Obtener cantidad de elementos.
● Está vacía.
● Destrucción.

Una explicación de cómo realizar cualquiera de estas operaciones se encuentra al inicio de este .txt

─────────────────────────────────────────────────────────────────────────¿Qué es una pila?

Una pila en C, es muy parecida a una pila de objetos. Es muy similar a una lista, pero sabiendo que las inserciones y extracciones se hacen siempre desde la última posición: se la conoce como lista LIFO: Last In First Out, haciendo referencia justamente a lo anterior.

En todo momento, a diferencia de la lista, solo se tiene acceso al último valor de la estructura.

Entonces, sus operaciones definidas son ligeramente diferentes a las de la lista:
● Creación
● Apilar al final.
● Desapilar del final.
● Obtener tope.
● Está vacía.
● Destrucción.

Para entenderlo, siempre se hace analogía a una pila de platos: el último que colocas es el primero que agarras.

Una explicación de cómo realizar cualquiera de estas operaciones se encuentra al inicio de este .txt

─────────────────────────────────────────────────────────────────────────¿Qué es una cola?

Una cola también es muy similar a una lista o a una pila, pero sabiendo que las inserciones y extracciones ya no se hacen por el mismo lado: se la conoce como lista FIFO: First In First Out, haciendo referencia a que se inserta por el final pero se elimina por la primera posición. Una analogía es la cola del supermercado: se atiende al primero de todos y si te queres sumar a la cola, tenés que ponerte al final de la misma.

En todo momento, a diferencia de la lista, solo se tiene información del primer elemento de la estructura.

Entonces, sus operaciones definidas son ligeramente diferentes a las de la lista:
● Creación
● Encolar al final.
● Desencolar del principio.
● Obtener primero.
● Está vacía.
● Destrucción.

Una explicación de cómo realizar cualquiera de estas operaciones se encuentra al inicio de este .txt

─────────────────────────────────────────────────────────────────────────¿Qué es un iterador?

Un iterador es un tipo de puntero que es utilizado por un algoritmo para recorrer los elementos almacenados en un contenedor, sin tener en cuenta su implementación específica.

Un iterador tiene dos operaciones principales: referenciar un elemento particular en una colección, y modificarse a sí mismo para que apunte al siguiente elemento.

El objetivo principal de un iterador, es permitir al usuario procesar cada elemento de una colección sin que el usuario sepa sobre la estructura interna de la misma. Esto permite a la colección almacenar elementos en cualquier forma, mientras permite al usuario tratarlo como si fuera una simple secuencia o lista de elementos.

Hay dos tipos de iteradores:
● Iterador interno.
● Iterador externo.

Normalmente el iterador que maneja el usuario es llamado "iterador externo", en cambio, si iterador automaneja la iteración, se conoce como "iterador interno". En este TDA, el iterador interno es lista_con_cada_elemento() y el externo es el iterador creado, que perfectamente podría ser un TDA aparte.

● Iterador Interno

Como se dijo antes, el iterador interno es el que nos permite recorrer los elementos de un TDA sin conocer la estructura interna del mismo. Se suele hacer esto usando una función la cual se envía como parámetro al llamar a este iterador interno. Además, se le suele enviar un contexto, y así controlar u obtener datos del recorrido del TDA.

● Iterador Externo

Es un TDA: nos provee un grupo de primitivas especiales para recorrer una lista. 

La idea es que conozca cómo está representada la lista a recorrer.

Este iterador tiene un puntero apuntando a una posición de la lista. Cada vez que quiera acceder al siguiente elemento, simplemente avanzo el puntero una posición.

Las funciones propias de un iterador externo son:

● Creación
● Avanzar
● Tiene siguiente
● Elemento actual
● Destruir

______________________________________________________________________________FIN______________________________________________________________________________

