# TPC6
## Autor
Lara Carvalho Alves, A111315, (![foto](foto.jpg))
## Resumo
Desenvolvimento de uma aplicação para gerir funcionalidades do Python.
## Resultados
#Aplicação funcionalidades Python 

tab_Meteo = [((2025,5,10), 5, 16, 0),((2022,10,1), 2, 17, 0.4), ((2022,1,23), 8, 18, 0.03)]
def menu():
    print("""
    (1)Temperatura Média
    (2)Guardar TabMeteo num ficheiro
    (3)Carregar tabMeteo
    (4)Temperatura mínima mais baixa
    (5)Amplitude Térmica
    (6)Precipitação Máxima
    (7)Precipitação Superior
    (8)Maior nº de dias consecutivos de precipitação inferior 
    (9)Gráfico de Temperatura Mínima, Máxima e de Pluviosidade
    (0)Sair 
    """)
def medias(tab_Meteo):
    res=[]
    for data, tmin, tmax, prec in tab_Meteo:
        media=(tmin+tmax)/2 
        res.append((data,media))
    return res 
print(medias(tab_Meteo))
def guardaTabMeteo(tab_Meteo, fnome):
    f=open(fnome,"w")
    res=""
    for data, tmin, tmax, prec in tab_Meteo:
        ano, mês, dia=data
        registo=f"{ano}-{mês}-{dia}|{tmin}|{tmax}|{prec}\n"
        f.write(registo)
    f.close()
    return 
def carregaTabMeteo(fnome):
    res = []
    f=open(fnome, "r")
    for linha in f:
        linha=linha.strip()
        campos=linha.split("|")
        data, tmin, tmax, prec=campos 
        ano, mês, dia=data.split("-")
        res.append(((int(ano), int(mês), int(dia)), float(tmin), float(tmax), float(prec)))   
    f.close()
    return res
def minMin(tab_Meteo):
    minima=tab_Meteo[0][1]
    for registo in tab_Meteo:
        tmin=registo[1]
        if tmin < minima:
            minima=tmin    
    return minima
def amplTerm(tab_Meteo):
    res = []
    for data, tmin, tmax, prec in tab_Meteo:
        amplTerm=tmax-tmin
        res.append(amplTerm)
    return res 
def maxChuva(tab_Meteo):
    max_data=tab_Meteo[0][0]
    max_prec=tab_Meteo[0][3]
    for data, tmin, tmax, prec in tab_Meteo:
        if prec>max_prec:
            max_prec=prec
            max_data=data
    return (max_data, max_prec)
def diasChuvosos(tab_Meteo, p):
    res=[]
    for data, tmin, tmax, prec in tab_Meteo:
        if prec > p:
            pares=(data,prec)
            res.append(pares)
    return res
def maxPeriodoCalor(tab_Meteo, p):
    res=0
    for data, tmin, tmax, prec in tab_Meteo:
        if prec<p and prec-1<p:
            res=res+1
    return res
def grafTabMeteo(t):
    x=[f"{data[0]}/{data[1]}/{data[2]}" for data, tmin, tmax, prec in t]
    y_min=[tmin for data, tmin, tmax, prec in t]
    y_max=[tmax for data, tmin, tmax, prec in t]
    prec=[prec for data, tmin, tmax, prec in t]
    
    #gráfico de linhas e pontos
    plt.plot(x, y_min, label= "Temperatura mínima (ªC)", color= "purple", marker="o")
    plt.plot(x, y_max, label="Temperatura máxima (ºC)", color="blue", marker="d")
    plt.legend() 
    plt.xticks(rotation=45)  
    plt.grid()  
    plt.show() 

    # gráfico de barras
    plt.bar(x,prec, label="Pluviosidade (mm)", color="c")
    plt.legend() 
    plt.xticks(rotation=45) 
    plt.grid()  
    plt.show() 
    return

cond=True
while cond==True:
    menu()
    acao=input("Introduz um número de 0 a 9, de acordo com o menu: ")
    try: 
        opcao=int(acao)
    except ValueError:
        opcao=-1
    
    if opcao==1:
        medias(tab_Meteo)
        print(medias(tab_Meteo))
    elif opcao==2:
        fnome=input("Nome do ficheiro: ")
        guardaTabMeteo(tab_Meteo, fnome)
        guardaTabMeteo(tab_Meteo, "listameteorologia.txt")
        print("A sua lista foi guardada.")
    elif opcao==3:
        fnome=input("Nome do ficheiro: ")
        carregaTabMeteo(fnome)
        tab_Meteo2 = carregaTabMeteo("listameteorologia.txt")
        print(tab_Meteo2)
    elif opcao==4:
        minMin(tab_Meteo)
        print(minMin(tab_Meteo)) 
    elif opcao==5:
        amplTerm(tab_Meteo)
        print(amplTerm(tab_Meteo))
    elif opcao==6:
        maxChuva(tab_Meteo)
        print(maxChuva(tab_Meteo))
    elif opcao==7:
        p=float(input("Escolha um limite p para a precipitação: "))
        diasChuvosos(tab_Meteo, p)
        print(diasChuvosos(tab_Meteo, p))
    elif opcao==8:
        p=float(input("Escolha um limite p para a precipitação: "))
        maxPeriodoCalor(tab_Meteo, p)
        print(maxPeriodoCalor(tab_Meteo, p))
    elif opcao==9:
        from matplotlib import pyplot as plt 
        grafTabMeteo(tab_Meteo)
    elif opcao==0:
        print("Saiu da aplicação. Obrigado pela visita.")
        cond=False
    else:
        print("Opção inválida. Escolha um número pertencente ao menu.")
