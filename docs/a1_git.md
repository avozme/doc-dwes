---
layout: page
title: Anexo I. Sistemas de control de versiones. Git
permalink: /scv-git/
nav_order: 9
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 1. Sistemas de control de versiones
(Fuente: www.genbetadev.com)
Tanto si trabajamos por nuestra cuenta como si lo hacemos por cuenta ajena, es habitual que no lo hagamos solos, sino que tengamos que hacerlo junto a un equipo de personas. El desarrollo de software de calidad es una tarea que exige a menudo de perfiles diferentes, cada uno especializado en un área (frontend, backend, administración de bases de datos, usabilidad…). Esto hace que necesitemos de un sistema eficiente para organizar al equipo. Y cómo no, existe una tremenda variedad de software destinado a facilitar esa organización.
¿Qué es un sistema de control de versiones?
Es casi inconcebible hoy en día trabajar desarrollando software y no utilizar un sistema para controlar los cambios que se van realizando, tanto por nosotros mismos como por nuestros compañeros de trabajo. Tales utilidades se denominan sistemas de control de versiones, y existen un buen puñado de ellas. La característica principal en que se dividen bien podría ser si se trata de un sistema centralizado o no. En el primer caso, existe un servidor común donde se encuentra el código fuente, tanto la versión actual en desarrollo como todas aquellas versiones intermedias desde que dio comienzo el proyecto. En el último caso, no es necesario (aunque a menudo es recomendable) poseer un servidor común, sino que se pueden enviar y recibir actualizaciones de cada uno de los miembros participantes de forma directa.
¿Cómo funciona un sistema de control de versiones?
Lo habitual es que cada programador realice los cambios necesarios en el código fuente para la tarea que se le ha encomendado. Una vez que dichos cambios están listos, los envía al servidor (o a los otros participantes), de modo que el resto pueda recibirlos en cualquier momento, y así trabajar sobre dichos cambios cuando tengan que realizar cualquier otra tarea. Se puede dar el caso de que varios programadores trabajen sobre el mismo fichero o ficheros, en cuyo caso el sistema lo detectará, y actuará para evitar posibles conflictos. Se pueden dar dos casos:
    • Los programadores han trabajado en porciones de código diferentes: En principio, no se han pisado las líneas en las que han trabajado, así que es probable que sea suficiente efectuar ambos cambios sobre el fichero, sin más. Casi todos los sistemas de control de versiones detectan esta situación y realiza la unión de los cambios de forma automática, notificándolo al usuario para que tenga constancia. 
    • Los programadores han trabajado en líneas de código comunes, modificando, eliminando o añadiendo líneas en la misma porción de código: En estos casos, el sistema suele señalar que hay un conflicto entre ambos cambios, y habitualmente genera un fichero intermedio convenientemente marcado para que se puedan revisar ambos cambios de forma simultánea, y así quedarse con uno, con el otro, o con una combinación de los dos, realizando la unión a mano y eliminando lo que sobra. 
Si bien sólo por esta característica ya merece la pena trabajar con un sistema de este tipo, espera a conocer las otras ventajas:
    • Puedes volver a cualquier punto del desarrollo para ver qué aspecto tenía un determinado fichero de código, o volver a una versión donde todo funcionaba antes de haber metido la pata. 
    • Puedes trabajar en distintas características de forma simultánea, guardando los cambios en cada una de ellas, y uniéndolos al desarrollo principal si ya han sido lo suficientemente probadas. O sencillamente puedes crear una nueva versión para probar un experimento, o corregir un bug que se acaba de detectar en producción, sin comprometer lo que ya llevas realizado. Estas distintas ramas de trabajo hacen que veamos el repositorio de código como un árbol, donde cada una de las ramas representan experimentos que se van creando, y que luego vuelven a unirse al tronco principal del árbol (la versión que pretende llevarse a producción). 
    • Puedes echar un vistazo para ver quién realizó un determinado cambio, y cuándo lo hizo. 
Y otras muchas características que suelen ser propias de un sistema de control de versiones específico.
Algunos de los más habituales son CVS, Subversion, Git, Mercurial, o Bazaar, si bien encontrarás otros muchos. Personalmente, me decanto por Git, el mismo que se utiliza para llevar un control del desarrollo del kernel de Linux (de hecho, fue creado inicialmente para esta tarea), y que además de ser muy popular, es un sistema distribuido, flexible, y para el que existe una gran cantidad de bibliografía. Pero te recomiendo que pruebes unos cuántos y te decidas por el que mejor se ajuste a tus necesidades.
¿Cómo puedo empezar a usarlo?
Existe una ingente cantidad de repositorios de software que ponen a disposición del usuario un sistema de control de versiones donde alojar su código. La mayoría de los repositorios de software libre más conocidos utilizan algunos de estos sistemas para acceder al código fuente, y poder colaborar si así se desea en el desarrollo del mismo, o crear tu propio proyecto y alojarlo en ellos de forma gratuita. Muchos otros también permiten alojar proyectos privados a los que sólo tienen acceso tanto tú como tus colaboradores.
Entre los más conocidos, cabe mencionar:
    • GitHub (que como habrás adivinado, es un servicio de almacenamiento de repositorios de software que utilizan Git), el cual permite alojar tanto proyectos de software libre de forma gratuita, como proyectos privados mediante una cuenta de pago. El coste depende del número de repositorios y de colaboradores, y va desde 7 dólares al mes hasta los 200 dólares al mes. 
    • SourceForge, exclusivamente para almacenar software libre. Soporta varios sistemas de control de versiones (CVS, Subversion, Git, Bazaar, Mercurial, y puede que algún otro que me esté dejando). 
    • Launchpad, también para almacenar software libre. Elaborado por Canonical, la empresa detrás del desarrollo de Ubuntu. Utiliza Bazaar como sistema de control de versiones. 
    • Bitbucket, otro servicio gratuito (hasta cinco programadores por repositorio, a partir de ahí hay que pagarlo) que soporta Git y Mercurial y cuenta con varias herramientas sociales integradas. 
Además, no dejes de echar un vistazo a los servicios unificados de gestión de proyectos, como Unfuddle, ya que éstos suelen traer a menudo la posibilidad de alojar tu código en su propio repositorio de software.

## Git básico

GIT – FLUJO DE TRABAJO BÁSICO


Workspace   Staging area (INDEX)  Local repo (HEAD)   Remote repo
    |             |                     |                  |
    | git add →   |                     |                  |
    |             |    git commit →     |                  |
    |             |                     |    git push →    |
    |             |                     |                  |
    |             |                     |   ← git fetch    |
    |             |                     |   ← git pull     |
    |             |                     |                  |
    |             |                     |                  |




1. Inicializar (solo la primera vez)

git init

git --config name “Mi nombre”
git --config email “Mi email”
git --config list

2. Flujo de trabajo habitual en local

crear/editar los archivos locales con mi editor favorito.

git add <file> (pasa <file> a INDEX -stage área-)
git add -A (pasa TODOS los ficheros modificados a la stage área)

git commit -m “Comentario” (pasa al HEAD o repo local TODOS los archivos del stage área)

git status (muestra estado actual del repositorio)
git log (muestra historial de cambios)
git log --oneline (muestra historial de cambios simplificado)

3. Configurar repositorios remotos

git clone <url-de-repositorio> (crea copia local de repositorio remoto)
git remote (muestra repos remotos actualmente configurados)
git remote add <nombre> <url-del-repositorio> (añade repositorio remoto)
(ej: git remote add mi-repo git://github.com/pepitoperez/mi-proyecto)



4. Enviar a repositorio remoto

git push <nombre-repo-remoto> <rama>  (<rama> será “master” si no hemos hecho ramas)


5. Traer desde repositorio remoto

git fetch <nombre-repo-remoto> (trae los ficheros del repo remoto pero los deja en otro branch)
git merge FETCH_HEAD (fusiona los ficheros que has traído con la rama principal)

git pull (abreviatura de las dos anteriores ejecutadas consecutivamente)



Más info:

https://git-scm.com/book/es/v2





