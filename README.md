# ProjetGSE

Après avoir installé le système Linux, le système ros, google cartographer, les packages ros du RPidar et de la caméra sur la carte et l'ordinateur, exécutez les commandes suivantes dans les terminaux:

odroid : le nom de carte
administreur-OptiPlex-9020 : le nom de votre PC


Terminal 1 de la carte: Exécuter swap et roscore .
    
    $ sudo swapon swapfile
    $ free –h
    $ source catkin_ws/devel_isolated/setup.bash
    $ ssh odroid
    $ roscore
    
Terminal 2 de la carte: Connecter Lidar

    $ sudo chmod 666 /dev/ttyUSB0
    $ source /home/odroid/catkin_ws/devel_isolated/setup.bash
    $ roslaunch rplidar_ros rplidar.launch
    
Terminal 3 de la carte: Connecter caméra

    $ export ROS_HOSTNAME=odroid
    $ export ROS_MASTER_URI=http://odroid:11311
    $ rosrun usb_cam usb_cam_node
---------------------------------------------------------------------

Terminal 1 du PC: Démarer cartographer et RVIZ

    $ cd catkin_ws
    $ ssh administreur-OptiPlex-9020
    $ export ROS_HOSTNAME=administreur-OptiPlex-9020
    $ export ROS_MASTER_URI=http://odroid:11311
    $ export DISPLAY=':0.0'
    $ source catkin_ws/devel_isolated/setup.bash
    $ roslaunch cartographer_ros demo_revo_lds.launch
    
Terminal 2 du PC: Démarer darknet

    $ cd catkin_ws
    $ ssh administreur-OptiPlex-9020
    $ export ROS_HOSTNAME=administreur-OptiPlex-9020
    $ export ROS_MASTER_URI=http://odroid:11311
    $ export DISPLAY=':0.0'
    $ source catkin_ws/devel_isolated/setup.bash
    $ roslaunch darknet_ros darknet_ros.launch
Terminal 3 du PC: Enregistrer le fichier de cartographer -> .bag file

    $ ssh administreur-OptiPlex-9020
    $ export ROS_HOSTNAME=administreur-OptiPlex-9020
    $ export ROS_MASTER_URI=http://odroid:11311
    $ export DISPLAY=':0.0'
    $ source catkin_ws/devel_isolated/setup.bash
    $ rosbag record -a

Avant d'exécuter ces commandes, assurez-vous que la carte et l'ordinateur se trouvent sur le même réseau local et connectez-les en modifiant le fichier /etc/hosts, c'est-à-dire que vous pouvez tester l'établissement de la communication via la commande ping.
