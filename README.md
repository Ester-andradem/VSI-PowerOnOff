# VSI Power On and Off with Cloud Functions
Este repositório explica como ligar e desligar o VSI usando IBM Cloud Functions - Python 3.7

Requisitos:
- Docker CE instalado
- Python 3.7 instalado




Os passos a seguir irão te ajduar a criar uma Action na IBM Cloud Functions. 
Esta Action é baseada em Python 3.7 e pode ser usada tanto para ligar quanto para desligar sua VSI.


1. Clone o repositório usando o comando "git clone" para ter acesso a pasta da aplicação
````shel
git clone https://github.com/Ester-andradem/VSI-PowerOnOff.git
````

2. Entre na pasta onde esta sua aplicação
````shel
cd VSI-PowerOnOdff
````

3. Faça o login na IBM Cloud
````shel
ibmcloud login --sso                   # Caso tenha IBM ID
ibmcloud target -g Default             # Especifica a região
ibmcloud target --cf                   # Especifica o espaço do Clound Foundry
````

4. Crie as duas Actions puxando o zip para o IBM Functions

### Ação para ligar VSI
```shel
ibmcloud fn action create vsi-classic-power-on vsi-classic-power.zip --kind python:3.7
```

### Ação para desligar VSI
```shel
ibmcloud fn action create vsi-classic-power-off vsi-classic-power.zip --kind python:3.7
```

5. Entre na IBM Cloud console com suas credenciais

6. No menu da esquerda clique em Funcitions

7. Clique em Actions e certifique que as actions "vsi-classic-power-on" e "vsi-classic-power-off" aparecem na lista 

8. Clique na Action "vsi-classic-power-on" e coloque os parâmetros:
```shel
vsi "nombre de VSI"
power "ON"
apikey "apikey de infrestructura clasica"
user "Usuario softlayer"
```

9. Salve a Action On. Clique na Action "vsi-classic-power-off" e coloque os parâmetros:
```shel
vsi "nombre de VSI"
power "OFF"
apikey "apikey de infrestructura clasica"
user "Usuario softlayer"
```

Exemplo:
```shel
vsi "testeshutdown"
power "ON"
apikey "73bc6c593e7ef22d38edb204c060055d09c5ad171715"
user "2059386_nome@ibm.com"
```

10. Selecione "Code" e aperte em Invoke

