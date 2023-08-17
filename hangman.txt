import random as r
Words=open('word.txt')
Words=Words.read().split()
while True:
    print(f"{'*'*30}WELCOME TO HANGMAN{'*'*30} \n 1. Enter 'P' for play \n 2. Enter 'A' for Administrator \n 3. Enter 'E' for Exit \n{'*'*90}")
    i = input("Select your choice: ").upper()
    if i == 'P':
        def Play():
            g = 6
            w = 3
            secret = r.choice(Words).lower()
            display = "_" * len(secret)
            print(display)
            Al = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't',
                  'u', 'v', 'w', 'x', 'y', 'z']
            length = len(secret)
            print(f'I am thinking of word which is of {length} letters')
            print("secret word", secret)
            while g > 0 and display != secret:
                Ast = "".join(Al)
                print(f"Total no of guesses = {g}\nTotal no of warnings = {w}\nAvailable Letters = {Ast}")
                wchoice = input("Enter your guess: ").lower()
                if wchoice in secret and wchoice in Al:
                    Al.remove(wchoice)
                    print("Good you find the correct letter")
                    for i in range(len(secret)):
                        if secret[i] == wchoice:
                            display = display[:i] + secret[i] + display[i + 1:]
                            print(display)
                elif wchoice in secret and wchoice not in Al:
                    print(display)
                    print("you repeat a wrong word")
                    if w > 0:
                        w -= 1
                    else:
                        g -= 1
                else:
                    print('Oh!letter not in secret word')
                    if wchoice in "aeiou":
                        if wchoice in Al:
                            print(display)
                            g -= 2
                            Al.remove(wchoice)
                        else:
                            print('Oh!letter not in secret word')
                            print(display)
                            if w > 0:
                                w -= 1
                            else:
                                g -= 1
                    elif wchoice in "bcdfghjklmnpqrstvwxyz":
                        if wchoice in Al:
                            print(display)
                            print('Oh! you guess a wrong consonant letter')
                            g -= 1
                            Al.remove(wchoice)
                        else:
                            print(display)
                            print('Oh! you guess a wrong consonant letter')
                            if w > 0:
                                w -= 1
                            else:
                                g -= 1
                    else:
                        print(display)
                        print('invalid character')
                        if w > 0:
                            w -= 1
                        else:
                            g -= 1
                if g == 6:
                    print('----------------')
                    print('|/              ')
                    print('|               ')
                    print('|               ')
                    print('|               ')
                    print('|               ')
                    print('|               ')

                if g == 5:
                    print('----------------')
                    print('|/              ')
                    print('|               ')
                    print('|       (O)     ')
                    print('|               ')
                    print('|               ')
                    print('|               ')
                if g == 4:
                    print('----------------')
                    print('|/              ')
                    print('|               ')
                    print('|       (O)     ')
                    print('|        |      ')
                    print('|        |      ')
                    print('|               ')
                if g == 3:
                    print('----------------')
                    print('|/              ')
                    print('|               ')
                    print('|       (O)     ')
                    print('|       /|\     ')
                    print('|        |      ')
                    print('|               ')
                if g == 2:
                    print('----------------')
                    print('|/              ')
                    print('|               ')
                    print('|       (O)     ')
                    print('|       /|\     ')
                    print('|        |      ')
                    print('|       / \     ')
                if g == 1:
                    print('----------------')
                    print('|/       |      ')
                    print('|        |      ')
                    print('|       (O)     ')
                    print('|       /|\     ')
                    print('|        |      ')
                    print('|       / \     ')
                if g == 0:
                    print('----------------')
                    print('|/       |      ')
                    print('|        |      ')
                    print('|       (O) < DEAD')
                    print('|       /|\     ')
                    print('|        |      ')
                    print('|       / \     ')
            secret_l = list(secret)
            count = 0
            for i in secret:
                secret_l.remove(i)
                if i in secret_l:
                    count += 1
            unique = len(secret) - count
            if display == secret:
                score = g*unique
                print(f'you win\nyour score={score}')
                with open ('score.txt','r+') as hs:
                    hs.write(f"{n}\t{str(score)}")
                    hs.flush()
                    hs.seek(0)
                    line = hs.readline()
                    highscore = 0
                    while line != '':
                        line=line.strip('\n')
                        line=line.split("\t")
                        if highscore < int(line[1]):
                            highscore = int(line[1])
                            nam=line
                        line = hs.readline()
                    if score>highscore:
                        print('Congrats you made highest score',n)
            else:
                print("Oh! you loss")
        n = input('ENTER YOUR NAME:')
        print(f'{"*"*80} WELCOME {n} {"*"*80}')
        Play()
        option = input('Do you want to play again?[y/n]')
        if option == "y" or option == "Y":
            Play()
        elif option == "n" or option == "N":
            continue
    if i=='A':
        while True:
            print(f"{' * ' * 10} Administrator Block {' * ' * 10}")
            Pas='hangman'
            Name='Manba'
            an=input('Enter your name:')
            ap=input('Enter password:')
            if an == Name and ap == Pas:
                print(f"1. Add words in file of words \n2. Reset highest score and name of player\n3.Exit from Administrator interface")
                ad=input('Select your choice:[add/reset/exit]').lower()
                if ad=='add':
                    ws=input('Add a new word in words.txt file :')
                    with open('words.txt','a+') as f:
                        f.write(ws)
                        continue
                elif ad=='reset':
                    rem=input('Reset score[y/n]').lower()
                    if rem=="y":
                        with open("score.txt","w+") as hs:
                            continue
                    elif rem=='n':
                        continue
                elif ad =='exit':
                    break
            elif an != Name:
                again=input('Wrong Name, do you want to enter name again?[y/n]').lower()
                if again=='y':
                    continue
                elif again=='n':
                        break
            elif an != Pas:
                again = input('Wrong Password , do you want to enter again?[y/n]').lower()
                if again == 'y':
                    continue
                elif again == 'n':
                    break
    if i == 'E':
        break