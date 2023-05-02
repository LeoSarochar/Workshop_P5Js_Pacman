# Découverte de P5.JS - Création d'un pacman

Ce workshop vous apprendra à créer un mini-jeu Pacman en utilisant le langage de programmation JavaScript et la bibliothèque p5.js.

Lien vers la documentation de p5.js: https://p5js.org/reference/

## Étape 1: Configuration

Créez un nouveau dossier pour votre projet Pacman.
<br>Dans ce dossier, créez un fichier index.html et un fichier sketch.js.
Ajoutez le code HTML suivant dans index.html:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pacman</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
    <script src="sketch.js"></script>
  </head>
  <body></body>
</html>
```

## Étape 2: Création de la carte

Dans sketch.js, ajoutez le code suivant:

```js
const map = [
  `xxxxxxxxxxxxxxxxxxxxxxxxxxx`,
  `x            x            x`,
  `x xxxx xxxxx x xxxxx xxxx x`,
  `x xxxx xxxxx x xxxxx xxxx x`,
  `x xxxx xxxxx x xxxxx xxxx x`,
  `x                         x`,
  `x xxxx x xxxxxxxxx x xxxx x`,
  `x      x     x     x      x`,
  `xxxxxx xxxxx!x!xxxxx xxxxxx`,
  `!!!!!x x!!!!!1!!!!!x x`,
  `xxxxxx x!xxxx_xxxx!x xxxxxx`,
  `x      !!x!!234!!x!!      x `,
  `xxxxxx x!xxxxxxxxx!x xxxxxx`,
  `!!!!!x x!!!!!!!!!!!x x`,
  `xxxxxx x!xxxxxxxxx!x xxxxxx`,
  `x            x            x`,
  `x xxxx xxxxx x xxxxx xxxx x`,
  `x    x       P       x    x`,
  `xxxx x x xxxxxxxxx x x xxxx`,
  `x      x     x     x      x`,
  `x xxxxxxxxxx x xxxxxxxxxx x`,
  `x                         x`,
  `xxxxxxxxxxxxxxxxxxxxxxxxxxx`,
];

// We copy the map to keep the original
const originalMap = map.map((row) => row);

const tileSize = 20;
```

Sur cette map, les murs sont représentés par la lettre x, les pac-gommes par les espaces, les fantômes par la lettre 1, 2, 3 ou 4, et Pacman par la lettre P.<br>
Les "!" sont les endroits où il n'y a pas de pac-gommes.

## Étape 3: Fonctions setup() et draw()

Ajoutez les fonctions setup() et draw() suivantes à votre fichier sketch.js. Vous compléterez la fonction draw() plus tard.

```js
function setup() {
  createCanvas(map[0].length * tileSize, map.length * tileSize);
}

function draw() {
  background(0);
  // Vous compléterez cette fonction plus tard.
}
```

Vous devriez désormais pouvoir tester votre programme, il suffit d'utiliser l'extension [LiveServer](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) pour Visual Studio Code qui permet de lancer un server web qui s'actualise à chaque changement.<br>
Si vous voyez un carré noir, tout est bon !

## Étape 4: Dessiner la carte

Ajoutez la fonction `drawMap()` dans sketch.js. Cette fonction permet de dessiner la carte Pacman.<br>Utilisez une boucle imbriquée pour parcourir chaque case de la carte et dessinez les éléments en fonction de leur type.<br>Par exemple, pour les murs (x), utilisez la couleur bleue et la fonction rect() pour dessiner des rectangles.

La position du rectangle doit être

```
x = x * tileSize
y = y * tileSize
w = tileSize
h = tileSize
```

```js
function drawMap() {
  for (let y = 0; y < map.length; y++) {
    for (let x = 0; x < map[y].length; x++) {
      switch (map[y][x]) {
        case "x":
          // Use fill fonction to draw in blue
          // Use rect fonction to draw a rectangle
          break;
        case " ":
          // pacgum
          fill(255, 255, 0);
          circle(x * tileSize + tileSize / 2, y * tileSize + tileSize / 2, 5);
          break;
      }
    }
  }
}
```

<span style="color: orange">N'oubliez pas d'appeler la fonction drawMap() dans la fonction draw().</span>

## Étape 5: Dessiner Pacman

Ajoutez la fonction `drawPacman(x, y)` dans sketch.js.

```js
let direction = "";

function drawPacman(x, y) {
  fill(255, 255, 0);
  const centerX = x * tileSize + tileSize / 2;
  const centerY = y * tileSize + tileSize / 2;
  let startAngle, endAngle;

  switch (direction) {
    case "right":
      startAngle = 0.25 * PI;
      endAngle = 1.75 * PI;
      break;
    case "down":
      startAngle = 0.75 * PI;
      endAngle = 2.25 * PI;
      break;
    case "left":
      startAngle = 1.25 * PI;
      endAngle = 0.75 * PI;
      break;
    case "up":
    default:
      startAngle = -0.25 * PI;
      endAngle = 1.25 * PI;
      break;
  }
  arc(centerX, centerY, 20, 20, startAngle, endAngle);
}
```

<span style="color: orange">N'oubliez pas d'appeler la fonction drawPacman() dans la fonction drawMap().</span>

```js
function drawMap() {
  for (let y = 0; y < map.length; y++) {
    for (let x = 0; x < map[y].length; x++) {
      switch (map[y][x]) {
        case "x":
          // Use fill fonction to draw in blue
          // Use rect fonction to draw a rectangle
          break;
        case " ":
          // pacgum
          fill(255, 255, 0);
          circle(x * tileSize + tileSize / 2, y * tileSize + tileSize / 2, 5);
          break;
        case "P":
          // Call drawPacman function
          break;
      }
    }
  }
}
```

## Etape 6 : Dessiner les fantômes

Ajoutez la fonction `drawGhost(x, y)` dans sketch.js.

```js
function drawGhost(x, y) {
  // Draw a ghost but don't set a color with fill, we will do it in the drawMap function
}
```

<span style="color: orange">N'oubliez pas d'appeler la fonction drawGhost() dans la fonction drawMap().</span>

```js
function drawMap() {
  for (let y = 0; y < map.length; y++) {
    for (let x = 0; x < map[y].length; x++) {
      switch (map[y][x]) {
        case "x":
          // Use fill fonction to draw in blue
          // Use rect fonction to draw a rectangle
          break;
        case "P":
          // Call drawPacman function
          break;
        case "1":
          // Use fill fonction to draw in red
          // Call drawGhost function
          break;
        case "2":
          // Use fill fonction to draw in orange
          // Call drawGhost function
          break;
        case "3":
          // Use fill fonction to draw in pink
          // Call drawGhost function
          break;
        case "4":
          // Use fill fonction to draw in cyan
          // Call drawGhost function
          break;
      }
    }
  }
}
```

## Étape 7: Gestion des mouvements

Tout d'abord, il faut récuprer la position de Pacman dans la carte. Pour cela, ajoutez la fonction `getPlayerPosition()` dans sketch.js.

```js
function getPlayerPosition() {
  // We loop over the map to find the position of Pacman, and return it
  // for each row
  // for each column
  // if the current tile is Pacman, we return the position
  // return {x, y}
}
```

Ensuite, il faut récupérer la touche appuyée par l'utilisateur. Pour cela, ajoutez la fonction `keyPressed()` dans sketch.js.

```js
function keyPressed() {
  // We check which key is pressed and we update the direction of Pacman
  // To do this we use the keyCode global variable
  // if the key is LEFT_ARROW, we set the direction global variable to "left"
  // if the key is RIGHT_ARROW, we set the direction to "right"
  // if the key is UP_ARROW, we set the direction to "up"
  // if the key is DOWN_ARROW, we set the direction to "down"
}
```

Enfin, il faut ajouter la fonction `move()` dans sketch.js. Cette fonction permet de déplacer Pacman dans la carte.

```js
// We need this utility fonction to replace a cell value in the map
String.prototype.replaceAt = function (index, replacement) {
  return (
    this.substring(0, index) +
    replacement +
    this.substring(index + replacement.length)
  );
};

function move() {
  // We get the position of Pacman using the getPlayerPosition function
  const { x, y } = getPlayerPosition();
  // We get the next position of Pacman depending on the direction
  let nextPosition = { x, y };
  switch (direction) {
    case "left":
      nextPosition.x--;
      break;
    // ...
  }
  // We check if the next position is a ghost, if it is, the game is over
  if (/* ... */) {
    window.alert("Game Over");
    window.location.reload();
  }
  // We check if the next position is valid (not a wall), If it is valid, we update the map
  if (/* ... */) {
    map[y] = map[y].replaceAt(x, "!");
    map[nextPosition.y] = map[nextPosition.y].replaceAt(nextPosition.x, "P");
  }
}
```

Il faut maintenant appeler la fonction `move()` dans la fonction `draw()` avec une clock.

```js
let previousTime = 0;
function draw() {
  background(0);
  if (millis() - previousTime > 150) {
    move();
    previousTime = millis();
  }
  drawMap();
}
```

Vous devriez pouvoir maintenant vous déplacer dans la map avec les flèches du clavier.

## Étape 8: Déplacement des fantômes

Pour le déplacement des fantômes, nous allons faire de l'aléatoire dans un premier temps.<br>
Ajoutez la fonction `getGhostPositions()` dans sketch.js.

```js
function getGhostPositions() {
  const ghostPositions = [];
  for (let y = 0; y < map.length; y++) {
    for (let x = 0; x < map[y].length; x++) {
      if (["1", "2", "3", "4"].includes(map[y][x])) {
        ghostPositions.push({ x, y, type: map[y][x] });
      }
    }
  }
  return ghostPositions;
}
```

Ensuite, ajoutez la fonction `isValidMove()` et `moveGhosts()` dans sketch.js.

```js
function moveGhosts() {
  // We get the positions of the ghosts
  const ghostPositions = getGhostPositions();
  // We loop over the ghosts
  for (const ghost of ghostPositions) {
    const { x, y, type } = ghost;
    // We define an array of directions
    const directions = [
      { x: -1, y: 0 }, // left
      { x: 1, y: 0 }, // right
      { x: 0, y: -1 }, // up
      { x: 0, y: 1 }, // down
    ];

    const randomDirection =
      directions[Math.floor(Math.random() * directions.length)];
    const nextX = x + randomDirection.x;
    const nextY = y + randomDirection.y;

    // You have to code the isValidMove function
    if (isValidMove(nextX, nextY)) {
      // If the next position is the position of Pacman, the game is over
      if (/* ... */) {
        window.alert("Game Over");
        window.location.reload();
      }
      const oldCharacter = originalMap[y][x];
      if (oldCharacter === " ") {
        map[y] = map[y].replaceAt(x, " ");
      } else {
        map[y] = map[y].replaceAt(x, "!");
      }
      map[nextY] = map[nextY].replaceAt(nextX, type);
    }
  }
}
```

<span style="color: orange">N'oubliez pas d'appeler la fonction moveGhosts() dans la fonction draw() dans la clock.</span>

## Étape 9: Ajout du score

Vous pouvez maintenant ajouter le score dans le jeu. Pour cela, vous devrez ajouter une variable `score` et l'incrémenter à chaque fois que Pacman mange une pac-gomme.

Ensuite utilisez les fonctions `text()` et `textSize()` pour afficher le score à l'écran.

```js
function drawScore() {
  // fill text color
  // set text size
  // draw text
}
```

N'oubliez pas d'appeler la fonction `drawScore()` dans la fonction `draw()`.

## Étape 10: Bonus

Si vous êtes arrivé jusque là vous pouvez essayer de faire les bonus suivants :

- Utiliser la librairie p5.sound pour ajouter de la musique et un son à chaque fois que Pacman mange une pac-gomme.
- Ajouter un menu de démarrage avec un bouton "Start" et un bouton "High Score".
- Utiliser la librairie p5.dom pour ajouter un champ de texte dans le menu de démarrage pour rentrer son nom.
- Utiliser la librairie p5.astar pour faire bouger les fantômes de manière intelligente.
