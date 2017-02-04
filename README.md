import random as r

legal_x = [0,10]
legal_y = [0,10]

class Turtle:
    def __init__(self):
        #初始体力
        self.power = 100
        #初始位置
        self.x = r.randint(legal_x[0],legal_x[1])
        self.y = r.randint(legal_y[0],legal_y[1])

    def move(self):
        #移动中的位置,随机移动
        new_x = self.x + r.choice([1,2,-1,-2])
        new_y = self.y + r.choice([1,2,-1,-2])
        #检查是否超出X边界
        if new_x < legal_x[0]:
            self.x = legal_x[0] - (new_x - legal_x[0])
        elif new_x > legal_x[1]:
            self.x = legal_x[1] - (new_x - legal_x[1])
        else:
            self.x =new_x
        #检查移动后是否超出场景Y边界
        if new_y < legal_y[0]:
            self.y = legal_y[0] - (new_y - legal_y[0])
        elif new_y > legal_y[1]:
            self.y = legal_y[1] - (new_y - legal_y[1])
        else:
            self.y = new_y
        #体力值消耗
        self.power -= 1
        return(self.x,self.y)

    def eat(self):
        self.power += 20
        if self.power > 100:
            self.power = 100
            

class Fish:
    def __init__(self):
        #初始位置
        self.x = r.randint(legal_x[0],legal_x[1])
        self.y = r.randint(legal_y[0],legal_y[1])

    def move(self):
        #随机移动，1
        new_x = self.x + r.choice([1,-1])
        new_y = self.y + r.choice([1,-1])
        #检查是否超出X边界
        if new_x < legal_x[0]:
            self.x = legal_x[0] - (new_x - legal_x[0])
        elif new_x > legal_x[1]:
            self.x = legal_x[1] - (new_x - legal_x[1])
        else:
            self.x =new_x
        #检查移动后是否超出场景Y边界
        if new_y < legal_y[0]:
            self.y = legal_y[0] - (new_y - legal_y[0])
        elif new_y > legal_y[1]:
            self.y = legal_y[1] - (new_y - legal_y[1])
        else:
            self.y = new_y
        #返回一个新位置
        return(self.x,self.y)
    
turtle = Turtle()
fish = []
for i in range(10):
    new_fish = Fish()
    fish.append(new_fish)

while True:
    if not len(fish):
        print('鱼全被乌龟吃掉啦！')
        break
    if not turtle.power:
        print('乌龟体力耗尽了，挂掉了！')
        break

    pos = turtle.move()
    #这里把列表拷贝给迭代器，然后对原来列表进行删除
    for each_fish in fish[:]:
        if each_fish.move() == pos:
            #鱼被吃的情况
            turtle.eat()
            fish.remove(each_fish)
            print('有一只鱼被吃掉了...')
