# Actividad dirigida 3

Esta actividad consite en hacer un ejercicio de programación literaria aprovechando un código que hemos usado en programación con python, donde realizameros *web scrapping*
    "A continuación pongo el código fuente"

## Instalar librerías


```python
pip install requests bs4 pandas termcolor
```

    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: requests in c:\programdata\anaconda3\lib\site-packages (2.27.1)
    Requirement already satisfied: bs4 in c:\users\marliege barría\appdata\roaming\python\python39\site-packages (0.0.1)
    Requirement already satisfied: pandas in c:\programdata\anaconda3\lib\site-packages (1.4.2)
    Requirement already satisfied: termcolor in c:\users\marliege barría\appdata\roaming\python\python39\site-packages (1.1.0)
    Requirement already satisfied: charset-normalizer~=2.0.0 in c:\programdata\anaconda3\lib\site-packages (from requests) (2.0.4)
    Requirement already satisfied: idna<4,>=2.5 in c:\programdata\anaconda3\lib\site-packages (from requests) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in c:\programdata\anaconda3\lib\site-packages (from requests) (2021.10.8)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in c:\programdata\anaconda3\lib\site-packages (from requests) (1.26.9)
    Requirement already satisfied: beautifulsoup4 in c:\programdata\anaconda3\lib\site-packages (from bs4) (4.11.1)
    Requirement already satisfied: pytz>=2020.1 in c:\programdata\anaconda3\lib\site-packages (from pandas) (2021.3)
    Requirement already satisfied: numpy>=1.18.5 in c:\programdata\anaconda3\lib\site-packages (from pandas) (1.21.5)
    Requirement already satisfied: python-dateutil>=2.8.1 in c:\programdata\anaconda3\lib\site-packages (from pandas) (2.8.2)
    Requirement already satisfied: six>=1.5 in c:\programdata\anaconda3\lib\site-packages (from python-dateutil>=2.8.1->pandas) (1.16.0)
    Requirement already satisfied: soupsieve>1.2 in c:\programdata\anaconda3\lib\site-packages (from beautifulsoup4->bs4) (2.3.1)
    Note: you may need to restart the kernel to use updated packages.
    

## Librerías
Vamos a instalar las siguientes librerías:

 ### Librerías del Sistema
    
    - 'time'
    - 'csv'
    - 're'
    - 'os'

### Librerías externas

    - 'requests'
    - 'bs4'
    - 'pandas'
    - 'termcolor'

### Importar librerías
    Las librerías que vienen con Python no hay que instalarlas pero las otras sí
- [requests](https://requests.readthedocs.io/en/latest/) : Es una biblioteca HTTP elegante y simple para Python
- [time](https://docs.python.org/es/3/library/time.html) : Este módulo proporciona varias funciones relacionadas con el tiempo
- [csv](https://docs.python.org/es/3/library/csv.html) : El tan llamado CSV (Valores Separados por Comas) es el formato más común de importación y exportación de hojas de cálculo y bases de datos.
- [re](https://docs.python.org/es/3/library/re.html) : Este módulo proporciona operaciones de coincidencia de expresiones regulares similares a las encontradas en Perl.
- [bs4](https://www.crummy.com/software/BeautifulSoup/) : Beautiful Soup analiza cualquier cosa que le des y hace el recorrido del árbol por ti. Puede decirle \"Encuentre todos los enlaces
- [pandas](https://bioinf.comav.upv.es/courses/linux/python/pandas.html) : Pandas es un paquete de Python que proporciona estructuras de datos similares a los dataframes de R.
- [termcolor](https://pypi.org/project/termcolor/) : Importación de colores"


```python
import requests
import time
import csv
import re
from bs4 import BeautifulSoup
import os
import pandas as pd
from termcolor import colored 
```

### Objetos/variables
    Vamos a crear una serie de objetos o variables:


```python
resultados = []
```

Si le paso la función type() veremos que se trata de un objeto tipo 'list' o \"lista\" de Python.


```python
type (resultados)
```




    list



#### Web scrpping para dividir los códigos

##### Impresión de titulares principales de El País


```python
req = requests.get("https://resultados.elpais.com")
```


```python
type (req)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup = BeautifulSoup(req.text, 'html.parser')
```


```python
tags = soup.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    “Aquí han pasado muchas cosas malas”: la ruta caliente del tráfico de migrantes también mata en Estados Unidos
    La OTAN se pertrecha para una época de conflicto de potencias
    Las píldoras, nuevo frente en la guerra contra el aborto en EE UU
    Los mercados castigan al peso argentino tras el cepo a los dólares para importaciones
    Vitalicios
    Mi querido doctor Sharpe
    Biden, ¿con Bolsonaro?
    Todo puede esperar cuando suena tu canción favorita
    Cuando los pájaros no cantaban: historias del conflicto armado en Colombia  
    Iván Duque, el presidente que se ausentó de la paz
    Las recomendaciones de la Comisión: cambiar la política de seguridad, la paz con el ELN y una reforma rural
    Francisco de Roux: “Colombia conoció lo que significa la paz y no va a renunciar a ello”
    Así es el barrio de Pekín donde hay “robotaxi” y la compra llega en vehículo sin conductor
    Los republicanos moderados avanzan en otra jornada de primarias en EE UU
    Guillermo Lasso salva una votación sobre su destitución como presidente de Ecuador 
    El jefe del Ejército colombiano renuncia para evitar caminar junto a Petro el día de la investidura
    Los 15 minutos que salvaron a Andrii del infierno de Kremenchuk
    El caso del profesor que debe ir escoltado en una universidad por el acoso de compañeros: “Tengo miedo de que me tiren por las escaleras”
    Los dos principales cárteles de la droga mexicanos aterrizan en Chile 
    Los animales de sangre fría parece que no envejecen
    La brasileña Marisa Monte confía en que a la ola reaccionaria le siga una iluminista
    El macrojuicio por los atentados de 2015 en París llega a su fin: los jueces preparan las condenas
    Ghislaine Maxwell, condenada a 20 años de cárcel por proporcionar menores al depredador sexual Epstein
    Jens Stoltenberg, el joven pacifista que acabó dirigiendo la OTAN
    Lecciones desde Montevideo: cómo dejar de ser un agresor de mujeres
    El PRI propone que la gente pueda armarse ante la inseguridad en México
    Adam y Hussein: huir de Sudán y saltar la valla
    Peter Weir, un Oscar honorífico que sabe a poco para el director de ‘El show de Truman’
    Calamaro en Madrid, locura y genio en directo de la leyenda argentina
    Courtney Barnett, la reina en los festivales: “Hacer cosas que no te apasionan solo trae resentimiento e infelicidad”
    La Orquesta Sinfónica de Kiev, el frente cultural, vuelve a sonar
    La ‘venganza’ de William Levy: “De joven, en Cuba, viví demasiadas injusticias”
    Periodismo de investigación, una herramienta para la construcción de un mejor sistema democrático
    Travis Barker, ingresado de urgencia
    Los famosos opinan de la derogación del aborto en EE UU: “Voy a renunciar a mi ciudadanía”
    Giorgio Armani: “Para mí no hay estilo sin ética”
    Roban en la casa del futbolista Ronaldo en Ibiza dinero y joyas por casi cuatro millones de dólares
    Dakota Johnson se sincera sobre el rodaje de ‘50 sombras de Grey’ y sus batallas con la escritora
    El ‘Plato’ de Harvard para que los niños coman bien: cómo ayuda a prevenir la obesidad infantil
    Serena Williams, de mazazo en mazazo
    Nadal sufre a Cerúndolo en su vuelta a Londres
    Badosa, en busca del clic que se le resiste
    ¿El éxito en ventas es sinónimo de trascendencia?
    ¿Son necesarias las escuelas de arte?
    Gustavo Petro: “Si fracaso, las tinieblas arrasarán con todo”
    América Latina gira hacia una nueva izquierda
    Francia Márquez, Marta Lucía Ramírez y ‘las niñas’
    Nuevo balance de fuerzas en un mundo en conflicto
    Biden announces increase in US military deployment in Europe
    Suntory killer: A man with expensive tastes who drew a gun against his wife
    Mummified baby woolly mammoth found in northern Canada
    Where are the extraterrestrial civilizations?
    Hikaru Nakamura: the world’s wealthiest chess player
    Letras Americanas: la actualidad literaria de un continente vista por el escritor Emiliano Monge
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Toda la actualidad científica en el boletín de Materia
    Ideas: reportajes y entrevistas para entender el mundo
    Sturgeon anuncia un nuevo referéndum de independencia en Escocia para el 19 de octubre de 2023
    Un ataque ruso a un centro comercial lleno de civiles deja al menos 18 muertos
    Talíria Petrone, una diputada negra frente al dominio blanco del poder en Brasil
    Joseph Oughourlian, presidente de PRISA: “Es el momento de mirar hacia el futuro con ilusión y ambición”
    Muere Leonardo Del Vecchio, el hombre que le puso gafas al mundo
    La imparable subida de tasas de interés pone a prueba a la economía mexicana 
    California decidirá en noviembre si eleva el derecho al aborto a la Constitución local
    Cuando la homosexualidad te obliga a vivir huyendo
    El objetivo de vacunación mundial del 70% contra la covid-19 está obsoleto
    Canetti, Cortázar, Calvino, Sabato: las cartas de Mario Muchnik desvelan la trastienda de medio siglo de literatura
    Tres camiones españoles para empaquetar los museos de Ucrania
    Del ‘Paraíso perdido’ al ciclo ‘queer’: el director del festival Grec de Barcelona, Cesc Casadesús, recomienda sus espectáculos favoritos  
    Simon Levin: “No tenemos otra opción que creer que podemos hacer lo necesario para que la humanidad sobreviva” 
    ¿Existe tratamiento contra la sífilis?
    Hallada en Canadá una cría de mamut en excepcional estado de conservación 
    El Torneo de Candidatos de ajedrez de Madrid, en directo
    Salma Paralluelo se pierde la Eurocopa 2022 por lesión y Teresa Abelleira la sustituye
    La ‘cooperativa’ de futbolistas que ganó 500.000 euros apostando a los partidos que amañaban
    Conservacionistas demuestran el uso de redes de pesca ilegales por parte de embarcaciones marroquíes en el Mediterráneo 
    El inesperado musgo luminoso que puede salvar un barrio de Vigo
    La trampa mortal del trasvase Tajo-Segura: así se ahogan corzos y jabalíes en el canal 
    Lorena Jaume-Palasí: “Crear principios éticos universales para  la inteligencia artificial es una iniciativa cosmética”
    Inteligencia artificial ¿para qué?
    Acelerando la ciencia a 314.000 billones de operaciones por segundo
    Así le compró un constructor un piso al ‘número dos’ de Rita Barberá
    El PSOE reprocha “prisas e inacción” al juez del ‘caso Púnica’ para “blindar” a Aguirre
    Un guardia civil amenaza a un policía en El Prat: “La suerte que tienes es que hay cámaras”
    ‘Iosi, el espía arrepentido’ o el terrorismo de Estado
    ‘First Class’: ¿por qué estáis todas en barcos?’, por Paloma Rando
    ‘El manglar de la publicidad en abierto’, por Jimina Sabadú
    El mejor perro del mundo es un fox terrier llamado ‘Funfair Foxhouse’ y se ha coronado en Madrid
    Federico y Mary de Dinamarca sacan a su hijo mayor de su escuela por casos de acoso escolar y abusos sexuales
    Gracias, Locomía
    Volver a la escuela tras dos años de pandemia
    La discriminación contra las minorías sexuales limita el desarrollo de Latinoamérica
    Así es el primer campo de golf de España convertido en una reserva natural
    Chanel, la vida después de Eurovisión: “No soy un títere”
    Algo sucede cuando nos vamos al campo
    América Latina gira hacia una nueva izquierda
    Orgullo y poderío de la diversidad sexual: el gran negocio de cuatro billones de dólares
    Tener casa en la playa se pone por las nubes: estos son los precios que se están pagando
    De Margaret Atwood a Neil Young: la interrupción del embarazo en la cultura norteamericana
    Viaje a la melancolía fotográfica de Javier Campano
    Una exposición contra el abandono del Sahel: “El silencio y el olvido matan”
    Por qué el sector privado es un aliado fundamental para la cooperación española
    Viaje a las Lofoten, islas de montañas, frailecillos y leyendas de troles
    El espectro de Riba de Santiuste y otras curiosas historias de castillos
    Ellos no bailaron solos: la mujer detrás de la loca historia de Locomía
    ¿Y si no fuese necesario dejar descansar las uñas entre manicuras?
    Esto no se puede emitir: la historia de 10 episodios que fueron demasiado lejos para la televisión 
    Miqui Puig: “Vengo de una estirpe sin papás ricos, tengo el miedo de dónde va a salir el dinero para los discos”
    Los efectos negativos del ‘delivery’: de la contaminación a la mala nutrición
    Ensalada de pepino, sandía y fresas
    Abengoa pedirá el preconcurso para varias filiales tras el rescate frustrado
    María del Monte: “No he estado nunca en ningún armario. Habrá quien tenga polillas, pero yo no”
    Ponte a prueba con nuestros crucigramas, sopas de letras, sudokus y juegos arcade
    Sánchez saluda a los Reyes, pasa de largo y se oye lo que le dicen Letizia y Felipe
    Rodrygo: “Tenemos un gran vestuario, somos amigos”
    ‘Los campaneros de Avilés y el algoritmo esclavista de Amazon’, por Antonio Maestre 
    

#### Impresión de los titulares internacionales 


```python
req2 = requests.get("https://elpais.com/internacional")
```


```python
type (req2)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup2 = BeautifulSoup(req2.text, 'html.parser')
```


```python
tags = soup2.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Biden anuncia un refuerzo en el despliegue militar de EE UU en Europa
    España, satisfecha por la definición de integridad territorial de la OTAN que ampara a Ceuta y Melilla 
    Los 15 minutos que salvaron a Andrii del infierno de Kremenchuk
    El cambio de postura militar en la OTAN y sus retos
    La visión de Japón en la cumbre de la OTAN
    Comienza el espectáculo
    Putin teme a la UE más que a la OTAN
    Exiliados rusos
    Turquía levanta el veto a las candidaturas de Suecia y Finlandia en Madrid
    Vídeo | Las imágenes, las anécdotas y los gestos en la cena de gala ofrecida por los Reyes
    Cumbre de la OTAN 2022 en Madrid, en directo | La OTAN aprueba su hoja de ruta para la próxima década en la que señala a Rusia como la “amenaza más significativa y directa”
    La Audiencia Nacional da carpetazo a la denuncia presentada contra Gustavo Petro
    El macrojuicio por los atentados de 2015 en París llega a su fin: los jueces preparan las condenas
    Biden y Sánchez pactan ampliar en un 50% los destructores en la base de Rota
    El Rey llama a los mandatarios de la OTAN a mantener la unidad ante un mundo “más incierto y más peligroso”
    Claves de la cumbre de la OTAN en Madrid: Rusia, ampliación y terrorismo
    Gustavo Petro: “Si fracaso, las tinieblas arrasarán con todo”
    El jefe del Ejército colombiano renuncia para evitar caminar junto a Petro en su investidura 
    Colombia hace examen de conciencia
    Una testigo clave del 6 de enero asegura que Trump sabía que la turba estaba armada y aun así la instigó a que marchara hacia el Capitolio
    El cierre de la fundición Ventanas marca un giro histórico en la política ambiental de Chile
    El Supremo de Nueva York revoca el derecho de voto en elecciones locales de 800.000 inmigrantes con papeles
    Hallada en Canadá una cría de mamut en excepcional estado de conservación 
    La pobreza y la inflación alimentan el nuevo estallido de Ecuador 
    

#### Impresión de artículos de opinión


```python
req3 = requests.get("https://elpais.com/opinion")
```


```python
type (req3)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup3 = BeautifulSoup(req3.text, 'html.parser')
```


```python
tags = soup3.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Una OTAN más europea 
    Víctimas desamparadas
    La OTAN contra el terrorismo: misión incumplida
    Por qué el algoritmo de Google no es una persona
    Simplemente fútbol
    El cambio de postura militar en la OTAN y sus retos
    Todo puede esperar cuando suena tu canción favorita
    Integridad territorial
    Mi querido doctor Sharpe
    Vitalicios
    Proteger la eutanasia
    La amenaza del ‘caso Assange’ 
    El Gobierno no tiene quien le quiera
    El Roto
    Peridis
    Flavita Banana
    Riki Blanco
    Sciammarella
    Planeta de Plástico, por Malagón
    Envía tu carta
    Un eslogan de moda: ‘low cost’
    Tragedia en la frontera con Melilla
    Derechos vulnerados   
    Opinar sin insultar
    Contra el conflicto de intereses, transparencia
    Entre los derechos de Esther López y los de los lectores
    El defensor del lector contesta
    

#### Impresión de titulares con palabras más buscadas en El País


```python
os.system("clear")
```




    1




```python
print(colored("A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:", 'blue', attrs=['bold']))
print(colored("Feminismo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "feminismo" in s]
print("\n".join(str_match))

print(colored("Igualdad", 'green', attrs=['bold']))

str_match = [s for s in resultados if "igualdad" in s]
print("\n".join(str_match))

print(colored("Mujeres", 'green', attrs=['bold']))

str_match = [s for s in resultados if "mujeres" in s]
print("\n".join(str_match))

print(colored("Mujer", 'green', attrs=['bold']))

str_match = [s for s in resultados if "mujer" in s]
print("\n".join(str_match))

print(colored("Brecha salarial", 'green', attrs=['bold']))

str_match = [s for s in resultados if "brecha salarial" in s]
print("\n".join(str_match))

print(colored("Machismo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "machismo" in s]
print("\n".join(str_match))

print(colored("Violencia", 'green', attrs=['bold']))

str_match = [s for s in resultados if "violencia" in s]
print("\n".join(str_match))

print(colored("Maltrato", 'green', attrs=['bold']))

str_match = [s for s in resultados if "maltrato" in s]
print("\n".join(str_match))

print(colored("Homicidio", 'green', attrs=['bold']))

str_match = [s for s in resultados if "homicidio" in s]
print("\n".join(str_match))

print(colored("Género", 'green', attrs=['bold']))

str_match = [s for s in resultados if "género" in s]
print("\n".join(str_match))

print(colored("Asesinato", 'green', attrs=['bold']))

str_match = [s for s in resultados if "asesinato" in s]
print("\n".join(str_match))

print(colored("Sexo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "sexo" in s]
print("\n".join(str_match))
```

    [1m[34mA continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:[0m
    [1m[32mFeminismo[0m
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    [1m[32mIgualdad[0m
    
    [1m[32mMujeres[0m
    Lecciones desde Montevideo: cómo dejar de ser un agresor de mujeres
    [1m[32mMujer[0m
    Lecciones desde Montevideo: cómo dejar de ser un agresor de mujeres
    Ellos no bailaron solos: la mujer detrás de la loca historia de Locomía
    [1m[32mBrecha salarial[0m
    
    [1m[32mMachismo[0m
    
    [1m[32mViolencia[0m
    
    [1m[32mMaltrato[0m
    
    [1m[32mHomicidio[0m
    
    [1m[32mGénero[0m
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    [1m[32mAsesinato[0m
    
    [1m[32mSexo[0m
    
    

## Código fuente


```python
import requests
import time
import csv
import re
from bs4 import BeautifulSoup
import os
import pandas as pd
from termcolor import colored

resultados = []

req = requests.get("https://resultados.elpais.com")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup = BeautifulSoup(req.text, 'html.parser')

tags = soup.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req2 = requests.get("https://elpais.com/internacional")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup2 = BeautifulSoup(req2.text, 'html.parser')

tags = soup2.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req3 = requests.get("https://elpais.com/opinion")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup3 = BeautifulSoup(req3.text, 'html.parser')

tags = soup3.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req4 = requests.get("https://elpais.com/espana/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup4 = BeautifulSoup(req4.text, 'html.parser')

tags = soup4.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req5 = requests.get("https://elpais.com/economia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup5 = BeautifulSoup(req5.text, 'html.parser')

tags = soup5.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req6 = requests.get("https://elpais.com/sociedad/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup6 = BeautifulSoup(req6.text, 'html.parser')

tags = soup6.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req7 = requests.get("https://elpais.com/educacion/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup7 = BeautifulSoup(req7.text, 'html.parser')

tags = soup7.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req8 = requests.get("https://elpais.com/clima-y-medio-ambiente/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup8 = BeautifulSoup(req8.text, 'html.parser')

tags = soup8.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req9 = requests.get("https://elpais.com/ciencia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup9 = BeautifulSoup(req9.text, 'html.parser')

tags = soup9.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req10 = requests.get("https://elpais.com/cultura/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup10 = BeautifulSoup(req10.text, 'html.parser')

tags = soup10.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req11 = requests.get("https://elpais.com/babelia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup11 = BeautifulSoup(req11.text, 'html.parser')

tags = soup11.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req12 = requests.get("https://elpais.com/deportes/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup12 = BeautifulSoup(req12.text, 'html.parser')

tags = soup12.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req13 = requests.get("https://elpais.com/tecnologia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup13 = BeautifulSoup(req13.text, 'html.parser')

tags = soup13.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req14 = requests.get("https://elpais.com/tecnologia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup14 = BeautifulSoup(req14.text, 'html.parser')

tags = soup14.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req15 = requests.get("https://elpais.com/gente/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup15 = BeautifulSoup(req15.text, 'html.parser')

tags = soup15.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req16 = requests.get("https://elpais.com/television/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup16 = BeautifulSoup(req16.text, 'html.parser')

tags = soup16.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req17 = requests.get("https://elpais.com/eps/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup17 = BeautifulSoup(req17.text, 'html.parser')

tags = soup17.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)


os.system("clear")

print(colored("A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:", 'blue', attrs=['bold']))
print(colored("Feminismo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "feminismo" in s]
print("\n".join(str_match))

print(colored("Igualdad", 'green', attrs=['bold']))

str_match = [s for s in resultados if "igualdad" in s]
print("\n".join(str_match))

print(colored("Mujeres", 'green', attrs=['bold']))

str_match = [s for s in resultados if "mujeres" in s]
print("\n".join(str_match))

print(colored("Mujer", 'green', attrs=['bold']))

str_match = [s for s in resultados if "mujer" in s]
print("\n".join(str_match))

print(colored("Brecha salarial", 'green', attrs=['bold']))

str_match = [s for s in resultados if "brecha salarial" in s]
print("\n".join(str_match))

print(colored("Machismo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "machismo" in s]
print("\n".join(str_match))

print(colored("Violencia", 'green', attrs=['bold']))

str_match = [s for s in resultados if "violencia" in s]
print("\n".join(str_match))

print(colored("Maltrato", 'green', attrs=['bold']))

str_match = [s for s in resultados if "maltrato" in s]
print("\n".join(str_match))

print(colored("Homicidio", 'green', attrs=['bold']))

str_match = [s for s in resultados if "homicidio" in s]
print("\n".join(str_match))

print(colored("Género", 'green', attrs=['bold']))

str_match = [s for s in resultados if "género" in s]
print("\n".join(str_match))

print(colored("Asesinato", 'green', attrs=['bold']))

str_match = [s for s in resultados if "asesinato" in s]
print("\n".join(str_match))

print(colored("Sexo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "sexo" in s]
print("\n".join(str_match))
```
