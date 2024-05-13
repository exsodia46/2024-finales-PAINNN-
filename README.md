import pygame 
import winsound
from player import player
from fire import fireball
from NPC import npc
#from enemy import enemy
pygame.init()
pygame.display.set_caption("top down grid game")
screen = pygame.display.set_mode((1200, 800))
clock = pygame.time.Clock()
gameover = False
mapNum = 1
winsound.PlaySound('life.wav', 0)
p1 = player()
ball = fireball()
bob = npc()
ticker = 0
#constantsw
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3
SPACE = 4
w = 5
keys = [False,False,False,False, False]


map = [[2,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],
       [2,0,0,0,0,2,2,4,0,2,0,0,0,0,3,0,2,2,2,2,0,0,0,2],
       [2,0,0,0,0,2,2,0,0,2,0,2,2,2,2,0,0,0,0,2,0,0,0,2],
       [2,0,0,2,2,2,2,0,0,2,0,2,4,0,0,0,2,2,0,2,0,0,0,2],
       [2,2,0,0,0,0,0,0,0,2,0,2,2,0,0,0,0,0,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,2,0,2,0,0,2,0,2,2,2,2,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,2,0,2,0,0,2,0,0,0,0,2,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,2,0,2,0,0,2,2,2,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,3,0,2,0,0,2,2,2,0,0,2,0,0,0,2],
       [2,2,2,3,2,2,2,2,2,2,2,2,0,0,0,0,0,1,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,2,2,2,2,2,3,2,0,0,0,2],
       [2,3,2,2,2,2,0,2,2,2,2,2,2,2,2,2,2,2,0,2,0,0,0,2],
       [2,0,2,0,2,0,0,2,2,4,0,1,0,0,0,0,0,2,0,2,0,0,0,2],
       [2,0,2,0,0,2,2,2,2,2,2,2,2,2,2,2,3,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,0,0,5],
       [2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2]]

map2 = [[2,3,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,2],
       [2,0,2,0,0,2,2,0,0,0,0,0,0,0,0,2,2,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,2,0,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,0,2,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2]]


wall = pygame.image.load('wall.png')
brick = pygame.image.load('brick.png')
door = pygame.image.load('door.png')
chest = pygame.image.load('chest.png')
exitdoor = pygame.image.load('exit.door.png')


while not gameover:
    clock.tick(60)
    ticker +=1

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            gameover = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = True
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = True
            elif event.key == pygame.K_UP:
                keys[UP] = True
            elif event.key == pygame.K_DOWN:
                keys[DOWN] = True
            elif event.key == pygame.K_SPACE:
                keys[SPACE] = True
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = False
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = False
            elif event.key == pygame.K_UP:
                keys[UP] = False
            elif event.key == pygame.K_DOWN:
                keys[DOWN] = False
            elif event.key == pygame.K_SPACE:
                keys[SPACE] = False    
        
 #physics-----------------------------------------------------------------------------------------
    ball.move()
    p1.move(keys, map)
   
    bob.move(map,ticker,p1.xpos,p1.ypos)

    if mapNum == 1:
        if map[int((p1.ypos ) / 50)][int( (p1.xpos) / 50)] ==5:
            mapNum = 2
            p1.xpos = 50
    
    if mapNum == 2:
        if map2[int((p1.ypos ) / 50)][int( (p1.xpos) / 50)] ==5:
            mapNum = 1
            p1.xpos = 1100

    
   
    if mapNum == 1:
        p1.move(keys , map)
    elif mapNum ==2:
        p1.move(keys , map2)
    
    if keys[SPACE] == True:
        print(p1.direction)
        ball.shoot(p1.xpos, p1.ypos, p1.direction)
    

 #renders-----------------------------------------------------------------------------------------
    


    screen.fill((0,0,0))

    p1.draw(screen)
    

    #draw FIRE
    if ball.isAlive == True:
        ball.draw(screen)
    if mapNum == 1:
        for i in range(16):
                for j in range(24):
                    if map[i][j] == 2:
                        screen.blit(brick, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 1:
                        screen.blit(wall, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 3:
                        screen.blit(door, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 4:
                        screen.blit(chest, (j * 50, i * 50), (0, 0, 50, 50))
                    if map[i][j] == 5:
                         screen.blit(exitdoor, (j * 50, i * 50), (0, 0, 50, 50))


    elif mapNum == 2: 
        for i in range(16):
                for j in range(24):
                    if map2[i][j] == 2:
                        screen.blit(brick, (j * 50, i * 50), (0, 0, 50, 50))
                    if map2[i][j] == 1:
                        screen.blit(wall, (j * 50, i * 50), (0, 0, 50, 50))
                    if map2[i][j] == 3:
                        screen.blit(door, (j * 50, i * 50), (0, 0, 50, 50))
                    if map2[i][j] == 4:
                        screen.blit(chest, (j * 50, i * 50), (0, 0, 50, 50))
                    if map2[i][j] == 5:
                        screen.blit(exitdoor, (j * 50, i * 50), (0, 0, 50, 50))
    
    
    bob.draw(screen)

    pygame.display.flip()



pygame.quit()
