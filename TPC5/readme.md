# TPC5

## Autor

Beatriz Antunes da Torre, a110500, (![foto](Foto.jpg))

## Resumo
Criação de uma aplicação para gestão de alunos.

## Resultados

#Modelo 
#aluno = (nome,id, [nota TPC,notaProj,nota Teste])
#turma = [aluno]
#nome = string
#id = int 
#notas = float

turma = []
nome_turma = ""

def existe_turma(nome_turma): #Verificar se uma dada turma já existe 
    cond = False
    if nome_turma != "":
        cond =True
    return cond 

def criar_turma():  #Criar turma 
    nome_turma =  input ("Nome da nova turma:")
    turma = []
    print (f" A turma {nome_turma} foi criada com sucesso. ")
    return nome_turma,turma

def inserir_aluno(nome_turma,turma):  # Inserir aluno 
    if existe_turma(nome_turma):
        turma_escolhida = input("Nome da turma onde deseja inserir o aluno: ")
        if turma_escolhida == nome_turma:
            nome_aluno = input ("Nome do aluno: ")
            id = int(input("Id aluno: "))
            nota_TPC = float(input("Nota TPC (0-20):"))
            nota_Proj = float(input("Nota Projeto (0-20):"))
            nota_Teste = float(input("Nota do teste (0-20):"))
            aluno = (nome_aluno, id, [nota_TPC,nota_Proj,nota_Teste])
            turma.append(aluno)
            print ("Aluno inserido com sucesso.")
        else:
            print (f"A turma {turma_escolhida} não existe.")
    else:
        print ("Ainda não existe nenhuma turma.")
    return turma

def listar_turma(nome_turma,turma):  #listar turma 
    if existe_turma(nome_turma):
        if len(turma)==0:
            print ("Turma vazia.")
        else:
            print (f"Lista de alunos da turma {nome_turma}:")
            for aluno in turma:
                nome_aluno, id, notas = aluno 
                print (f"ID:{id}; Nome {nome_aluno}, Notas: TPC = {notas[0]}, Projeto = {notas[1]}, Teste = {notas[2]}")
    else:
        print ("Ainda não existe nenhuma turma.")


def consultar_aluno(nome_turma,turma): # consultar aluno pelo seu id 
    if existe_turma(nome_turma):
        id_procurar = int(input("Id do aluno a consultar:"))
        encontrado = False
        for aluno in turma:
                if aluno[1] == id_procurar:
                    nome_aluno, id, notas = aluno 
                    print(f"Aluno encontrado: Nome = {aluno[0]}, Notas: TPC = {notas[0]}, Projeto = {notas[1]}, Teste = {notas[2]}.")
                    encontrado = True
        if encontrado == False:
            print ("Aluno não encontrado.")
    else: 
        print ("Ainda não existe nenhuma turma.")

def guardar_turma(nome_turma,turma): # guardar turma num ficheiro
    if existe_turma(nome_turma):
        nome_ficheiro = input("Nome do ficheiro para guardar:")
        ficheiro = open(nome_ficheiro,"w")
        i = 0
        while i < len(turma):
            nome_aluno, id, notas = turma[i]
            linha = (f"{nome_aluno};{id};{notas[0]};{notas[1]};{notas[2]}\n")
            ficheiro.write(linha)
            i = i + 1
        ficheiro.close()
        print (f"Turma {nome_turma} guardada no ficheiro {nome_ficheiro}.")
    else:
        print ("Ainda não existe nenhuma turma.")

def carregar_turma(): # carregar turma de um ficheiro
    nome_turma = input("Nome da turma a carregar:")
    nome_ficheiro = input("Nome do ficheiro a carregar:")
    turma = []
    ficheiro = open(nome_ficheiro,"r")
    linha = ficheiro.readline()
    while linha !="":    
        linha = linha.strip() #remove os espaços e o \n
        dados = linha.split(";")  #separar os valores
        nome_aluno = dados [0]
        id = int(dados[1])
        notas = [float(dados[2]),float(dados[3]),float(dados[4])]
        aluno = (nome_aluno, id, notas)
        turma.append(aluno)
        linha = ficheiro.readline()
    ficheiro.close()
    if len (turma) > 0:
        print (f"Turma {nome_turma} carregada do ficheiro {nome_ficheiro}.")
    else:
        print ("Nenhum aluno foi carregado. Ficheiro vazio ou inválido.")
    return nome_turma, turma

def menu():
    print("Gestão de Alunos")
    print("(1) Criar turma")
    print("(2) Inserir aluno na turma")
    print("(3) Listar turma")
    print("(4) Consultar um aluno por id")
    print("(5) Guardar a turma num ficheiro")
    print("(6) Carregar uma turma de um ficheiro")
    print("(0) Sair da aplicação")

def main():
    cond = True 
    while cond == True:
        menu()
        opçao = input("Escolha uma opção:")

        if opçao == "1":  #Criar turma
            nome_turma,turma = criar_turma()
        elif opçao == "2": # Inerir aluno
            turma = inserir_aluno(nome_turma,turma)
        elif opçao == "3": # Listar turma
            listar_turma(nome_turma,turma)
        elif opçao == "4": #Consultar aluno por id
            consultar_aluno(nome_turma,turma)
        elif opçao == "5": # guardar turma num ficheiro 
            guardar_turma(nome_turma,turma)
        elif opçao == "6": # carregar uma turma de um ficheiro 
            nome_turma, turma = carregar_turma()
        elif opçao == "0":  # sair 
            print ("A sair da aplicação.")
            cond = False
        else:
            print("Operação inválida.")

main()