# VSI Power On and Off with Cloud Functions - Python 3.7
Este repositório explica como ligar e desligar sua VSI usando IBM Cloud Functions

Requisitos:
- Conta na IBM Cloud
- <a href="https://cloud.ibm.com/docs/cli?topic=cloud-cli-install-ibmcloud-cli">IBM Cloud CLI instalado</a>
- <a href="https://cloud.ibm.com/docs/cli?topic=cloud-cli-plug-ins">Functions Plugin instalado</a>

Os passos a seguir irão te ajudar a criar uma Action na IBM Cloud Functions, 
esta Action é baseada em Python 3.7 e pode ser usada tanto para ligar quanto para desligar sua VSI.


1. Clone o repositório usando o comando "git clone" para ter acesso a pasta da aplicação
````shel
git clone https://github.com/Ester-andradem/VSI-PowerOnOff.git
````

2. Entre na pasta onde esta sua aplicação
````shel
cd VSI-PowerOnOff
````

3. Faça o login na IBM Cloud
````shel
ibmcloud login --sso                   # Caso tenha IBM ID
ibmcloud target -g Default             # Especifica a região
ibmcloud target --cf                   # Especifica o espaço do Clound Foundry
````

4. Crie as duas Actions puxando o zip para o IBM Functions:

### Action para ligar VSI
```shel
ibmcloud fn action create vsi-classic-power-on vsi-classic-power.zip --kind python:3.7
```

### Action para desligar VSI
```shel
ibmcloud fn action create vsi-classic-power-off vsi-classic-power.zip --kind python:3.7
```

5. Entre na IBM Cloud Console com suas credenciais

6. No menu da esquerda clique em "Functions"

7. Clique em "Actions" e certifique que as Actions "vsi-classic-power-on" e "vsi-classic-power-off" criadas aparecem na lista 

8. Clique na Action "vsi-classic-power-on" e coloque os parâmetros:

<p><strong>Parâmetros Action ON</strong>:</p>

```shel
vsi "nome da VSI"
power "ON"
apikey "softlayer_api_key"
user "Usuario softlayer"
```
	  
9. Salve a Action On. Clique na Action "vsi-classic-power-off" e coloque os parâmetros:

<p><strong>Parâmetros Action OFF</strong>:</p>

```shel
vsi "nome da VSI"
power "OFF"
apikey "softlayer_api_key"
user "Usuario softlayer"
```
> <p><strong>Obs: O nome da VSI não requer o domínio!</strong></p>

> <p>Para achar o <strong>user</strong> que será usado como um dos parâmetros da Action, entre na IBM Cloud Console (https://cloud.ibm.com), no Menu (do lado direito) clique em "Manage", logo em seguida clique em "Access (IAM)". No menu da esquerda selecione a opção "Users" e clique em cima do seu nome, na opção "VPN password" copie seu "User name", este será o parâmetro <strong>user</strong>.</p> 

> <p>A <strong>apikey</strong> encontra-se na mesma página que o "User name". Localize "API Keys" (logo abaixo de "VPN password") e clique nos três pontinhos do lado direito de "Classic Infraestrusture API Key". Logo em seguida clique em "Details" e copie sua <strong>apikey</strong>.</p> 


Exemplo:
```shel
vsi "testeshutdown"
power "ON"
apikey "apikey"
user "2059XXX_nome@ibm.com"
```

10. Dentro de uma da suas Actions, selecione a opção "Code" e aperte em "Invoke" para testar. Certifique-se que sua Action rodou corretamente.


## Criar um Function Periodic Trigger (Opcional)

1. Clique em "Trigger" e depois em "Create"

2. Clique em "Trigger"

3. Clique em "Periodic"

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

7. Clique em "Create"

8. Na próxima tela clique em "Add" e depois em "Select Existing" e associe a Action com o Trigger criado 

9. Clique em "Add". Sua Function foi criada com um Trigger e Action para ligar sua VSI!

11. Siga os mesmos passos para criar o Trigger de desligar a VSI


### Referências:
- https://github.com/itirohidaka/PowerOff-Functions
- https://github.com/mariolarte19/Schedule-a-VSI-Power-On-and-Off-Using-IBM-Cloud-Functions
