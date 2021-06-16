---
layout: page
title: 1.3 Moodle
permalink: /cms/moodle
nav_order: 3
has_children: false
parent: 1 Sistemas gestores de contenido (CMS)
grand_parent: Desarrollo Web en Entorno Servidor
---

## 1.3. Moodle
{: .no_toc }

- TOC
{:toc}

### 1.3.1. Características de Moodle

Moodle es un sistema de gestión de contenidos orientado a **crear comunidades de aprendizaje** en línea. Este tipo de plataformas tecnológicas también se conoce como **LMS (Learning Management System)**. Su licencia es GPL (es decir: es software libre).

Está programado en lenguaje PHP y puede usar diferentes gestores de bases de datos para almacenar el contenido: MySQL o PostgreSQL son los más habituales, pero también es posible utilizar Oracle o SQL Server.

Las características más destacables de Moodle son:

* Su arquitectura y herramientas son apropiadas para la educación a distancia, así como también para complementar el aprendizaje presencial. 
* Tiene una interfaz de navegador de tecnología sencilla, ligera y compatible con todos los navegadores. Eso sí, es más complejo que otras soluciones como Google Classroom, aunque Moodle también es muchísimo más potente.
* La instalación es sencilla (¡casi siempre!), requiriendo tan solo una plataforma que soporte PHP y la disponibilidad de una base de datos. 
* Da mucha importancia a la seguridad: todos los formularios son revisados, las cookies cifradas, etc. 
* Las áreas de introducción de texto pueden ser editadas usando un editor WYSIWYG.
* Es fuertemente configurable, permitiendo la instalación de módulos adicionales (plugins) para incrementar sus posibilidades.
* Es un sistema enorme que consume *muchos* recursos en el servidor.

### 1.3.2. Algunos módulos de Moodle

En Moodle, los recursos se organizan en categorías llamadas **módulos**. Cada módulo tiene sus propias características y está orientado a un tipo de actividad distinta: cuestionarios en línea, lecciones, tareas para que los alumnos suban, encuestas y un largo etcétera.

Aquí solo mencionaremos los módulos más populares.

#### Módulo de archivos

Los archivos son documentos que sube el profesor/a y que estarán accesibles al alumnado.

* Los documentos pueden ser de cualquier tipo: Word, Libreoffice, Powerpoint, vídeo, audio, etc. 

#### Módulo de Tareas

Este módulo sirve para que el alumnado envíe tareas al profesor/a. Estas tareas pueden constar de un texto en línea o uno o varios archivos subidos a la plataforma.

* Puede especificarse la fecha final de entrega de una tarea y la calificación máxima que se le podrá asignar. 
* Los estudiantes pueden subir sus tareas (en cualquier formato de archivo) al servidor. Se registra la fecha en que se han subido. 
* Se permite enviar tareas fuera de tiempo, pero el profesor puede ver claramente el tiempo de retraso. 
* Para cada tarea en particular, puede evaluarse a cada estudiante (calificaciones y comentarios) en una única página con un único formulario. Incluso se puede corregir el documento escribiendo encima, como haríamos con una tarea hecha en papel.
* Las observaciones del profesor se adjuntan a la página de la tarea de cada estudiante y se le envía un mensaje de notificación. 
* El profesor tiene la posibilidad de permitir el reenvío de una tarea tras su calificación (para volver a calificarla). 

#### Módulo de consultas

Las consultas son votaciones. Puede usarse para votar sobre algo o para recibir una respuesta de cada estudiante (por ejemplo, para pedir su consentimiento para algo).

* El profesor puede ver una tabla que presenta de forma intuitiva la información sobre quién ha elegido qué. 
* Se puede permitir que los estudiantes vean un gráfico actualizado de los resultados. 

#### Módulo de foro

Hay diferentes tipos de foros disponibles: exclusivos para los profesores, de noticias del curso y abiertos a todos.

* Todos los mensajes llevan adjunta la foto del autor. 
* Las discusiones pueden verse anidadas, por rama, o presentar los mensajes más antiguos o los más nuevos primero. 
* El profesor puede obligar la suscripción de todos a un foro o permitir que cada persona elija a qué foros suscribirse de manera que se le envíe una copia de los mensajes por correo electrónico. 
* El profesor puede elegir que no se permitan respuestas en un foro (por ejemplo, para crear un foro dedicado a anuncios). 
* El profesor puede mover fácilmente los temas de discusión entre distintos foros. 

#### Módulo de Cuestionarios

Los cuestionarios son los típicos exámenes tipo test. Pueden utilizarse como exámenes, como ejercicios de autoevaluación, como pruebas de evaluación inicial, etc.

* Los profesores pueden definir una base de datos de preguntas que podrán ser reutilizadas en diferentes cuestionarios. Esto requiere una gran inversión de tiempo al principio, pero luego pueden reutilizarse las preguntas toda la vida. Y existen bancos de preguntas disponibles en internet.
* Las preguntas pueden ser almacenadas en categorías de fácil acceso, y estas categorías pueden ser "publicadas" para hacerlas accesibles desde cualquier curso del sitio. 
* Los cuestionarios se califican automáticamente, y pueden ser recalificados si se modifican las preguntas. 
* Los cuestionarios pueden tener un límite de tiempo a partir del cual no estarán disponibles. 
* El profesor puede determinar si los cuestionarios pueden ser resueltos varias veces y si se mostrarán o no las respuestas correctas y los comentarios 
* Las preguntas y las respuestas de los cuestionarios pueden ser mezcladas (aleatoriamente) para disminuir las copias entre los alumnos. 
* Las preguntas pueden crearse en HTML y con imágenes. 
* Las preguntas pueden importarse desde archivos de texto externos. 
* Las preguntas pueden tener diferentes métricas y tipos de captura.

#### Módulo de encuestas

* Se proporcionan encuestas ya preparadas (COLLES, ATTLS) y contrastadas como instrumentos para el análisis de las clases en línea. 
* Se pueden generar informes de las encuestas los cuales incluyen gráficos. Los datos pueden descargarse con formato de hoja de cálculo Excel o como archivo de texto CSV. 
* La interfaz de las encuestas impide la posibilidad de que sean respondidas sólo parcialmente. 
* A cada estudiante se le informa sobre sus resultados comparados con la media de la clase. 

#### Módulo de Wikis

* El profesor puede crear este modulo para que los alumnos trabajen en grupo en un mismo documento. 
* Todos los alumnos podrán modificar el contenido incluido por el resto de compañeros. 
* De este modo cada alumno puede modificar el wiki del grupo al que pertenece, pero podrá consultar todos los wikis. 
    
