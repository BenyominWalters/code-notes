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
This code finds the distance to the nearest enemy.

```js
// Tell the wizard the distance to the coming ogres.

// This function finds the nearest enemy and returns the distance to it.
function nearestEnemyDistance() {
    var enemy = hero.findNearestEnemy();
    // If there is no enemy, the function returns 0.
    var result = 0;
    if (enemy) {
        result = hero.distanceTo(enemy);
    }
    return result;
}

while (true) {
    // Call nearestEnemyDistance() and
    // save the result in the variable enemyDistance.
    var enemyDistance = nearestEnemyDistance();
    // If the enemyDistance is greater than 0: 
    if (enemyDistance > 0) {
    // Say the value of enemyDistance variable.
        hero.say(enemyDistance);        
    }
             
}
```
This code has the hero wait until enemies are close to attack.

```js
// You are trapped. Don't move, it'll be painful.

// This function checks if the enemy is in your attack range.
function inAttackRange(enemy) {
    var distance = hero.distanceTo(enemy);
    // Almost all swords have attack range of 3.
    if (distance <= 3) {
        return true;
    } else {
        return false;
    }
}

// Attack ogres only when they're within reach.
while (true) {
    // Find the nearest enemy and store it in a variable.
    var  enemy = hero.findNearestEnemy();
    // Call inAttackRange(enemy), with the enemy as the argument
    // and save the result in the variable canAttack.
    var canAttack = inAttackRange(enemy);
    // If the result stored in canAttack is true, then attack!
    if (canAttack === true) {
        hero.attack(enemy);
    }
}
```
Here is a better version that includes the cleave attack.

```js
// You are trapped. Don't move, it'll be painful.

// This function checks if the enemy is in your attack range.
function inAttackRange(enemy) {
    var distance = hero.distanceTo(enemy);
    // Almost all swords have attack range of 3.
    if (distance <= 3) {
        return true;
    } else {
        return false;
    }
}

// Attack ogres only when they're within reach.
while (true) {
    // Find the nearest enemy and store it in a variable.
    var  enemy = hero.findNearestEnemy();
    // Call inAttackRange(enemy), with the enemy as the argument
    // and save the result in the variable canAttack.
    var canAttack = inAttackRange(enemy);
    // If the result stored in canAttack is true, then attack!
    if (canAttack === true) {
       if(hero.isReady("cleave")) {
            hero.cleave(enemy);}
        // else, just attack target!
        else {
            hero.attack(enemy);}
    }
}
```
This code uses logic to decide if the hero should pickup an item or not. Similar code could be used to charge "thrower" enemies, and wait for regular enemies to attack.

```js
// Ogres are attacking a nearby settlement!
// Be careful, though, for the ogres have sown the ground with poison.
// Gather coins and defeat the ogres, but avoid the burls and poison!

while(true) {
    var enemy = hero.findNearestEnemy();
    if(enemy.type == "munchkin" || enemy.type == "thrower") {
        hero.attack(enemy);
    }
    var item = hero.findNearestItem();
    // Check the item type to make sure the hero doesn't pick up poison!
    // Look for types: 'gem' and 'coin'
 if(item.type == 'gem' || item.type == 'coin') {
       if (item) {
            // Move to the position of the item.
            var pos = item.pos;
            var x = pos.x;
            var y = pos.y;
            hero.moveXY(x, y);
        }        
    }
}
```

This code allows hero to make a two-part decision with AND logic.

```js
// Certain coins and gems attract lightning.
// The hero should only grab silver coins and blue gems.

while (true) {
    var item = hero.findNearestItem();
    // A silver coin has a value of 2.
    // Collect if item.type is equal to "coin"
    // AND item.value is equal to 2.
    if (item.type == "coin" && item.value == 2) {
        hero.moveXY(item.pos.x, item.pos.y);
    }
    // A blue gem has a value of 10.
    // Collect if item.type is equal to "gem"
    // AND item.value is equal to 10.
    if (item.type == "gem" && item.value == 10){
        hero.moveXY(item.pos.x, item.pos.y);   
    }
}
```
