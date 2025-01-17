# Flappy Bird for Gymnasium

![Python versions](https://img.shields.io/pypi/pyversions/flappy-bird-gymnasium)

This repository contains the implementation of two Gymnasium environments for
the Flappy Bird game. The implementation of the game's logic and graphics was
based on the [flappy-bird-gymnasium](https://github.com/markub3327/flappy-bird-gymnasium) project, by
[@markub3327](https://github.com/markub3327). 

## State space

The "FlappyBird-rgb-v0" environment, yields RGB-arrays (images)
representing the game's screen. The "FlappyBird-v0" environment, on the other
hand, yields simple numerical information about the game's state as
observations.

### `FlappyBird-v0`
* the last pipe's horizontal position
* the last top pipe's vertical position
* the last bottom pipe's vertical position
* the next pipe's horizontal position
* the next top pipe's vertical position
* the next bottom pipe's vertical position
* the next next pipe's horizontal position
* the next next top pipe's vertical position
* the next next bottom pipe's vertical position
* player's vertical position
* player's vertical velocity
* player's rotation

### `FlappyBird-rgb-v0`
The RGB image of size 288, 512 pixels. The pixel values are from range [0, 255]. The image does not contain score of bird.

## Action space

* 0 - **do nothing**
* 1 - **flap**

## Rewards

* +0 - **every frame it stays alive**
* +5.0 - **successfully passing a pipe**
* -2.0 - **dying** (hit pipe, floor, or ceiling)

<br>

<p align="center">
  <img align="center" 
       src="https://github.com/markub3327/flappy-bird-gymnasium/blob/main/imgs/dqn.gif?raw=true" 
       width="200"/>
</p>

## Installation
    python setup.py
## Usage

Like with other `gymnasium` environments, it's very easy to use `flappy-bird-gymnasium`.
Simply import the package and create the environment with the `make` function.
Take a look at the sample code below:

```
import time
import flappy_bird_gymnasium
import gymnasium
env = gymnasium.make("FlappyBird-v0")

obs, _ = env.reset()
while True:
    # Next action:
    # (feed the observation to your agent here)
    action = env.action_space.sample()

    # Processing:
    obs, reward, terminated, _, info = env.step(action)
    
    # Rendering the game:
    # (remove this two lines during training)
    env.render()
    time.sleep(1 / 30)  # FPS
    
    # Checking if the player is still alive
    if terminated:
        break

env.close()
```

## Playing

To play the game (human mode), run the following command:

    $ flappy_bird_gymnasium
    
To see a random agent playing, add an argument to the command:

    $ flappy_bird_gymnasium --mode random

To see a Deep Q Network agent playing, add an argument to the command:

    $ flappy_bird_gymnasium --mode dqn
