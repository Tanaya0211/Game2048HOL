Create the Game 2048 with Java 8 and JavaFX
===========
By developing the famous game 2048 with JavaFX and Java 8 in this hands‐on lab session, you will encounter several new language features such as Stream API, lambda expressions, and new util classes and methods. You will also learn basic concepts of JavaFX 2‐D animations, parallel processing, UI design, CSS 
styling, and more. 
 
# Project Base
Open the repo and have a look at the project: 
```
https://github.com/jperedadnr/Game2048HOL.git
```
The starting project is a JavaFX application with the following Java classes:
- Game2048
- GameManager
- Board
- Tile
- Location
- Direction
- GridOperator

And the following resources to style the visual:
- game.css
- ClearSans‐Bold.ttf 

Some classes and methods are lacking implementations. Follow this guide step by step to fullfil the missing code. Complete the methods and have a fully operative version of the game 2048 FX. Basically you’ll just have to copy and paste the snippets of code available on each step. 

Please follow carefully every step. Try to build and run the application every now and then to check you didn’t miss any step and everything is in place. Fill free to ask any questions along the way. 

## STEP 0. Clone the repository
Open NetBeans 8.0 and under **Team ‐> Git** select **Clone** ant type this URL:
```
https://github.com/jperedadnr/Game2048Empty.git
```

 * Accept the default destination folder or choose one
 * Select branch and click Next/Finish
 * Wait till the local copy is created, and the project is opened in NetBeans
 * Select Build and Run to test the (empty) application

Now follow these steps

### INDEX
##### 1. [Add GameManager into Game2048][I1]
##### 2. [Add a Board into GameManager][I2]
##### 3. [Create a score to visualize points][I3]
##### 4. [Define rectangle corner border size][I4]
##### 5. [Draw a grid of rectangles in the Board][I5]
##### 6. [Add Tiles into the grid][I6]
##### 7. [Create a random Tile][I7]
##### 8. [Layout the tile at its location][I8]
##### 9. [Let's start the Game!][I9]
##### 10. [CSS styling][I10]
##### 11. [Connect arrow keys with Direction][I11]
##### 12. [Moving one tile][I12]
##### 13. [Moving tiles on the board][I13]
##### 14. [Listening to arrow keys][I14]
##### 15. [Initializing the game][I15]
##### 16. [Random tiles, random locations][I16]
##### 17. [How far can a tile go?][I17]
##### 18. [A new approach to move the tiles][I18]
##### 19. [Animating one tile movement][I19]
##### 20. [Animating all the tiles together][I20]
##### 21. [Find a random available location][I21]
##### 22. [Adding and animating new tiles][I22]

***

## STEP 1. Add GameManager into Game2048
Create an instance of `GameManager` in `Game2048` class and add it to the `root` object (StackPane).

### SOLUTION CODE
* *Class*: `Game2048`
* *Method*: `start`
* [preview][1]
* Copy and paste the following code snippet:
```java
gameManager = new GameManager();
root.getChildren().add(gameManager);
```
Back to [Index][I0]
***
## STEP 2. Add a Board into GameManager
Create an instance of `Board` in `GameManager` class and add it to its list of children.

### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: constructor
* [preview][2]
* Copy and paste the following code snippet:
```java
board = new Board();
getChildren().add(board);
```
Back to [Index][I0]
***
## STEP 3. Create a score to visualize points
Create nodes for `hTop` in `createScore()`, with these steps: 
- Create a `Label` named `lblTitle` with text `"2048"` and other named `lblSubtitle` with text`"FX"`
- Create an empty `HBox` named `hFill` and set its horizontal grow priority to grow always
- Create a `VBox` named `vScores` and an `HBox`named `hScores` with spacing 5
- Create a `Label` named `lblTit` with text `"SCORE"`, and add it to `vScore`, as well as `lblScore`
- Create a `VBox` named `vRecord` and a `Label` named `lblTitBest` with text `"BEST"`, and add it to `vRecord`, as well as `lblBest`
- Add `vScore` and `vRecord` to `hScores`, create a `VBox` named `vFill` with vertical grow priority to grow always, and add `hScores`and `vFill` to `vScores`
- Finally, add `lblTitle`, `lblSubtitle`, `hFill` and `vScores` to `hTop` 
 
#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `createScore()`
* [preview][3.1]
* Copy and paste the following code snippet:
```java
createScore() {
    Label lblTitle = new Label("2048");
    Label lblSubtitle = new Label("FX");

    HBox hFill = new HBox();
    HBox.setHgrow(hFill, Priority.ALWAYS);

    VBox vScores = new VBox();
    HBox hScores = new HBox(5);

    Label lblTit = new Label("SCORE");
    vScore.getChildren().addAll(lblTit, lblScore);

    VBox vRecord = new VBox(0);
    Label lblTitBest = new Label("BEST");
    vRecord.getChildren().addAll(lblTitBest, lblBest);

    hScores.getChildren().addAll(vScore,vRecord);
    VBox vFill = new VBox();
    VBox.setVgrow(vFill, Priority.ALWAYS);
    vScores.getChildren().addAll(hScores,vFill);

    hTop.getChildren().addAll(lblTitle, lblSubtitle, hFill,vScores);
}
```

Call the method `createScore()` from the constructor of `Board`

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: constructor
* [preview][3.2]
* Copy and paste the following code snippet:
```java
createScore();
```
Back to [Index][I0]
***
## STEP 4. Define rectangle corner border size
Create a rectangle located in corners `i*cell_size`, `j*cell_size`, of size `cell_size`x`cell_size`, filled with white color, and with border grey

### SOLUTION CODE
* *Class*: `Board`
* *Method*: `createCell`
* [preview][4]
* Copy and paste the following code snippet:
```java
cell = new Rectangle(i * CELL_SIZE, j * CELL_SIZE, CELL_SIZE, CELL_SIZE);
cell.setFill(Color.WHITE);
cell.setStroke(Color.GREY);
```
Back to [Index][I0]
***
## STEP 5. Draw a grid of rectangles in the Board
Add 4x4 cells to gridGroup, by calling `createCell` method for every cell

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `createGrid`
* [preview][5.1]
* Copy and paste the following code snippet:
```java
for(int i=0; i<4; i++){
    for(int j=0; j<4; j++){
        gridGroup.getChildren().add(createCell(i, j));
    }
}
```

Call method `createGrid()` from constructor of class `Board` 

#### SOLUTION CODE
* *Class*: `Board`
* *Method*: constructor
* [preview][5.2]
* Copy and paste the following code snippet:
```java
createGrid();
```

### Screenshot after Step 5
Run the project to see the application after completing the first 5 steps
![Game2048 after 5 steps][screen5]

Back to [Index][I0]
***
## STEP 6. Add Tiles into the Grid
- Set the size of the tile to `Board.CELL_SIZE-13` to account for the stroke width
- For now, style the tile background with `#c9c9c9` color
- Set the tile alignement centered
- Assign the value from the argument to `value`
- Finally, set the text with this value, and initialized `merged` as false.
 
### SOLUTION CODE
* *Class*: `Tile`
* *Method*: private constructor
* [preview][6]
* Copy and paste the following code snippet:
```java
final int squareSize = Board.CELL_SIZE - 13;
setMinSize(squareSize, squareSize);
setMaxSize(squareSize, squareSize);
setPrefSize(squareSize, squareSize);
setStyle("-fx-background-color: #c9c9c9;");
setAlignment(Pos.CENTER);

this.value = value;
this.merged = false;
setText(Integer.toString(value));
```
Back to [Index][I0]
***
## STEP 7. Create a random Tile 
Create a new `Tile` instance, which value being **2** with a 90% possibility or **4** with the 10% remaining

### SOLUTION CODE 
* *Class*: `Tile`
* *Method*: `newRandomTile`
* [preview][7]
* Copy and paste the following code snippet:
```java
return newTile(new Random().nextDouble() < 0.9 ? 2 : 4);
```
Back to [Index][I0]
***
## STEP 8. Layout the tile at its location
Set the tile layout by getting from its location the position at the center of the cell and 
substracting half of the tile dimensions

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `moveTile`
* [preview][8.1]
* Copy and paste the following code snippet:
```java
double layoutX = tile.getLocation().getLayoutX(CELL_SIZE) - (tile.getMinWidth() /
2);
double layoutY = tile.getLocation().getLayoutY(CELL_SIZE) - (tile.getMinHeight()
/ 2);
tile.setLayoutX(layoutX);
tile.setLayoutY(layoutY);
```

Add a call to `moveTile` when a tile is added

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `addTile`
* [preview][8.2]
* Copy and paste the following code snippet:
```java
moveTile(tile, tile.getLocation());
```
Back to [Index][I0]
***
## STEP 9. Let's start the Game! 
Add a random tile a location of your choosing to the board

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `startGame`
* [preview][9.1]
* Copy and paste the following code snippet:
```java
Tile tile0 = Tile.newRandomTile();
tile0.setLocation(new Location(1,2));
board.addTile(tile0);
```

Add a call to `startGame` in the `GameManager` constructor 

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: constructor
* [preview][9.2]
* Copy and paste the following code snippet:
```java
startGame();
```
### Screenshot after #9 
Run the project to see the application after completing the first 9 steps
![Game2048 after 9 steps][screen9]
 
Back to [Index][I0]
*** 
## STEP 10. CSS styling
Load the font *ClearSans-Bold.ttf* at the beginning of the application

#### SOLUTION CODE 
* *Class*: `Game2048`
* *Method*: `init`
* [preview][10.1]
* Copy and paste the following code snippet:
```java
Font.loadFont(Game2048.class.getResource("ClearSans-Bold.ttf").toExternalForm(),10.0);
```

Enable css styling in the application by loading the *game.css* file. Apply `"game-root"` selector to the root

#### SOLUTION CODE 
* *Class*: `Game2048`
* *Method*: `start`
* [preview][10.2]
* Copy and paste the following code snippet:
```java
scene.getStylesheets().add(Game2048.class.getResource("game.css").toExternalForm());
root.getStyleClass().addAll("game-root");
```

Apply the styles to nodes in the `hTop` container: 
- `lblTitle`: `"game-label"`, `"game-title"` 
- `lblSubtitle`: `"game-label"`, `"game-subtitle"` 
- `vScore` and `vRecord`:, `"game-vbox"`
- `lblScore`: `"game-label"`, `"game-score"` 
- `lblTit`: `"game-label"`, `"game-titScore"`
- `lblTitBest`: `"game-label"`, `"game-titScore"` 
- `lblBest`: `"game-label"`, `"game-score"`

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `createScore`
* [preview][10.3]
* Copy and paste the following code snippet:
```java
lblTitle.getStyleClass().addAll("game-label","game-title");
lblSubtitle.getStyleClass().addAll("game-label","game-subtitle");
vScore.getStyleClass().add("game-vbox");
lblTit.getStyleClass().addAll("game-label","game-titScore");
lblScore.getStyleClass().addAll("game-label","game-score");
vRecord.getStyleClass().add("game-vbox");
lblTitBest.getStyleClass().addAll("game-label","game-titScore");
lblBest.getStyleClass().addAll("game-label","game-score");
```

Adjust arc size in cells to `cell_size/6` and apply `"game-grid-cell"` style

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `createCell`
* [preview][10.4]
* Copy and paste the following code snippet:
```java
cell.setArcHeight(CELL_SIZE/6d);
cell.setArcWidth(CELL_SIZE/6d);
cell.getStyleClass().add("game-grid-cell");
```

Apply `"game-grid"` to `gridGroup` and `"game-backGrid"` to `hBottom` 

#### SOLUTION CODE 
* *Class*: `Board`
* *Method*: `createGrid`
* [preview][10.5]
* Copy and paste the following code snippet:
```java
gridGroup.getStyleClass().add("game-grid");
hBottom.getStyleClass().add("game-backGrid");
```

Apply to tiles the styles `"game-label"` and `"game-tile-"+value`, and remove 
the previusly assigned style. 

#### SOLUTION CODE 
* *Class*: `Tile`
* *Method*: private constructor
* [preview][10.6]
* Copy and paste the following code snippet:
```java
getStyleClass().addAll("game-label", "game-tile-" + value);
```

### Screenshot after #10
Run the project to see the application after completing the first 10 steps
![Game2048 after 10 steps][screen10]
 
Back to [Index][I0]
***
## STEP 11. Connect arrow keys with Direction
Return the enum constant of the type with the specified name from a KeyCode 

### SOLUTION CODE 
* *Class*: `Direction`
* *Method*: `valueFor`
* [preview][11]
* Copy and paste the following code snippet:
```java
return valueOf(keyCode.name());
```
Back to [Index][I0]
***
## STEP 12. Moving one tile 
Return a new Location based on the actual and an offset in the specified direction 

### SOLUTION CODE 
* *Class*: `Location`
* *Method*: `offset`
* [preview][12]
* Copy and paste the following code snippet:
```java
return new Location(x + direction.getX(), y + direction.getY());
```
Back to [Index][I0]
***
## STEP 13. Moving tiles on the board 
- Get a list of tiles in the `gridGroup` and then remove all the list from 
the `gridGroup`
- Create new tiles based in the old ones, applying an offset in the specified direction
to their current location, checking if the new location is valid and it doesn't contain another tile. 
Otherwise keep the previous location. Then add them to the `gridGroup`
 
### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][13]
* Copy and paste the following code snippet:
```java
List<Tile> tiles=board.getGridGroup().getChildren().stream()
        .filter(g->g instanceof Tile).map(t->(Tile)t)
        .collect(Collectors.toList());
board.getGridGroup().getChildren().removeAll(tiles);
tiles.forEach(t->{
    Tile newTile = Tile.newTile(t.getValue());
    final Location newLoc=t.getLocation().offset(direction);
    if(newLoc.isValidFor() && 
       !tiles.stream().filter(t2->t2.getLocation().equals(newLoc)).findAny().isPresent()){
        newTile.setLocation(newLoc);
    } else {
        newTile.setLocation(t.getLocation());
    }
    board.addTile(newTile);
});
```

Back to [Index][I0]
***
## STEP 14. Listening to arrow keys 
Add a listener to the scene for keys pressed, then get the key code, check if it is an arrow key. 
In such case get the direction for that arrow and move tile

### SOLUTION CODE 
* *Class*: `Game2048`
* *Method*: `start`
* [preview][14]
* Copy and paste the following code snippet:
```java
scene.setOnKeyPressed(ke -> {
    KeyCode keyCode = ke.getCode();
    if(keyCode.isArrowKey()){
        Direction dir = Direction.valueFor(keyCode);
        gameManager.move(dir);
    }
});
```

### Screenshot after #14 
Run the project to see the application after completing the first 14 steps. 
Press the right arrow and check the tile from [Screenshot #10][screen10] moves one cell to the right
![Game2048 after 14 steps][screen14]

Back to [Index][I0]
***
## STEP 15. Initializing the game 
Clear the gameGrid map and the locations list, and then initialize both with all 4x4 valid locations, 
and null tiles

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `initializeGameGrid`
* [preview][15.1]
* Copy and paste the following code snippet:
```java
gameGrid.clear();
locations.clear();
for(int i=0; i<4; i++){
    for(int j=0; j<4; j++){
        Location location = new Location(i,j);
        locations.add(location);
        gameGrid.put(location, null);
    }
}
```

Call `initializeGameGrid` before `startGame`

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: constructor
* [preview][15.2]
* Copy and paste the following code snippet:
```java
initializeGameGrid();
gameGrid.clear()
```

Back to [Index][I0]
***
## STEP 16. Random tiles, random locations 
Shuffle a copy of `locations` list, and add two random tiles at the first two locations of the shuffled 
list to `gameGrid` and call `redrawTilesInGameGrid`

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `startGame`
* [preview][16.1]
* Copy and paste the following code snippet:
```java
List<Location> locCopy=locations.stream().collect(Collectors.toList());
Collections.shuffle(locCopy);
tile0.setLocation(locCopy.get(0));
gameGrid.put(tile0.getLocation(), tile0);
Tile tile1 = Tile.newRandomTile();
tile1.setLocation(locCopy.get(1));
gameGrid.put(tile1.getLocation(), tile1);

redrawTilesInGameGrid();
```

Add to the board all valid tiles in gameGrid

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `redrawTilesInGameGrid`
* [preview][16.2]
* Copy and paste the following code snippet:
```java
gameGrid.values().stream().filter(Objects::nonNull).forEach(board::addTile);
```

Back to [Index][I0]
***
## STEP 17. How far can a tile go?
Search for the farthest location a tile can be moved in the specified direction, 
over empty cells and inside the grid

### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `findFarthestLocation`
* [preview][17]
* Copy and paste the following code snippet:
```java
do {
    farthest = location;
    location = farthest.offset(direction);
} while (location.isValidFor() && gameGrid.get(location)==null);
```

Back to [Index][I0]
***
## STEP 18. A new approach to move the tiles   
Instead of using `board.gridGroup` from [Step 13][I13] to move the tiles, we'll use now `gameGrid`, 
using a double `IntStream` to traverse the grid. 

For every valid tile:
- Find the farthest location possible. 
- If it's different from the actual one:
  - Set its layout with `board.moveTile()`
  - Update `gameGrid` in the old location with null
  - Update `gameGrid` with the tile in the new location, 
  - Finally set the location of the tile.

> **Note**: There's an issue with this approach, as the followed order is from top to bottom or left to right. 
The first tiles can't be moved as the next ones hasn't been moved jet, and they get stuck. This will be addressed later on.

### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][18]
* Copy and paste the following code snippet:
```java
IntStream.range(0, 4).boxed().forEach(i->{
    IntStream.range(0, 4).boxed().forEach(j->{
        Tile t=gameGrid.get(new Location(i,j));
        if(t!=null){
            final Location newLoc=findFarthestLocation(t.getLocation(),direction);
            if(!newLoc.equals(t.getLocation())){
                board.moveTile(t, newLoc);
                gameGrid.put(newLoc, t);
                gameGrid.replace(t.getLocation(),null);
                t.setLocation(newLoc);
            }
        }
    });
});
```

Back to [Index][I0]
***
## STEP 19. Animating one tile movement 
Animate the tile translation from its actual location to the new one, in 65 ms. 
### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `animateExistingTile`
* [preview][19]
* Copy and paste the following code snippet:
```java
KeyValue kvX = new KeyValue(tile.layoutXProperty(),
                            newLocation.getLayoutX(Board.CELL_SIZE) - (tile.getMinHeight() / 2), 
                            Interpolator.EASE_OUT);
KeyValue kvY = new KeyValue(tile.layoutYProperty(),
                            newLocation.getLayoutY(Board.CELL_SIZE) - (tile.getMinHeight() / 2), 
                            Interpolator.EASE_OUT);
KeyFrame kfX = new KeyFrame(Duration.millis(65), kvX);
KeyFrame kfY = new KeyFrame(Duration.millis(65), kvY);
timeline.getKeyFrames().add(kfX);
timeline.getKeyFrames().add(kfY);
```

Back to [Index][I0]
***
## STEP 20. Animating all the tiles together
All the tile animations will be executed at the same time using a `ParallelTransition`. 
While playing no movement will be allowed. Use the volatile `movingTiles` to exit `move` when it's true

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][20.1]
* Copy and paste the following code snippet:
```java
synchronized (gameGrid) {
    if (movingTiles) {
        return;
    }
}
```
While traversing the grid with valid tiles, add those that are moving to the `parallelTranstion`, 
instead of using `board.moveTile`

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][20.2]
* Copy and paste the following code snippet:
```java
parallelTransition.getChildren().add(animateExistingTile(t, newLoc));
```

Add a listener to find when the animations have finished, and there set `movingTiles` to false

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][20.3]
* Copy and paste the following code snippet:
```java
parallelTransition.setOnFinished(e -> {
    synchronized (gameGrid) {
        movingTiles = false;
    }
});
```

Set `movingTiles` to true. start the animation and clear de list of animations.

#### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][20.4]
* Copy and paste the following code snippet:
```java
synchronized (gameGrid) {
    movingTiles = true;
}
parallelTransition.play();
parallelTransition.getChildren().clear();
```

### Screenshot after #20 
Run the project to see the application after completing the first 20 steps. 
Press an arrow and check the tiles are moving smoothly to the farthest position in the grid
![Game2048 after 20 steps][screen20]

Back to [Index][I0]
***
## STEP 21. Find a random available location 
Get a list of available locations on the grid with no tile, shuffle this collection to get a random position, 
if there's any left, returning the first one in that case

### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `findRandomAvailableLocation`
* [preview][21]
* Copy and paste the following code snippet:
```java
List<Location> availableLocations = locations.stream().filter(l -> gameGrid.get(l) == null)
    .collect(Collectors.toList());

if (availableLocations.isEmpty()) {
    return null;
}

Collections.shuffle(availableLocations);
location = availableLocations.get(0);
```

Back to [Index][I0]
***
## STEP 22. Adding and animating new tiles
Create a new tile at the specified location, with scale set to 0. Add it to the `board`, and to the `gameGrid`.
Create a `ScaleTransition` to scale it to 1, in 125 ms, with an easy_out interpolation and play it
 
### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `addAndAnimateRandomTile`
* [preview][22]
* Copy and paste the following code snippet:
```java
Tile tile = Tile.newRandomTile();
tile.setLocation(randomLocation);
tile.setScaleX(0); 
tile.setScaleY(0);
board.addTile(tile);
gameGrid.put(tile.getLocation(), tile);

final ScaleTransition scaleTransition = new ScaleTransition(Duration.millis(125), tile);
scaleTransition.setToX(1.0);
scaleTransition.setToY(1.0);
scaleTransition.setInterpolator(Interpolator.EASE_OUT);

scaleTransition.play();
```

Back to [Index][I0]
***
## STEP 23 
When the parallel transition has finished, get a random location, check if it is not null, 
and create a random tile, add call `addAndAnimateRandomTile`. Else print "Game Over" for the time being 

### SOLUTION CODE 
* *Class*: `GameManager`
* *Method*: `move`
* [preview][23]
* Copy and paste the following code snippet:
```java
parallelTransition.setOnFinished(){
Location randomAvailableLocation = findRandomAvailableLocation();
if (randomAvailableLocation != null){
    addAndAnimateRandomTile(randomAvailableLocation);
} else {
    System.out.println("Game Over");
}
```

### Screenshot after #23 
Run the project to see the application after completing the first 23 steps. 
Press the arrows in any directions, check the tiles are moving smoothly to the farthest position 
in the grid, and after each movement a new tile appears
![Game2048 after 23 steps][screen23]

Back to [Index][I0]
***
## STEP 24 
In GridOperator, traverseGrid method, apply the application of a functional to every cell of the 
grid, returning an int with the sum of the results of this functional. 
### SOLUTION CODE 
traverseGrid(){
traversalX.forEach(x -> {
traversalY.forEach(y -> {
at.addAndGet(func.applyAsInt(x, y));
});
});
}
Back to [Index][I0]
***
## STEP 25 
In GameManager. initializeGameGrid method, replace the double for with the traverseGrid 
method. 
In GameManager.move method, replace the IntStreams with the traverseGrid method. Assign 
to  tilesWereMoved  to account for the tiles moved.  
In GameManager.move.setOnFinished, before adding a tile, check there were some 
movements done. 
In Board.createGrid, replace the double for with the traverseGrid 
### SOLUTION CODE 
initializeGameGrid(){
GridOperator.traverseGrid((i, j) -> {
Location location = new Location(i,j);
locations.add(location);
gameGrid.put(location, null);
return 0;
});
}
move(){
tilesWereMoved = GridOperator.traverseGrid((i,j)->{
Tile t=gameGrid.get(new Location(i,j));
if(t!=null){
final Location
newLoc=findFarthestLocation(t.getLocation(),direction);
if(!newLoc.equals(t.getLocation())){
parallelTransition.getChildren().add(animateExistingTile(t,
newLoc));
gameGrid.put(newLoc, t);
gameGrid.replace(t.getLocation(),null);t.setLocation(newLoc);
return 1;
}
}
return 0;
});
}
move(){
setOnFinished(){
if(tilesWereMoved>0){
addAndAnimateRandomTile(randomAvailableLocation);
}
}
}
createGrid(){
GridOperator.traverseGrid((i, j) -> {
gridGroup.getChildren().add(createCell(i, j));
return 0;
});
}
Back to [Index][I0]
***
## STEP 26 
In GridOperator, sort the traverse X,Y list, so for Right or Down directions traverseX,Y are taken 
in reverse order. In move, first of all call sortGrid before traverseGrid. 
### SOLUTION CODE 
sortGrid(){
Collections.sort(traversalX, direction.equals(Direction.RIGHT) ?
Collections.reverseOrder() : Integer::compareTo);
Collections.sort(traversalY, direction.equals(Direction.DOWN)?
Collections.reverseOrder() : Integer::compareTo);
}
move(){
GridOperator.sortGrid(direction);
}
Back to [Index][I0]
***
## STEP 27 
In Tile. merge method, add to tile’s value the value of the tile to be merged to, set the text of 
the label with the new value and replace the old style ‘game‐title‐“‐value with the new one. In 
Tile.isMergeable Check it this.tile can be merged with anotherTile 
### SOLUTION CODE 
merge(){getStyleClass().remove("game-tile-" + value);
this.value += another.getValue();
setText(Integer.toString(value));
merged = true;
getStyleClass().add("game-tile-" + value);
}
isMergeable(){
return anotherTile != null && getValue()==anotherTile.getValue();
}
Back to [Index][I0]
***
## STEP 28 
In GameManager. animateMergedTile method, add a sequential animation, with two scale 
animations, from 1 to 1.2, ease_in, and from 1.2 to 1 ease_out, in 80 ms each 
### SOLUTION CODE 
animateMergedTile(){
final ScaleTransition scale0 = new ScaleTransition(Duration.millis(80), tile);
scale0.setToX(1.2);
scale0.setToY(1.2);
scale0.setInterpolator(Interpolator.EASE_IN);
final ScaleTransition scale1 = new ScaleTransition(Duration.millis(80), tile);
scale1.setToX(1.0);
scale1.setToY(1.0);
scale1.setInterpolator(Interpolator.EASE_OUT);
return new SequentialTransition(scale0, scale1);
}
Back to [Index][I0]
***
## STEP 29 
In GameManager.move method, get tile for an offset, check if it's a valid tile, not merged, and 
check if tiles can be merged. Then merge  this new tile with the old one, move to front the new 
tile, put the nextLocation on the map, with the new tile and replace last location with null. Add 
old tile to animateExistingTile, and new one to animateMerdedTile. Add old tile to 
mergedToBeRemoved, and return 1. 
### SOLUTION CODE 
move(){
Location nextLocation = newLoc.offset(direction);
Tile tileToBeMerged = nextLocation.isValidFor() ? gameGrid.get(nextLocation) :
null;
if (tileToBeMerged != null && !tileToBeMerged.isMerged() &&
t.isMergeable(tileToBeMerged)) {
tileToBeMerged.merge(t);tileToBeMerged.toFront();
gameGrid.put(nextLocation, tileToBeMerged);
gameGrid.replace(t.getLocation(), null);
parallelTransition.getChildren().add(animateExistingTile(t,
nextLocation));
parallelTransition.getChildren().add(animateMergedTile(tileToBeMerged));
mergedToBeRemoved.add(t);
return 1;
}
}
Back to [Index][I0]
***
## STEP 30 
In GameManager.move, on finished method, remove the tiles in the set from the gridGroup 
and clear the set. For all the tiles on the board: set to false their merged value. 
### SOLUTION CODE 
move(){
setOnFinished(){
board.getGridGroup().getChildren().removeAll(mergedToBeRemoved);
mergedToBeRemoved.clear();
gameGrid.values().stream().filter(Objects::nonNull).forEach(t-
>t.setMerged(false));
}
}
Screenshot after #30 
Back to [Index][I0]
***
## STEP 31 
In Board.createGrid, to avoid dropshadow effect of higher tiles move the grid, add a rectangle 
to clip hBottom. 
### SOLUTION CODE 
createGrid(){
Rectangle rect = new Rectangle(GRID_WIDTH, GRID_WIDTH);
hBottom.setClip(rect);
}
Back to [Index][I0]
***
## STEP 32 
In Board.createScore, add style for lblPoints, add to board. Add a listener to text changes, so it 
gets centered right below the center of vScore. 
### SOLUTION CODE 
createScore(){
lblPoints.getStyleClass().addAll("game-label","game-points");
lblPoints.setAlignment(Pos.CENTER);
lblPoints.setMinWidth(100);
getChildren().add(lblPoints);
}
Back to [Index][I0]
***
## STEP 33 
In Board.createScore, bind lblPoints  to gameMovePoints with a “+” prefix, if points>0, and 
bind the lblScore text property with the gameScore property. 
In Board.addPoints, add the points to gameMove and gameScore property. 
In GameManager.move, reset the points before traverseGrid, and add the points for every 
merged cell 
### SOLUTION CODE 
createScore(){
lblPoints.textProperty().bind(Bindings.createStringBinding(()->
(gameMovePoints.get()>0)?"+".concat(Integer.toString(gameMovePoints.get()
)):"", gameMovePoints.asObject()));
lblScore.textProperty().bind(gameScoreProperty.asString());
}
addPoints(){
gameMovePoints.set(gameMovePoints.get() + points);
gameScoreProperty.set(gameScoreProperty.get() + points);
}
move(){
board.setPoints(0);
}move(){
board.addPoints(tileToBeMerged.getValue());
}
Back to [Index][I0]
***
## STEP 34 
In Board.createScore, add a listener to lblPoints text changes, so it gets centered right below 
the center of vScore. 
### SOLUTION CODE 
createScore(){
lblPoints.textProperty().addListener((ov,s,s1)->{
lblPoints.setLayoutX(0);
double midScoreX=vScore.localToScene(vScore.getWidth()/2d,0).getX();
lblPoints.setLayoutX(lblPoints.sceneToLocal(midScoreX, 0).getX()-
lblPoints.getWidth()/2d);
});
}
Back to [Index][I0]
***
## STEP 35 
In Board.createScore, create the timeline to translate the lblPoints in Y from 20 to 100 and 
reduce its opacity from 1 to 0 in 600 ms. 
In Board.animateScore, start the animation. 
In GameManager.move call board.animateScore after traverseGrid. 
### SOLUTION CODE 
createScore(){
final KeyValue kvO0 = new KeyValue(lblPoints.opacityProperty(), 1);
final KeyValue kvY0 = new KeyValue(lblPoints.layoutYProperty(), 20);
final KeyValue kvO1 = new KeyValue(lblPoints.opacityProperty(), 0);
final KeyValue kvY1 = new KeyValue(lblPoints.layoutYProperty(), 100);
final KeyFrame kfO0 = new KeyFrame(Duration.ZERO, kvO0);
final KeyFrame kfY0 = new KeyFrame(Duration.ZERO, kvY0);
Duration animationDuration = Duration.millis(600);
final KeyFrame kfO1 = new KeyFrame(animationDuration, kvO1);
final KeyFrame kfY1 = new KeyFrame(animationDuration, kvY1);
animateAddedPoints.getKeyFrames().addAll(kfO0,kfY0,kfO1,kfY1);
}
animateScore(){
animateAddedPoints.playFromStart();
}move(){
board.animateScore();
}
Screenshot after #35 
 
Back to [Index][I0]
***
## STEP 36 
In GameManager.mergeMovementsAvailable, traverse the grid in two directions (Up, Left) and 
for every tile look if the offset tile is mergeable. 
### SOLUTION CODE 
mergeMovementsAvailable(){
Stream.of(Direction.UP, Direction.LEFT).parallel().forEach(direction -> {
GridOperator.traverseGrid((x, y) -> {
Location thisloc = new Location(x, y);
Tile t1=gameGrid.get(thisloc);
if(t1!=null){
Location nextLoc=thisloc.offset(direction);
if(nextLoc.isValidFor()){
Tile t2=gameGrid.get(nextLoc);
if(t2!=null && t1.isMergeable(t2)){
numMergeableTile.incrementAndGet();
}
}
}
return 0;});
});
}
Back to [Index][I0]
***
## STEP 37 
In GameManager.move.setOnFinished, call mergeMovementsAvailable if 
randomAvailableLocation == null and print Game Over, else try to add a new tile if tiles were 
moved 
In GameManager.addAndAnimateRandomTile, after last movement on full grid, check if there 
are movements available  
### SOLUTION CODE 
setOnFinished(){
if(mergeMovementsAvailable()==0){
System.out.println("Game Over");
};
}
addAndAnimateRandomTile(){
scaleTransition.setOnFinished(e -> {
if (gameGrid.values().parallelStream().noneMatch(Objects::isNull) &&
mergeMovementsAvailable()==0 ) {
System.out.println("Game Over");
}
});
}
Back to [Index][I0]
***
## STEP 38 
In GameManager.move, check if the merged tile is 2048, and print win.  
### SOLUTION CODE 
move(){
if(tileToBeMerged.getValue()==2048){
System.out.println("You win!");
}
}
Back to [Index][I0]
***
## STEP 39 
In Board.initGameProperties, style buttons, set listeners to click. In both, remove overlay. In 
bTry also remove tiles and reset all game properties.  
### SOLUTION CODE 
initGameProperties(){
bTry.getStyleClass().add("game-button");
bTry.setOnAction(e->{getChildren().removeAll(overlay, buttonsOverlay);
gridGroup.getChildren().removeIf(c->c instanceof Tile);
resetGame.set(false);
gameScoreProperty.set(0);
gameWonProperty.set(false);
gameOverProperty.set(false);
resetGame.set(true);
});
bContinue.getStyleClass().add("game-button");
bContinue.setOnAction(e->getChildren().removeAll(overlay, buttonsOverlay));
}
Back to [Index][I0]
***
## STEP 40 
In Board.initGameProperties, add listeners to game over, won properties. Set style to overlay, 
set text and its style, add buttons, and add overlay to board. 
### SOLUTION CODE 
initGameProperties(){
gameOverProperty.addListener((observable, oldValue, newValue) -> {
if (newValue) {
overlay.getStyleClass().setAll("game-overlay","game-overlay-
over");
lOvrText.setText("Game over!");
lOvrText.getStyleClass().setAll("game-label","game-lblOver");
buttonsOverlay.getChildren().setAll(bTry);
this.getChildren().addAll(overlay,buttonsOverlay);
}
});
gameWonProperty.addListener((observable, oldValue, newValue) -> {
if (newValue) {
overlay.getStyleClass().setAll("game-overlay","game-overlay-won");
lOvrText.setText("You win!");
lOvrText.getStyleClass().setAll("game-label","game-lblWon");
buttonsOverlay.getChildren().setAll(bContinue, bTry);
this.getChildren().addAll(overlay,buttonsOverlay);
}
});
}
Back to [Index][I0]
***
## STEP 41 
In Board constructor call initGameProperties. In GameManager.move, add set win with setGameWin, and setGameOver in onFinished 
In GameManager.addAndAnimateRandomTile, add setGameOver. 
### SOLUTION CODE 
Board(){
initGameProperties();
}
move(){
board.setGameWin(true);
}
move(){
setOnFinished(){
board.setGameOver(true);
}
}
addAndAnimateRandomTile(){
board.setGameOver(true);
}
Back to [Index][I0]
***
## STEP 42 
In GameManager constructor add a listener to reset game property to start the game again 
with a clear grid. 
### SOLUTION CODE 
GameManager(){
board.resetGameProperty().addListener((ov, b, b1) -> {
if (b1) {
initializeGameGrid();
startGame();
}
});
}
Screenshots after #42  
 
Back to [Index][I0]
***
## STEP 43 
In GameManager.optionalTile, return an Optional of nullable from a given location on the map 
gameGrid. 
### SOLUTION CODE 
optionalTile(){
return Optional.ofNullable(gameGrid.get(loc));
}
Back to [Index][I0]
***
## STEP 44 
In GameManager.mergeMovementsAvailable, use optionalTile to find pairs of mergeable tiles 
### SOLUTION CODE 
mergeMovementsAvailable (){
optionalTile(thisloc).ifPresent(t1->{
optionalTile(thisloc.offset(direction)).filter(t2->t1.isMergeable(t2))
.ifPresent(t2->numMergeableTile.incrementAndGet());
});
}
Back to [Index][I0]
***
## STEP 45 
In GameManager.move, use optionalTile to traverse the grid, with an atomicInteger to return 
the results 
### SOLUTION CODE 
move (){
GridOperator.sortGrid(direction);
board.setPoints(0);
tilesWereMoved = GridOperator.traverseGrid((i, j) -> {
AtomicInteger result=new AtomicInteger();optionalTile(new Location(i,j)).ifPresent(t1->{
final Location newLoc=findFarthestLocation(t1.getLocation(),
direction);
Location nextLocation = newLoc.offset(direction); // calculates to
a possible merge
optionalTile(nextLocation).filter(t2->t1.isMergeable(t2) &&
!t2.isMerged()).ifPresent(t2->{
t2.merge(t1);
t2.toFront();
gameGrid.put(nextLocation, t2);
gameGrid.replace(t1.getLocation(), null);
board.addPoints(t2.getValue());
if(t2.getValue()==2048){
board.setGameWin(true);
}
parallelTransition.getChildren().add(animateExistingTile(t1
, nextLocation));
parallelTransition.getChildren().add(animateMergedTile(t2))
;
mergedToBeRemoved.add(t1);
result.set(1);
});
if(result.get()==0 && !newLoc.equals(t1.getLocation())){
parallelTransition.getChildren().add(animateExistingTile(t1
, newLoc));
gameGrid.put(newLoc, t1);
gameGrid.replace(t1.getLocation(),null);
t1.setLocation(newLoc);
result.set(1);
}
});
return result.get();
});
}
Back to [Index][I0]
***
 
[1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Game2048.java#L34-35
[2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L50-51
[3.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L77-98
[3.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L66
[4]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L170-172
[5.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L185-189
[5.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L66
[6]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Tile.java#L32-46
[7]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Tile.java#L20
[8.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L234-238
[8.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L226
[9.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L107-111
[9.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L69
[10.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Game2048.java#L24
[10.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Game2048.java#L40-41
[10.3]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L102-109
[10.4]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L176-178
[10.5]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Board.java#L201-202
[10.6]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Tile.java#L40
[11]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Direction.java#L37
[12]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Location.java#L64
[13]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L157-170
[14]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/Game2048.java#L45-51
[15.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L79-89
[15.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L65
[16.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L113-121
[16.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L132
[17]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L357-360
[18]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L176-194
[19]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L375-384
[20.1]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L147-151
[20.2]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L186
[20.3]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L296-299
[20.4]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L338-342
[21]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L399-407
[22]: https://github.com/jperedadnr/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L420-443
[23]: https://github.com/jperedadn/Game2048Solution/blob/master/src/org/hol/game2048/GameManager.java#L310-323

[screen5]: https://raw.githubusercontent.com/jperedadnr/Game2048HOL/master/src/doc/screenshot-Step5.jpg
[screen9]: https://raw.githubusercontent.com/jperedadnr/Game2048HOL/master/src/doc/screenshot-Step9.jpg
[screen10]: https://raw.githubusercontent.com/jperedadnr/Game2048HOL/master/src/doc/screenshot-Step10.jpg
[screen14]: https://raw.githubusercontent.com/jperedadnr/Game2048HOL/master/src/doc/screenshot-Step14.jpg
[screen20]: https://raw.githubusercontent.com/jperedadnr/Game2048HOL/master/src/doc/screenshot-Step20.jpg
[screen23]: https://raw.githubusercontent.com/jperedadnr/Game2048HOL/master/src/doc/screenshot-Step23.jpg

[I0]: https://github.com/jperedadnr/Game2048HOL#index
[I1]: https://github.com/jperedadnr/Game2048HOL#step-1-add-gamemanager-into-game2048
[I2]: https://github.com/jperedadnr/Game2048HOL#step-2-add-a-board-into-gamemanager
[I3]: https://github.com/jperedadnr/Game2048HOL#step-3-create-a-score-to-visualize-points
[I4]: https://github.com/jperedadnr/Game2048HOL#step-4-define-rectangle-corner-border-size
[I5]: https://github.com/jperedadnr/Game2048HOL#step-5-draw-a-grid-of-rectangles-in-the-board
[I6]: https://github.com/jperedadnr/Game2048HOL#step-6-add-tiles-into-the-grid
[I7]: https://github.com/jperedadnr/Game2048HOL#step-7-create-a-random-tile
[I8]: https://github.com/jperedadnr/Game2048HOL#step-8-layout-the-tile-at-its-location
[I9]: https://github.com/jperedadnr/Game2048HOL#step-9-lets-start-the-game
[I10]: https://github.com/jperedadnr/Game2048HOL#step-10-css-styling
[I11]: https://github.com/jperedadnr/Game2048HOL#step-11-connect-arrow-keys-with-direction
[I12]: https://github.com/jperedadnr/Game2048HOL#step-12-moving-one-tile
[I13]: https://github.com/jperedadnr/Game2048HOL#step-13-moving-tiles-on-the-board
[I14]: https://github.com/jperedadnr/Game2048HOL#step-14-listening-to-arrow-keys
[I15]: https://github.com/jperedadnr/Game2048HOL#step-15-initializing-the-game
[I16]: https://github.com/jperedadnr/Game2048HOL#step-16-random-tiles-random-locations
[I17]: https://github.com/jperedadnr/Game2048HOL#step-17-how-far-can-a-tile-go
[I18]: https://github.com/jperedadnr/Game2048HOL#step-18-a-new-approach-to-move-the-tiles
[I19]: https://github.com/jperedadnr/Game2048HOL#step-19-animating-one-tile-movement
[I20]: https://github.com/jperedadnr/Game2048HOL#step-20-animating-all-the-tiles-together
[I21]: https://github.com/jperedadnr/Game2048HOL#step-21-find-a-random-available-location
[I22]: https://github.com/jperedadnr/Game2048HOL#step-22-adding-and-animating-new-tiles