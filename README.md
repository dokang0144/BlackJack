# BlackJack
파이썬으로 만든 블랙잭 카지노
![image](https://user-images.githubusercontent.com/88234731/196957791-d9b83afb-abe1-4287-908e-918586d8c510.png)
## 블랙잭 룰
+ <b>1.</b> 딜러와 플레이어 모두에게 먼저 2 장씩 카드를 받습니다.
+ <b>2.</b> 자신이 갖고 있는 카드의 합이 21에 가까워 지도록 카드를 추가하거나 스탠드를 선택할 수 있습니다.
+ <b>3.</b> 카드의 합이 21을 넘어 버린 시점에서 패배가 결정됩니다.
+ <b>4.</b> 플레이어는 21을 초과하지 않는 한 원하는만큼 카드를 추가 할 수있습니다.
+ <b>5.</b> 플레이어가 스탠드를 하면 딜러의 카드 합과 비교하여 카드 합이 더 큰 쪽이 이기는 게임입니다.

```
히트(Hit) : 카드 한 장을 추가한다.

스탠드(Stand) : 카드를 추가하지 않는다 (현재의 수치 인 채로 딜러와 승부)

서렌더(Surrender) : 처음 받은 2장의 카드를 확인하고 “이길 수 없다”라고 판단될 경우 “항복”하여 베팅의 절반을 돌려받을 수 있습니다.
```
## 실행하기

>### 먼저 프로그램을 실행하면 카지노에 입장할건지 선택합니다.
>>![image](https://user-images.githubusercontent.com/88234731/197225376-5bfacfad-89fe-42f5-b4b9-b9aa4c051ff4.png)
>### 카지노에 입장하면 처음에 500$가 지급되고 배팅을 합니다.
>>![image](https://user-images.githubusercontent.com/88234731/197392315-ea74d2b9-333f-4b83-93c2-3be481a95714.png)
>### 배팅을 한 후 게임이 시작되고 카드 두 장을 뽑습니다.
>### 이제 플레이어는 선택을 해야하는데 카드 합이 21 또는 21에 가장 가까운 숫자가 만들어 지도록 합니다.
>>![image](https://user-images.githubusercontent.com/88234731/197392381-50a8cbec-a2d6-422e-8b2f-1157e5dfa090.png)
>### 카드가 9, 2이므로 한번 히트하고 스탠드를 하였습니다.
>### 저의 카드 합이 딜러의 카드 합보다 더 크기 때문에 베팅한 금액의 2배를 받습니다.
>>![image](https://user-images.githubusercontent.com/88234731/197393832-e3dabe9e-f815-45f4-a533-d99d5c9550a7.png)
>### 이번엔 1,000$를 배팅하고 서렌더를하면 500$만 돌려받습니다.
>>![image](https://user-images.githubusercontent.com/88234731/197394156-f0d81929-d96f-41e0-849f-432e3f639aaf.png)
>### 게임을 그만하면 프로그램이 종료됩니다.
>>![image](https://user-images.githubusercontent.com/88234731/197394347-59cea049-355b-41dc-9a41-19546b7f12d3.png)
><br>
## 소스코드
```python
import random

print("★ ☆ ★ ☆ ★ 블랙잭 카지노 ★ ☆ ★ ☆ ★")
print("블랙잭 카지노에 오신 것을  환영합니다.")
print("1.입장하기 2.나가기")
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
