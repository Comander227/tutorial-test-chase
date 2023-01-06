# Chase The Balloons Enhanced

## {Introduction @unplugged}

In this tutorial you will create a basic chase game with a bit of a twist at the end. 

## Step 1 : Background
### The first part of this project is to create the base game. We will start with our background. 


- :tree: Grab the ``||scene: set background color to ()||`` block and place it in the ``||loops:on start||`` container. 
- :paint brush: **Click** on the **grey circle** and pick a color for your background. 

```blocks
//@highlight
scene.setBackgroundColor(12)
``` 

## Step 2: Characters
### Let's create the player character. 

- :paper plane: Open the ``||sprites: Sprites||`` category and grab a ``||variables: Set mySprite to||`` ``||sprites: sprite [ ] of kind Player||`` and place it in the ``||loops: on start||`` container. 

- :paint brush: **Click** on the **grey** box and open the sprite editor. Open the **Gallery** section and pick a character for your game. 

```blocks
scene.setBackgroundColor(12)
//@highlight
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
```

## Step 3: Controlling the Character
### Now that we have a character, let's setup the controls. 

- :game: Open the ``||controller: Controller||`` category and grab the ``||controller: move mySprite with buttons||`` block and add it under your ``||variables: Set mySprite to||`` ``||sprites: sprite [ ] of kind Player||`` block in the ``||loops: on start||`` container.


```blocks
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
//@highlight
controller.moveSprite(mySprite)

```

## Step 4: Keeping the Character On Screen

### Right now, if we are not careful then our character will run right off the screen. We have to fix that.

- :paper plane: Grab a ``||sprites: set mySprite stay on screen||`` block from the ``||sprites: Sprites||`` category and place it under the ``||controller: move mySprite with buttons||`` block. 
- :mouse pointer: set the value to **On**


```blocks
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
//@highlight
mySprite.setStayInScreen(true)

```

## Step 5: Let's Make Something to Chase
### Now that we are finished with our character let's give them something to chase.

- :paper plane: Grab another ``||variables: Set mySprite2 to||`` ``||sprites: sprite [ ] of kind Player||`` and place it in the ``||loops: on start||`` container.
- :mouse pointer: Click on where it says ``||sprites:Player||`` to change the kind of the sprite it is. **Click** ``||sprites:New Kind||`` and name it **Collectible**
- :mouse pointer: **Click** on ``||variables:mySprite2||`` and select the ``||variables:Rename variable||`` option. Change the name from **mySprite2** to **Balloons**.
- :paint brush: **Click** on the **grey** block and open the gallery. Pick the Image that you want your character to chase. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
//@highlight
let Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)

```
## Step 6: What a Catch!

### Now that we have an object to catch, we need to setup the collision code for our game to work.

- :paper plane: Grab an ``||sprites: on sprite of kind Player overlaps otherSprite of kind Player||`` container from the ``||sprites:Sprites||`` category and place it into the workspace.
- :mouse pointer: Change the ``||variables:otherSprite||`` kind from ``||sprites:Player||`` to ``||sprites:Collectible||``.


```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
//@highlight
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
	
})
``` 
## Step 7: Adding A Score.

### Every good video game needs a scoring system. Let's add one to our game. 
 
- :id card: Open the ``||info:Info||`` category and add the ``||info: change score by 1||`` block to the new ``||sprites:overlap||`` container that we just added. 

```blocks

sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
	//@highlight
	 info.changeScoreBy(1)
})
``` 


## Step 8: Too Many Points
### Right now we are scoring too many points because our chase sprite does not move. We need to fix this.

- :paper plane: From the ``||sprites:Sprites||`` category grab a ``||sprites: set mySprite position to x (0) y (0)||`` block and place it in the ``||sprites:overlap||`` container.
- :mouse pointer: Change **mySprite** to **Balloons**. 

```blocks
let Balloons: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    //@highlight
    Balloons.setPosition(0, 0)
})
```

## Step 9: Randomizing The Position of our Chase Object
### Now that our chase object moves, we need to add some randomness to the game to make it a challenge. 

- :calculator: Open the ``||math:Math||`` category and grab the ``||math: pick random (0) to (10)||`` circle and place it in the ``||sprites: x(0)||`` value.
- :calculator: Grab another ``||math: pick random (0) to (10)||`` circle and place it in the ``||sprites: y(0)||`` value. 

```blocks
let Balloons: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    //@highlight
    Balloons.setPosition(randint(0, 10), randint(0, 10))
})
```

## Step 10: Even More Randomization

### Randomizing the positions between 0 and 10 is not enough. Let's stretch that range a bit. 

- :tree: From the ``||scene:Scene||`` category, grab the ``||scene:screen width||`` circle and place it in the ``||sprites:x||`` value's **10** circle. 
- :tree: From the ``||scene:Scene||`` category, grab the ``||scene:screen hight||`` circle and place it in the ``||sprites:y||`` value's **10** circle. 

```blocks
let Balloons: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    //@highlight
    Balloons.setPosition(randint(0, scene.screenWidth()), randint(0, scene.screenHeight()))
})
```
## Step 11: Adding a Sense of Urgency
### Right now there is no motivation for our player to move quickly. We need to give them a timer to let them know when the game ends. 

- :id card: Open the ``||info:Info||`` category and grab the ``||info:start countdown (10)s||`` and place it into the bottom of the ``||loops:on start||`` container. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
info.startCountdown(10)

```

## Step 12: Keep the Snowball Rolling
### We don't want to make the game that short so let's see if we can allow the player to extend the game time.

- :id card: Open the ``||info:Info||`` category and grab a ``||info:set countdown (10)s||`` block and add it to the bottom of our ``||Sprites:overlap||`` container.
- :mouse pointer: You may adjust the amount of time the player has once they catch the chase object. 

```blocks
let Balloons: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    Balloons.setPosition(randint(0, scene.screenWidth()), randint(0, scene.screenHeight()))
    //@highlight
    info.startCountdown(10)
})
```


## Step 13: Adding an End Game Condition
### All good things must come to an end, same with our video game. We are going to add a timer to create an end to our game. 

- :id card: Grab the ``||info:on countdown ends||`` container and place it in the workspace. 

- :circle: Open the ``||game:Game||`` category and grab the ``||game:game over||`` block and place it inside the ``||info:on countdown ends||`` container. 
- :mouse pointer: Set the ``||game:game over||`` value to **Win**. Feel free to click the **+** button to add an effect. 

```blocks
info.onCountdownEnd(function () {
    //@highlight
    game.over(true, effects.confetti)
})
```

## Step 14: Complete Game

### Here is the complete code for the game so far. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
info.onCountdownEnd(function () {
    game.over(true, effects.confetti)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    Balloons.setPosition(randint(0, scene.screenWidth()), randint(0, scene.screenHeight()))
    info.startCountdown(10)
})
let Balloons: Sprite = null
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
info.startCountdown(10)

```


## Part 2: Chase the Pizza Arena

### Now that we have made a simple game and have had the chance to customize the experience, let's expand on this concept.

## Step 1: Adding a tile map. 
### I have provided you with a premade tile map arena that we can use to be more organized about how our chase object spawns. Let's add that tile map to the game. *Note that this will break the game, we will fix it next.* 

- :tree: Add the tile map using ``||scene:set tile map to []||``. 
- :mouse pointer: Click on the grey box to open the tilemap editor. Open the **My Assets** section and select the tilemap called **Arena Demo**. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
//@highlight
tiles.setCurrentTilemap(tilemap`Arena Demo`)
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
info.startCountdown(10)

```

## Step 2: Fixing our Sprite's Movement
### Right now our player can not access the rest of the tilemap because we have locked them to the screen. Let's change the property of the sprite so it can leave the screen.

- :mouse pointer: Change the value for ``||sprites:set mySprite stay on screen||`` from **On** to **Off**. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
tiles.setCurrentTilemap(tilemap`Arena Demo`)
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
//@highlight
mySprite.setStayInScreen(false)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
info.startCountdown(10)
```
## Step 3: Following Our Character
### Now that we have given our player access to the rest of the tilemap, we need to make sure that they can see their character. 

- :tree:Grab the ``||scene:camera follow sprite||`` ``||variables:mySprite||`` from the ``||scene:Scene||`` category and place it in the ``||loops:on start||``container under the ``||sprites:set mySprite stay on screen||`` block. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
tiles.setCurrentTilemap(tilemap`Arena Demo`)
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(false)
//@highlight
scene.cameraFollowSprite(mySprite)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
info.startCountdown(10)
```   
## Step 4: Setting the Starting Position.
### We don't want the player to start in a random position every time. So let's set a specific set of starting positions for the player. 

- :tree: From the ``||scene:Scene||`` category grab the block ``||scene:place||`` ``||variables:mySprite||`` ``||scene:on top of random []||`` block and place it under the ``||scene:camera follow sprite||`` ``||variables:mySprite||`` block in the ``||loops:on start||`` container. 
- :mouse pointer: **Click** on the **grey** box and select the **blue** tile labeled **Start**. 


```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
tiles.setCurrentTilemap(tilemap`Arena Demo`)
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(false)
scene.cameraFollowSprite(mySprite)
//@highlight
tiles.placeOnRandomTile(mySprite, assets.tile`Start`)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
info.startCountdown(10)

```
## Step 5: Fixing the Collectible Spawning. 

### Now that we have fixed the start point for our player character, we need to fix the way that our collectible spawns. 


- :tree: Add another ``||scene:place||`` ``||variables:mySprite||`` ``||scene:on top of random []||`` from the ``||scene:Scene||`` category and add it under the ``||variables:Set Balloons to||`` ``||sprites: sprite [] of kind Food||`` in the ``||loops:on start||`` container. 
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Balloons||``. 
- :mouse pointer: **Click** on the **grey** box and select the purple tile labeled **Spawn**.


```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
tiles.setCurrentTilemap(tilemap`Arena Demo`)
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(false)
scene.cameraFollowSprite(mySprite)
tiles.placeOnRandomTile(mySprite, assets.tile`Start`)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
tiles.placeOnRandomTile(Balloons, assets.tile`Spawn`)
info.startCountdown(10)
```

## Step 6: Fixing the Collision Code.
### We need to update the code that runs when we try to pick up our object. This means adding a new block and removing one that no longer works.  

- :mouse pointer: **Right Click** on the ``||scene:place||`` ``||variables:Balloons||`` ``||scene:on top of random [spawn]||`` and select **Duplicate**.
- :mouse pointer: Drag your new ``||scene:place||`` ``||variables:Balloons||`` ``||scene:on top of random [spawn]||`` block to the ``||sprites: on sprite of kind Player overlaps otherSprite of kind Food||`` container. 
- :mouse pointer: **Right Click** on the ``||sprites:set mySprite position||`` block and select **Delete Blocks**.

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
let Balloons: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
   //@highlight
    tiles.placeOnRandomTile(Balloons, assets.tile`Spawn`)
    info.startCountdown(10)
})
```
## Step 7:Customize the Complete Game
### Now that you have a tilemap to play with, feel free to reskin this game with your own sprites, tiles, and background. 

- :paint brush: Open the **Assets** section and click on the green **New** square. Here is where you can add and create your own assets including sprites, images, tiles, tile maps, and animations. 
- :paper plane: **Sprites** are used as characters as well as the base for animations.
- :tree: **Images** are used as larger pictures for backgrounds or additional textures. Smaller ones can be used for sprites or arrays.
- :tree: **Tiles** are each block used in a tile map.
- :tree: **Tilemaps** are organized tiles that create a larger game space for your video game. Note the Wall tool is used to highlight which blocks should be walls or not. 
- :redo: **Animations** are a series of sprites or images that give the illusion of a character moving. 

```blocks
namespace SpriteKind {
    export const Collectible = SpriteKind.create()
}
info.onCountdownEnd(function () {
    game.over(true, effects.confetti)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    tiles.placeOnRandomTile(Balloons, assets.tile`Spawn`)
    info.startCountdown(10)
})
let Balloons: Sprite = null
tiles.setCurrentTilemap(tilemap`Arena Demo`)
scene.setBackgroundColor(12)
let mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(false)
scene.cameraFollowSprite(mySprite)
tiles.placeOnRandomTile(mySprite, assets.tile`Start`)
Balloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)
tiles.placeOnRandomTile(Balloons, assets.tile`Spawn`)
info.startCountdown(10)

```
