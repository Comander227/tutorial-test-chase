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


```assetjson
{
  "README.md": " ",
  "assets.json": "",
  "images.g.jres": "{\n    \"|y#eS|N5[gbL)[kt8F_r\": {\n        \"data\": \"hwQOAA4AAADMzM/8DwAAABw7Gxv7//8AHLsTH4G78QDAuxH7ixsPAAC/u7uLGw8AAL+7u4sb/wDAuxH7i7vxABy7Ex+Buw8AHDsbG7gbDwDMzM/8vxvxAAAAAADw+/8AAAAA+//7AAAAAAAfsfsAAAAAAPv/DwAA\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Ezra\"\n    },\n    \"image1\": {\n        \"data\": \"hwQQABAAAAAA3cwAAADgvtAzM+7u7u69Paoz493dvb09OjMz7rvuvT06M1MMAOC9PaozEwwA3gutqjM1DAC+C9A6M8Ps7u0AAN3NPDPj7QAAAMwzM8PuAAAAPTozMwwAAAA9OjNTDAAAADyqOhMMAAAA0KM6NQwAAAAAPTPDAAAAAADQzAwAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Balloons\"\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myImages\"\n    }\n}",
  "images.g.ts": "// Auto-generated code. Do not edit.\nnamespace myImages {\n\n    helpers._registerFactory(\"image\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"|y#eS|N5[gbL)[kt8F_r\":\n            case \"Ezra\":return img`\nc c c . . . . c c c . . . . \nc 1 1 c . . c 1 1 c . . . . \nc b b b f f b b b c . . . . \nc 3 b b b b b b 3 c . . . . \nf b 3 1 b b 1 3 b f . . . . \nc 1 1 1 b b 1 1 1 c . . . . \nc b f b b b b f b c . b f b \nf 1 1 f b b f 1 1 f . f 1 f \nf b 1 b b b b 1 8 f . f 1 f \n. f 8 8 8 8 8 8 b b f f b f \n. f b b b b b b b b b b b f \n. f b 1 1 1 b b 1 1 f f f . \n. f 1 f f f 1 f f 1 f . . . \n. f f . . f f . . f f . . . \n`;\n            case \"image1\":\n            case \"Balloons\":return img`\n. . d d d d d . . . . . . . . . \n. d 3 3 3 3 a d . . . . . . . . \nd 3 a a a a a a d . . . . . . . \nd 3 a 3 3 a a 3 d . . . . . . . \nc 3 3 3 3 3 3 3 d c d d c . . . \nc 3 3 3 3 3 3 3 c c 3 3 3 d . . \n. e 3 3 3 3 5 3 c 3 a a a 3 d . \n. e e 3 5 1 3 c 3 3 3 3 a a 3 d \n. e d e c c c c 3 3 3 3 a a 3 c \n. e d e . . . e 3 3 3 3 3 3 3 c \n. e d b . . . e 3 3 3 3 3 5 3 c \n. e d b . . . e e c 3 5 1 3 c . \n. e d e . e e d d e c c c c . . \ne e b e e d b e e e . . . . . . \ne d d d d b b . . . . . . . . . \nb b b b b . . . . . . . . . . . \n`;\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"animation\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n",
  "main.blocks": "<xml xmlns=\"https://developers.google.com/blockly/xml\"><variables><variable id=\"B*op_;vID=]dy#fqp_Xa\">mySprite</variable><variable id=\":VHCEev)8zKnE:J_=$|4\">Balloons</variable><variable type=\"KIND_SpriteKind\" id=\"duV:Ag?+i3:PIN@Id5;Z\">Player</variable><variable type=\"KIND_SpriteKind\" id=\"O7$%=eycd`9n:CZ}DA^*\">Projectile</variable><variable type=\"KIND_SpriteKind\" id=\";Ep}1%kK`OTd$*}o$-+e\">Food</variable><variable type=\"KIND_SpriteKind\" id=\"7x^g]gWKN$y5W+)O*jV5\">Enemy</variable><variable type=\"KIND_SpriteKind\" id=\"@0|L;Ft`$x5~CJa{P{_!\">Collectible</variable></variables><block type=\"pxt-on-start\" x=\"0\" y=\"0\"><statement name=\"HANDLER\"><block type=\"set_current_tilemap\"><value name=\"tilemap\"><shadow type=\"tiles_tilemap_editor\"><field name=\"tilemap\">tilemap`Arena Demo`</field><data>{\"commentRefs\":[],\"fieldData\":{\"tilemap\":\"level2\"}}</data></shadow></value><next><block type=\"gamesetbackgroundcolor\"><value name=\"color\"><shadow type=\"colorindexpicker\"><field name=\"index\">12</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"B*op_;vID=]dy#fqp_Xa\">mySprite</field><value name=\"VALUE\"><shadow xmlns=\"http://www.w3.org/1999/xhtml\" type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Ezra`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.|y#eS|N5[gbL)[kt8F_r\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value></block></value><next><block type=\"game_control_sprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"true\"></mutation><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"B*op_;vID=]dy#fqp_Xa\">mySprite</field></block></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">100</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">100</field></shadow></value><next><block type=\"spritesetsetstayinscreen\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"B*op_;vID=]dy#fqp_Xa\">mySprite</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">false</field></shadow></value><next><block type=\"camerafollow\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"B*op_;vID=]dy#fqp_Xa\">mySprite</field></block></value><next><block type=\"mapplaceonrandomtile\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"B*op_;vID=]dy#fqp_Xa\">mySprite</field></block></value><value name=\"tile\"><shadow type=\"tileset_tile_picker\"><field name=\"tile\">assets.tile`Start`</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\":VHCEev)8zKnE:J_=$|4\">Balloons</field><value name=\"VALUE\"><shadow xmlns=\"http://www.w3.org/1999/xhtml\" type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Balloons`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image1\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Collectible</field></shadow></value></block></value><next><block type=\"mapplaceonrandomtile\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\":VHCEev)8zKnE:J_=$|4\">Balloons</field></block></value><value name=\"tile\"><shadow type=\"tileset_tile_picker\"><field name=\"tile\">assets.tile`Spawn`</field></shadow></value><next><block type=\"gamecountdown\"><value name=\"duration\"><shadow type=\"math_number\"><field name=\"NUM\">10</field></shadow></value></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></statement></block><block type=\"gamecountdownevent\" x=\"670\" y=\"90\"><statement name=\"HANDLER\"><block type=\"gameOver\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"1\" _input_init=\"true\"></mutation><field name=\"effect\">effects.confetti</field><value name=\"win\"><shadow type=\"toggleWinLose\"><field name=\"win\">true</field></shadow></value></block></statement></block><block type=\"spritesoverlap\" x=\"390\" y=\"510\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Collectible</field></shadow></value><statement name=\"HANDLER\"><block type=\"hudChangeScoreBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value><next><block type=\"mapplaceonrandomtile\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\":VHCEev)8zKnE:J_=$|4\">Balloons</field></block></value><value name=\"tile\"><shadow type=\"tileset_tile_picker\"><field name=\"tile\">assets.tile`Spawn`</field></shadow></value><next><block type=\"gamecountdown\"><value name=\"duration\"><shadow type=\"math_number\"><field name=\"NUM\">10</field></shadow></value></block></next></block></next></block></statement></block></xml>",
  "main.ts": "namespace SpriteKind {\n    export const Collectible = SpriteKind.create()\n}\ninfo.onCountdownEnd(function () {\n    game.over(true, effects.confetti)\n})\nsprites.onOverlap(SpriteKind.Player, SpriteKind.Collectible, function (sprite, otherSprite) {\n    info.changeScoreBy(1)\n    tiles.placeOnRandomTile(Balloons, assets.tile`Spawn`)\n    info.startCountdown(10)\n})\nlet Balloons: Sprite = null\ntiles.setCurrentTilemap(tilemap`Arena Demo`)\nscene.setBackgroundColor(12)\nlet mySprite = sprites.create(assets.image`Ezra`, SpriteKind.Player)\ncontroller.moveSprite(mySprite)\nmySprite.setStayInScreen(false)\nscene.cameraFollowSprite(mySprite)\ntiles.placeOnRandomTile(mySprite, assets.tile`Start`)\nBalloons = sprites.create(assets.image`Balloons`, SpriteKind.Collectible)\ntiles.placeOnRandomTile(Balloons, assets.tile`Spawn`)\ninfo.startCountdown(10)\n",
  "pxt.json": "{\n    \"name\": \"Chase The Pizza Enchanced Empty Redo\",\n    \"description\": \"\",\n    \"dependencies\": {\n        \"device\": \"*\",\n        \"color-coded-tilemap\": \"*\"\n    },\n    \"files\": [\n        \"main.blocks\",\n        \"main.ts\",\n        \"README.md\",\n        \"assets.json\",\n        \"tilemap.g.jres\",\n        \"tilemap.g.ts\",\n        \"images.g.jres\",\n        \"images.g.ts\"\n    ],\n    \"targetVersions\": {\n        \"branch\": \"v1.10.34\",\n        \"tag\": \"v1.10.34\",\n        \"commits\": \"https://github.com/microsoft/pxt-arcade/commits/d026f937a64c15c6ac4f338585ca2255bb9ac8db\",\n        \"target\": \"1.10.34\",\n        \"pxt\": \"8.3.7\"\n    },\n    \"preferredEditor\": \"tsprj\"\n}\n",
  "tilemap.g.jres": "{\n    \"transparency16\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true\n    },\n    \"tile4\": {\n        \"data\": \"hwQQABAAAABmZmZmZmZmZpaZZpmZZplplmmWyZxplmmWZplpzJlmaWaWmWacmWlmZpmZZpmZmWaWyZmWZmaZaZbMnJaZZsZplmxmmWnJzGmWmWZmaZmcaWaZmZlmmZlmZpaZyWaZaWaWZpnMlplmaZZplsmcaZZplplmmZlmmWlmZmZmZmZmZg==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"Start\"\n    },\n    \"tile1\": {\n        \"data\": \"hwQQABAAAADMzMzMzMzMzMzMzLzMzMzMzMvMzMzMvMzMzMzMzMzMzMzMzMzMzMzMzMzMzLzMzMzMzLzMzMzMzMzMzMzMzMzLzMzMzMzMzMy8zMzMzMzMzMzMzMzMzMzMzMy8zLzMzMzMzMzMzMzMzMzMzMzMzLzMvMzMzMzMzMzMzMzMzMzMzA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"Spawn\"\n    },\n    \"tile2\": {\n        \"data\": \"hwQQABAAAAC8zMzMzMzMzLvMzLzMzMzMzMzMzMzMvMzMzMzMzMzMzMzMzMzMzMzMzMzMzLzMzMzMzLzMzMzMzMzMzMzMzMzLzMzMzMzMzMy8zMzMzMzMzMzMzMzMzMzMzMy8zLzMzMzMzMzMzMzMzMzMzMzMzLzMvMzMzMzMzMzMzMzMzMzMzA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"Rug 1\"\n    },\n    \"tile3\": {\n        \"data\": \"hwQQABAAAADMzMzMzMzMzMzMzLzMzMzMzMvMzMzMvMzMzMzMzMzMzMzMzMzMzMzMzMzMzLzMzMzMzLzMzMzMzMzMzMzMzMzLzMzMzMzMzMy8zMzMzMzMzMzMzMzMzMzMzMy8zLzMzMzMzMzMzMzMzMzMzMzMzLzMu8zMzMzMzMy8zMzMzMzMzA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"Rug 2\"\n    },\n    \"tile5\": {\n        \"data\": \"hwQQABAAAADMzMzMzMzMzMzMzMzMzMzLzMvMzMzMzMzMzMzMzMzMzMzMzMvMy8zMzMzMzMzMzMzMzMzMzMzMy8zMzMzMzMzMvMzMzMzMzMzMzMzMzMvMzMzMzMvMzMzMzMzMzMzMzMzMzMzMzMzMzMzLzMzMzMzMzMzMzMvMzLvMzMzMzMzMyw==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"Rug 3\"\n    },\n    \"tile6\": {\n        \"data\": \"hwQQABAAAADMzMzMzMzMy7zMzMvMzMy7zMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzLzLzMzMzMzMzMzMzMzMzMzMzMzMzLzMzMzMzMzMzMzMvMzMvMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzMzLzMzMzLzMzMzMzMvMzMzMzMzMzMzMzA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true,\n        \"displayName\": \"Rug 0\"\n    },\n    \"level5\": {\n        \"id\": \"level5\",\n        \"mimeType\": \"application/mkcd-tilemap\",\n        \"data\": \"MTAxMDAwMTAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMA==\",\n        \"tileset\": [\n            \"myTiles.transparency16\"\n        ],\n        \"displayName\": \"level5\"\n    },\n    \"level2\": {\n        \"id\": \"level2\",\n        \"mimeType\": \"application/mkcd-tilemap\",\n        \"data\": \"MTAxMDAwMTAwMDAyMGUwZTBjMGUwYzBlMDYwNjBlMGMwZTBjMGUwZTAxMGYxMTAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDExMGIwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYjEwMDAwMDEyMTUxNTE1MTUxNTE1MTUxNTEyMDAwMDBkMGYwMDAwMTMxMjE1MTUxNTE1MTUxNTEyMTUwMDAwMGIxMDAwMDAxMzEzMTIxNTE1MTUxNTEyMTUxNTAwMDAwZDBmMDAwMDEzMTMxMzEyMTUxNTEyMTUxNTE1MDAwMDBiMDUwMDAwMTMxMzEzMTMxMjEyMTUxNTE1MTUwMDAwMDcwNTAwMDAxMzEzMTMxMzEyMTIxNTE1MTUxNTAwMDAwNzBmMDAwMDEzMTMxMzEyMTQxNDEyMTUxNTE1MDAwMDBiMTAwMDAwMTMxMzEyMTQxNDE0MTQxMjE1MTUwMDAwMGQwZjAwMDAxMzEyMTQxNDE0MTQxNDE0MTIxNTAwMDAwYjEwMDAwMDEyMTQxNDE0MTQxNDE0MTQxNDEyMDAwMDBkMGYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGIwZjExMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMTEwYjAzMDkwOTBhMDkwYTA5MDgwODA5MGEwOTBhMDkwOTA0MjIyMjIyMjIyMjIyMjIyMjAyMDAwMDAwMDAwMDAwMjAwMjAwMDAwMDAwMDAwMDIwMDIwMDAwMDAwMDAwMDAyMDAyMDAwMDAwMDAwMDAwMjAwMjAwMDAwMDAwMDAwMDIwMDIwMDAwMDAwMDAwMDAyMDAyMDAwMDAwMDAwMDAwMjAwMjAwMDAwMDAwMDAwMDIwMDIwMDAwMDAwMDAwMDAyMDAyMDAwMDAwMDAwMDAwMjAwMjAwMDAwMDAwMDAwMDIwMDIwMDAwMDAwMDAwMDAyMDAyMDAwMDAwMDAwMDAwMjAwMjAwMDAwMDAwMDAwMDIwMjIyMjIyMjIyMjIyMjIyMg==\",\n        \"tileset\": [\n            \"myTiles.transparency16\",\n            \"sprites.dungeon.purpleOuterNorthEast\",\n            \"sprites.dungeon.purpleOuterNorthWest\",\n            \"sprites.dungeon.purpleOuterSouthEast\",\n            \"sprites.dungeon.purpleOuterSouthWest\",\n            \"sprites.dungeon.purpleOuterWest2\",\n            \"sprites.dungeon.purpleOuterNorth2\",\n            \"sprites.dungeon.purpleOuterEast2\",\n            \"sprites.dungeon.purpleOuterSouth2\",\n            \"sprites.dungeon.purpleOuterSouth1\",\n            \"sprites.dungeon.purpleOuterSouth0\",\n            \"sprites.dungeon.purpleOuterEast1\",\n            \"sprites.dungeon.purpleOuterNorth1\",\n            \"sprites.dungeon.purpleOuterEast0\",\n            \"sprites.dungeon.purpleOuterNorth0\",\n            \"sprites.dungeon.purpleOuterWest0\",\n            \"sprites.dungeon.purpleOuterWest1\",\n            \"sprites.dungeon.collectibleInsignia\",\n            \"myTiles.tile1\",\n            \"myTiles.tile2\",\n            \"myTiles.tile5\",\n            \"myTiles.tile3\"\n        ],\n        \"displayName\": \"Arena Demo\"\n    },\n    \"level1\": {\n        \"id\": \"level1\",\n        \"mimeType\": \"application/mkcd-tilemap\",\n        \"data\": \"MTAxMDAwMTAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMA==\",\n        \"tileset\": [\n            \"myTiles.transparency16\"\n        ],\n        \"displayName\": \"level1\"\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myTiles\"\n    }\n}",
  "tilemap.g.ts": "// Auto-generated code. Do not edit.\nnamespace myTiles {\n    //% fixedInstance jres blockIdentity=images._tile\n    export const transparency16 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile4 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile1 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile2 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile3 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile5 = image.ofBuffer(hex``);\n    //% fixedInstance jres blockIdentity=images._tile\n    export const tile6 = image.ofBuffer(hex``);\n\n    helpers._registerFactory(\"tilemap\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"level5\":\n            case \"level5\":return tiles.createTilemap(hex`1000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000`, img`\n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n`, [myTiles.transparency16], TileScale.Sixteen);\n            case \"Arena Demo\":\n            case \"level2\":return tiles.createTilemap(hex`10001000020e0e0c0e0c0e06060e0c0e0c0e0e010f11000000000000000000000000110b0f00000000000000000000000000000b1000001215151515151515151200000d0f00001312151515151515121500000b1000001313121515151512151500000d0f00001313131215151215151500000b05000013131313121215151515000007050000131313131212151515150000070f00001313131214141215151500000b1000001313121414141412151500000d0f00001312141414141414121500000b1000001214141414141414141200000d0f00000000000000000000000000000b0f11000000000000000000000000110b0309090a090a090808090a090a090904`, img`\n2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 . . . . . . . . . . . . . . 2 \n2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 \n`, [myTiles.transparency16,sprites.dungeon.purpleOuterNorthEast,sprites.dungeon.purpleOuterNorthWest,sprites.dungeon.purpleOuterSouthEast,sprites.dungeon.purpleOuterSouthWest,sprites.dungeon.purpleOuterWest2,sprites.dungeon.purpleOuterNorth2,sprites.dungeon.purpleOuterEast2,sprites.dungeon.purpleOuterSouth2,sprites.dungeon.purpleOuterSouth1,sprites.dungeon.purpleOuterSouth0,sprites.dungeon.purpleOuterEast1,sprites.dungeon.purpleOuterNorth1,sprites.dungeon.purpleOuterEast0,sprites.dungeon.purpleOuterNorth0,sprites.dungeon.purpleOuterWest0,sprites.dungeon.purpleOuterWest1,sprites.dungeon.collectibleInsignia,myTiles.tile1,myTiles.tile2,myTiles.tile5,myTiles.tile3], TileScale.Sixteen);\n            case \"level1\":\n            case \"level1\":return tiles.createTilemap(hex`1000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000`, img`\n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n`, [myTiles.transparency16], TileScale.Sixteen);\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"tile\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"transparency16\":return transparency16;\n            case \"Start\":\n            case \"tile4\":return tile4;\n            case \"Spawn\":\n            case \"tile1\":return tile1;\n            case \"Rug 1\":\n            case \"tile2\":return tile2;\n            case \"Rug 2\":\n            case \"tile3\":return tile3;\n            case \"Rug 3\":\n            case \"tile5\":return tile5;\n            case \"Rug 0\":\n            case \"tile6\":return tile6;\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n"
}
```