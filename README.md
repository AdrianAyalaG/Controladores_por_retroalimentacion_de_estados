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
