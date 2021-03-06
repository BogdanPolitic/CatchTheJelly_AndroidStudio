# Catch The Jelly  [[Play Store link](https://play.google.com/store/apps/details?id=co.snOmOtiOn.bogdan.catchthejellyv112020)]

<h3> General description </h3>

Simple real-strategy 2D Android game. The main task is "chasing" the jelly entity lurking around a rectangular network on a path determined by rules. The "chase" is a simple screen touch on the exact place the entity is, at the right time. Due to the little amount of time the jelly rests on a cell, players must predict the next cell he could trap the jelly into.
The multiple levels and a limited number of failed attempts - "hearts" - develop a nice in-game progress system. Every two levels guarantee an extra "heart" upon completion.
Players can also load a specific level that they want to play, but it requires that all previous levels are unlocked. To unlock a level, they should simply complete it once.

<p style="align:center;">
  <image src="https://play-lh.googleusercontent.com/Bk5Rt8mHHen1VcvCgx5YbLpkCuX6zad2NIgpqwbvcUeLY0hCd1jH5i92dZSMSQurDB4=w1920-h969-rw" />
</p>

<h3> Demo showing a game loss </h3>
![Demo](https://github.com/BogdanPolitic/Demos/blob/main/jellyloss.gif?raw=true)

<h3> Demo showing a game win </h3>
![Demo](https://github.com/BogdanPolitic/Demos/blob/main/jellywin.gif?raw=true)

<h3> Short background & gameplay description </h3>

The game follows the story of a little jelly baby. It tries to outrun humans, so that they can't eat it, but eventually you will try your best to chase it. Be careful, there is also a timer base on which the jelly can escape your sights forever! Also, as any other thingies today, this jelly is a powerful AI machine that constantly learns to make his way faster and trickier. Thus, the more you advance level-wise, the more difficult the jelly is to be chased.
You have a number of chances to chase the jelly as it is shown by the number of 'hearts' at the bottom of the screen.

<h3> App implementation </h3>

The app is written in Java language, using the Android Studio platform. It consists of a **menu** window, a **game progress window** and the **gameplay scene**.

The gameplay **cell network** is represented a static array of objects. Depending on the game level, a dynamic array (the **entity's path**) is spanning over the network based on rules and restrictions. For example, the first level contains a spiral path spanning uniformly over the width and height of the network. Throughout level completion, the next ones become more and more difficult and start to develop the element of random so that the path is increasingly difficult to be figured out.
After the level choice, on loading screen the path building rules are selected and a path is generated for the upcoming level.

The app is operated by multiple **threads** which fire up at spefic time and conditions, and make up the motions of the game. Thus, a Handler().postDelayed() function is performed to a Runnable object (thread). Each thread executes transforms on certain game elements and their execution is interrupted upon completion. For example, the entity will only stay above a cell for **TotalTime / path.length** seconds. For the first **TotalTime / path.length** seconds, the first Runnable() object is executing, which positions the entity on the first position of the path. For the next **TotalTime / path.length** seconds, another Runnable() object is fired up and keeps the entity on the second position of the path for the specific amount of time. This is equivalent to a SurfaceView onDrawFrame() implementation, where the scene is rendered continuously, at each frame (unless specified otherwise).
