---
title: contest 10 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 10](../contests#contest-10) > ```{{page.title}}```

### A - Counting Triangles
<details> 
  <summary>Hint</summary>
  Una opción es ver para cada trío se segmentos, si todos se intersectan de a dos entonces forman un triángulo. Acumulando las veces que se formen triángulos se otendrá la respuesta.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución consiste en usar el hint. Para saber si segmentos intersectan pueden usar el hint 3 de la pregunta A.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Kattis/CountingTriangles.cpp">Código de ejemplo</a>
</details>

### B - Treasure Spotting
<details> 
  <summary>Hint 1</summary>
  Se debe chequear para cada pirata la visibilidad del tesoro, para eso debemos chequear tres cosas, que el tesoro esté en el semidisco visible para el pirata, que para toda muralla no lo tape y que para todo otro pirata no lo tape. Si podemos hacer cada chequeo en tiempo constante el algoritmo pasará en tiempo.
</details>
<details> 
  <summary>Hint 2</summary>
  Para chequear que el tesoro se encuentra en el semidisco de visión basta ver que este a una distancia menor o igual a la del radio entregado por input (se calcula como la distancia entre los puntos entregados para el pirata en R2) y que además el producto punto entre el vector de visión entregado AB y el vector al tesoro AT sea mayor o igual a 0.
</details>
<details> 
  <summary>Hint 3</summary>
  Para chequear que cada muralla no tape basta con chequear si los segmentos AT y CD intersectan, donde AT es del pirata al tesoro y CD es la muralla. Para chequear intersección de segmentos se puede ver que para cada segmento, los puntos del otro segmento estén a lados distintos de la recta generada por el segmento analizado, si esto pasa para ambos hay intersección. También habrá intersección si alguno de los puntos de un segmento está en el otro segmento.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución consiste en usar los hints e implementarlo correctamente teniendo en cuenta la precisión, para evitar problemas evitar el uso de doubles a menos que se considere pequeñas variaciones.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Kattis/TreasureSpotting.cpp">Código de ejemplo</a>
</details>

### E - Inside or outside?
<details> 
  <summary>Hint</summary>
  Para cada punto, para que esté dentro del polígono basta que este en el mismo lado en todos los segmentos del polígono, es decir, que siempre esté a la izquierda de la linea generada por cada segmento o siempre a la derecha. Basta chequear con producto cruz.
</details>
<details> 
  <summary>Solución + código</summary>
  Basta usar el hint para obtener la solución.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/InsideOrOutside.cpp">Código de ejemplo</a>
</details>

### F - Left, right or center?
<details> 
  <summary>Hint</summary>
  Pueden detectar a que lado de una recta generada por un segmento se encuentra un punto haciendo uso del producto cruz, si la recta esta dada por el segmento AB y el punto está en P, el producto AB x AP será positivo si el punto está a la derecha o negativo en caso contrario.
</details>
<details> 
  <summary>Solución + código</summary>
  La respuesta consiste en usar el hint directamente.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/LeftRightOrCenter.cpp">Código de ejemplo</a>
</details>

<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 10](../contests#contest-10) > ```{{page.title}}```
