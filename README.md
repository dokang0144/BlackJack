# BlackJack
파이썬으로 만든 블랙잭 카지노
![image](https://user-images.githubusercontent.com/88234731/196957791-d9b83afb-abe1-4287-908e-918586d8c510.png)
## 실행하기
먼저 프로그램을 실행하면 카지노에 입장할건지 선택합니다.<br>
![image](https://user-images.githubusercontent.com/88234731/197225376-5bfacfad-89fe-42f5-b4b9-b9aa4c051ff4.png)


```python
import random

print("★ ☆ ★ ☆ ★ 블랙잭 카지노 ★ ☆ ★ ☆ ★")
print("블랙잭 카지노에 오신 것을  환영합니다.")
print("1.입장하기 2.나가기")1
Awake = int(input())
money = 500

def StartGame(bet):
    print("========== 게임을 시작합니다. ==========")
    print("카드 두 장을 드리겠습니다.")

    MyCard = []

    MyCard.append(random.randrange(1,12))
    MyCard.append(random.randrange(1,12))

    print(MyCard)

    Select(MyCard, bet)

    if(money==0):
        print("돈이 0원이어서 쫓겨났습니다.")
        exit()

    print("게임을 다시 하시겠습니까?")
    print("1.예 2.아니요 ")

    Re = int(input())

    if(Re==1):
        Bet()
    else:
        input("안녕히 가십시오 . . .")
        exit()

    

def Select(MyCard, bet):
    global money
    if(sum(MyCard)<=21):
        print("1.히트 2.스탠드 3.서렌더")
        select = int(input())

        if(select==1):
            print("히트를 하셨습니다.")
            print("카드 한 장을 드리겠습니다.")
            MyCard.append(random.randrange(1,12))
            print(MyCard)
            Select(MyCard, bet)
        elif(select==2):
            print("스탠드를 하셨습니다.")

            print("당신의 카드 합")
            print(sum(MyCard))
            ComCard = random.randrange(2,22)
            print("딜러 카드 합")
            print(ComCard)

            if(sum(MyCard)>ComCard and sum(MyCard)<=21):
                print("당신의 승리입니다."+"        획득상금("+"\033[32m"+format(bet, ',d')+"$"+"\033[0m"+")")
                money += bet
                return MyCard, money, bet
            else:
                print("당신의 패배입니다.       돈을 잃으셨습니다.")
                money -= bet
                return MyCard,  money, bet
            
        else:
            print("서렌더를 하셨습니다.")
            print("금액의 50%를 돌려받습니다.")
            print("돌려받은 금액 : "+"\033[32m"+format(round(bet/2), ',d')+"$"+"\033[0m"+")")
            money -= int(bet/2)
            return MyCard, money, bet

    else:
        print("21이 넘어갔습니다.")
        print("당신의 패배입니다.       돈을 잃으셨습니다.")
        money -= bet
        return MyCard, money, bet

def Bet():
        print("얼마를 배팅하시겠습니까? "+"현재금액("+"\033[32m"+format(money, ',d')+"$"+"\033[0m"+")")
        bet = int(input("배팅할 금액 : "))

        if(bet<=0):
            print("0 이하로 입력하지마세요 . . .\n")
            Bet()
        
        elif(bet <= money):
            StartGame(bet)

        else:
            print("배팅하기에 금액이 부족합니다 . . .\n")
            Bet()

if(Awake==1):
    Bet()
               
else :
    input("안녕히 가십시오 . . .")
```
