# Design of Game AI

## Overview

Game AI generally works based on the current state of the game and predicted distance to a win state for the game. 

Here, the AI works based on a predicted number of future generations combined with the impact of that card on those
future generations. 

The value prediction function that is developed here is also helpful for those who are wanting to understand why the 
AI valued that particular card and chose to play it at that point in time. This could also be applied to those who 
want to better train an internal value function for cards during their own play. 

## Value Function

Every behavior can be thought of as having a predicted value over the life of the game. You can think of this as a return
on investment. 

For example, let's say you know that you only have one generation left in the game. Playing "Acquired Company" for the cost of 10 MC when it produces only 3 MC per turn means that you technically take a loss of 7 MC to play that card. If you had to buy that card to put it in your hand as well, then the value of the card gets worse because it cost 13 MC total
to play that card and you will only get back 3 MC next generation. This means that the card has a value of -10 when purchased
and -7 when drawn. 

However, let's say you play it in the mid-game with 6 generations left, then the value of the card is (3\*generations)-(cost+acquisitionCost) = 5 MC if you purchased the card for 3 MC and is = 8 MC if you drew it off something like AI Central.

Unfortunately, there's extra complication introduced by effect cards as they can change the entire flow of a game but they are not straightforward in their impact. My current thought to handle those is to calculate the probability of that effect being activated based on the discard pile and the cards we have seen. Then calculating the value of that as the probability multipled by the actual effect of the effect.

All of this becomes simpler if I can simulate the impact of a card on the game state to predict the overall impact of the card. Then I can see how all the other potential effects in play impact a card. Phobolog Corporation combined with Advanced Alloys might be well worth it if you have a good chance of playing lots of mine cards that lets you grow the amount of metals you have available per turn. But if the chance of you getting any metal is near 0 then you likely shouldn't make that purchase as it will not actually impact the overal value of your system. 

These are my thoughts so far, I need to actually implement this system though which is the next stp. 