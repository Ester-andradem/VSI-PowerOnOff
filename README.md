# VSI-Power-On-Off-Using-IBM-Cloud-Functions
Este repositório explica como ligar e desligar o VSI usando IBM Cloud Functions - Python 3.7

Requisitos:
- Docker CE instalado
- Python 3.7 instalado


Os passos a seguir irão te ajduar a criar uma Action na IBM Cloud Functions. 
Esta Action é baseada em Python 3.7 e pode ser usada tanto pra ligar quanto pra desligar sua VSI.


1. Clone o repositório usando o comando "git clone" para ter acesso a pasta da aplicação
````shel
git clone https://github.com/Ester-andradem/VSI-PowerOnOff.git
````

2. Entre na pasta onde esta sua aplicação
````shel
cd VSI-PowerOnOdff
````

3.
  - Para Linux: Crie o Python virtualenv usando o comando Docker
````shel
docker run --rm -v "$PWD:/tmp" openwhisk/python2action bash -c "cd /tmp && virtualenv virtualenv && source virtualenv/bin/activate && pip install -r requirements.txt"
````

- Para Windows: Crie o Python virtualenv usando o comando Docker
docker run --rm -v "%cd%:/tmp" openwhisk/python2action bash -c "cd /tmp && virtualenv virtualenv && source virtualenv/bin/activate && pip install -r requirements.txt"

