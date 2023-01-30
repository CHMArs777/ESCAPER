# ESCAPER
# Подключение библиотек 
# from turtle import color
import pygame 
import time
from random import randint

# Инициализация библиотеки pygame
pygame.init()


dis_width = 800
dis_height  = 400

# Объявление переменных для цвета
white = (100, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)

dis = pygame.display.set_mode((dis_width, dis_height))

pygame.display.set_caption('ESCAPER')

game_over = False
#  начальное положение
x1 = (dis_width - min_Width)/4 
y1 = dis_height / 2

# Размер змейки
hero_block = 20

x1_change = 0
y1_change = 0
 
clock = pygame.time.Clock()
hero_speed = 5
 
# Яблоко
x_guard = 0
y_guard = 0
guard = False
guard_size = 30

# Счетчик
count = 0
countStr = ''


def randomGuard(x_apple,y_apple):
    x_guard = randint(0, dis_width)
    y_guard = randint(0, dis_height)
    
    return x_apple, y_apple

font_style = pygame.font.SysFont(None, 50)
# Функция вывода сообщения
def message(msg, color, x, y):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [x, y])


while not game_over:

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                x1_change = -snake_block
                y1_change = 0
            elif event.key == pygame.K_RIGHT:
                x1_change = snake_block
                y1_change = 0
            elif event.key == pygame.K_UP:
                y1_change = -snake_block
                x1_change = 0
            elif event.key == pygame.K_DOWN:
                y1_change = snake_block
                x1_change = 0
            elif event.key == pygame.K_SPACE:
                y1_change = 0
                x1_change = 0
     
#  Условия Проигрыша
    if ((x1 > dis_width or x1 < 0) or (y1 > dis_height or y1 < 0)):
        game_over = True
    x1 += x1_change
    y1 += y1_change
    dis.fill(white)

   # Для добавления используем метод draw
    pygame.draw.rect(dis, black, [x1, y1, hero_block, hero_block])
    pygame.draw.rect(dis, green, [x_guard, y_guard, guard_size, guard_size], 50)


    if changeColor != 255:
        

    # Рисуем яблоко
    if(guard == False):
        x_guard = randint(0, dis_width)
        y_guard = randint(0, dis_height)
        pygame.draw.rect(dis, green, [x_guard, y_guard, guard_size, guard_size], 50)
        apple = True

    # Проверка на столкновение координат
    if(((x_apple < x1) and (x_apple+apple_size > x1)) and ((y_apple < y1) and ((y_apple+apple_size) > y1)) or ((x_apple < x1+hero_block) and (x_apple+apple_size > x1+hero_block)) and ((y_apple < y1) and ((y_apple+apple_size) > y1)) or ((x_apple < x1) and (x_apple+apple_size > x1)) and ((y_apple < y1+hero_block) and ((y_apple+apple_size) > y1+hero_block)) or ((x_apple < x1+hero_block) and (x_apple+apple_size > x1+snake_block)) and ((y_apple < y1+snake_block) and ((y_apple+apple_size) > y1+snake_block))):
        x_guard = randint(guard_size, dis_width-guard_size)
        y_guard = randint(guard_size, dis_height-guard_size)
        count+=1
        hero_speed +=1
    countStr = str(count)
    message(countStr, red, 10, 100)
    pygame.display.update()
    
    clock.tick(hero_speed)


message("You lost",red)
pygame.display.update()
time.sleep(2)
 
pygame.quit()
quit()
