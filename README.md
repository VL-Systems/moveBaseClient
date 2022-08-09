# moveBaseClients
Пакет ROS, который содержит несколько клиентов для навигации move_base.  
Этот пакет предоставляет клиенты move_base для различных языков, таких как C++, Python, HTML. Вы можете получить доступ к move_base различными способами. А файлы запуска могут помочь вам адаптировать параметры клиентов к вашему уникальному роботу.
## Launch files
* move_base_clients.launch  
Это файл запуска для клиента C++ с классом. Задайте аргументы для вашего робота, например  
`roslaunch move_base_clients move_base_clients.launch move_base_node:=move_base move_base_action:=move_base use_amcl:=false enable_clear_costmap:=false use_turtlebot3_buzzer:=false x:=1.0 y:=1.5 theta:=-1.57`  
### Arguments
1. move_base_node  
Имя узла ROS move_base.
2. move_base_client  
Имя клиента movie_base. 
3. enable_clear_costmap  
Установите для этого значение true, если вы хотите, чтобы клиент вызывал службу clear costmap, когда планировщик не может получить траекторию в начале. **Для этого требуется имя узла move_base.**
4. use_amcl  
Установите это значение равным true, если вы хотите обновить локализацию AMCL, когда робот движется медленно. Иногда из-за неправильной локализации глобальный планировщик не может определить подходящую траекторию для робота, и это заставляет робота двигаться медленно или колебаться. Таким образом, в этом случае эта опция может выполнить обновление AMCL без перемещения на определенное расстояние или угол. **Этот параметр следует использовать только при запуске AMCL в качестве модуля локализации.**
5. use_turtlebot3_buzzer  
Если вы работаете с [Turtlebot 3](http://manual.robotics.com/docs/en/platform/turtlebot3/overview /), вы можете установить для этого аргумента значение true.
6. x y theta  
Положение и ориентация цели. 
## Dynamic reconfigure
1. clear_costmap_threshold_dist  
2. clear_costmap_active_time  
Если робот не удалит clear_costmap_threshold_dist на расстояние нескольких метров от начальной позиции в течение секунд clear_costmap_active_time, будет вызвана служба clear_costmaps. 
3. nmu_request_timer  
Номер сброса на время отсутствия обновления amcl. 
## Executables
* simple_client  
Простой клиент C++, который вы можете легко использовать с помощью команды rosrun. например
`rosrun move_base_clients simple_client 3.5 -0.34 -3.14`
* client.py  
Простой клиент Python, который вы можете легко использовать с помощью команды rosrun. например
`rosrun move_base_clients client.py 3.5 -0.34 -3.14`
* client_with_class  
Сложный клиент на C++. Вам лучше начать с **move_base_clients.launch**.  
* web_nav.html  
Клиент навигации по веб-страницам, который вы можете открыть с помощью веб-браузера. Вы можете взаимодействовать с веб-страницей, например, с RViz. Для получения более подробной информации, пожалуйста, посетите (http://wiki.ros.org/nav2djs/Tutorials/Creating Базовый Навигационный 2D-Виджет).
* client_with_smach.py  
Клиент Python с конечным автоматом smach, который содержит меню опций. например
`rosrun move_base_clients client_with_smach.py`  
* publish_point.py  
Вспомогательный клиент Python, который вы можете использовать инструмент rviz __Publish Point__ для последовательной установки целей. Робот направится к следующей цели, когда достигнет текущей цели.