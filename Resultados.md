

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

Los valores de tiempo en el archivo son acumulativos, entonces, para el análisis de la frecuenia en que ocurren los eventos tendríamos q restar cada uno con su anterior.
Esto permitirá obtener el intervalo entre eventos e identificar picos de actividad o inactividad.


Resulado: 
```
Resta: [1.3907499996079764e-07, 0.02242032618699996, 1.6191500007423087e-07, 0.02499045767800001, 3.0032499998000617e-07, 0.03383699605500001, ...

```

![image](https://github.com/user-attachments/assets/3a63aa16-5d86-4519-b9b2-9d4ef5a87491)

---
