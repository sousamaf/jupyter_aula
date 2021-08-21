# jupyter_aula
Jupyter Notebook para as disciplinas de ministradas pelo professor Marco Antonio do curso de Sistemas de Informação.


# Instalação e uso

## Para utilizar a partir do Docker Hub:

Para CPU
docker pull sousamaf/jupyter_aula
docker run -d -it -p 8888:8888 sousamaf/jupyter_aula

Para GPU:
docker pull sousamaf/jupyter_aula:gpu
docker run -d -it -p 8888:8888 sousamaf/jupyter_aula:gpu

Será criado o diretório "notebooks" em seu home para
persistir os arquivos criados durante o uso da ferramenta.

## Para clonar o projeto:
git clone https://github.com/sousamaf/jupyter_aula.git

## Para construi a imagem docker:
docker-compose build 

## Para levantar o serviço:
docker-compose up jupyter &

## Para acessar o serviço:
Copie o endereço local fornecido ao levantar o serviço e cole no navegador de sua preferência. 
O endereço será algo do tipo: http://127.0.0.1:8888/
A senha padrão é: "aula"