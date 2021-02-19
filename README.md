# VSI Power On and Off with Cloud Functions
Este repositório explica como ligar e desligar sua VSI usando IBM Cloud Functions - Python 3.7

Requisitos:
- Docker CE instalado
- Python 3.7 instalado


\n\n

Os passos a seguir irão te ajudar a criar uma Action na IBM Cloud Functions. 
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

5. Entre na IBM Cloud Console com suas credenciais

6. No menu da esquerda, clique em Functions

7. Clique em Actions e certifique que as Actions "vsi-classic-power-on" e "vsi-classic-power-off" criadas aparecem na lista 

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

10. Selecione "Code" e aperte em Invoke para testar


## Criar um Function Periodic Trigger

1. Clique em Trigger e depois em Create
2. Clique em Trigger
3. Clique em Periodic
4. Escreva o nome do Trigger
5. Selecione o padrão que deseja executar as Actions (data e hora)
6. Em "JSON Payload, digite:
```shel
{
"vsi": "<name_of_the_vsi>",
"power": "<power_action>"
}
```

Exemplo:
```shel
{
"vsi": "testeshutdown",
"power": "ON"
}
```

7. Clique em criar 
8. Na próxima tela, clique em "Add" e depois em "Select Existing" e associe a Action com o Trigger criado 
9. Clique em "Add"
10. Sua Function foi criada com um Trigger e Action para ligar sua VSI
11. Siga os mesmos passos para criar o Trigger de desligar a VSI
