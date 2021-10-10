# conversao-distancia

# Passo 01
Identificar qual linguagem de programação a aplicação trabalha e se faz uso de algum banco de dados.
Analisando o código e o arquivo requirements identifiquei a necessidade python  e a instalação de algumas bibliotecas que localizei no arquivo requirements.txt 

# Passo 02 
Construir o Dockerfile com informações da imagem padrão adicionar bibliotecas e expor a porta de acesso a aplicação. 


FROm python:3.8
WORKDIR /app
COPY requirements.txt .
RUN python -m pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["gunicorn", "--workers=3", "--bind", "0.0.0.0:5000", "app:app"]

Comando para construção da imagem 

docker build -t jchelp/desafio1-conversao-distancia:v1 .

## Testar a imagem 

docker container run -d -p 8080:5000 jchelp/desafio1-conversao-distancia:v1
## Gerar imagem lastest e dar push para o hub.docker 

docker tag jchelp/desafio1-conversao-distancia:v1 jchelp/desafio1-conversao-distancia:latest

## Push na imagem 

docker login - garantir sucesso 

docker push jchelp/desafio1-conversao-distancia:v1

docker push jchelp/desafio1-conversao-distancia:latest