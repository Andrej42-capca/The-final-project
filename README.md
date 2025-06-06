Я Зебницкий Андрей из группы Мф-72 сделал проект , рассчитывающий полет тела.(Сам код находиться в папке Code)
Этот код моделирует полет снаряда , брошенного под углом к горизонту, с учетом начальной скорости, угла броска и силы тяжести. Программа вычисляет траекторию, максимальную высоту, дальность полета и строит график.
Работа этого кода:
1. Импорт библиотек
python
import math          # Для математических расчетов (синусы, косинусы)
import numpy as np   # Для работы с массивами чисел
import matplotlib.pyplot as plt  # Для построения графиков
2. Функция calculate_projectile_motion(v0, angle_deg, y0=0.0, g=9.81)
Принимает параметры:

v0 – начальная скорость (м/с),

angle_deg – угол броска (в градусах),

y0 – начальная высота (по умолчанию 0),

g – ускорение свободного падения (по умолчанию 9.81 м/с²).

3. Разложение скорости на компоненты
python
angle_rad = math.radians(angle_deg)  # Переводим угол из градусов в радианы
vx = v0 * math.cos(angle_rad)        # Горизонтальная составляющая скорости
vy = v0 * math.sin(angle_rad)        # Вертикальная составляющая скорости
Горизонтальная скорость (vx) остается постоянной (если не учитывать сопротивление воздуха).

Вертикальная скорость (vy) меняется из-за ускорения свободного падения (g).

4. Расчет времени подъема и максимальной высоты
python
t_up = vy / g  # Время подъема до максимальной точки
h_max = y0 + (vy ** 2) / (2 * g)  # Максимальная высота
Время t_up – это момент, когда вертикальная скорость vy становится равной нулю.

Формула h_max выводится из уравнения равноускоренного движения.

5. Расчет общего времени полета и дальности
python
t_total = t_up + math.sqrt((2 * (h_max if y0 == 0 else (h_max + y0))) / g)
L = vx * t_total  # Дальность полета
t_total – общее время полета (включая подъем и падение).

L – расстояние, которое пролетит снаряд (vx * время).

6. Построение траектории
python
t_points = np.linspace(0, t_total, 100)  # 100 точек времени от 0 до t_total
x_points = vx * t_points  # Горизонтальные координаты
y_points = y0 + vy * t_points - 0.5 * g * t_points**2  # Вертикальные координаты
x_points и y_points – массивы координат снаряда в разные моменты времени.

