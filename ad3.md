# Actividad dirigida 3

Esta actividad consite en hacer un ejercicio de programación literaria aprovechando un código que hemos usado en programación con python donde realizameros *web scrapping*
    "A continuación pongo el código fuente"

## Instalar librerías

Para iniciar el web scraping, procedimos a instalar las librerías que nos ayudarían a todo el proceso.


```python
pip install requests bs4 pandas termcolor
```

    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: requests in c:\programdata\anaconda3\lib\site-packages (2.27.1)
    Requirement already satisfied: bs4 in c:\users\marliege barría\appdata\roaming\python\python39\site-packages (0.0.1)
    Requirement already satisfied: pandas in c:\programdata\anaconda3\lib\site-packages (1.4.2)
    Requirement already satisfied: termcolor in c:\users\marliege barría\appdata\roaming\python\python39\site-packages (1.1.0)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in c:\programdata\anaconda3\lib\site-packages (from requests) (1.26.9)
    Requirement already satisfied: certifi>=2017.4.17 in c:\programdata\anaconda3\lib\site-packages (from requests) (2021.10.8)
    Requirement already satisfied: idna<4,>=2.5 in c:\programdata\anaconda3\lib\site-packages (from requests) (3.3)
    Requirement already satisfied: charset-normalizer~=2.0.0 in c:\programdata\anaconda3\lib\site-packages (from requests) (2.0.4)
    Requirement already satisfied: beautifulsoup4 in c:\programdata\anaconda3\lib\site-packages (from bs4) (4.11.1)
    Requirement already satisfied: pytz>=2020.1 in c:\programdata\anaconda3\lib\site-packages (from pandas) (2021.3)
    Requirement already satisfied: python-dateutil>=2.8.1 in c:\programdata\anaconda3\lib\site-packages (from pandas) (2.8.2)
    Requirement already satisfied: numpy>=1.18.5 in c:\programdata\anaconda3\lib\site-packages (from pandas) (1.21.5)
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

Luego de haber enlazado cada una de las librerías, procedimos a importarlas para que los comandos respondan adecuadamente.


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

Luego de haber creado los objetivo o variables que trabajeremos, procedemos a la impresión del código fuente, en este caso detallaremos algunas secciones del diario El País.
Para ello seccioné cada uno de los códigos, les añadí un **type** para que devuelva el mediante el request lo que se está pidiendo en la url.
Posteriormente mediante un soup, hacemos la impresión del texto que hemos destacado en el request.
Este proceso es realizado en los códigos a continuación:

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

    López Obrador pide a Biden “audacia” con la inmigración
    Estados Unidos mata al líder del ISIS en Siria en un ataque con dron
    Las carreteras de Colombia, Bolivia y Ecuador, entre las más lentas del mundo
    Pragmatismo en Argentina
    Una mejor manera de entender la relación México-Estados Unidos
    El sueño de San Martín y Bolívar y la profecía papal
    Educación híbrida: de la emergencia al cambio
    Las nuevas imágenes del telescopio ‘James Webb’ muestran planetas gigantes y galaxias chocando a altísima velocidad
    Óscar Marín: “Variando pequeñas piezas de la corteza cerebral se generan capacidades de superhéroe”
    La ingeniera que enseña a nuestro cuerpo a autorrepararse: “Hemos regenerado piel, cartílagos y vasos sanguíneos”
    Juan Carlos Blanco: “Ahora es casi imposible encontrar un cuento sobre un lobo malo”
    Boric anuncia una ayuda de 120 dólares para 7,5 millones de personas en medio de la crisis inflacionaria
    Twitter califica de “inválida” la renuncia de Elon Musk a comprarla
    El dólar alcanza la paridad con el euro por primera vez en 20 años
    Una nueva era recesiva parece inevitable
    Miles de japoneses despiden a Shinzo Abe tras un funeral privado con aires solemnes 
    La política boliviana se “narcotiza” con acusaciones en todas las direcciones
    ‘Succession’ y ‘Ted Lasso’ lideran las nominaciones a los Emmy 2022
    Polyforum Siqueiros: el sueño imposible de un empresario español y un pintor comunista
    Pedro Sánchez anuncia impuestos a eléctricas y bancos y medidas sociales ante el golpe de la inflación en España
    El padre de una víctima de un tiroteo interrumpe a un Biden en sus horas más bajas
    Estados Unidos extiende el estatus de protección a los migrantes venezolanos
    Boris Johnson bloquea la moción de censura presentada por la oposición laborista 
    Kiev y Jersón, dos errores que marcan el curso de la guerra en Ucrania
    Un nuevo triángulo de la muerte en Michoacán: una fosa masiva resucita el horror en México
    Uber intentó recaudar impuestos de sus conductores mientras desviaba millones a sociedades opacas
    El informante de ‘Uber Files’: “La empresa estaba dispuesta a romper todas las normas”
    Documentos secretos desvelan las estrategias de Uber para implantarse en decenas de países
    “Somos esclavos de Uber”: el coste para los conductores de un modelo de negocio imposible
    Las infinitas posibilidades de un tablero de ajedrez
    “No hay pensamiento sin tiempo para pensar”
    “En el hospital, la enseñanza es una medicina más”
    “Lo dieron todo y no tuvieron a nadie”: el filme que desvela la cara más oscura de ‘Kids’
    Cómo el cine transformó a las diosas mitológicas en superheroínas
    Perder el tiempo, ganar la vida: un elogio de la distracción
    El ‘Indiana Jones del arte’ encuentra en la puerta de su casa un relicario medieval robado 
    Marilyn Monroe hizo ricos a muchos hombres mientras se empobrecía: “No tuvo ni para un funeral decente”
    La respuesta de Florence Pugh a las feroces críticas a su pecho: “Respeten los cuerpos. Maduren”
    Cómo organizar un viaje al Amazonas, el destino de los grandes exploradores
    La máxima responsable del fútbol femenino en la UEFA: “El negocio no puede ser un copiar y pegar del masculino”
    Luis León ataca, pero la etapa del Tour de Francia la gana Cort y Pogacar no suelta el amarillo
    El campeón olímpico Mo Farah revela que fue víctima de tráfico ilegal y explotación en Reino Unido
    Las tribulaciones de Cristiano Ronaldo pasan por Qatar
    Jamie Dimon, el banquero más poderoso: “Las cosas pueden ir mucho peor”
    Los 50 años de Sofia Vergara, la mujer que permitió que la encasillasen para convertirse en la actriz mejor pagada de la televisión
    La vida de Rodrigo Londoño tras el final del guerrillero Timochenko
    EL PAÍS América gana el Premio de la Asociación Mundial de Editores al mejor sitio de noticias de Latinoamérica
    Jamie Dimon, the world’s most powerful banker: ‘Things can get much worse. We are facing very problems’
    Father of shooting victim interrupts Biden’s gun safety speech 
    US extends protected status to Venezuelan migrants
    Uber forged deals with top Putin allies in failed bid to break into Russian market
    James Webb space telescope: A guide to the first full-color image
    The taboo of menopause: ‘You worry you’ll be labeled as old or incapable’
    Mar Castellanos, neurologist: ‘Stroke increasingly affects working-age people’
    Letras Americanas: la actualidad literaria de un continente vista por el escritor Emiliano Monge
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Toda la actualidad científica en el boletín de Materia
    Ideas: reportajes y entrevistas para entender el mundo
    El padre de una víctima de un tiroteo interrumpe a un Biden en sus horas más bajas
    La oposición francesa exige investigar los lazos de Macron con Uber
    El Partido Conservador endurece las normas de las primarias para acelerar la sustitución de Boris Johnson
    El dólar alcanza la paridad con el euro por primera vez en 20 años
    El aeropuerto londinense de Heathrow restringe el número de vuelos hasta septiembre 
    Uber intentó recaudar impuestos de sus conductores mientras desviaba millones de euros a sociedades opacas
    Mônica Benício: “Quiero que Lula sea presidente, pero quiero que haga políticas feministas y para la población LGTBI”
    ‘Antes de que lleguen las nubes’: una novela negra nórdica con flamenco y ‘pescaíto’ frito
    El noble y valiente jefe shawnee Tecumseh lidera la nueva incursión de libros sobre los indios norteamericanos
    Beethoven veranea por fin en Noruega
    El tabú de la menopausia: “Hay vergüenza, preocupa ser identificadas como viejas o incapaces”
    Óvulos que se agotan y declive del esperma: todo lo que ignoramos sobre fertilidad hasta el momento de querer hijos
    Rosaly Lopes, la persona que más volcanes ha descubierto: “Puede haber vida en Titán” 
    España lo tiene todo en el Mundial de hockey hierba
    Nadine Kessler, máxima responsable del fútbol femenino en la UEFA: “El negocio no puede ser un copiar y pegar del masculino”
    La Superliga, a los países contrarios a una competición cerrada: “Creen que la UEFA es solidaria, pero solo les da limosna”
    Si convence a un tercio de sus vecinos puede poner placas solares en la azotea: “El autoconsumo colectivo es imparable”
    En la lancha de los vigilantes del pulmón del Mediterráneo: “Está usted sobre una pradera de posidonia” 
    El Papa urge a los jóvenes a comer menos carne “para salvar el medio ambiente”
    La inteligencia artificial de Google es capaz de aprender como un bebé
    Las activistas que dejaron sin anuncios a la web de Steve Bannon van ahora a por Fox News
    Jorge Stolfi: “Soy catedrático de informática. Como mis colegas, sé que la tecnología de bitcoin es basura”
    El Constitucional avala que los acusados del ‘procés’ no pudieran delegar su voto parlamentario
    Los delitos de tráfico aumentan pese al descenso de la movilidad y de los muertos en carretera
    El juez ordena buscar ADN en la ropa interior de las tres niñas de Alcàsser
    Sonsoles Ónega ficha por Atresmedia 
    ‘Disculpen a Almeida, quizá estaba viendo el Orgullo por la tele’, por Paloma Rando
    ‘Un gran poder conlleva una gran corrupción’, por Jimina Sabadú
    Jennifer Lopez sufrió bloqueos y ataques de pánico por agotamiento que le hicieron cambiar sus hábitos de vida
    La DJ B Jones, de las noches en la carretera al olimpo de la música electrónica: “Ahora somos el centro de la fiesta” 
    El espectáculo (teatral) debe continuar en la alta costura de París
    El Panamá indígena busca empoderar a sus mujeres
    Volver a la escuela tras dos años de pandemia
    El restaurante madrileño en el que la cocina gaditana y la francesa se enamoraron
    ¿Dónde está exactamente el origen del mal?
    Alemanes, no tomar partido por Ucrania es ser parte. La respuesta del historiador Timothy Snyder a Jürgen Habermas
    Maneras de vivir después de muerto
    Los artesanos del coche del futuro son españoles
    Primas más altas para asegurar un mundo enloquecido
    Tristes, drogados, periféricos: la nueva literatura que refleja el dolor de los polígonos
    La ‘Safo’ de Christina Rosenvinge no convence
    Arte NFT para sacar de la cárcel a mujeres insolventes en Egipto
    Atrapados en la encrucijada migratoria de Agadez
    Cómo organizar un viaje al Amazonas, el destino de los grandes exploradores
    ‘La casa de papel’ y ‘Valeria’, guías perfectas por la ciudad de Madrid
    Infidelidad financiera, cuando lo que se oculta es el extracto bancario
    De Olivia de Havilland a Raquel Welch: el biquini estuvo solo permitido a las grandes divas
    Róisín Murphy: “Los gays entienden la opresión de las mujeres. No se detienen ante nada”
    Rebecca Makkai: “Solo los extremistas creen que no se puede escribir desde otros puntos de vista”
    Ensalada de albaricoques, queso y lechuga
    Boquerones ‘amoragaos’: la receta de Granada en la que menos es más
    El Gobierno podrá vetar la compra de inmuebles por fondos extranjeros
    Iglesias, tras los audios de Villarejo: “No es grave porque me haya hecho daño a mí, sino a uno de los pilares de la democracia”
    Ponte a prueba con nuestros crucigramas, sopas de letras, sudokus y juegos arcade
    Momentazo en el Congreso: Feijóo saluda a Garzón y ojo a lo que hace Irene Montero
    Pablo Torre convence a Xavi
    ‘Uber, el capitalismo salvaje de los que parten la pana’, por Sergio C. Fanjul
    

### Impresión de los titulares internacionales 


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

    Boris Johnson bloquea la moción de censura presentada por la oposición laborista 
    López Obrador pide a Biden “audacia” con la inmigración
    Kiev y Jersón, dos errores que marcan el curso de la guerra en Ucrania
    La guerra de Ucrania durará
    Goodbye, Boris?
    Shinzo Abe transformó y transformará Japón
    Un magnicidio inusual que hace sentir a los japoneses vulnerables 
    Populistas occidentales por el desagüe de la historia
    EE UU mata al líder del ISIS en Siria en un ataque con dron
    La oposición francesa exige investigar los lazos de Macron con Uber
    Miles de japoneses despiden a Shinzo Abe tras un funeral privado con aires solemnes 
    El preso político más famoso de Egipto cumple 100 días en huelga de hambre
    Alemania teme que el corte del gas ruso por mantenimiento del Nord Stream 1 se convierta en definitivo
    Los manifestantes se atrincheran en el palacio presidencial de Sri Lanka
    El Gobierno de Macron supera con facilidad la moción de censura de la izquierda
    López Obrador se reúne con Kamala Harris para tratar la migración en Centroamérica
    El Partido Conservador endurece las normas de las primarias para acelerar la sustitución de Boris Johnson
    La economía de Ucrania, la otra gran víctima de la guerra
    El padre de una víctima de un tiroteo interrumpe a un Biden en sus horas más bajas
    Boric anuncia una ayuda de 120 dólares para 7,5 millones de personas en medio de la crisis inflacionaria
    Estados Unidos extiende el estatus de protección a los migrantes venezolanos
    Biden y López Obrador negociarán el refuerzo de las fronteras 
    La política boliviana se “narcotiza” con acusaciones en todas las direcciones
    El padre de una víctima de un tiroteo interrumpe a un Biden en sus horas más bajas
    

###  Impresión de artículos de opinión


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

    Multa a las constructoras
    Pragmatismo en Argentina
    La buena muerte
    ¿El PSOE de antes?
    Entre líneas
    Hacerse cargo
    Preservar la cohesión social, prioridad económica
    A por todas… y a por todo
    Miguel Ángel
    Fausto en Downing Street
    Putin y el mar
    El don de la curiosidad
    Becas Ayuso: y ahora también un Ingreso Máximo Vital
    El Roto
    Peridis
    Flavita Banana
    Riki Blanco
    Sciammarella
    Planeta de Plástico, por Malagón
    Envía tu carta
    Si no hay castigo, se repetirá la jugada 
    La empresa es el nuevo dogma
    Izquierdas, derechas y la casa sin barrer
    En la calle circulan rumores
    Opinar sin insultar
    Contra el conflicto de intereses, transparencia
    El defensor del lector contesta
    

### Impresión de El País de España


```python
req4 = requests.get("https://elpais.com/espana/")
```


```python
type(req4)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup4 = BeautifulSoup(req4.text, 'html.parser')
```


```python
tags = soup4.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Sánchez anuncia impuestos a eléctricas y bancos y medidas sociales ante el golpe de la inflación
    Inflación, paro, precio de la energía: guía para entender el estado de la nación antes del debate 
    El ‘caso Esther López’, tras las huellas de un atropello mortal
    Ante la crisis, ¿gestionas o lideras?
    El almirante Cervera y el honor de España
    El Gran Retroceso
    Santa Bárbara y la cultura de la defensa
    ¿Es posible disentir de esta retórica belicista?
    El vocabulario del presidente, mirado con lupa  
    Gamarra desviste a Feijóo con el estilo Casado
    Gamarra equipara el espíritu de Ermua tras el asesinato de Miguel Ángel Blanco a la oposición al Gobierno de Sánchez
    El incendio en la comarca cacereña de Las Hurdes avanza sin control y obliga a desalojar a 400 personas
    La ola de calor entra en su fase crítica con un aviso rojo en Galicia por máximas de 42° 
    Los delitos de tráfico aumentan pese al descenso de la movilidad y de los muertos en carretera
    La policía recupera el cadáver de una mujer con signos de violencia en una alcantarilla de Málaga
    Los socios usarán el debate para exigir a Sánchez una reforma fiscal de izquierdas
    El PP de Feijóo eludió dar la batalla parlamentaria para que su líder participara 
    Sánchez anunciará medidas de protección para las clases medias
    El Gobierno y el PP cierran sin acuerdo la negociación para desbloquear el Poder Judicial 
    Un paraíso en el que avistar más de 20 especies de cetáceos
    El secreto de Fuerteventura se hace viral: la ‘playa de las palomitas’
    Un vino para triunfar entre los mileniales
    Artesanía y cultura que conquista a las ‘influencers’
    Más allá de la capital. El triunfo de la vida rural madrileña
    

### Importar la sección de economía


```python
req5 = requests.get("https://elpais.com/economia/")
```


```python
type(req5)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup5 = BeautifulSoup(req5.text, 'html.parser')
```


```python
tags = soup5.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    El dólar alcanza la paridad con el euro por primera vez en 20 años
    La banca cierra en Bolsa con una caída cercana al 5% tras el nuevo impuesto anunciado por Sánchez 
    Estas son las medidas anunciadas por Sánchez: impuesto a bancos y energéticas; abonos de Renfe gratis y complemento a las becas
    Marta Ortega en su primera junta como presidenta: “Inditex tiene aciertos y errores, pero nunca se detiene”
    Paridad inquietante
    El Supremo, contra los consumidores
    Las Bolsas y la ‘Quinta’ de Chaikovski
    Empresas grandes y sueldos diferentes
    Riesgos de recesión (y alguna luz)
    Cuatro de cada 10 municipios españoles no tienen acceso a servicios bancarios
    El aeropuerto londinense de Heathrow restringe el número de vuelos hasta septiembre 
    Los aeropuertos españoles recuperaron el 82% de los viajeros en el primer semestre
    Enagás invertirá casi 4.800 millones hasta 2030 para capear la crisis energética
    Twitter califica de “inválida e injusta” la renuncia de Elon Musk a comprarla 
    Los trabajadores siguen perdiendo poder adquisitivo: en junio su salario creció ocho puntos menos que la inflación 
    Los trabajadores de Paradores cobrarán un plus de dos millones por estar en su casa durante el confinamiento
    El préstamo pedido por un matrimonio sólo lo paga el cónyuge que lo utilizó
    Los artesanos del coche del futuro son españoles
    Primas más altas para asegurar un mundo enloquecido
    Uber intentó recaudar impuestos de sus conductores mientras desviaba millones de euros a sociedades opacas
    Jamie Dimon, el banquero más poderoso del mundo: “Los problemas económicos no son pasajeros. Las cosas pueden ir mucho peor”
    Ezentis se asoma al precipicio
    Vecinos al borde de un ataque de nervios: morosos que usan la piscina, trasteros que son despensas y ruidos diarios
    Caso Laso: ¿Me pueden echar tras sufrir un infarto?
    Remite el riesgo de estanflación
    El Ejecutivo acortará a tres meses el plazo para autorizar inversiones extranjeras
    Enagas confía en que España puede afrontar un corte total del suministro ruso
    Los caseros estudian fórmulas para reclamar al Estado 1.700 millones por el tope al IPC
    Cada 32 horas un nuevo municipio se queda sin oficina bancaria
    El préstamo pedido por un matrimonio sólo lo paga el cónyuge que lo utilizó
    No se puede desheredar a un familiar con el que no se tiene relación, según el Supremo
    Líos en la piscina comunitaria: normas y sentencias para un chapuzón seguro
    Música que transforma vidas y esboza futuros
    El futuro probable de una sociedad insostenible
    Francisco Javier Blasco: “Llevamos años sin mejorar la eficacia de las políticas activas de empleo”
    La hora del bienestar corporativo
    Cancerberos del bienestar de la empresa
    Cómo garantizar la seguridad en un mundo de amenazas híbridas
    ¿Cuáles son los dilemas éticos del uso de la inteligencia artificial?
    Las aventuras de un par de calcetines que dan empleo a todo un pueblo
    Cultura financiera como punto de partida para volver a empezar
    ¿Puede convertirse España en una de las potencias logísticas del futuro?
    Por qué digitalizar una pyme aporta más empleo
    ‘Coopetir’: la actitud DFactory
    Así serán las ciudades de la (nueva) última milla
    Cinco errores habituales al digitalizar un negocio 
    PERTE Agroalimentario: ¿cómo acceder a los fondos europeos?
    Fondos soberanos: ¿Cómo funcionan las cajas fuertes de los estados más ricos?
    ¿Crisis de deuda mundial a la vista?
    El método Muñoz para triunfar en cada reto que se propone
    Gloria Ramos, cuando el afán de superación acaba en la alfombra roja 
    Ocho ‘startups’ innovadoras con nombre propio
    Hotmart y su plataforma 360 para creadores de contenidos
    

### Imprimir sección de sociedad


```python
req6 = requests.get("https://elpais.com/sociedad/")
```


```python
type(req6)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup6 = BeautifulSoup(req6.text, 'html.parser')
```


```python
tags = soup6.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Absuelto un conductor que se dio a la fuga tras arrollar a un ciclista: “Te sientes atropellado por el coche y la justicia”
    Europa amplía la vacunación contra la viruela del mono a las personas con prácticas sexuales de riesgo ante el alza de casos
    El deporte ya no es solo deporte: el sector atrae todo tipo de perfiles profesionales
    Educación híbrida: de la emergencia a la transformación 
    Jóvenes atrapados en el efecto cicatriz
    La libertad guiando (dicen) a la escuela
    El control del cuerpo de las mujeres
    El Tribunal Supremo avala el indulto parcial de Juana Rivas
    Los sanfermines de este año registran su primera denuncia por violación
    Juan Carlos Blanco: “Ahora es casi imposible encontrar un cuento sobre un lobo malo”
    Si convence a un tercio de sus vecinos puede poner placas solares en la azotea: “El autoconsumo colectivo es imparable”
    Rusia perseguirá la difusión pública de manifestaciones de afecto entre homosexuales y de apoyo al colectivo LGTBI
    Gabriela Ossenbach, experta en manuales escolares: “Con los libros de texto se puede crear fácilmente alarma social, pero no está justificada”
    El Papa urge a los jóvenes a comer menos carne “para salvar el medio ambiente”
    Madres solas con menos de mil euros al mes: cuando las vacaciones no son una opción
    Mônica Benício: “Quiero que Lula sea presidente, pero quiero que haga políticas feministas y para la población LGTBI”
    Un paso atrás, dos adelante: el avance de los derechos LGTBI en la antigua Yugoslavia
    La escalada vertiginosa de notas en Bachillerato: los sobresalientes de los que llegan a Selectividad se doblan en seis años
    Residuos para mover el mundo
    Se buscan profesionales en economía circular
    ¿Por qué hablar de VIH en el Orgullo y no en los sanfermines?
    Mitos, falsedades, bulos y realidades sobre el VIH 40 años después
    Qué son las evidencias científicas y por qué están revolucionando la educación
    Munic, el joven redimido por el trap
    El tremendo peso de la obesidad en España
    Interactivo | Los 14 cambios en los aeropuertos españoles que no ves y que ya están ocurriendo
    Encontrar empleo pese a los obstáculos. Por dónde empezar la búsqueda
    La fórmula de Carboneros para evitar el éxodo rural: trabajar cuidando a los vecinos 
    Consejos y cuidados para el primer verano con un gatito o un perrito
    ¿Qué tienen en común perros y gatos cuando son cachorros?
    La guía definitiva para alimentarnos mejor (y cuidar nuestra salud y la del planeta)
    El metro como refugio. De los andenes de Madrid en 1936 a los de Kiev en 2022
    La salud mental de los refugiados: cómo abrirse para cerrar las heridas
    Yogures con menos azúcar, paso firme hacia la alimentación infantil del futuro
    Conectada con el mercado laboral y tecnológica: así es la universidad del presente
    Así es la formación más abierta y flexible, a prueba de crisis
    

### Imprimir sección de educación


```python
req7 = requests.get("https://elpais.com/educacion/")
```


```python
type (req7)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup7 = BeautifulSoup(req7.text, 'html.parser')

```


```python
tags = soup7.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Educación híbrida: de la emergencia a la transformación 
    El deporte ya no es solo deporte: el sector atrae todo tipo de perfiles profesionales
    Gabriela Ossenbach, experta en manuales escolares: “Con los libros de texto se puede crear fácilmente alarma social, pero no está justificada”
    La libertad guiando (dicen) a la escuela
    Intento de rebelión de los directores de primaria de Cataluña por los nuevos horarios de septiembre
    La escalada vertiginosa de notas en Bachillerato: los sobresalientes de los que llegan a Selectividad se doblan en seis años
    El 60% del dinero destinado a becas educativas en Madrid será para los centros privados
    El 60% de los universitarios no se ve preparado para un mercado laboral que no encuentra los perfiles necesarios  
    ¿Cómo se cierra un colegio público?
    ¿Hay que obligar a los niños a hacer deberes en verano? Los expertos recomiendan actividades que no se parezcan a las tareas escolares
    Los sindicatos educativos catalanes convocan huelga el 7 de septiembre, primer día de curso en los institutos, y el 28
    Sin currículos
    La escuela concertada ante las desigualdades: el debate pendiente
    La equidad frente a las políticas educativas de privatización en Andalucía
    No hay lunes al sol en la Universidad
    El nuevo sistema para evaluar los conocimientos digitales de los profesores valdrá en toda España
    Ofrecer comedor gratis en todos los colegios públicos es “alcanzable y urgente”: costaría 1.664 millones al año, según la ONG Educo  
    Una fórmula para que la escuela pública compita mejor con la concertada
    La pérdida de alumnos por el descenso de la natalidad está afectando con más fuerza a la escuela pública que a la concertada
    La escalada vertiginosa de notas en Bachillerato: los sobresalientes de los que llegan a Selectividad se doblan en seis años
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    El techo de cristal del grado medio de FP: candidatos demasiado preparados se quedan con los puestos
    La implantación del nuevo Bachillerato general fracasa pese a su demanda potencial: “Creímos que lo pedirían seis alumnos y lo han hecho 27”
    Toni Solano, director de instituto: “Veo mal a los niños, necesitan muchísima ayuda”
    Una historia en la que caben Alaska, García Lorca, Suárez y Popper: la Universidad Internacional Menéndez Pelayo cumple 90 años 
    Subirats reinterpreta la ley de Universidades: freno a la precariedad, facilidades para los alumnos extranjeros y ciencia abierta
    Las universitarias desertan del grado de Matemáticas ahora que tiene pleno empleo. ¿Por qué?
    Golpe a la temporalidad en las universidades: 25.000 profesores asociados serán indefinidos a tiempo parcial
    Las infinitas posibilidades de un tablero de ajedrez
    “No hay pensamiento sin tiempo para pensar”
    “En el hospital, la enseñanza es una medicina más”
    

### Imprimir sección de clima y medio ambiente


```python
req8 = requests.get("https://elpais.com/clima-y-medio-ambiente/")
```


```python
type (req8)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup8 = BeautifulSoup(req8.text, 'html.parser')
```


```python
tags = soup8.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Las claves de una ola de calor que desafía todos los récords de intensidad, extensión y duración
    Absuelto un conductor que se dio a la fuga tras arrollar a un ciclista: “Te sientes atropellado por el coche y la justicia”
    El incendio en la comarca cacereña de Las Hurdes avanza sin control y obliga a desalojar a 400 personas
    Juan Carlos Blanco: “Ahora es casi imposible encontrar un cuento sobre un lobo malo”
    Si convence a un tercio de sus vecinos puede poner placas solares en la azotea: “El autoconsumo colectivo es imparable”
    El Papa urge a los jóvenes a comer menos carne “para salvar el medio ambiente”
    Segunda ola calor del verano: al menos cuatro días con máximas de hasta 46° y noches tórridas a más de 25°
    Europa baraja eliminar el biodiésel de soja y palma para frenar la deforestación tropical
    Portugal se enfrenta a una oleada de incendios que han afectado ya a 6.400 hectáreas
    En la lancha de los vigilantes del pulmón del Mediterráneo: “Está usted sobre una pradera de posidonia” 
    La sobrexplotación amenaza a las especies silvestres de las que dependen miles de millones de personas en el mundo
    Un plan de retirada  
    Crisis energética y precios del carbono
    La lección del martín pescador para afrontar la crisis ecológica
    Estocolmo+50: mirar atrás para tomar impulso
    Ríos imposibles: las 171.000 barreras que rompen el curso de agua en España
    La UE abraza las renovables para romper la dependencia de Rusia
    La lucha en un pueblo de Teruel para salvar su última montaña
    ¿Qué aire respiran los niños de Madrid y Barcelona? En el 46% de los colegios se supera la contaminación permitida
    Las infinitas posibilidades de un tablero de ajedrez
    “No hay pensamiento sin tiempo para pensar”
    “En el hospital, la enseñanza es una medicina más”
    

### Imprimir la sección de ciencia


```python
req9 = requests.get("https://elpais.com/ciencia/")
```


```python
type(req9)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup9 = BeautifulSoup(req9.text, 'html.parser')

```


```python
tags = soup9.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Las nuevas imágenes del telescopio ‘James Webb’ muestran planetas gigantes, estrellas agonizantes y galaxias chocando a altísima velocidad
    No son estrellas sino galaxias: guía rápida de la primera foto del telescopio ‘James Webb’
    El telescopio ‘James Webb’ desvela miles de galaxias en el universo profundo, en su primera imagen a todo color
    Óscar Marín, neurocientífico: “Variando pequeñas piezas de la corteza cerebral se generan capacidades de superhéroe”
    La ingeniera que enseña a nuestro cuerpo a autorrepararse: “Hemos regenerado piel, cartílagos y vasos sanguíneos, pero todavía tenemos que hacer más”
    El ‘James Webb’ se prepara para su gran hito: las primeras imágenes
    El tabú de la menopausia: “Hay vergüenza, preocupa ser identificadas como viejas o incapaces”
    Mar Castellanos, neuróloga: “El ictus afecta cada vez más a personas en edad laboral. Las enfermedades cardiovasculares son una epidemia”
    ¿Es la consciencia una ilusión intrascendente?
    Óvulos que se agotan y declive del esperma: todo lo que ignoramos sobre fertilidad hasta el momento de querer hijos
    Hallada en Atapuerca la cara del humano más antiguo de Europa
    El humano más antiguo de Europa: prehistoria que hace historia
    Rosaly Lopes, la persona que más volcanes ha descubierto: “Puede haber vida en Titán” 
    Una cena conflictiva
    ‘Meraxes gigas’: descubierta en la Patagonia argentina una nueva especie de dinosaurio carnívoro gigante
    La cola vestigial, el apéndice oculto del hombre que venció a Napoleón en Waterloo
    ¿Dónde hay civilizaciones extraterrestres?
    Las mentes humanas detrás de las mentes artificiales
    Matemáticas para describir los remolinos, los taxis del océano
    Reaparece la tesis de María Wonenburger, la pionera matemática española que permaneció décadas en el olvido
    Técnicas criptográficas que se fundamentan en lo impredecible
    Alrededor de la mesa
    Fracciones egipcias
    El problema del huerto
    La cola vestigial, el apéndice oculto del hombre que venció a Napoleón en Waterloo
    Molinos y gigantes, adelantos tecnológicos y el síndrome bicicleta
    El síndrome del hombre lobo y la realidad lógica de su fábula
    La locura como juego; más allá del Quijote y de las novelas de Pérez Galdós
    El andar del borracho, las huellas del azar y el juego de dados en algunos libros malditos
    ¿Son mejores las hormonas bioidénticas?
    ¿Qué surgió antes, el ARN o el ADN?
    ¿Por qué se sabe que los núcleos de la Tierra rotan?
    ¿Qué son los mini reactores nucleares?
    Invitados indeseables por Navidad: el muérdago y otras plagas que evitar durante las fiestas
    Las ‘apps’ nutricionales o cómo comer bien no debería depender de uno mismo
    Malnutrición invisible: el impacto de la pobreza en la salud infantil
    El óxido de etileno, la sustancia cancerígena que ha obligado a retirar miles de alimentos en la UE
    Que no te líen con los ingredientes: aceites y grasas de mala calidad nutricional
    

### Imprimir la sección de cultura


```python
req10 = requests.get("https://elpais.com/cultura/")
```


```python
type(req10)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup10 = BeautifulSoup(req10.text, 'html.parser')
```


```python
tags = soup10.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    ‘Antes de que lleguen las nubes’: una novela negra nórdica con flamenco y ‘pescaíto’ frito
    El ‘Indiana Jones del arte’ encuentra en la puerta de su casa un relicario medieval robado 
    Muere el exministro José Guirao, referente de la gestión cultural en España
    Fallecimiento de José Guirao: Con las alas de la cultura
    El libro que vendrá
    Muerte de José Guirao: Poner nombre a los árboles 		 
    Fallecimiento de José Guirao: A tu sonrisa, Pepe
    Los límites del cine estallan en Tabakalera
    El Prado se inventa un paseo entre las estrellas
    Nuevo urbanismo cívico y digital
    El Gobierno pone en marcha la creación de la Oficina de Derechos de Autor
    Un homenaje a Ucrania, una pianista legendaria y un ‘tour de force’ violinístico culminan el Festival de Música y Danza 
    El noble y valiente jefe shawnee Tecumseh lidera la nueva incursión de libros sobre los indios norteamericanos
    Beethoven veranea por fin en Noruega
    Descubierta una desconocida ciudad romana con “edificios de proporciones monumentales” al pie de los Pirineos
    Huracán Nathy Peluso cierra a lo grande el Mad Cool de la tortuosa vuelta a casa
    Blanca Berlín: “Hay más divismo entre los fotógrafos que empiezan”
    ‘Outlander’, la historia de amor de 200 años, prepara en España su recta final
    J Balvin y su buena “vibra” llegan para quedarse al Bilbao BBK Live
    Florence Welch ejerce de suma sacerdotisa del amor en una comparecencia efectista y apoteósica en Mad Cool 
    Cuándo un gallego te dice que sí, aunque esté pensando que no. La retranca gallega y otros misterios que descubrir en el Camino Inglés
    El último atardecer de Europa se ve solo desde este lugar. Un viaje hacia el infinito por el Camino de Fisterra-Muxía
    Lorca, en la ciudad al margen
    El Pirineo oscense, para entrar a vivir
    Toda la lectura del verano, en el bolsillo
    Longsellers: los libros más vendidos a lo largo de la historia
    Libros para descubrir el mundo recomendados por Benjamín Prado
    El exilio republicano en el Museo Reina Sofía
    'La fotógrafa de Monte Veritá'
    'KLIMT. La experiencia inmersiva'
    'Nabucco' desde un palco del Teatro Real
    El sexto encierro de San Fermín 2022, en imágenes
    Cinco heridos, uno de ellos por asta, en el rápido y emocionante sexto encierro de San Fermín 
    Un torero de Pamplona
    Muy peligroso y emocionante quinto encierro de San Fermín con los toros de Cebada Gago
    

### Imprimir sección de babelia


```python
req11 = requests.get("https://elpais.com/babelia/")
```


```python
type(req11)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup11 = BeautifulSoup(req11.text, 'html.parser')
```


```python
tags = soup11.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Cómo el cine transformó a las diosas mitológicas en superheroínas
    Tristes, drogados, periféricos: la nueva literatura que refleja el dolor de los polígonos
    La fuga de Siberia de Trotsky, la revelación de Marta D. Riezu y otros libros de la semana
    El desvío experimental de Perfume Genius, los salmos de Nick Cave y otros discos del mes
    Jardines secretos en la jungla de asfalto: cómo resistir a la especulación plantando un árbol
    Los nuevos diaristas son vendedores de vidas
    La ‘Safo’ de Christina Rosenvinge no convence
    La gran música eleva a una compañía de danza inmadura
    Trampantojo: De veraneo
    ‘Agua y jabón’: más que un libro, una constelación de genialidades
    Ayn Rand, ‘rednecks’ e inclusividad forzada: el mundo virtual como escenario político
    Un clavo quita otro, quizás
    Músicas ocultas
    Lo que siento (no se olviden de Ucrania) 
    No eran marcianos, eran humanos
    ‘La máquina de proyectar sueños’, un retorno a la infancia delicioso y temible
    ‘Veinte años de Sol’ o cómo olvidar el pasado con un implante en el cerebro
    ‘La fuga de Siberia en un trineo de renos’, de Trotsky: aventuras de un comunista en plena huida 
    ‘Magallanes & Co.’, los preparativos y aventuras de la primera vuelta al mundo
    Silvia Agüero: “De no ser escritora habría sido vendedora ambulante”
    Antoni Muntadas: “Supe que me dedicaría al arte cuando dejé de pintar”
    Manuel Estrada: “Me agrada que una portada guste más después de leer el libro”
    Óscar Esquivias: “No hace falta ser creyente para leer la Biblia”
    Amelia Castilla: “Los ritos nos ayudan a hacer viable el trance de la muerte”
    

### Imprimir sección de deportes


```python
req12 = requests.get("https://elpais.com/deportes/")
```


```python
type(req12)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup12 = BeautifulSoup(req12.text, 'html.parser')
```


```python
tags = soup12.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Luis León ataca, pero la etapa del Tour de Francia la gana Cort y Pogacar no suelta el amarillo
    El campeón olímpico Mo Farah revela que fue víctima de tráfico ilegal y explotación en Reino Unido
    Alemania mide a España en la Eurocopa 
    Las tribulaciones de Cristiano Ronaldo pasan por Qatar  
    Cuánto tarda en hervir un Tour
    El tenis es, ante todo, repetición
    El desorden es la baza de Kyrgios
    El viaje de Jon Rahm a Saint Andrews: de la furgoneta a Seve
    La Superliga, a los países contrarios a una competición cerrada: “Creen que la UEFA es solidaria, pero solo les da limosna”
    Nadine Kessler, máxima responsable del fútbol femenino en la UEFA: “El negocio no puede ser un copiar y pegar del masculino”
    El Tour de Francia 2022 es el más rápido de la historia gracias a la aerodinámica
    España lo tiene todo en el Mundial de hockey hierba
    Inglaterra tritura (8-0) a Noruega en una jornada triunfal en Brighton
    Gareth Bale, tras su llegada al LAFC: “Mi objetivo es ganar un campeonato”
    Londres reestimula a Sir Novak Djokovic
    Djokovic: “Solo necesitaba tiempo para despejar la tormenta”
    El pelotón está sano: todas las PCR del Tour de Francia han dado resultado negativo
    El granítico Djokovic detiene a Kyrgios y eleva en Wimbledon su 21º grande
    El equilibrio de Jordi Cruyff
    Severiano Ballesteros, el inglés
    “Si no tenemos en quién mirarnos es muy difícil saber qué queremos ser”
    “Nunca acepto un no por respuesta”
    La nadadora que dejó de competir para hacer campeones de básquet
    Crónica de dos ciudades moldeadas por la misma pasión 
    Guélfand reina en León por 2º año seguido, a los 54, tras más de cuatro horas trepidantes
    El tenis es, ante todo, repetición
    El granítico Djokovic detiene a Kyrgios y eleva en Wimbledon su 21º grande
    Cuando la memoria se enreda
    Reacciones de la final de Wimbledon | Djokovic, tras igualar los siete títulos de Sampras: “Siempre soñé con jugar aquí. Ganarlo es un orgullo”
    La final de Wimbledon 2022 entre Djokovic y Kyrgios, en imágenes
    Bob Jungels saca provecho de la fuga y gana la novena etapa del Tour de Francia
    Leclerc gana sobrado y Sainz sale quemado en el Gran Premio de Austria
    

### Imprimir sección de tecnología


```python
req13 = requests.get("https://elpais.com/tecnologia/")
```


```python
type(req13)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup13 = BeautifulSoup(req13.text, 'html.parser')
```


```python
tags = soup13.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Google News está de vuelta en España: qué es y cómo exprimirlo al máximo
    Dialexis (‘mater ex machina’)
    La ingeniera que enseña a nuestro cuerpo a autorrepararse: “Hemos regenerado piel, cartílagos y vasos sanguíneos, pero todavía tenemos que hacer más”
    La inteligencia artificial de Google es capaz de aprender como un bebé
    Las activistas que dejaron sin anuncios a la web de Steve Bannon van ahora a por Fox News
    “¿Quieres cobrar tu salario en streaming?” Por qué los proyectos cripto son tan difíciles de entender
    El misterio de la carta del soldado alemán
    El porqué de los desafíos criptográficos: conocerte a ti mismo, conocer a tu enemigo
    Con el relax del verano se acentúan los peligros cibernéticos: así puede protegerse durante las vacaciones
    Meta presenta un traductor capaz de operar en tiempo real con 200 idiomas
    “Soy catedrático de informática. Como mis colegas, sé que la tecnología de bitcoin es basura”
    El sector biotecnológico supera las cifras de 2020 y capta 180 millones de euros de inversión privada
    Las mentes humanas detrás de las mentes artificiales
    El juego de la técnica
    Daniel Innerarity: “Los algoritmos son conservadores y nuestra libertad depende de que nos dejen ser imprevisibles”
    En defensa de la procrastinación. Elogio del tiempo perdido (frente al que las redes te roban)
    Instagram, el mejor de los mundos posibles
    Del terrorismo youtuber al influencer rabioso: el odio inunda la red
    Cronodiversidad. ¿Por qué el tiempo cada vez va más rápido?
    El impacto de la tecnología en la hostelería: de la comanda digital al pago con código QR
    Herramientas que ayudan a crecer a las empresas (más allá de los pagos)
    Cinco razones por las que este ‘smartphone’ es sencillamente tentador
    La cámara de este ‘smartphone’ es pura magia
    Por qué los nuevos coches ya no los diseñarán las personas
    Un campus de programación para adquirir todas las habilidades ‘tech’
    

### Imprimir la sección de gente


```python
req15 = requests.get("https://elpais.com/gente/")
```


```python
type(req15)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup15 = BeautifulSoup(req15.text, 'html.parser')
```


```python
tags = soup15.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    La DJ B Jones, de las noches en la carretera al olimpo de la música electrónica: “Ahora somos el centro de la fiesta” 
    Marilyn Monroe hizo ricos a muchos hombres mientras se empobrecía: “No tuvo ni para un funeral decente”
    Pippa Middleton da a luz a su tercer hijo, una niña
    Huertos urbanos: siete errores de principiante y cómo evitarlos 
    Jennifer Lopez sufrió bloqueos y ataques de pánico por agotamiento que le hicieron cambiar sus hábitos de vida
    10 accesorios de piscina para no salir de su perímetro 24/7
    De Kate Middleton a Tom Cruise: los famosos llenan las gradas de Wimbledon, en imágenes
    Espectáculo, lujo y fantasía: la Alta Moda de Dolce & Gabbana lo apuesta todo al escapismo
    Los 50 años de Sofia Vergara, la mujer que permitió que la encasillasen para convertirse en la actriz mejor pagada de la televisión
    La guerra no estropea las vacaciones de los superricos rusos: vetados en la Costa Azul, pero bienvenidos en Dubái y Turquía
    Teresa Helbig: “Hubiera matado por vestir a Lola Flores”
    Hotel Piet Hein Eek: arte, buen gusto y pasión por el detalle en Eindhoven 
    El Baile de la Rosa vuelve a llenar Mónaco de glamur y famosos tras dos años de parón
    El espectáculo (teatral) debe continuar en la alta costura de París
    Realismo, entretenimiento y democracia: la alta costura se deshace por fin de sus estereotipos en París
    Nostalgia ‘retro’, punto multicolor y otras pistas para vestir este verano
    La dictadura de la perfección, misoginia y Jeffrey Epstein: los ángeles y demonios de Victoria’s Secret
    Dios y diamantes: lo que Kendrick Lamar nos quiso decir a través de su corona de espinas
    La cocinera que trasladó las flores del jarrón al plato
    En verano, el mejor queso del mundo se hace helado
    El placer de lo rancio y otros gustos y aromas que recuerdan la niñez
    Trece aperitivos
    

### Imprimir sección de televisión


```python
req16 = requests.get("https://elpais.com/television/")
```


```python
type(req16)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup16 = BeautifulSoup(req16.text, 'html.parser')

```


```python
tags = soup16.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    ‘Succession’ y ‘Ted Lasso’ lideran las nominaciones a los Emmy 2022
    El secreto de ‘Atrápame si puedes’, el concurso de Aragón TV que tiene más éxito que ‘Pasapalabra’
    Sonsoles Ónega ficha por Atresmedia 
    Disculpen a Almeida, quizá estaba viendo el Orgullo por la tele
    Un gran poder conlleva una gran corrupción
    La guerra de los selfis
    Menos mal que quedan los libros
    Cine y series: los datos prueban que no son universos tan conectados como parece
    ‘The Janes’: la red clandestina de mujeres que practicaba abortos ilegales en el Estados Unidos de los años sesenta
    Carlos Fernández: “Netflix quiere ser de mayor una televisión en abierto, pero de pago” 
    Muere a los 79 años Tony Sirico, Paulie en ‘Los Soprano’
    ‘Encerrado con el diablo’: Dennis Lehane busca en el fondo del alma humana
    ‘La noche más larga’ y ‘La lista final’: palomitas sin sabor para el verano
    Los dilemas de ‘La firma de Dios’: ¿y si el virus detrás de una pandemia tuviera conciencia y voluntad propia?
    Arturo Valls pasa de presentador a recluso por rebasar los límites del humor en ‘Dos años y un día’
    Entre novedades y apuestas de bajo riesgo: así es el verano en la televisión en abierto
    EGM 2022: La SER cierra temporada de nuevo como la radio más escuchada
    ¿Qué ver hoy en TV? Martes 12 de julio de 2022
    Nueve capítulos para recordar ‘The Wire’ en su 20º aniversario
    Harry Palmer: el tercer vértice del mágico triángulo de espías británicos
    Las series de junio de 2022: ‘The Boys’ en Amazon Prime Video; ‘Peaky Blinders’ en Netflix y otras
    La fuerza acompaña a ‘Obi-Wan Kenobi’, una serie deslumbrante
    

### Impresión de sección eps


```python
req17 = requests.get("https://elpais.com/eps/")
```


```python
type(req17)
```




    requests.models.Response




```python
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup17 = BeautifulSoup(req17.text, 'html.parser')
```


```python
tags = soup17.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Andaluz no: ‘Andalûh’
    Carme Elías: “Me siento más ligera que nunca, como si la vida me hubiera preparado para este momento”
    El resurgir del turismo
    Orgullo con todas las letras
    El restaurante madrileño en el que la cocina gaditana y la francesa se enamoraron
    ¿Dónde está exactamente el origen del mal?
    Las heridas abiertas de la infancia en Irak
    Pietro Beccari: “El desfile de Sevilla es uno de los mejores, si no el mejor, que ha hecho Maria Grazia Chiuri en Dior”
    La cocinera que trasladó las flores del jarrón al plato
    El hombre que persigue la gaita más antigua del mundo
    La uva más denostada de  Castilla-La Mancha resurge de sus cenizas
    La rebelión de las cocineras de España: “Hay mujeres, falta reconocimiento”
    En busca de la huella de Camarón de la Isla, leyenda viva del flamenco
    Kia Niro: cambio de imagen y tecnología a la carta
    El engaño a los ojos
    Reír a lágrima viva
    Las fiestas de la sangre
    Libros sin Feria
    Harina enriquecida para acabar con el “hambre oculta”
    Lugares de esperanza para salvar los océanos
    Los guardianes del clima que llevan medio siglo leyendo las advertencias de los glaciares
    Epidemia de violencia: claves del negocio de las armas en Estados Unidos
    Los ejecutivos voladores y la ética medioambiental
    Ibiza, entre la noche desenfrenada y el turismo tranquilo 
    Luz Casal: “Tengo el alma rockera. Nada ha doblegado mi rebeldía”
    Rashid Johnson: “Los pensadores y creadores negros estamos cansados de que nos nieguen un espacio autónomo”
    Sergio Hernández: “En el mundo, la gente ya no quiere verdades, quiere mentiras”
    Elvira Sastre: “No hay que perdonarlo todo”
    La trinidad del taco perfecto: “Buena tortilla, delicioso relleno y una salsa sabrosa”
    La casa de Nina Urgell Cloquell, un piso en el que las paredes hablan
    Garbanzos verdes y puchero
    Bikôkô y Julio Peña, dos estrellas en ebullición  
    Cuando Chufy encontró a Rossy: dos amigas, una isla y una colección de moda
    República Dominicana, donde la vida fluye por el río infinito
    Retrato Robot 
    Ilusiones hipnóticas
    El poder del hormigón
    ‘Fantasías en el Prado’, por Alberto García-Alix
    

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
    La escuela concertada ante las desigualdades: el debate pendiente
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    [1m[32mMujeres[0m
    El Panamá indígena busca empoderar a sus mujeres
    Arte NFT para sacar de la cárcel a mujeres insolventes en Egipto
    Róisín Murphy: “Los gays entienden la opresión de las mujeres. No se detienen ante nada”
    El control del cuerpo de las mujeres
    ‘The Janes’: la red clandestina de mujeres que practicaba abortos ilegales en el Estados Unidos de los años sesenta
    La rebelión de las cocineras de España: “Hay mujeres, falta reconocimiento”
    [1m[32mMujer[0m
    Los 50 años de Sofia Vergara, la mujer que permitió que la encasillasen para convertirse en la actriz mejor pagada de la televisión
    El Panamá indígena busca empoderar a sus mujeres
    Arte NFT para sacar de la cárcel a mujeres insolventes en Egipto
    Róisín Murphy: “Los gays entienden la opresión de las mujeres. No se detienen ante nada”
    La policía recupera el cadáver de una mujer con signos de violencia en una alcantarilla de Málaga
    El control del cuerpo de las mujeres
    Los 50 años de Sofia Vergara, la mujer que permitió que la encasillasen para convertirse en la actriz mejor pagada de la televisión
    ‘The Janes’: la red clandestina de mujeres que practicaba abortos ilegales en el Estados Unidos de los años sesenta
    La rebelión de las cocineras de España: “Hay mujeres, falta reconocimiento”
    [1m[32mBrecha salarial[0m
    
    [1m[32mMachismo[0m
    
    [1m[32mViolencia[0m
    La policía recupera el cadáver de una mujer con signos de violencia en una alcantarilla de Málaga
    Epidemia de violencia: claves del negocio de las armas en Estados Unidos
    [1m[32mMaltrato[0m
    
    [1m[32mHomicidio[0m
    
    [1m[32mGénero[0m
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    [1m[32mAsesinato[0m
    Gamarra equipara el espíritu de Ermua tras el asesinato de Miguel Ángel Blanco a la oposición al Gobierno de Sánchez
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
