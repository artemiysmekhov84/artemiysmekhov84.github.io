Ранее я писал про принцип работы и назначение [датчика профилей](/professional-projects?id=10) (лазерного триангуляционного 2D сканера). Для того, чтобы максимально использовать все возможности такого сканера, его часто крепят на фланец промышленного робота. Это позволяет, при условии синхронизации движения робота и захвата профилей со сканера, использовать 2D сканер в качестве 3D датчика. Однако для этого необходимо откалибровать сканер на роботе, то есть найти преобразование из системы координат сканера в систему координат фланца. Эта процедура называется внешней калибровкой (extrinsic calibration). Целью этой работы было создание алгоритма, который бы позволил проводить такую калибровку в автоматическом режиме.

Существуют различные способы выполнения внешней калибровки. Часто они, так или иначе, используют некоторый калибровочный объект с известной геометрией. В данной работе использовалась сфера известного радиуса (бильярдный шар).

Суть реализованного алгоритма заключается в автоматизированном сборе профилей со сферы при различных положениях фланца робота и подборе таких параметров преобразования координат, которые бы минимизировали отклонение полученных профилей от поверхности сферы. Мной была разработана двухэтапная процедура поиска целевого преобразования. На первом этапе происходит сбор профилей при фиксированной ориентации сканера. Это позволяет вычислить три угла (roll, pitch, yaw), определяющие матрицу поворота сканера. На втором этапе происходит сбор профилей с различными ориентациями сканера. Это позволяет, используя углы, найденные на предыдущем этапе, вычислить смещение (x, y, z) сканера.

На анимированных изображениях ниже можно видеть автоматизированный процесс сбора профилей калибровочной сферы (2 этап). В качестве датчика профилей использовался промышленный сканер [Wenglor MLSL 123](https://www.wenglor.com/en/2D3D-Sensors/2D3D-Profile-Sensors/2D3D-Profile-Sensor/p/MLSL123). Также на анимациях показан процесс численного поиска решения, которое даёт наименьшее возможное отклонение собранных профилей от поверхности сферы.