# TPC7
## Autor
Lara Carvalho Alves, A111315, (![foto](foto.jpg))
## Resumo
Desenvolvimento de um teste diagnóstico.
## Resultados
Resolução do teste diagnóstico.


for elem in lista1:
    if elem not in lista2:
        ncomuns.append(elem)
for elem in lista2:
    if elem not in lista1:
        ncomuns.append(elem)

print (ncomuns)

for pal in texto.split():
    if len(pal)>3:
        lista.append(pal)

print (lista)

for i in range(len(lista)):
    listaRes.append((i+1,lista[i]))

print(listaRes)

def strCount(s, subs):
    return s.count(subs)

def produtoM3(lista):
    tres_menores=sorted(lista)[:3]
    produto=tres_menores[0]*tres_menores[1]*tres_menores[2]
    return produto

def reduxInt(n):
    while n>=10:
        soma=0
        for dig in str(n):
            soma=soma+int(dig)
        n=soma
    return n

def myIndexOf(s1, s2):
    res=-1
    for i in range(len(s1)-len(s2)+1):
        if s1[i:i+len(s2)]==s2:
            res=i
    return res

def quantosPost(redeSocial):
    return len(redeSocial)

def postsAutor(redeSocial, autor):
    lista_posts=[]
    for post in redeSocial:
        if post['autor']==autor:
            lista_posts.append(post)

    return  lista_posts

def autores(redeSocial):
    lista_autores=[]
    for post in redeSocial:
        autor=post['autor']
        if autor not in lista_autores:
            lista_autores.append(autor)
    lista_autores.sort()
    return  lista_autores

def insPost(redeSocial, conteudo, autor, dataCriacao, comentarios):
    novo_id='p' + str(len(redeSocial)+1)
    post={
        'id':novo_id,
        'conteudo':conteudo,
        'autor':autor,
        'dataCriacao':dataCriacao,
        'comentarios':comentarios
    }
    redeSocial.append(post)
    return redeSocial

def remPost(redeSocial, id):
    indice=-1
    for i in range(len(redeSocial)):
        if redeSocial[i]['id']==id:
            indice=i
    if i !=-1:
        redeSocial.pop(indice)
    return redeSocial

def postsPorAutor(redeSocial):
    distribuicao={}
    for post in redeSocial:
        autor=post['autor']
        if autor not in distribuicao:
            distribuicao[autor]=[]
        distribuicao[autor].append(post)
    return distribuicao

def comentadoPor(redeSocial, autor):
    lista_comentarios=[]
    for post in redeSocial:
        for comentario in post['comentarios']:
            if comentario['autor']==autor and post not in lista_comentarios:
                lista_comentarios.append(post)
    return lista_comentarios

