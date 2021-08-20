# jupyter_aula
Jupyter Notebook para as disciplinas de ministradas pelo professor Marco Antonio do curso de Sistemas de Informação.


# Instalação e uso

## Para utilizar a partir do Docker Hub:

docker pull sousamaf/jupyter_aula

docker run -it -p 8888:8888 -v ~/aula:/tf/work sousamaf/jupyter_aula

Obs: após a primera execução altere o proprietário do diretório "aula" criado em seu home:
sudo chown -R 1000:1000 aula

## Para clonar o projeto:
git clone https://github.com/sousamaf/jupyter_aula.git

## Para construi a imagem docker:
docker-compose build 

## Para levantar o serviço:
docker-compose up jupyter &

## Para acessar o serviço:
Copie o endereço local fornecido ao levantar o serviço e cole no navegador de sua preferência. 
O endereço será algo do tipo: http://127.0.0.1:8888/?token=TOKEN