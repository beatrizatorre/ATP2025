# TPC2

## Autor

Beatriz Antunes da Torre, a110500, (![foto](Foto.jpg))

## Resumo

Criação de um programa em Python para jogar o jogo "Jogo dos Fósforos".

## Resultados 

* Res 1 - import random 

print ("Bem vindo ao Jogo dos Fósforos!\n O jogo começa com 21 fósforos.\n Em cada jogada só pode tirar entre 1 e 4 fósforos.\n Perde quem ficar com o último fósforo!\n")
fosforos = 21 
começa = input ("Quem começa a jogar? (u = utilizador ou c = computador)") #escolher quem começa

while fosforos > 1:
    print (f"Restam {fosforos} fósforos.")
    if começa =="u": #o utilizador é o primeiro a jogar
        while True:
            tirar = int (input(f"Quantos fósforos quer tirar (1-4)?"))

            if (1 <= tirar <=4 ) and (tirar < fosforos):
                break
            else:
                print  ("Número inválido. Tente novamente.")

        fosforos = fosforos - tirar
        print (f"Você retirou {tirar} fósforos, agora, restam {fosforos} fósforos.")

        if fosforos == 1:
            print ("Sobrou 1 fósforo. Você perdeu!")
            break

        computador = 5 - tirar  #computador joga em segundo, por isso ganha sempre
        if computador >= fosforos:
            computador = fosforos - 1

        fosforos = fosforos - computador
        print (f"O computador retira {computador} fósforos. Restam {fosforos} fósforos.")

        if fosforos == 1:
            print ("Sobrou 1 fósforo. Você perdeu!")
            break

    elif começa == "c": #o computador é o primeiro a jogar
        
        if fosforos == 21:
            computador = random.radint(1,4)

        else:
            if fosforos % 5 != 1:  #computador testa o raciocínio do utilizador
                computador = (fosforos-1) % 5
                if computador == 0:
                    computador = 1
            else:
                computador = random.radint(1,4)
                if computador >= fosforos:
                    computador = fosforos - 1 

        fosforos = fosforos - computador 
        print (f" O computador retira {computador} fósforos. Restam {fosforos} fósforos.")

        if fosforos == 1: #o utilizador joga em segundo
            print ("Sobrou 1 fósforo. O computador perdeu!")
            break

        while True:
            tirar = int (input(f"Quantos fósforos quer tirar (1-4)?"))
            if (1 <= tirar <=4 ) and (tirar <fosforos):
                break
            else:
                print  ("Número inválido. Tente novamente.")

        fosforos = fosforos - tirar
        print (f"Você retirou {tirar} fósforos, agora, restam {fosforos} fósforos.")

        if fosforos == 1:
                print ("Sobrou 1 fósforo. Você perdeu!")
                break
    else:
        print ("Escolha inválida. Reinicie o jogo.")
        break