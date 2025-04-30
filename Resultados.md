

## Resultados de la simulación
```
Tiempo: 1.023317491465, Nodo: host[2], Origen: 10.0.0.2, Reenviado por: 10.0.0.2, TTL: 32, TQ: 255, Hops: 0, SeqNum: 1, Distancia: N/A
Tiempo: 1.02331763054, Nodo: host[3], Origen: 10.0.0.2, Reenviado por: 10.0.0.2, TTL: 32, TQ: 255, Hops: 0, SeqNum: 1, Distancia: N/A
Tiempo: 1.045737956727, Nodo: host[3], Origen: 10.0.0.3, Reenviado por: 10.0.0.3, TTL: 32, TQ: 255, Hops: 0, SeqNum: 1, Distancia: N/A
Tiempo: 1.045738118642, Nodo: host[1], Origen: 10.0.0.3, Reenviado por: 10.0.0.3, TTL: 32, TQ: 255, Hops: 0, SeqNum: 1, Distancia: N/A
Tiempo: 1.07072857632, Nodo: host[2], Origen: 10.0.0.4, Reenviado por: 10.0.0.4, TTL: 32, TQ: 255, Hops: 0, SeqNum: 1, Distancia: N/A
Tiempo: 1.070728876645, Nodo: host[1], Origen: 10.0.0.4, Reenviado por: 10.0.0.4, TTL: 32, TQ: 255, Hops: 0, SeqNum: 1, Distancia: N/A
Tiempo: 1.1045658727, Nodo: host[2], Origen: 10.0.0.3, Reenviado por: 10.0.0.3, TTL: 31, TQ: 0, Hops: 1, SeqNum: 1, Distancia: N/A
Tiempo: 1.104566173711, Nodo: host[1], Origen: 10.0.0.3, Reenviado por: 10.0.0.3, TTL: 31, TQ: 0, Hops: 1, SeqNum: 1, Distancia: N/A
Tiempo: 1.115108167276, Nodo: host[2], Origen: 10.0.0.2, Reenviado por: 10.0.0.2, TTL: 31, TQ: 0, Hops: 1, SeqNum: 1, Distancia: N/A
...
...
...


```

## Interpretación de TXT

- **Tiempo**: instante en segundos cuando ocurrió el evento.
- **Nodo:** nodo que recibió el OGM (Originator Message) es un tipo de paquete que envía un nodo para anunciar su existencia en la red. 
- **Origen:** nodo que originó el OGM.
- **Reenviado por:** nodo que envió el paquete (en este caso, el mismo nodo origen).
- **TTL (Time to Live):** número de saltos permitidos antes de descartar el paquete.
- **TQ (Transmit Quality):** calidad del enlace entre el nodo que envía el paquete y quien lo recibe (máximo 255, mejor calidad).
- **Hops:** número de saltos que ha dado el paquete desde su origen (0 indica que es el primer envío).
- **SeqNum (Sequence Number):** número de secuencia del OGM (incrementa con el tiempo, permite detectar OGMs antiguos).
- **Distancia:** N/A — BATMAN no usa métrica de distancia física.

---
# Tiempo

Los valores de tiempo en el archivo son acumulativos, entonces, para el análisis de la frecuenia en que ocurren los eventos tendríamos que restar cada uno con su anterior.
Esto permitirá obtener el intervalo entre eventos e identificar picos de actividad o inactividad.


Resulado: 
```
Resta: [1.3907499996079764e-07, 0.02242032618699996, 1.6191500007423087e-07, 0.02499045767800001, 3.0032499998000617e-07, 0.03383699605500001, ...

```

![image](https://github.com/user-attachments/assets/3a63aa16-5d86-4519-b9b2-9d4ef5a87491)


Los OGMs se generan de forma regular aunque hay picos de intervalos más largos.

---
## TTL VS Tiempo

Para ver si los paquetes se degradan mucho 
Un TTL bajo puede significar rutas largas o reenvíos excesivos. 

![image](https://github.com/user-attachments/assets/d9eca491-df3a-46dc-a946-18475f91d513)

---
## Origem

Para concocer cuántos OGMs envió cada nodo y detectar nodos activos, silenciados o que participan más en la red.

![image](https://github.com/user-attachments/assets/8f83edd9-4943-440f-8074-00f1a376a5db)

---
## TQ (Transmit Quality) 

Para evaluar la calidad de los enlaces, TQ bajo puede significar interferencias o rutas inestables.

![image](https://github.com/user-attachments/assets/a1c2161f-ca90-45d7-932e-68e89728f298)

---
# Distancia 

BATMAN no trabaja con la distancia física entre los nodos, debido a varios factores, está diseñado para redes ad-hoc, lo que significa que no dependen de una infraestructura centralizada como enrutadores o puntos de acceso fijos, se dinámico. Los nodos de la red pueden unirse y abandonarla en cualquier momento, y la topología de la red se forma espontáneamente.

Está  optimizado para entornos donde los nodos pueden moverse, sus rangos de cobertura cambian, las conexiones se pierden y se establecen nuevas. Incluso si los nodos permanecen estáticos, la calidad de los enlaces inalámbricos entre ellos puede variar debido a interferencias.

**B.A.T.M.A.N. no considera distancia física entre nodos en su funcionamiento, se basa en la calidad de los enlaces (TQ) y la topología de la red.
No calcula la distancia completa entre un origen y un destino, sino que se enfoca en encontrar el mejor nodo para el siguiente salto y luego deja que ese nodo haga lo mismo hasta que el paquete llegue al destino. 
Cada nodo mantiene información sobre el mejor siguiente salto para cada destino, lo que implica una distancia variable según la configuración de la red.

**Aproximación:**

Por los fines de la simulación, se podría aproximar la distancia contando el número de saltos que el paquete sigue hasta el destino, considerando la información de la tabla de enrutamiento de cada nodo en el camino. Cada vez que un paquete de un salto se puede sumir que avanzó cierta distancia promedio 
EJM:
- 0 hops = 0m
- 1 hops = 100m 

Usando TQ (calidad de enlace) podriamos asumir que:
- **TQ = 255** es un enlace perfecto, distancia muy corta.
- **TQ = 0** enlace roto o muy lejano.
Podemos hacer una estimación porporcional donde el rango máximo son 100 metros.

```
Distancia= rangoMaximo * (1- (TQ/255))

```
Ejemplo:
- TQ= 255 entonces, Distancia = 0 metros
- TQ= 127 -> Distancia = 150 metros. 
