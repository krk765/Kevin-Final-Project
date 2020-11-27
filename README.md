# Kevin-Final-Project

Obstacle Project - Kevin Khauv


Main Menu
    Unity UI Canvas and text to display instructions.
    Unity UI buttons to control back or next scene navigation.

Platform (Ground Tile)
    Platform utilises Probuilder to create hexagonal grid platform.
    Each with Convex collider mesh for performance.
    Navigationally static to provide NavMesh for our Duck Creeps.

    Upon collision with robot explosion animation, will drop, turn off mesh renderer to become invisible, activate
    NavMesh Obstacle then return to platform level to carve out section of NavMesh so Ducks cannot walk over the hole.
    Mesh collider will also be disabled allowing the player to faller through the hole.

SkyBox
    Free unity store asset Fantasy SkyBox by Render Knight

Game HUD and Counter
    Keeps track of the elapsed time of the level, and displaying as Minute : Seconds : Split seconds.

    Pause Menu will be called upon "Enter" press. Which will open pause menu, stop player controller movement, player camera movement
    Duck movement, robot movement and stop the time counter.

    Upon gameover, will display counter of ducks killed and elapsed time.

    Scene Manager to change between level scene and Main Menu. Can only get to GameOver screen when player falls below a certain Y axis.

Player/User
    Player model using free unity store asset RPG Hero PBR HP Polyart by Dungeon Mason model and animations. 3rd person movement and camera untilises character
    controller component and Cinemachine with custom code to control character movement and 3rd person camera.

    Grounding Check done through box casts.

    Animation will be dependent on movement. Attack animation uses only upper half of humanoid rig so walking
    animation unaffected by attack animation.

    PlayerRadius involves sphere collider, which upon collision will call a WithinPlayerRadius action/delegate, and upon leaving
    will call OutsidePlayerRadius. Each creep (layer which includes the duck) will listen to the delegate, and check if its ID
    matches that of the one which collided with the player radius sphere.

    Attacking utilises a box overlap collision check as well as interface IDamageable to check if collide with a Creep

Duck (Creep Layer)
    Model and animation from free unity store asset Lovely Animals PACK by JKTimmons.
    Duck Spawner involves creating a gameobject pool of the prefab Duck upon starting, and activating the gameobjects
    when required (ie when there a no active ducks on the platform). Saving memory through recyling instead of
    instantiating and destroying duck gameobjects.
    Will randomly spawn the duck in a tile which has not been destroyed/invisible, and delay spawn between each duck by 3s.


    Movement utilising NavMesh Agent component on top of platform NavMesh of the platform.
    Animation will depend on character speed or idle/stopped.
    NavMesh destinations assigned randomly with coroutines within given radius, with 3/10 chance to wait at given location.

    If Duck is within the player radius sphere, will enable "!!!" billboard, increase movement speed, and set new
    nav mesh destinations which are away from the player.

Robot
    Model and animation from free unity store asset RobotSphere by Razgrizzz Demon.
    Same as the duck spawner, the robot spawner will also create a robot gameobject pool to recycle, and increase if required.

    Will spawn robots upon action/delegate call from HUD/counter at certain second interviews, which will shorten depending on
    duck killed count.
    Each Robot will spawn above a random platform tile (which is not destroyed). Line Renderer will display a line which increases
    in thickness depending on how close to the platform it is.

    Upon collision with the ground tile mesh, will change animation, wait a delay then play particle system, making an "explosion".

Audio
    BFxr random sound generator and free asset BGM from Box Cat Games.


This game relies on actions/delegates to connect the different gameobjects and change logic/ enable actions to occur.
