# Introduccion_a_la_cuantizacion

El link al repositorio es: [github](https://github.com/GonzaloGmv/Introduccion_a_la_cuantizacion)

Los participantes son:

- Gonzalo Martínez

- José Luis Rodríguez

- Alexandre Muñoz

## Conclusion

El tamaño del modelo GPT-2 es de 510,342,192 bytes o lo que es lo mimso, 486,58 MB en FP32. En el siguiente gráfico podemos ver la comparación entre el model original y los cuantificados:

![image](https://github.com/GonzaloGmv/Introduccion_a_la_cuantizacion/assets/91721237/c5d70eaf-d33d-439b-9348-05cdcedd4d57)
![image](https://github.com/GonzaloGmv/Introduccion_a_la_cuantizacion/assets/91721237/800f9764-1eac-4c82-beec-6168d983d29d)


Los tres gráficos son bastante similares, con un pico alrededor de 0. Este pico muestra que nuestra cuantización tiene bastantes pérdidas ya que invertir el proceso no genera los valores originales

Ahora para comparar el rendimiento de los modelos,primero generaremos los siguientes 50 tokens de los modelos y a continuación veremos la perplejidad de cada uno. El tecxto inicial del que partirán los modelos para generar texto estará en inglés ya que de esta forma hemos comprobado que la salida es significativamente mejor. Ponemos como texto inicial "Once upon a time", que es un texto que puede dar lugar a buenos resultados debido a que el texto generado puede ser muy variado.

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
--------------------------------------------------
LLM.int8() model:
I have a dreamcr unusuallyOUSverning dispersed aimedheartedly metal Conan enrolledBALL HawkFontSizeheartedly idiotsSomeearchers cl���� multiporeAndOnline FaWaterwithstandingSur Broadway journalists allergicrespectedodi active Kyr Lia stretch motivation sport hardship355 Dres WEEK Address sport Cannabis VIS VIS VIS
```

Y a continuación implementamos una función para calcular la complejidad. Y este es el resultado:

```
Original perplexity:  15.47
Absmax perplexity:    20.15
Zeropoint perplexity: 21.05
Perplexity (LLM.int8()): 15823.67
```
Como podemos ver, la perplejidad de los modelos Absmax y Zeropoint son ligeramente superiores que la del original, pero si vemos la del LLM.int8, ya vemos que es exageradamente superior, y si observamos el texto generado de cada una esto se ve perfectamente, ya que entre el original, Absmax y Zeropoint no sabríamos decir cuál tiene mejor rendimiento, pero si vemos el modelo LLM.int8, observamos como este tiene un mal rendimiento.
