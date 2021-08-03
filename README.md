# onda-ecuation-pag-743-Burden-
#Entradas
L = 1.0 #Valor maximo x
T = 1.0 #Valor maximo de tiempo

alpha = 2.0 #Constante de velocidad
m = 10 #discretizacion x (i)
N = 20 #discretizacion t (j)

L_x = np.linspace(0,L,m+1)#lista valores x
L_t = np.linspace(0,T,N+1)#lista valores t

#Condicion inicial
U0 = np.sin(np.pi*L_x)
dU0 = np.zeros(U0.shape)

Q0 = np.hstack((U0,dU0))#estructura de datos
                        #[posicion, velocidad]
Qs = odeint(OndaO2_01,Q0,L_t)

# solucion exacta

U_exact = lambda t,x:np.sin(np.pi*x)*np.cos(2*np.pi*t)

###visualizar
##for q in range(21):
##    pl.plot(L_x,Qs[q,:11],'bo-')
##    pl.plot(L_x,U_exact(L_t[q],L_x),'r+-')
##    pl.legend(['Numerica','Exacta'])
##    
##    pl.title("Posicion a t= "+str(L_t[q]))
##    pl.ylim([-1,1])
##    pl.grid('on')
##    pl.show()
##
##for q in range(21):
##    pl.plot(L_x,Qs[q,11:],'bo-')
##    pl.title("Velocidad a t= "+str(L_t[q]))
##    pl.ylim([-10,10])
##    pl.grid('on')
##    pl.show()
##
##for q in range(21):
##    pl.subplot(2,1,1)
##    pl.plot(L_x,Qs[q,:11],'bo-')
##    pl.plot(L_x,U_exact(L_t[q],L_x),'r+-')
##    pl.legend(['Numerica','Exacta'])
##    pl.title("Posicion a t= "+str(L_t[q]))
##    pl.ylabel("altura")
##    pl.ylim([-1,1])
##    pl.grid('on')
##
##    pl.subplot(2,1,2)
##    pl.plot(L_x,Qs[q,11:],'bo-')
##    pl.xlabel("tiempo(sg)")
##    pl.ylabel("Velocidad")
##    pl.ylim([-10,10])
##    pl.grid('on')
##    pl.show()
##    
##

#tabla de comparacion
print("Metodo Lineas")
print("Comparacion Tabla 12.6")
print("--x--+-----w----")
for i,q in enumerate(Qs[-1,:11]):
	print(L_x[i],q)


###grafico 3d

mpl.rcParams['legend.fontsize'] = 10
fig = pl.figure()
ax = fig.gca(projection='3d')

t = L_t
zo = np.zeros(t.shape)
for j in range(11):
    z = Qs[:,j]
    x = L_x[j]*np.ones(t.shape)
    ax.plot(x, t, z,'r*-')
    ax.plot(x, t, zo,'go')


pl.xlabel("Eje x")
pl.ylabel("Tiempo")
pl.title("problema 1 pag 743 (Burden)")
pl.show()
