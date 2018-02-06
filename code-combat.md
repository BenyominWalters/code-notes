## Snippets from Code Combat with notes.



This snippet has two parts.

The first creates a function that tells the hero to wait and only attack when close to enemies.
The second part is a while loop that searches for the nearest enemy, and attacks it with the new function.
Because these are separte functions, their variables are "private" and so the same object can have a different name. In the first function the enemy is called "target", in the second it is called "enemy".

```js
// This shows how to define a function called cleaveWhenClose
// The function defines a parameter called target
function cleaveWhenClose(target) {
    if(hero.distanceTo(target) < 5) {
        // Put your attack code here
        // If cleave is ready, then cleave target
        if(hero.isReady("cleave")) {
            hero.cleave(enemy);}
        // else, just attack target!
        else {
            hero.attack(enemy);}
    }
}

// This code is not part of the function.
while(true) {
    var enemy = hero.findNearestEnemy();
    if(enemy) {
        // Note that inside cleaveWhenClose, we refer to the enemy as target.
        cleaveWhenClose(enemy);
    }
}
```

This code practices concatenating strings and accessing variables...

```js
// Peasants and peons are gathering in the forest.
// Command the peasants to battle and the peons to go away!

while(true) {
    var friend = hero.findNearestFriend();
    if(friend) {
        hero.say("To battle, " + friend.id + "!");
    }
    // Now find the nearest enemy and tell them to go away.
    var enemy = hero.findNearestEnemy();
    if(enemy) {
        hero.say("Go away, " + enemy.id + "!");
    }
}
```
This code moves the hero to an item's location. A similar method can be used to move hero to enemy.

```js
// Follow the trail of coins to the red X at the exit.

while (true) {
    // This finds the nearest item.
    var item = hero.findNearestItem();
    if (item) {
        // This stores the item's pos, or position in a variable.
        var itemPosition = item.pos;
        // Put the X and Y coordinates of the item into variables.
        var itemX = itemPosition.x;
        var itemY = itemPosition.y;
        // Now, use moveXY to move to itemX and itemY:
        hero.moveXY(itemX, itemY);
    }
}
```
