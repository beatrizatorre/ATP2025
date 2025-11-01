# TPC7

## Autor
Beatriz Antunes da Torre, a110500, (![foto](Foto.jpg))

## Resumo
Realização dos diversos problemas do teste de aferição.

## Resultados 

* Res1.a - ncomuns = [x for x in lista1 if x not in lista2] + [x for x in lista2 if x not in lista1]
* Res1.b - lista = [x for x in texto.split() if len(x)>3]
* Res1.c - listaRes = [(i+1,lista[i]) for i in range(len(lista))]

* Res2.a - def strCount(s, subs):
    contar=0
    i=0
    while i<= len(s) - len(subs): 
        if s[i:i+len(subs)] == subs:
            contar=contar+1
            i=i+len(subs)
        else:
            i=i+1
    return contar

* Res2.b - def produtoM3(lista):
    ordenar = sorted(lista)
    menores = ordenar[:3]
    produto = menores[0] * menores [1] * menores[2]
    return  produto

* Res2.c - def reduxInt(n):
    while len (str(n)) > 1:
        soma=0
        for elem in str(n):
            soma = soma + int(elem)
        n=soma
    return n

* Res2.d - def myIndexOf(s1, s2):
    indice = -1 
    for i in range (len(s1) - len (s2) + 1 ): 
        if s1[i:i + len(s2)] == s2  and indice == -1 : 
            indice = i 
    return indice 

* Res3.a - def quantosPost(redeSocial):
    num_post = len(redeSocial)
    return num_post

* Res3.b - def postsAutor(redeSocial, autor):
    lista_posts = []
    for post in redeSocial:
        if post["autor"] == autor:
            lista_posts.append(post)
    return lista_posts

* Res3.c - def autores(redeSocial):
    lista_autores = []
    for post in redeSocial:
        autor = post["autor"]
        if autor not in lista_autores:
            lista_autores.append(autor)
    lista_autores.sort() 
    return  lista_autores

* Res3.d - def insPost(redeSocial, conteudo, autor, dataCriacao, comentarios):
    if not redeSocial:
        novo_id = "p1" # se não houver nenhum post
    else:
        numeros = []
        for post in redeSocial:
            num = int(post["id"][1:]) # vê os números sem o p
            numeros.append(num)
        
        maior = numeros[0]  #percorrer a lista de números para ver o maior 
        for n in numeros[1:]:
            if n > maior:
                maior = n

        proximo = maior + 1 #número do próximo post
        novo_id = "p" + str(proximo)

    novopost = {                     #criar novo post 
        "id": novo_id,
        "conteudo": conteudo,
        "autor": autor,
        "dataCriacao": dataCriacao,
        "comentarios": comentarios if comentarios else []
    }
    redeSocial.append(novopost) #acrescenta o novo post
    return redeSocial

* Res3.e - def remPost(redeSocial, id):
    encontrar = False
    for post in redeSocial:
        if post ["id"] == id:
            encontrar = True 
            redeSocial.remove(post)
    return redeSocial

* Res3.f - def postsPorAutor(redeSocial):
    distribuicao = {}
    for post in redeSocial:
        autor = post["autor"]
        if autor in distribuicao:
            distribuicao[autor] = distribuicao[autor] + 1 # como o autor já existe, apenas acrescenta mais 1 
        else: 
            distribuicao[autor] = 1 #primeiro post do autor 
    return distribuicao

* Res3.g - def comentadoPor(redeSocial, autor):
    lista_posts = []
    for post in redeSocial:
        for comentario in post ["comentarios"]:
            if comentario ["autor"] == autor:
                lista_posts.append(post)
    return lista_posts