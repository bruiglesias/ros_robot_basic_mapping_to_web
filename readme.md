# Exemplo 

<img src="https://github.com/bruiglesias/ros_robot_basic_mapping_to_web/blob/master/src/webpages/images/image01.png" width="600"/> 

# Iniciando o mundo, modelo e rviz ( if want just clone and run)

roslaunch my_simulations my_world.launch --screen

roslaunch robot_description spawn.launch

roslaunch robot_description rviz.launch

roslaunch rosbridge_server rosbridge_websocket.launch

roslaunch robot_description hector_mapping.launch

open webpage folder index file 


# Criando o projeto  (if want re-create step-by-step)

cd ros_workspaces

mkdir ros_bruno_robot

cd ros_bruno_robot

mkdir src

catkin init

source devel/setup.bash

catkin_make

# add models to gazebo

mkdir ~/clones 

cd clones 

git clone https://github.com/osrf/gazebo_models.git

sudo gedit ~/.bashrc

add line: export GAZEBO_MODEL_PATH=~/clones/gazebo_models


# criando o mundo

catkin_create_pkg my_simulations

(criar as pastas launch e worlds, depois criar os arquivos)

cd ..

catkin_make


## add diferencial robot two wheels

cd ~/clones

git clone https://bitbucket.org/theconstructcore/two-wheeled-robot-simulation.git

~/ros_workspaces/ros_bruno_robot/src

catkin_create_pkg robot_description

copiar as pastas launch e urdf de  ~/clones/two-wheeled-robot-simulation para esta pasta

(mudar todas as referências de m2wr para robot)

cd ..

catkin_make

# correcao de erros - rviz.launch

No arquivo, substituir a linha parecida por:

```
<param name="robot_description" command="$(find xacro)/xacro --inorder '$(find robot_description)/urdf/robot.xacro'" />

```
e também por:

```
<node name="robot_state_publisher" pkg="robot_state_publisher" type="robot_state_publisher" />
```

# iniciando o mundo, modelo e rviz

roslaunch my_simulations my_world.launch --screen

roslaunch robot_description spawn.launch

roslaunch robot_description rviz.launch

roslaunch rosbridge_server rosbridge_websocket.launch

roslaunch robot_description hector_mapping.launch

rosrun teleop_twist_keyboard teleop_twist_keyboard.py
