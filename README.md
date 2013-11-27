Plataphorma
===========

Meteor pet project created to teach my students the following Meteor functionality: 

* Collection's publish/subscribe 
* Deps.autorun 
* Meteor.methods/call 
* Integration of non-Meteor code in compatibility folder (HTML5 games Alien Invasion and Froot Wars)
* Usage of allow to control client access to collections

![ScreenShot](/screenshot.png)


Plataphorma offers the possibility to run 2 different HTML5 games: Alien Invasion and Froot Wars. 

On the right side of the screen the best players of each game are shown, updated in real time each time a signed in player finishes a game. If no game is selected, the best players overall are shown.

On the left side of the screen a chatroom for the current game is available. Only signed in users can post messages. If no game is selected a general chatroom is shown.

The original code of the two HTML5 games integrated in this project is available here:
* Alien Invasion: https://github.com/cykod/AlienInvasion
* Froot Wars: http://www.wrox.com/WileyCDA/WroxTitle/Professional-HTML5-Mobile-Game-Development.productCd-1118301323,descCd-DOWNLOAD.html

Bootstrap style (file bootstrap.min.css) provided by http://bootswatch.com


Running the project
-------------------

A live version of this code is running here: http://plataphorma.meteor.com

To run the project locally, clone the repo and run ```meteor``` inside it. You can see in .meteor/packages that this Meteor project uses these packages:
* ```meteor remove autopublish```
* ```meteor remove insecure```
* ```meteor add bootstrap```
* ```meteor add accounts-ui```
* ```meteor add accounts-password```


//P8-preguntas:

1) Click en botón de juego.
Se ha publicado la colección de Games, los mensajes asociados a current_game las partidas asociadas a current_game y
los nombres de usuario.(lineas 4,10,26,35 de server.js). 
En el momento en el que arranca el estado de “current_game” parte a none (linea 38 client.js), y además el
cliente se subscribe solo a los mensajes referentes a ese estado y solo a las partidas correspondientes a
ese estado (lineas 25,29 client.js) . Cuando se hace click en cualquiera de los dos botones de juego, ese
estado cambia al valor nombre del juego (linea 112 client.js), se oculta el #container (bloque que contiene
el canvas) y se muestra el juego correspondiente (#gamecontainer), y como esa subscripción cambia y es una
fuente reactiva, se muestran los mensajes correspondientes a none o a algún juego y la información perteneciente
a las partidas, mediante los helpers correspondientes. 

2) se escribe mensaje chat sin estar autenticado.
Al escribir un mensaje como el templare encargado de esto es una fuente reactiva, 
en el momento en el que se escribe, se actualiza su estado. En el caso de escribir 
un mensaje y introducir un intro en la caja de texto, el código client.js va a intentar
buscar el id del usuario que lo ha introducido (linea 87) si no lo encuentra, entonces 
imprimirá un mensaje de error de login. (linea 101).


3) se escribe mensaje chat estando autenticado.
En el momento de introducir una cadena y pulsar intro (keydown 13), 
el templare de mensajes reacciona y busca el id del usuario en la base de datos
 y guarda una entrada en la tabla mensajes que se va a componer de la cadena introducida,
el id del usuario, la fecha y el id del juego asociado al estado de la sesión que esta en current_game

(podrá ser none, frootwars y alieninvasion). y al haberse efectuado un cambio, se vuelve a actualizar 
el contentido del chat. que mostrará un chat u otro dependiendo del valor de la sesión current_game. 

4) se termina partida con puntuación sin estar autenticado.
Si estamos en alieninvasion, por ejemplo, jugamos una partida y
terminamos con puntuación, se ejecutara una función u otra en el caso de que ganemos 
o que perdamos: si ganamos (game.js de alieninvasion linea 103) si perdemos (linea 113 de game.js 
de alieninvasion). En cada una de estas funciónes se llama una función que se encuentra declarada como
metodo disponible en server.js (linea 104 y 114 de game.js y linea 47 de server.js). A la que se le pasa
el valor de la sesión current_game para saber de qué juego se trata y los puntos. Esta función comprueba 
que el usuario esta autenticado, y si no lo está no almacena ninguna partida. 

5) se termina partida con puntuación estando autenticado.
Al igual que en el apartado anterior, solo que ahora si el usuario está autenticado, se guarda la información
correspondiente a la partida que ha jugado. (linea 51 server.js).

6)¿qué sale en la consola cuando te autenticas (sign in)?

7)¿qué sale en la consola cuando sales (sign out)?