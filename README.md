# Flor-de-vida
Explicación del código llamado "Flor de vida"
---

---

Imagen del código con 3 círculos

---
<img width="800" height="860" alt="image" src="https://github.com/user-attachments/assets/ac3ebbfa-b60f-43ec-97c2-0b649d720d01" />


---

1.- Inicialización y Gestión de Memoria (bpy.ops)

---
A diferencia del código anterior que manipulaba datos de malla a bajo nivel, este utiliza operadores de alto nivel (bpy.ops).

  ¬Limpieza de Escena: Se ejecuta un barrido total de la base de datos de objetos activos (select_all y delete). Esto asegura que el sistema de coordenadas global esté despejado para la nueva generación procedimental.

---

2.- Definición de Parámetros Cinemáticos y Geométricos

---
El script establece constantes para controlar la topología del patrón:

    ¬radio = 3: Define la magnitud del vector posición desde el origen a cada centro de los círculos periféricos.
    ¬paso_angular = 60: Es el incremento en grados 0. Dado que una circunferencia completa tiene 360 grados, un paso de 60 grados garantiza la creación de exactamente 6 elementos simétricos (360/60 = 6).

---

3.- Generación del Nodo Central

---
bpy.ops.mesh.primitive_circle_add(...)

Se instancia el primer objeto en el origen (0, 0, 0). El parámetro vertices=64 define la resolución de la curva; a mayor número de vértices, mayor aproximación a una circunferencia perfecta (continuidad visual).
  
---

4.- Transformación de Coordenadas Polares a Cartesianas

---
Para posicionar los círculos periféricos, el script realiza una conversión de coordenadas. Dado un ángulo alpha y un radio r, la posición (x, y) se determina mediante las funciones trigonométricas fundamentales:

  ¬math.radians(angulo_actual): Es una función crítica de pre-procesamiento. Las funciones de la librería math de Python operan en radianes (0 a 2pi), mientras que la lógica humana suele estructurarse en grados (0 a 360). Esta línea normaliza la unidad de medida.

---

5.- Iteración de Posicionamiento (Patrón Manual)

---
  
El script procede a calcular el nuevo centro sumando el paso_angular al acumulador angulo_actual.

    ¬Círculo 1: Se ubica en 0 grados (sobre el eje positivo X).
    ¬Círculo 2: Se desplaza 60 grados, calculando las nuevas coordenadas mediante el nuevo valor de la variable de estado angulo_actual.




¿Qué hace que podamos crear más círculos?
---


---

Imagen de la Flor de vida con más círculos

---
<img width="800" height="860" alt="image" src="https://github.com/user-attachments/assets/0e026bd1-c1bb-4412-8532-667b55439094" />

---

1.- El Bucle Condicional (while)

---
La sentencia while angulo_actual < 360: actúa como un vigilante lógico.

       ¬Condición de parada: El programa evalúa si el valor de angulo_actual es menor a 360 grados (una vuelta completa).
       ¬Reutilización de código: En lugar de escribir manualmente la función primitive_circle_add para cada círculo, el bucle obliga a la computadora a re-ejecutar el mismo bloque de código mientras la condición sea verdadera.

---

2.- El Incremento de Estado (Acumulador)

---
En la línea 28, el comando angulo_actual += paso_angular es lo que permite que el patrón progrese.

       ¬Si el paso_angular es pequeño (en tu imagen es 10), el bucle se ejecutará 36 veces (360 / 10 = 36), creando una densidad mucho mayor de círculos.
       ¬En el código manual anterior, el ángulo era estático o se cambiaba una sola vez. Aquí, cada vez que el ciclo termina una vuelta, "salta" a la siguiente posición angular automáticamente.

---

3.- Dinamismo en las Coordenadas Cartesianas

---
Dentro del bucle, las variables x e y ya no son valores fijos (como x1 o y1). Ahora son variables dinámicas que se recalculan en microsegundos en cada iteración:

Iteración 1: Ángulo 0 → x=3, y=0.
Iteración 2: Ángulo 10 → x=2.95, y=0.52.
Iteración 3: Ángulo 20... y así sucesivamente.

---

4.- Eficiencia Algorítmica

---
Al usar esta estructura, has pasado de un código de "fuerza bruta" (escribir cada paso) a un algoritmo procedimental. Esto te permite cambiar la complejidad de la figura simplemente modificando una variable:

       ¬Si cambias paso_angular = 1, Blender dibujará 360 círculos casi instantáneamente, creando una forma geométrica compleja llamada toroide o un patrón de interferencia visual, algo que sería humanamente imposible de programar manualmente sin errores.



Fórmulas eficientes:
---

---

1. Fórmula de Iteraciones (Control de Bucles)

---
Para determinar cuántos círculos se dibujarán exactamente en la escena, aplicamos la lógica de saltos discretos. Si el bucle corre desde 0 grados hasta un límite L con un incremento P, la cantidad de objetos N se define como:

<img width="595" height="236" alt="image" src="https://github.com/user-attachments/assets/9fcfbe7b-1351-40f7-82a9-267f883eb73e" />

A esto debes sumar el Círculo Central que creaste antes del bucle, dando un total de 37 objetos en la colección de Blender.


---

2. Fórmula de Posicionamiento (Vectores de Traslación)

---
Para comprobar que cada círculo está en el lugar correcto, validamos la posición del centro de cada nueva instancia mediante la conversión de coordenadas polares a cartesianas. La posición del $n$-ésimo círculo está dada por:

<img width="640" height="228" alt="image" src="https://github.com/user-attachments/assets/ee91512b-4993-46d6-bccb-da36d5f76c52" />


---

3. Comprobación de Densidad Visual

---
Existe una relación inversamente proporcional entre el paso_angular y la densidad del patrón:

<img width="640" height="104" alt="image" src="https://github.com/user-attachments/assets/595a8690-0f75-4a15-8e89-185dd3d32cb7" />


