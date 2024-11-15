14/11/2024
# Controladores por retroalimentación de estados
En sistemas de control digital y de movimiento se analizan dos variables importantes en el análisis de las mismas: la observabilidad y la controlabilidad. Estas dos variables determinan si un sistema puede ser completamente controlado o si sus estados pueden ser determinados a partir de las salidas observables. Las variables de estado son las que permiten conocer estas dos características, que son importantes para garantizar el diseño efectivo de controladores, la estabilidad del sistema y su capacidad de seguir o responder adecuadamente a señales de referencia. 
## Controlabilidad 
>🔑 Definición: Un sistema es controlable si puede desplazarse desde cualquier punto a otro mediante las variables de estado. Este tipo de prueba se realiza evaluando el rango o la determinante de la matriz de controlabilidad (Sale del modelo de estados).

$$U = [B AB A^{2}B A^{3}B ...A^{n-1}B ]$$

* Matriz de controlabilidad, vector columnas.
* La matriz de controlabilidad debe tener el mismo tamaño de la matriz principal A que sale de:
  
  $$x(k+1)=Ax(k)+Bu(k)$$
  
  $$𝒚(k) = 𝑪𝑿 (𝑘) + 𝑫𝒖(𝑘)$$

Ahora bien, para determinar si un sistema es controlable o no, se realizan de dos formas: 
|Primera forma (Determinante) | Segunda forma (Rango) |
| ------ | ------ | 
| If $$U[]\not\equiv 0$$ (Sistema controlable)  | If rango de la matriz = Cant de variables de estado (Sistema controlable) | 
| If U[] = 0 (Sistema NO controlable) | If rango de la matriz $$\not\equiv$$ Cant de variables de estado Sistema NO controlable)   | 

## 💡Ejemplo 1:
IMG1
Ahora se realiza el proceso de multiplicación de matrices y al tener la matriz U se analiza el determinante:
IMG2
Al tener U diferente de 0 se obtiene que el sistema es controlable.

## Observabilidad
>🔑 Definición: Se puede saber con solo la salida, las variables de estado, porque hay veces en donde estas no son medibles, es decir, no son visibles y esta variable es muy valiosa. Este tipo de prueba se realiza evaluando el rango o la determinante de la matriz de observabilidad.

imgadc

* Matriz de observabilidad, vector filas.
* La matriz de observabilidad debe tener el mismo tamaño de la matriz principal A que sale de:
  
  $$x(k+1)=Ax(k)+Bu(k)$$
  
  $$𝒚(k) = 𝑪𝑿 (𝑘) + 𝑫𝒖(𝑘)$$

Ahora bien, para determinar si un sistema es observable o no, se realizan de dos formas:
|Primera forma (Determinante) | Segunda forma (Rango) |
| ------ | ------ | 
| If $$V[]\not\equiv 0$$ (Sistema controlable)  | If rango de la matriz = Cant de variables de estado (Sistema controlable) | 
| If V[] = 0 (Sistema NO controlable) | If rango de la matriz $$\not\equiv$$ Cant de variables de estado Sistema NO controlable)   |

## 💡Ejemplo 2:
En base al ejercicio 1, se interpreta la siguiente matriz de observabilidad: 
Tercer img
* El sistema es OBSERVSABLE
* Este tipo de variable es más desde el punto matemático, pues la realidad es que el 99.9% de los sistemas son controlables y observables, es por eso que tenemos áreas como la física, la matemática y las ingenierías.

## 💡Ejemplo 3:
Cuartaimg
* El sistema es controlable
Quinta IMG 
* El sistema NO es observable
* Se concluye que el sistema es canónico controlable

## 💡Ejemplo 4:
Sexta img
* Con el siguiente sistema se analiza por medio de MATLAB muy similar al anterior ejercicio y se obtiene que el sistema es observable, pero no controlable, ¿Por qué sucede esto si son mismos valores organizados de manera distinta? R/ Este es el efecto que se obtiene al tener la forma canónica observable de un sistema.

## Control por retroalimentación de estados
>🔑 Propósito: Asignar los polos del sistema en lazo cerrado arbitrariamente mediante ganancias proporcionales (K).

Lo anterior se define mediante $$u(k)=−Kx(k)$$, donde como se mencionó anteriormente, K es una matriz de ganancias que es calculada para lograr la dinámica deseada del sistema.

Séptima img

Donde se deben tener en cuenta dos condiciones importantes: 
1. Todas las variables de estado deben ser MEDIBLES.
2. El sistema si o si debe ser controlable. 
Es decir, las dos variables explicadas al comienzo de este tema deben cumplirse para poder retroalimentar los estados.

### PASOS PARA IMPLEMENTAR LA RETROALIMENTACIÓN
1.	Comprobar si el sistema efectivamente es controlable para garantizar que el diseño pueda ser posible.
2.	Calcular el polinomio característico, teniendo en cuenta que: $$|zI -A|= z^{n}+a_{1}z^{n-1}+...+a_{n-1}z+a_{n}$$
3.	Analizar la transformación T basada en la matriz de controlabilidad, donde T= UW, pero si y solo si el sistema es canónico controlable T adopta el valor de I que es la matriz identidad o bien conocida en valor numérico como 1. En caso de que no sea controlable la única matriz que falta analizar es W:
   
Novenimg

5.	Diseñar el polinomio que ubique los polos en lazo cerrado: $$z^{n}+ \alpha z^{n-1}+...+ \alpha_{n-1}z+ \alpha_{n}$$
6.	Finalmente calcular la matriz de ganancias en la retroalimentación de estados con la siguiente forma: 
$$K = [\alpha_{n}-a_{n}, \alpha_{n-1}-a_{n-1},...,\alpha_{1}-a_{1}]T^{-1}$$ 

° La retroalimentación modifica la dinámica de A para ubicar los polos deseados. 

## 💡Ejemplo 5:
Para el sistema con matrices :

Octava img

° Polos deseados: $$𝑧 = −0.2±𝑗0.4, z=−0.02$$
1.	Según la variable de controlabilidad dando un determinante de -1 , se puede saber que el sistema es controlable, asi que se pueden seguir con los siguientes pasos.
2.	Ahora bien, calculando el polinomio característico en lazo abierto: $$z^{3}+6z^{2}+5z+1$$
3.	Determinar la matriz T teniendo en cuenta :
   
DECIMAIMG

Sin embargo, al ser un sistema canónico controlable se adopta la matriz identidad: 

Onceimg

5.	Calcular polinomio característico en lazo cerrado:
   
$$𝑧^{3} + 0.402𝑧^{2} + 0.2008𝑧 + 0.0004$$

7.	Realizando la matriz de ganancias K, se obtiene que los alpha menos las a, terminan en:
   
$$K = [-0.996, -4.799, -5.598]$$

° Hay que tener en cuenta para todos estos tipos de cálculos que el valor que acompaña a la z con mayor potencia debe ser siempre de 1. 
° Para MATLAB tener en cuenta función Acker (A,B,Polos) 

# 📚Ejercicios 
1. Considerando el sistema lineal en espacio de estados definido por:
   
Doceimg 

1.	Calcular matriz de controlabilidad
2.	Determinar si el sistema es controlable 

* Solución:
  
Treceimg

El sistema es controlable

2. Considerando las matrices
   
Catorceimg

1.	Calcular matriz de observabilidad.
2.	Determinar si el sistema es observable verificando si el rango de V es igual al número de estados del sistema.
   
* Solucion:
  
Quinceimg

° Si el rango es igual al numero de estados, n= 2, el sistema es efectivamente observable 
 Rango (V) = 2

## Conclusiones 
La controlabilidad y la observabilidad son fundamentales para garantizar el control efectivo de un sistema y su monitoreo y/o análisis. La controlabilidad asegura que, mediante las entradas, es posible mover el estado del sistema desde cualquier condición inicial a cualquier estado deseado, lo cual permite diseñar controladores que modifiquen la dinámica del sistema. Por esa misma razón mediante estos sistemas se pueden calcular ganancias de retroalimentación de estados (K) que ajusten los polos del sistema en lazo cerrado para obtener características deseadas como estabilidad, rapidez o puede ser que amortiguamiento. Por otro lado, la observabilidad garantiza que se puedan deducir todos los estados del sistema a partir de sus salidas medidas. Esto es crucial cuando no se puede medir directamente el estado completo del sistema. En conjunto, la controlabilidad y la observabilidad permiten ajustar tanto la dinámica del sistema en lazo cerrado entre otras, asegurando que el sistema sea robusto, estable y capaz de cumplir con los objetivos deseados en su operación.

## Referencias
[1] 


