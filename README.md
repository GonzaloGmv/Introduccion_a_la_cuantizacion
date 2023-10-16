# Introduccion_a_la_cuantizacion

El link al repositorio es: [github](https://github.com/GonzaloGmv/Introduccion_a_la_cuantizacion)

Los participantes son:

- Gonzalo Martínez

- José Luis Rodríguez

- Alexandre Muñoz

## Conclusion

El tamaño del modelo GPT-2 es de 510,342,192 bytes o lo que es lo mimso, 486,58 MB en FP32. En el siguiente gráfico podemos ver la comparación entre el model original y el cuantificado:

![image](https://github.com/GonzaloGmv/Introduccion_a_la_cuantizacion/assets/91721237/c5d70eaf-d33d-439b-9348-05cdcedd4d57)

Ambos gráficos son bastante similares, con un pico sorprendente alrededor de 0. Este pico muestra que nuestra cuantización tiene bastantes pérdidas ya que invertir el proceso no genera los valores originales

Ahora para comparar el rendimiento de los modelos,primero generaremos los siguientes 50 tokens de los modelos y a continuación veremos la perplejidad de cada uno:

Esta es la salida del generador de texto con cada uno de los modelos: 

```
Original model:
Once upon a time, we did not know that the world had arrived. He who had never seen it then knew that there were no more stars that looked to us.

"He who had seen it still knew that it was in its turn
--------------------------------------------------
Absmax model:
Once upon a time

He saw the dark corners of the palace. There stood a girl in silk dress with silver hair covering her face. She looked at him. His gaze had gone down upon them for a moment. Then, after his hands
--------------------------------------------------
Zeropoint model:
Once upon a time, I think it's time for the media to put a lid on your ignorance."

So I wrote a quick article about how I can do something to prevent it from happening and this blog post with its answers to some of
```

Y a continuación implementamos una función para calcular la complejidad. Y este es el resultado:

```
Original perplexity:  15.47
Absmax perplexity:    20.15
Zeropoint perplexity: 21.05
```

Con estos resultados podemos comprobar que el modelo con mejor rendimiento es el Zeropoint, luego el Absmax y por último el original.
