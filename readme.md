# TPC6

## Autor

Beatriz Antunes da Torre, a110500, (![foto](Foto.jpg))

## Resumo

Criação de um programa com várias funcionalidades para tratar dados de temperaturas.

## Resultados 
* Res 1 - # TabMeteo = [(Data,TempMin,TempMax,Precipitacao)] # Data = (Int,Int,Int) # TempMin = Float # TempMax = Float #Precipitacao = Float

def inserirTabMeteo():
    tab = []
    continuar = True
    while continuar == True :
        print("\nInsira um novo registo meteorológico:")
        ano = int(input("Ano: "))
        mes = int(input("Mês: "))
        dia = int(input("Dia: "))
        tmin = float(input("Temperatura mínima (ºC): "))
        tmax = float(input("Temperatura máxima (ºC): "))
        prec = float(input("Precipitação (mm): "))
        tab.append(((ano, mes, dia), tmin, tmax, prec))
        resposta = input("Deseja inserir outro registo? (s/n): ").lower()
        if resposta != 's':
            continuar = False
    return tab

def guardaTabMeteo(t, fnome): #guardar tabela meteorológica num ficheiro de texto
    file = open (fnome,"w")
    for data,tmin,tmax,prec in t:  
        ano,mes,dia = data
        registo = f"{ano}-{mes}-{dia}|{tmin}|{tmax}|{prec}\n"
        file.write(registo)
    file.close()
    return
 
def carregaTabMeteo(fnome): #carregar uma tabela meteoro´lógica de um ficheiro texto
    res = []
    file = open(fnome,"r")
    #text =f.read()
    for linha in file:
        linha = linha.strip() #Tirar os espaços(em branco) que estão à frente e atrás
        campos = linha.split("|")
        data,tmin,tmax,prec = campos
        ano,mes,dia = data.split("-")
        res.append(((int(ano),int(mes),int(dia)),float(tmin),float(tmax),float(prec)))
    file.close()
    return res

def medias(tabMeteo): #média da temperatura de cada dia
    res=[] 
    for dia in tabMeteo:
        tempmin = dia[1]
        tempmax = dia[2]
        media = (dia[1]+dia[2])/2
        res.append ((dia[0],media))
    return res


def minMin(tabMeteo): #Calcular a temperatura mais baixa que foi registada
    minima = tabMeteo[0][1]
    for dia in tabMeteo:
        if minima > dia[1]:
            minima = dia[1]
    return minima

def amplTerm(tabMeteo): #calcular a amplitude térmica de cada dia 
    res = []
    for dia in tabMeteo:
        amplitude_termica = dia[2] - dia[1]
        res.append ((dia[0],amplitude_termica))
    return res 

def maxChuva(tabMeteo): #calcular o dia em que a precipitação foi máxima
    max_prec = tabMeteo[0][3]
    max_data = tabMeteo[0][0]
    for dia in tabMeteo:
        if max_prec < dia [3]:
            max_prec = dia [3]
            max_data = dia [0]
    return (max_data, max_prec)

def diasChuvosos(tabMeteo, p): #receber uma tabela e um limitee calcular os dias em que a precipitação foi inferior ao limite
    res = []
    for dia in tabMeteo:
        if dia [3] < p:
            res.append ((dia[0],dia[3]))
    return res

def maxPeriodoCalor(tabMeteo, p): #receber uma tabela e um limite e retomar o maior nº consecutivo de dias com a precipitação abaixo do limite
    diasconsecutivos = 0 #dias consecutivos abaixo do limite
    contardias = 0
    for dia in tabMeteo:
        if dia[3] < p:  #verificar se a precipitação está abaixo do limite
            diasconsecutivos = diasconsecutivos + 1
            if diasconsecutivos > contardias:
                contardias = diasconsecutivos
        else: 
            diasconsecutivos = 0
    return contardias

from matplotlib import pyplot as plt 

def grafTabMeteo(t): #desenhar gráficos das temperarutas e da precipitação
    x = [f"{data[0]}/{data[1]}/{data[2]}" for data,tmin,tmax,prec in t]
    ymin = [tmin for data,tmin,tmax,prec in t]
    ymax = [tmax for data,tmin,tmax,prec in t]
    precs =[prec for *_, prec in t]

    plt.plot(x,ymin, label="Temperatura mínima(ºC)", color="blue",marker="o")
    plt.plot(x,ymax, label= "Temperatura Máxima(ºC)", color="red", marker="o")
    plt.legend() #legenda
    plt.grid() #grelha de trás 
    plt.xticks(rotation=45)
    plt.show() #amostrar o gráfico 


    plt.bar(x,precs, label="Precipitação", color="c")
    plt.legend() #legenda
    plt.grid()  #grelha de trás 
    plt.xticks(rotation=45) #rotação 
    plt.show() 
    return

def menu():
    print("Registo de temepartura e precipitação")
    print("(1) Inserir tabela de registos meteorológicos")
    print("(2) Guardar uma tabela meteorológica num ficheiro texto")
    print("(3) Carregar uma tabela meteorológica  de num ficheiro texto")
    print("(4) Temperatura média de cada dia")
    print("(5) Temperatura minima mais baixa registada")
    print("(6) Amplitude térmica de cada dia")
    print("(7) Dia com precipitação máxima")
    print("(8) Dias em que a precipitação foi inferior ao limite")
    print("(9) Maior  número de dias consecutivos em que a precipitação foi abaixo do limite")
    print("(10) Apresentação dos gráficos da temperatura mínima, máxima e da precipitação ")
    print("(0) Sair")

def main():
    tabMeteo = []
    cond = True 
    while cond == True:
        menu()
        opçao = input("Escolha uma opção:")
        if opçao == "1": 
            nova_tab = inserirTabMeteo()
            tabMeteo = tabMeteo + nova_tab
            print("Registos adicionados com sucesso!")
        elif opçao == "2":
            nome = input("Nome do ficheiro: ")
            guardaTabMeteo(tabMeteo, nome)
            print("Tabela guardada com sucesso!")
        elif opçao == "3":
            nome = input("Nome do ficheiro: ")
            tabMeteo = carregaTabMeteo(nome)
            print("Tabela carregada com sucesso!")
        elif opçao == "4": #temperatura média de cada dia 
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                medias_dias = medias(tabMeteo)
                for d, m in medias_dias:
                    print(f"{d}: {m:.2f} ºC")
        elif opçao == "5":
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                print("Temperatura mínima mais baixa:", minMin(tabMeteo), "ºC")
        elif opçao == "6":
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                amp = amplTerm(tabMeteo)
                for d, a in amp:
                    print(f"{d}: {a:.2f} ºC")
        elif opçao == "7":
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                data, valor = maxChuva(tabMeteo)
                print(f"Dia com maior precipitação: {data} ({valor} mm)")
        elif opçao == "8":
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                limite = float(input("Insira o limite de precipitação: "))
                res = diasChuvosos(tabMeteo, limite)
                for d, p in res:
                    print(f"{d}: {p} mm")
        elif opçao == "9":
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                limite = float(input("Insira o limite de precipitação: "))
                print("Maior período consecutivo:", maxPeriodoCalor(tabMeteo, limite), "dias")
        elif opçao =="10":
            if len(tabMeteo) == 0:
                print("Tabela vazia. Insira registos primeiro.")
            else:
                grafTabMeteo(tabMeteo)
        elif opçao == "0":
            print("Saindo...")
            cond = False
        else:
            print("Opção inválida. Tente novamente.")

main()