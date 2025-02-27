# nav-gym

A OpenAI-gym compatible navigation simulator, which can be integrated into the robot operating system (ROS) with the goal for easy comparison of various approaches including state-of-the-art learning-based approaches and conventional ones.

**Note:** This reporsitory is part of [ICRA 2023 paper](https://arxiv.org/pdf/2305.19746.pdf). Please visit our [hrl-nav](https://github.com/leekwoon/hrl-nav) repo for more details. 

![indoor.gif](assets/indoor.gif)
![outdoor.gif](assets/outdoor.gif)

## Install

The package has been tested on Ubuntu 18.04 / Python 3.6 / ROS Melodic.

To install without ROS-supported:  

```bash
virtualenv ~/venv/hrlnav --python=python3.6
source ~/venv/hrlnav/bin/activate

git clone https://github.com/leekwoon/nav-gym.git

cd nav-gym/nav_gym
pip install -e .
```

To install with ROS-supported:  

```bash
virtualenv ~/venv/hrlnav --python=python3.6
source ~/venv/hrlnav/bin/activate

cd ~/YOUR_CATKIN_WORKSPACE/src
git clone https://github.com/leekwoon/nav-gym.git

# install nav_gym_env
cd nav-gym/nav_gym
pip install -e .

cd ~/YOUR_CATKIN_WORKSPACE
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3
source devel/setup.bash # or you can write it on ~/.bashrc
```

## Usage

```python
import gym
import nav_gym_env

env = gym.make("NavGym-v0")
obs = env.reset()

done = False
while not done:
    action = env.action_space.sample() # Your agent code here
    obs, reward, done, info = env.step(action)
    env.render()
```

We recommend installing our package with ROS-supported since RViz visualization is fast and interactive. If you want to use RViz visualization, first run:

```bash
roslaunch nav_gym start_nav_gym.launch
```

and in another terminal, run:

```bash
roslaunch nav_gym view_robot.launch
```

now we can simulate:

```python
import gym
import nav_gym_env
from nav_gym_env.ros_env import RosEnv

env = gym.make("NavGym-v0")
env = RosEnv(env)
obs = env.reset()

done = False
while not done:
    action = env.action_space.sample() # Your agent code here
    obs, reward, done, info = env.step(action)
```

## Reference

```
@software{lee2023nav,
  author={Lee, Kyowoon and Kim, Seongun and Choi, Jaesik},
  title={nav-gym},
  url={https://github.com/leekwoon/nav-gym},
  year={2023}
}
```

## License

This repository is released under the MIT license. See [LICENSE](LICENSE) for additional details.

## Credits

Our codebase builds based on [all-in-one-DRL-planner](https://github.com/ignc-research/all-in-one-DRL-planner), [navrep](https://github.com/ethz-asl/navrep) and [
flatland](https://github.com/avidbots/flatland). 
