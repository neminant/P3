PAV - P3: estimación de pitch
=============================

Esta práctica se distribuye a través del repositorio GitHub [Práctica 3](https://github.com/albino-pav/P3).
Siga las instrucciones de la [Práctica 2](https://github.com/albino-pav/P2) para realizar un `fork` de la
misma y distribuir copias locales (*clones*) del mismo a los distintos integrantes del grupo de prácticas.

Recuerde realizar el *pull request* al repositorio original una vez completada la práctica.

Ejercicios básicos
------------------

- Complete el código de los ficheros necesarios para realizar la estimación de pitch usando el programa
  `get_pitch`.

   * Complete el cálculo de la autocorrelación e inserte a continuación el código correspondiente.
![Captura de pantalla de 2023-05-07 21-47-19](https://user-images.githubusercontent.com/126669600/236699515-d7182659-b59a-41ba-822c-7d6b2b1e1b2e.png)

   * Inserte una gŕafica donde, en un *subplot*, se vea con claridad la señal temporal de un segmento de
     unos 30 ms de un fonema sonoro y su periodo de pitch; y, en otro *subplot*, se vea con claridad la
	 autocorrelación de la señal y la posición del primer máximo secundario.

	 NOTA: es más que probable que tenga que usar Python, Octave/MATLAB u otro programa semejante para
	 hacerlo. Se valorará la utilización de la biblioteca matplotlib de Python.
	 
![Captura de pantalla de 2023-05-07 22-14-48](https://user-images.githubusercontent.com/126669600/236700678-181cf0e9-d994-41d9-9519-a61c82c59121.png)

Si mirem on cauren dos mínims, podem obtenir que el període és aproximadament 9ms, de manera que el pitch és l'invers del període, per tant obtenim un pitch de 110Hz. Aquest valor concorda amb la gràfica de l'autocorrelació

   * Determine el mejor candidato para el periodo de pitch localizando el primer máximo secundario de la
     autocorrelación. Inserte a continuación el código correspondiente.
![Captura de pantalla de 2023-05-07 21-55-06](https://user-images.githubusercontent.com/126669600/236699871-bba6f54f-f79c-4761-bac9-89ebe0663e7a.png)

   * Implemente la regla de decisión sonoro o sordo e inserte el código correspondiente.
![Captura de pantalla de 2023-05-07 21-57-26](https://user-images.githubusercontent.com/126669600/236699968-3ba49e83-38a6-4a7a-800f-746aa3597bd9.png)

Per saber si un so és sord o sonor, mirarem la potència de la senyal, ja que la potència serà major si és sonor.

   * Puede serle útil seguir las instrucciones contenidas en el documento adjunto `código.pdf`.

- Una vez completados los puntos anteriores, dispondrá de una primera versión del estimador de pitch. El 
  resto del trabajo consiste, básicamente, en obtener las mejores prestaciones posibles con él.

  * Utilice el programa `wavesurfer` para analizar las condiciones apropiadas para determinar si un
    segmento es sonoro o sordo. 
	
	  - Inserte una gráfica con la estimación de pitch incorporada a `wavesurfer` y, junto a ella, los 
	    principales candidatos para determinar la sonoridad de la voz: el nivel de potencia de la señal
		(r[0]), la autocorrelación normalizada de uno (r1norm = r[1] / r[0]) y el valor de la
		autocorrelación en su máximo secundario (rmaxnorm = r[lag] / r[0]).

		Puede considerar, también, la conveniencia de usar la tasa de cruces por cero.

	    Recuerde configurar los paneles de datos para que el desplazamiento de ventana sea el adecuado, que
		en esta práctica es de 15 ms.

      - Use el estimador de pitch implementado en el programa `wavesurfer` en una señal de prueba y compare
	    su resultado con el obtenido por la mejor versión de su propio sistema.  Inserte una gráfica
		ilustrativa del resultado de ambos estimadores.
     
		Aunque puede usar el propio Wavesurfer para obtener la representación, se valorará
	 	el uso de alternativas de mayor calidad (particularmente Python).
  
  * Optimice los parámetros de su sistema de estimación de pitch e inserte una tabla con las tasas de error
    y el *score* TOTAL proporcionados por `pitch_evaluate` en la evaluación de la base de datos 
	`pitch_db/train`..
![Captura de pantalla de 2023-05-07 21-57-26](https://user-images.githubusercontent.com/126669600/236702447-15df37f3-74ed-4cc3-aaef-fe3fa2ca25e2.png)

Els valors utilitzats per a rmaxnorm, r1norm i pot són aquests:

![Captura de pantalla de 2023-05-07 23-04-35](https://user-images.githubusercontent.com/126669600/236702535-68e67c95-1ebe-43ab-af63-e167f0e92007.png)

![Captura de pantalla de 2023-05-07 23-02-17](https://user-images.githubusercontent.com/126669600/236702450-528f5280-7a07-4cb1-95e5-5948fd758cc2.png)

Hem obtingut resultats força favorables ja que són majors del 90%


Ejercicios de ampliación
------------------------

- Usando la librería `docopt_cpp`, modifique el fichero `get_pitch.cpp` para incorporar los parámetros del
  estimador a los argumentos de la línea de comandos.
  
  Esta técnica le resultará especialmente útil para optimizar los parámetros del estimador. Recuerde que
  una parte importante de la evaluación recaerá en el resultado obtenido en la estimación de pitch en la
  base de datos.

  * Inserte un *pantallazo* en el que se vea el mensaje de ayuda del programa y un ejemplo de utilización
    con los argumentos añadidos.

![Captura de pantalla de 2023-05-07 23-19-23](https://user-images.githubusercontent.com/126669600/236703094-33adb728-04e1-4c35-8788-627ccba3a569.png)


- Implemente las técnicas que considere oportunas para optimizar las prestaciones del sistema de estimación
  de pitch.

  Entre las posibles mejoras, puede escoger una o más de las siguientes:

  * Técnicas de preprocesado: filtrado paso bajo, diezmado, *center clipping*, etc.

Aplicant el mètode Center Clipping hem aconseguit millorar el percentatge del detector de pitch:

![Captura de pantalla de 2023-05-07 23-27-18](https://user-images.githubusercontent.com/126669600/236703364-bcf35eed-5c94-4b06-af1f-03679f98a349.png)

Per tal d'obtenir aquest resultat hem modificat el codi, afegint-hi aquestes línies:
![Captura de pantalla de 2023-05-07 23-25-51](https://user-images.githubusercontent.com/126669600/236703454-d8fea0bc-af27-4ae7-b149-0a43c2e293a5.png)

On la constant CENTERCLIP val 0.004

  * Técnicas de postprocesado: filtro de mediana, *dynamic time warping*, etc.
  * Métodos alternativos a la autocorrelación: procesado cepstral, *average magnitude difference function*
    (AMDF), etc.
  * Optimización **demostrable** de los parámetros que gobiernan el estimador, en concreto, de los que
    gobiernan la decisión sonoro/sordo.
  * Cualquier otra técnica que se le pueda ocurrir o encuentre en la literatura.

  Encontrará más información acerca de estas técnicas en las [Transparencias del Curso](https://atenea.upc.edu/pluginfile.php/2908770/mod_resource/content/3/2b_PS%20Techniques.pdf)
  y en [Spoken Language Processing](https://discovery.upc.edu/iii/encore/record/C__Rb1233593?lang=cat).
  También encontrará más información en los anexos del enunciado de esta práctica.

  Incluya, a continuación, una explicación de las técnicas incorporadas al estimador. Se valorará la
  inclusión de gráficas, tablas, código o cualquier otra cosa que ayude a comprender el trabajo realizado.

  También se valorará la realización de un estudio de los parámetros involucrados. Por ejemplo, si se opta
  por implementar el filtro de mediana, se valorará el análisis de los resultados obtenidos en función de
  la longitud del filtro.
   

Evaluación *ciega* del estimador
-------------------------------

Antes de realizar el *pull request* debe asegurarse de que su repositorio contiene los ficheros necesarios
para compilar los programas correctamente ejecutando `make release`.

Con los ejecutables construidos de esta manera, los profesores de la asignatura procederán a evaluar el
estimador con la parte de test de la base de datos (desconocida para los alumnos). Una parte importante de
la nota de la práctica recaerá en el resultado de esta evaluación.
