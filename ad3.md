# Actividad dirigida 3

Esta actividad consite en hacer un ejercicio de programación literaria aprovechando un código que hemos usado en programación con python, donde realizameros *web scrapping*
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

    Boris Johnson dimite
    Johnson reúne al nuevo gabinete tras anunciar su dimisión
    ¿Cómo se elige un nuevo líder conservador?
    Populistas por el desagüe de la historia
    Vargas Llosa, el equivocado eres tú
    La baloncestista Brittney Griner se declara culpable de posesión de drogas en Rusia
    Deriva reaccionaria en Estados Unidos
    El eterno retorno de lo mismo
    Dios y la carne
    Deja quieta la comida
    ‘Meraxes gigas’: descubierta en Argentina una nueva especie de dinosaurio carnívoro gigante
    Vladimir Padrino, el eterno ministro chavista aliado de Rusia
    La posibilidad de un cambio de Gobierno en Brasil dispara la depredación en la Amazonia
    El enorme desafío que lastra a la economía Argentina
    El abogado del expresidente mexicano Peña Nieto compró un piso de megalujo mientras estaba siendo investigado por blanqueo
    Marcos López Hoyos, inmunólogo: “Deberíamos usar mascarillas en interiores y comer en terrazas”
    La frontera sur de Estaados Unidos se calienta días antes de la visita de López Obrador a Biden
    Apple asegura que el software espía Pegasus ya no podrá entrar en sus teléfonos
    La cola vestigial, el apéndice oculto del hombre que venció a Napoleón
    Haití, sin presidente y sin Estado a un año del asesinato de Jovenel Moïse
    La guerra de los drones se vuelve contra Hezbolá
    La agenda de la NASA para volver a la Luna (y quedarse)
    La guerra en Ucrania impulsa el perfil de Polonia
    EL PAÍS América gana el Premio de la Asociación Mundial de Editores al mejor sitio de noticias de Latinoamérica
    “No hay pensamiento sin tiempo para pensar”
    “En el hospital, la enseñanza es una medicina más”
    Un alegato por la paz y la cultura
    Muere el actor James Caan, célebre por encarnar a Sonny Corleone en ‘El padrino’, a los 82 años
    Qué une a Leonardo da Vinci y a Susan Sontag: una enciclopedia de genios
    La tragedia de la redada masiva de judíos en París, a través de la mirada de Cabu
    El golazo literario de Roberto Santiago con ‘Los futbolísimos’
    Con R de Reinona y A de Apoteósico: Rosalía inicia su gira mundial
    Qué tiene Harry Styles que no tuvieron los demás para terminar con la maldición de la ‘boy band’
    Elon Musk tuvo gemelos en secreto con una ejecutiva de una de sus empresas
    Por qué es importante conocer tu personalidad erótica
    Qué ver en Washington, la ciudad donde casi todo es gratis
    Aló Comidista: “¿Tomar gazpacho es un pecado nutricional?”
    Nadal confirma que jugará contra Kyrgios en Wimbledon
    Las jugadoras de Inglaterra piden a Nike cambiar el color del pantalón por la regla
    El Barcelona espera por Lewandowski mientras presenta a Christensen
    La entrega de la nueva Constitución sella el inicio de una nueva era en Chile
    Francisco de Roux: “Si no se acaba con el narco, Colombia no tendrá paz”
    La economía mundial se desinfla: así es la crisis que viene
    Gilda Love, la transformista de 97 años que sobrevivió a todo
    UK Prime Minister Boris Johnson agrees to step down
    Highland Park gunman had threatened to kill his own family
    ‘Republicans aren’t going to stop: they’ll try to criminalize abortion throughout the US’
    Jorge Stolfi: ‘Bitcoin and blockchain technology is garbage’
    CERN’s Large Hadron Collider, the biggest experiment on Earth, is back in action
    EL PAÍS America wins World Association of News Publishers award for best news site in Latin America
    Letras Americanas: la actualidad literaria de un continente vista por el escritor Emiliano Monge
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Toda la actualidad científica en el boletín de Materia
    Ideas: reportajes y entrevistas para entender el mundo
    Ucrania presenta en Suiza un ambicioso plan de reconstrucción de 720.000 millones 
    López Obrador pide “desmontar la estatua de la libertad” si EE UU condena a Julian Assange
    La investigación de EE UU sobre la muerte de la periodista palestina se cierra en falso por el mal estado de la bala 
    Silvina Batakis, una economista de bajo perfil para aplacar la guerra de poder en Argentina
    Muere a los 63 años el secretario general de la OPEP, Mohammad Barkindo
    El Parlamento Europeo respalda el sello verde de la UE al gas y energía nuclear
    La ola de violencia en México abre una brecha entre la Iglesia católica y el Gobierno
    Chile presenta la primera Constitución paritaria y con perspectiva de género
    Ese cuerpo
    El hallazgo de la tumba de Tutankamón, convertido en novela criminal a lo Agatha Christie
    La verdad de por qué los Oscar se llaman así
    Nikki Lane: forajida de botas vaqueras y calidad 
    La agenda de la NASA para volver a la Luna (y quedarse)
    ¿Qué es la incompatibilidad de Rh madre/hijo?
    Un novedoso estudio sobre estrés adolescente propone un nuevo método para afrontarlo: optimizarlo en lugar de evitarlo
    Kyrgios - Nadal y Djokovic - Norrie: dónde ver las semifinales de Wimbledon 2022
    La fiesta en el estreno de la Eurocopa femenina la pone el público con un récord de asistencia en el torneo
    El fútbol moderno reduce el mercado de Cristiano Ronaldo
    Empresas, expertos, políticos y científicos reclaman compromiso ante la emergencia climática: “Lo fundamental es cumplir”
    Vídeo | Las primeras imágenes del año de una osa parda y sus dos crías en el Valle de Arán
    Las emisiones de efecto invernadero volvieron a crecer en 2021 en España aunque sin sobrepasar los niveles previos a la pandemia
    Con el relax del verano se acentúan los peligros cibernéticos: así puede protegerse durante las vacaciones
    Meta presenta un traductor capaz de operar en tiempo real con 200 idiomas
    Jorge Stolfi: “Soy catedrático de informática. Como mis colegas, sé que la tecnología de bitcoin es basura”
    La Puerta de Alcalá pasa por el ‘quirófano’: una lona gigante tapará el monumento más icónico de Madrid
    El comité de crisis de la coalición de Gobierno: cinco encuentros entre la formalidad y el enfrentamiento
    Los socios piden al Gobierno un giro “decisivo” a la izquierda en el debate de la nación
    Los dilemas de ‘La firma de Dios’: ¿y si el virus detrás de una pandemia tuviera conciencia y voluntad propia?
    ‘Sanfermines: maltrato animal en riguroso directo’, por Eva Güimil
    ‘La ciudad es nuestra’ o la corrupción policial’, por Ángel Sánchez-Harguindey
    Realismo, entretenimiento y democracia: la alta costura se deshace por fin de sus estereotipos en París
    ‘Foodificación’ o cómo un chuletón a la brasa puede transformar por completo la identidad de una ciudad
    Matthew Bronfman, el ‘príncipe’ de Wall Street y heredero de un imperio licorero que se ha reunido con el rey Felipe VI
    Volver a la escuela tras dos años de pandemia
    La discriminación contra las minorías sexuales limita el desarrollo de Latinoamérica
    El hombre que persigue la gaita más antigua del mundo
    'La palabra médico', por Martín Caparrós 
    Ecosofía: la filosofía de tratar el entorno natural como algo divino 
    Marta Segarra: “Quien diga que el hombre es el único animal que viola se equivoca”
    Manual para sobrevivir al calentón del euríbor
    La carrera por las oposiciones ha empezado: en juego hay 45.000 trabajos para toda la vida
    Max Aub, el escritor español que mejor contó la experiencia de la guerra y los refugiados 
    La Bienal del Whitney habla mucho y dice poco
    Qué nos enseña ‘El Quijote’ sobre la nueva ley contra el desperdicio de alimentos
    Un argentino en medio de la crisis humanitaria en Mozambique: “He intentado salir de esto y no he podido”
    Qué ver en Washington, la ciudad donde casi todo es gratis
    24 horas en Tánger: entre la ‘kasbah’, la medina y las huellas de la generación Beat
    Nicole Kidman aparece como modelo sorpresa en el chocante desfile de Balenciaga
    El ‘influencer’ más varguardista del momento crea parodias de la moda desde una de las islas más pobres del mundo
    A-ha: cómo tres tipos que no se soportan sobrevivieron a la canción pop más grande de los ochenta 
    Una granja llena de armas y dos denuncias por secuestro: ¿cómo ha llegado Ezra Miller hasta aquí?
    ¿Cuál es la mejor marca de tónica?
    Las quejas de los lectores: alud de maicena para un pollo frito
    Apple asegura que el software espía Pegasus ya no podrá entrar en sus teléfonos
    “Por Dios, haz lo que quieras pero tengo que jugar”: Xabi Alonso se abrió la rodilla dos horas antes de la semifinal del Mundial 
    Ponte a prueba con nuestros crucigramas, sopas de letras, sudokus y juegos arcade
    Feijóo dijo que Irene Montero fue a EE.UU de turismo y la réplica de la ministra es abrumadora
    “Tchouameni trabaja como nadie; seguro que se ganará su sitio”
    Los Planetas contra la ley de TikTok
    

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

    Boris Johnson dimite
    Boris Johnson: el final de la escapada del mago del Brexit
    Populistas occidentales por el desagüe de la historia
    Populistas occidentales por el desagüe de la historia
    Boris Johnson dimite
    La ultraderecha mundial y el control de los cuerpos
    Las otras fronteras de Rusia: entre el miedo (al imperio) y los intereses nacionales
    El lenguaje que Putin entiende
    ¿Cómo se elige un nuevo líder conservador?
    La Fiscalía investiga al expresidente Enrique Peña Nieto por recibir 26 millones de pesos en transferencias irregulares en el extranjero
    Cientos de yihadistas liberan a más de 800 presos en el asalto a una cárcel en la capital de Nigeria
    La guerra de los drones se vuelve contra Hezbolá 
    Turquía libera el barco ruso con trigo presuntamente robado de Ucrania
    La guerra en Ucrania impulsa el perfil internacional de Polonia
    El asesino de Highland Park había amenazado con matar a su familia y planeó otro ataque durante su huida
    El Gobierno alemán impulsa la regularización de más de 100.000 extranjeros sin permiso de residencia
    La primera ministra francesa pide “compromisos” a la oposición parlamentaria para sacar adelante las reformas
    Europol desmantela una red de tráfico de migrantes transportados en botes hinchables al Reino Unido
    El hambre en Colombia, el reto mayúsculo de Petro
    Vladimir Padrino, el eterno ministro chavista aliado de Rusia
    Haití, sin presidente y sin Estado un año después del asesinato de Jovenel Moïse
    Argentina salda con diez cadenas perpetuas los delitos cometidos en Campo de Mayo, el mayor centro clandestino del Ejército en la dictadura
    ‘Mi bebito fiu fiu’, el fenómeno mundial que viralizó uno de los mil escándalos de la política peruana
    Dimiten tres ministros y un alto cargo en Ecuador tras el acuerdo para poner fin a las protestas indígenas 
    

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

    Vendaval inflacionista
    Deriva reaccionaria en Estados Unidos
    Nuestro invierno del descontento
    El eterno retorno de lo mismo
    ‘Mi casa, mi árbol’
    Ley de desmemoria democrática
    Ante la crisis, ¿gestionas o lideras?
    Acusación en el espejo
    Deja quieta la comida
    Dios y la carne
    La fortaleza del empleo 
    Colombia necesita la paz 
    De guerreros y comerciantes
    El Roto
    Peridis
    Flavita Banana
    Riki Blanco
    Sciammarella
    Planeta de Plástico, por Malagón
    Envía tu carta
    Defender lo público
    Los excesos de Telmo Martín
    El culo y las témporas 
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

    Los socios piden al Gobierno un giro “decisivo” a la izquierda en el debate de la nación
    El comité de crisis de la coalición de Gobierno: cinco encuentros entre la formalidad y el enfrentamiento
    Villarejo: “Tengo un tema de la hostia contra Podemos”. Cospedal: “Es una bomba. Yo eso sí lo quiero”
    Ante la crisis, ¿gestionas o lideras?
    El almirante Cervera y el honor de España
    El Gran Retroceso
    Santa Bárbara y la cultura de la defensa
    ¿Es posible disentir de esta retórica belicista?
    Feijóo evita condenar la cacería a Podemos: “Estas cosas salen cuando al PP le va bien en las encuestas”
    Belarra denuncia una “alianza antidemocrática” contra Podemos tras conocer los audios de la conversación entre Villarejo y Cospedal
    La Audiencia Nacional rechaza suspender el juicio a Villarejo hasta septiembre
    Los sudaneses que fueron devueltos en caliente a Marruecos: “Unos guardias civiles me pegaron en los pies y me echaron gas”
    Un conductor octogenario recorre 35 kilómetros en sentido contrario por la A-7 al volver a su casa en la costa desde Valencia
    Heridos tres policías en Pamplona en una protesta al final durante la procesión de San Fermín
    Las becas de Ayuso para rentas altas, un debate más ideológico que jurídico 
    La doctrina del Constitucional no es concluyente sobre las becas con dinero público para estudiantes de centros privados
    Yolanda Díaz: “El presidente y yo llegaremos a un punto de encuentro” 
    El Gobierno recupera a sus socios para la reforma exprés con la que pretende renovar el Tribunal Constitucional
    Rajoy defiende al rey emérito y dice que no se le trata “como se merece”
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

    La CNMC multa con 204 millones a las seis mayores constructoras por pactar contratos públicos durante 25 años
    Claves sobre la multa histórica de la CNMC al cartel de constructoras
    Un incendio obliga a suspender la circulación de los trenes de alta velocidad entre Madrid y Andalucía
    La Fiscalía de Portugal investiga al rey del turismo náutico por fraude en la compra-venta de un ferry
    Bancos centrales, entre líneas
    Estado autonómico: Sobre las reformas pendientes
    Carlos Jiménez Villarejo: un hombre contra la desesperanza
    IPC: de la negación al riesgo de sobrerreacción
    A Unilever se le indigesta el helado 
    Aena lanza el mayor contrato del ‘handling’ de aeropuertos del mundo
    El pacto de rentas sigue en el limbo tras la última reunión del diálogo social 
    La CNMC asegura que las gasolineras no se aprovechan del descuento de 20 céntimos
    Lidl España pacta una subida salarial del 7% este año para 15.500 empleados
    Las gasolineras de bajo coste son las que más han subido los precios tras la bonificación del Ejecutivo
    Los hoteleros auguran un verano casi récord, pero las cancelaciones suben un 19% respecto a 2019
    Requena y Almendralejo rompen el monopolio catalán y colocan un vocal en el Consejo Regulador del cava
    Francia anuncia su intención de nacionalizar por completo la eléctrica EDF
    Indra convocará una junta extraordinaria para designar a los nuevos consejeros independientes
    El AVE no llegará a Galicia este verano por el retraso de Talgo
    Renfe bate récord de transporte de viajeros con su AVE a La Meca
    La carrera por las oposiciones ha empezado: en juego hay 45.000 trabajos para toda la vida
    Los jueces se ponen de parte de las víctimas de ‘phishing’ bancario
    Texas es la nueva China para  Elon Musk
    IPC: de la negación al riesgo de sobrerreacción
    A Unilever se le indigesta el helado 
    Telefónica y Repsol lanzan su negocio de energía fotovoltaica y crean la estructura operativa
    Los neobancos suben la apuesta por los depósitos
    
    ¿En qué valores invierten los fondos más rentables del semestre?
    Altum Faith, el fondo que triunfa con la doctrina del Vaticano
    No se puede desheredar a un familiar con el que no se tiene relación, según el Supremo
    Líos en la piscina comunitaria: normas y sentencias para un chapuzón seguro
    Parir en casa, educarlo por mi cuenta… ¿Qué puedo decidir sobre mi hijo y qué no?
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

    Las emisiones de efecto invernadero volvieron a crecer en 2021 en España aunque sin sobrepasar los niveles previos a la pandemia
    ¿Existe brecha generacional en el colectivo LGTBI? De la lucha por los derechos al debate identitario
    Marcos López Hoyos, inmunólogo: “Deberíamos usar mascarillas en interiores y comer en terrazas”
    El control del cuerpo de las mujeres
    No se gobierna con el catecismo romano
    Un día muy triste para todas las mujeres
    El Supremo de Estados Unidos destruye un derecho fundamental de las mujeres
    ¿Hay que obligar a los niños a hacer deberes en verano? Los expertos recomiendan actividades que no se parezcan a las tareas escolares
    Un alud letal y una histórica sequía: el cambio climático castiga al norte de Italia
    ‘Ley trans’: El Consejo de Estado plantea informes médicos para cambiar de sexo en el registro y aval judicial para los menores
    El Supremo confirma la condena para el encargado de un banco de alimentos por abusar de una mujer a cambio de comida
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    Un estudio de la Universidad de Oxford relaciona la privatización sanitaria con el aumento de la mortalidad evitable en Inglaterra
    Condenado el Ayuntamiento de Écija por discriminación salarial a las mujeres: “Éramos malas por reivindicar. Nos decían: ‘Portaos bien”
    La eterna provisionalidad de los sanitarios: “Llevo 19 años en urgencias y no ha salido ni una oposición para hacerme fija”
    La sanidad privada entra en cinco cárceles por la falta de médicos penitenciarios
    Los hospitalizados con covid crecen un 13% desde la semana pasada
    “Los republicanos no van a parar: tratarán de criminalizar el aborto en todo EE UU” 
    Se buscan profesionales en economía circular
    La economía circular llega a la ciudad. Te contamos dónde se encuentra 
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

    ¿Cómo se cierra un colegio público?
    Los sindicatos educativos catalanes convocan huelga el 7 de septiembre, primer día de curso en los institutos, y el 28
    ¿Hay que obligar a los niños a hacer deberes en verano? Los expertos recomiendan actividades que no se parezcan a las tareas escolares
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    Madrid, el paraíso de la educación privada: en la capital son minoría los alumnos de la pública
    Trabajar en el ‘big data’: “Nunca he tenido que echar currículum, las ofertas me han llegado solas”
    El Gobierno lanza una ofensiva contra las becas para rentas altas de Ayuso que Feijóo respalda
    José Manuel Bar, secretario de Estado de Educación: “Los docentes de secundaria deben empezar a estudiar pedagogía en su carrera”
    Ayuso se apunta ahora el tanto de la bajada de tasas universitarias, pese a que las llevó a los tribunales para no reducirlas
    Notas de Selectividad 2022 por comunidades: los aprobados rozan el 96%
    Becas públicas en centros privados de Madrid para familias que ganan más de 100.000 euros
    Sin currículos
    La escuela concertada ante las desigualdades: el debate pendiente
    La equidad frente a las políticas educativas de privatización en Andalucía
    No hay lunes al sol en la Universidad
    Ofrecer comedor gratis en todos los colegios públicos es “alcanzable y urgente”: costaría 1.664 millones al año, según la ONG Educo  
    Una fórmula para que la escuela pública compita mejor con la concertada
    La pérdida de alumnos por el descenso de la natalidad está afectando con más fuerza a la escuela pública que a la concertada
    El Ayuntamiento de Madrid guarda en un cajón una herramienta ya pagada para ver los datos de contaminación al detalle 
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    La implantación del nuevo Bachillerato general fracasa pese a su demanda potencial: “Creímos que lo pedirían seis alumnos y lo han hecho 27”
    Toni Solano, director de instituto: “Veo mal a los niños, necesitan muchísima ayuda”
    Niños, Administraciones y redes sociales: prohibir su uso con una mano y enseñar a crear contenidos con la otra
    El Gobierno aprueba el decreto de bachillerato: los alumnos podrán terminar con un suspenso y desembocará en una nueva Selectividad
    Las universitarias desertan del grado de Matemáticas ahora que tiene pleno empleo. ¿Por qué?
    Golpe a la temporalidad en las universidades: 25.000 profesores asociados serán indefinidos a tiempo parcial
    Antonio Abril: “Yo le decía a Castells: ‘Tienes que aguantar la presión, tienes que hacer la reforma universitaria”
    Los universitarios extranjeros podrán quedarse un año en España automáticamente al terminar la carrera
    “No hay pensamiento sin tiempo para pensar”
    “En el hospital, la enseñanza es una medicina más”
    Un alegato por la paz y la cultura
    

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

    Las emisiones de efecto invernadero volvieron a crecer en 2021 en España aunque sin sobrepasar los niveles previos a la pandemia
    El relato de un viaje sostenible: desde las finanzas verdes a la digitalización de la industria
    Los rinocerontes regresan a Mozambique 40 años después de su desaparición
    Carlos Nobre: “La Amazonia  ya muestra síntomas  de muerte”
    El Parlamento Europeo respalda el sello verde de la UE al gas y energía nuclear
    Un alud letal y una histórica sequía: el cambio climático castiga al norte de Italia
    Un año de espera por la bicicleta: el estallido de la demanda coincide con la escasez de suministro
    El anticiclón de las Azores se está expandiendo e intensificando
    Los peores incendios forestales de España: cómo se están intensificando los monstruos de fuego
    Las bicicletas son para el verano... o no 
    La última milla en el futuro del desarrollo urbano
    Un plan de retirada  
    Crisis energética y precios del carbono
    La lección del martín pescador para afrontar la crisis ecológica
    Estocolmo+50: mirar atrás para tomar impulso
    Ríos imposibles: las 171.000 barreras que rompen el curso de agua en España
    La UE abraza las renovables para romper la dependencia de Rusia
    La lucha en un pueblo de Teruel para salvar su última montaña
    ¿Qué aire respiran los niños de Madrid y Barcelona? En el 46% de los colegios se supera la contaminación permitida
    “No hay pensamiento sin tiempo para pensar”
    “En el hospital, la enseñanza es una medicina más”
    Un alegato por la paz y la cultura
    

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

    ‘Meraxes gigas’: descubierta en la Patagonia argentina una nueva especie de dinosaurio carnívoro gigante
    La cola vestigial, el apéndice oculto del hombre que venció a Napoleón en Waterloo
    La agenda de la NASA para volver a la Luna (y quedarse)
    El sector biotecnológico supera las cifras de 2020 y capta 180 millones de euros de inversión privada
    “La identidad de género no se elige, como prueba el fracaso de las terapias de conversión”
    Un novedoso estudio sobre estrés adolescente propone un nuevo método para afrontarlo: optimizarlo en lugar de evitarlo
    Las mentes humanas detrás de las mentes artificiales
    El cerebro está más caliente de lo que se pensaba 
    Cangrejos ermitaños: el arte de seleccionar la mejor concha
    Las temperaturas extremas también matan en América Latina
    Vuelve el LHC, el mayor experimento sobre la Tierra 
    La matemática Maryna Viazovska gana la medalla Fields tras descubrir la mejor forma de apilar naranjas en 24 dimensiones
    Cuánto pesa el estrés laboral en la salud mental: del ‘burnout’ a la depresión 
    Katalin Karikó, madre de la vacuna contra la covid: “Conoces a los jugadores de fútbol, pero no a quienes te salvan la vida” 
    Esta imagen no se mueve pero puede provocar cambios en tu pupila
    El anticiclón de las Azores se está expandiendo e intensificando
    ¿Dónde hay civilizaciones extraterrestres?
    Las mentes humanas detrás de las mentes artificiales
    Matemáticas para describir los remolinos, los taxis del océano
    Reaparece la tesis de María Wonenburger, la pionera matemática española que permaneció décadas en el olvido
    Técnicas criptográficas que se fundamentan en lo impredecible
    Fracciones egipcias
    El problema del huerto
    Números McNugget
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

    Rosalía en Almería, con R de reinona y A de apoteósico
    Metallica triunfa a base de oficio en un Mad Cool repleto
    Queen se aferra a su corona en el concierto del WiZink
    Lo que debemos a Patxo Unzueta
    La huida
    Un siglo de canciones, 1.500 artistas
    Peter Brook, el gran árbol del teatro
    Norma lleva al cómic a obtener por primera vez el Premio Nacional a la Mejor Labor Editorial
    Qué une a Leonardo da Vinci y a Susan Sontag: un ensayo recopila a los genios de la erudición
    Muere Kazuki Takahashi, creador del manga ‘Yu-Gi-Oh!’, a los 60 años
    Soria resucita su pasado judío en una ruta cultural: iluminadores de Biblias, poetas, amuletos y platos sin cerdo
    La tragedia de la redada masiva de judíos en París en 1942, a través de la mirada de Cabu
    La novela póstuma de Almudena Grandes, ‘Todo va a mejorar’ llegará en otoño
    Cinco minutos de aplausos y un bis de coro: el Teatro Real vive una noche histórica con el ‘Nabucco’
    Safo, una estrella del rock de la Grecia antigua reencarnada en Christina Rosenvinge
    El guitarrista Carlos Santana se desmaya durante un concierto en Estados Unidos
    Taika Waititi, director de ‘Thor: Love and Thunder’: “Las religiones solo provocan problemas”
    El festival Grec da voz a los vigilantes de salas de los museos en un espectáculo espléndido 
    Una ‘Salome’ descafeinada y descolorida enfría Aix-en-Provence
    La actriz trans Daniela Vega: “Para que tú y yo estemos aquí sentadas, hubo gente que peleó y murió”  
    El último atardecer de Europa se ve solo desde este lugar. Un viaje hacia el infinito por el Camino de Fisterra-Muxía
    Un paseo fluvial con museos y otro lleno de piscinas termales. Las sorpresas de la Vía de la Plata
    Lorca, en la ciudad al margen
    El Pirineo oscense, para entrar a vivir
    Toda la lectura del verano, en el bolsillo
    Longsellers: los libros más vendidos a lo largo de la historia
    Libros para descubrir el mundo recomendados por Benjamín Prado
    Encuentro virtual con la cantante Carla Morrison
    'Safo' en el Teatre Romea de Barcelona
    Preestreno de  'Entre dos amaneceres'
    'Padre no hay más que uno 3'
    El primer encierro de San Fermín 2022, en imágenes
    Un primer encierro rápido y limpio abre San Fermín 2022
    Desvaído rejoneo
    El chupinazo de San Fermín 2022, en imágenes
    

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

    Hay un río de oro negro bajo A Coruña
    Max Aub, el escritor español que mejor contó la experiencia de la guerra y los refugiados 
    La Bienal del Whitney habla mucho y dice poco
    Los primeros poemas de Severo Sarduy, una joya inédita
    Libros para el verano: 80 novedades recomendadas para estas vacaciones
    Rigoberta Bandini, Jordi Évole, Rosa Montero, Juan Diego Botto, Albert Serra y otros nombres de la cultura proponen sus lecturas estivales
    ‘The Murder of Crows’: por qué el arte sonoro es más poderoso que el visual
    El regreso de Perrate: fiesta, linaje y ocho gozosos minutos de bulerías
    Raíces y alas del flamenco: seis discos entre tradición y evolución
    Tres veces Calderón: variaciones sobre la tortura en una obra sugestiva e imaginativa
    Diego Luna, un actor magnético para una obra mediocre
    No eran marcianos, eran humanos
    El desafío de Frida Kahlo
    Lo que siento (no se olviden de Ucrania) 
    Otros turismos (lejos y aquí cerca)
    ‘Horas muertas’, en un Dublín hipnótico
    ‘Prometeo’, trío de ases
    ‘La memoria del alambre’, ese algo misterioso que daba miedo
    ‘Tarradellas. Una cierta idea de Cataluña’: manual de resistencia
    Antoni Muntadas: “Supe que me dedicaría al arte cuando dejé de pintar”
    Manuel Estrada: “Me agrada que una portada guste más después de leer el libro”
    Óscar Esquivias: “No hace falta ser creyente para leer la Biblia”
    Amelia Castilla: “Los ritos nos ayudan a hacer viable el trance de la muerte”
    Shuarma: “Me gusta de la poesía el silencio que encierra”
    

### Imprimir sección de deportes


```python
req12 = requests.get("https://elpais.com/deportes/")
```


```python
type(req12)
```




    requests.models.Response




```python
tags = soup12.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Nadal se retira de Wimbledon
    La familia de Nadal le pidió que abandonara el partido ante Fritz en Wimbledon
    Nadal: “Estoy preocupado, algo no está bien”
    El Big Data sigue sin explicar a Cruyff
    La perfección de la centenaria Catedral
    La castración del fútbol prosigue con dibujos animados
    Aquí Pablo Laso, aquí su obra
    La UEFA se blinda contra la Superliga 
    Pogacar impone su ley y ya es líder del Tour de Francia
    Tour de Francia 2022: así es la primera etapa de montaña entre Tomblaine y Super Planche des Belles Filles
    Nadal, el rey de lo increíble: lesión, remontada y a semifinales de Wimbledon
    Djokovic - Norrie: dónde ver la semifinal de Wimbledon 2022
    La baloncestista Brittney Griner se declara culpable de posesión de drogas en Rusia
    El Barcelona espera una respuesta del Bayern por Lewandowski mientras presenta a Christensen
    Las jugadoras de Inglaterra piden a Nike cambiar el color del pantalón por la regla
    Jorge Vilda: “Pronto veremos a una mujer entrenar a la selección masculina de fútbol”
    La fiesta en el estreno de la Eurocopa femenina la pone el público con un récord de asistencia en el torneo
    Biden asegura que busca “lo más pronto posible” la liberación de Brittney Griner, la estrella del baloncesto detenida en Rusia 
    Las figuras del Madrid rinden tributo a Pablo Laso mientras el club pasa página
    El fútbol moderno reduce el mercado de Cristiano Ronaldo
    “La pasión que genera el fútbol es inigualable”
    “Nunca acepto un no por respuesta”
    La nadadora que dejó de competir para hacer campeones de básquet
    Crónica de dos ciudades moldeadas por la misma pasión 
    Biden asegura que busca “lo más pronto posible” la liberación de Brittney Griner, la estrella del baloncesto detenida en Rusia 
    Videoanálisis | Una gran oportunidad perdida para sacar el ajedrez a la calle
    Vídeo | Cómo sobrevivir a Wimbledon: así ha evolucionado el tenis en el All England Club
    La perfección de la centenaria Catedral
    El fútbol moderno reduce el mercado de Cristiano Ronaldo
    Marc Soler, el ayudante inesperado de Pogacar en el pavés del Tour de Francia
    Djokovic, bajo la presión de Nadal y un horizonte incierto
    Iñaki Williams elige jugar con Ghana para ir al Mundial de Qatar
    

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

    Con el relax del verano se acentúan los peligros cibernéticos: así puede protegerse durante las vacaciones
    Meta presenta un traductor capaz de operar en tiempo real con 200 idiomas
    “Soy catedrático de informática. Como mis colegas, sé que la tecnología de bitcoin es basura”
    El sector biotecnológico supera las cifras de 2020 y capta 180 millones de euros de inversión privada
    Las mentes humanas detrás de las mentes artificiales
    El juego de la técnica
    Daniel Innerarity: “Los algoritmos son conservadores y nuestra libertad depende de que nos dejen ser imprevisibles”
    Regina Barzilay: “Tenemos que aprender a vivir en un mundo en el que la tecnología toma decisiones que no podemos supervisar”
    Herramientas y trucos para recordar la ubicación del coche gracias al móvil
    Las tres amigas que quieren revolucionar los materiales de construcción con fibras de hongos
    El Constitucional afianza el derecho al olvido en internet
    Dall-E Mini, el popular generador automático de imágenes que hace dibujos sexistas y racistas 
    Por qué el algoritmo de Google no es una persona
    Comunidades de energía: una fórmula barata, limpia y segura
    “Queremos que la programación sea el inglés del siglo XXI”
    En defensa de la procrastinación. Elogio del tiempo perdido (frente al que las redes te roban)
    Instagram, el mejor de los mundos posibles
    Del terrorismo youtuber al influencer rabioso: el odio inunda la red
    Cronodiversidad. ¿Por qué el tiempo cada vez va más rápido?
    El impacto de la tecnología en la hostelería: de la comanda digital al pago con código QR
    Herramientas que ayudan a crecer a las empresas (más allá de los pagos)
    Cinco razones por las que este ‘smartphone’ es sencillamente tentador
    La cámara de este ‘smartphone’ es pura magia
    Por qué los nuevos coches ya no los diseñarán las personas
    Una catapulta para el talento de ‘kilómetro cero’
    

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

    Juana Martín, primera mujer española “y gitana” en la alta costura de París, tras su desfile: “Me he dejado la piel”
    El espectáculo (teatral) debe continuar en la alta costura de París
    Elon Musk tuvo gemelos en secreto con una ejecutiva de una de sus empresas
    Por qué es importante conocer tu personalidad erótica para tener una vida sexual más satisfactoria
    Realismo, entretenimiento y democracia: la alta costura se deshace por fin de sus estereotipos en París
    Matthew Bronfman, el ‘príncipe’ de Wall Street y heredero de un imperio licorero que se ha reunido con el rey Felipe VI
    De Kate Middleton a Sienna Miller: los famosos llenan las gradas de Wimbledon, en imágenes
    ‘Foodificación’ o cómo un chuletón a la brasa puede transformar por completo la identidad de una ciudad
    Amalia de Orange celebra con siete meses de retraso su 18º cumpleaños con una gran fiesta de verano blindada
    Ricky Martin se defiende de las acusaciones de violencia doméstica: “Enfrentaré el proceso con la responsabilidad que me caracteriza” 
    Camila de Cornualles, editora de una revista campestre con Kate Middleton como su fotógrafa
    De Jessica Chastain a Kim Kardashian: las famosas le hacen la peineta al 4 de julio 
    Relojes de lujo escondidos dentro del airbag: detenido el grupo organizado que asaltó la villa de Ronaldo en Ibiza
    La dictadura de la perfección, misoginia y Jeffrey Epstein: los ángeles y demonios de Victoria’s Secret
    Dios y diamantes: lo que Kendrick Lamar nos quiso decir a través de su corona de espinas
    Entre Sevilla, Ascot, el pasado y el futuro: Mans condensa su universo en una colección sin miedo a los contrastes
    La colección de Palomo Spain para Correos: cómo la moda unió a una empresa centenaria y a otra rabiosamente joven
    Archie Alled-Martínez, el barcelonés que continúa el legado de Lagerfeld: “No hace falta llevar un arco iris para ser tú mismo”
    Trece aperitivos
    La rebelión de las cocineras de España: “Hay mujeres, falta reconocimiento”
    Vende menos comer que correr
    Breve guía de los mejores vinos blancos italianos para descubrir este verano
    

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

    ‘La noche más larga’ y ‘La lista final’: palomitas sin sabor para el verano
    Los dilemas de ‘La firma de Dios’: ¿y si el virus detrás de una pandemia tuviera conciencia y voluntad propia?
    Arturo Valls pasa de presentador a recluso por rebasar los límites del humor en ‘Dos años y un día’
    Sanfermines: maltrato animal en riguroso directo
    ‘La ciudad es nuestra’ o la corrupción policial
    La falta de diversidad en ‘Friends’: el juicio a los seis del Central Perk
    Publicidad convertida en lírica y humanismo 
    Entre novedades y apuestas de bajo riesgo: así es el verano en la televisión en abierto
    Vivir y morir en Colombia, ciencia desmitificada, un nuevo lugar del crimen y adictos a la cultura pop, entre los ‘podcasts’ de julio
    Promover el turismo en tiempos de nueva normalidad, pero con vieja publicidad
    Podium Podcast estrena web con más de 400 contenidos y nuevo diseño
    EGM 2022: La SER cierra temporada de nuevo como la radio más escuchada
    ¿Quién demonios votó a Podemos en La Moraleja?
    La voz de los más inocentes
    Las actrices de ‘Intimidad’: “Si una mujer no es complaciente en esta profesión, llegan las amenazas”
    Crecer dentro del fenómeno global ‘Stranger Things’: “Lo llevamos bien, con terapia”
    La ‘venganza’ de William Levy: “De joven, en Cuba, viví demasiadas injusticias”
    ¿Qué ver hoy en TV? Jueves 7 de julio de 2022
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

    El golazo literario de Roberto Santiago con ‘Los futbolísimos’
    ¿Dónde está exactamente el origen del mal?
    El hombre que persigue la gaita más antigua del mundo
    La uva más denostada de  Castilla-La Mancha resurge de sus cenizas
    La rebelión de las cocineras de España: “Hay mujeres, falta reconocimiento”
    En busca de la huella de Camarón de la Isla, leyenda viva del flamenco
    Oliviero Toscani: “El fascismo resulta muy cómodo porque no te exige razonar”
    La importancia del respeto para sentirnos bien
    República Dominicana, donde la vida fluye por el río infinito
    El placer de lo rancio y otros gustos y aromas que recuerdan la niñez
    Un misterio en el Real Madrid y un fantasma en Gales: ¿quién diablos es Gareth Bale?
    Así es el barrio de Pekín donde hay “robotaxi” y la compra llega en vehículo sin conductor
    Saborear el momento
    Nissan Ariya: imagen futurista y conducción exquisita
    La palabra médico
    El cuerpo
    Cuento de Catherine del Biombo 5
    Vende menos comer que correr
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
    Retrato Robot 
    Ilusiones hipnóticas
    El poder del hormigón
    Maulévrier, Japón a la francesa
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
    
    [1m[32mMujeres[0m
    
    [1m[32mMujer[0m
    
    [1m[32mBrecha salarial[0m
    
    [1m[32mMachismo[0m
    
    [1m[32mViolencia[0m
    La ola de violencia en México abre una brecha entre la Iglesia católica y el Gobierno
    [1m[32mMaltrato[0m
    ‘Sanfermines: maltrato animal en riguroso directo’, por Eva Güimil
    [1m[32mHomicidio[0m
    
    [1m[32mGénero[0m
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Chile presenta la primera Constitución paritaria y con perspectiva de género
    [1m[32mAsesinato[0m
    Haití, sin presidente y sin Estado a un año del asesinato de Jovenel Moïse
    Haití, sin presidente y sin Estado un año después del asesinato de Jovenel Moïse
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
