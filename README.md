# rotten-potatoes


ROTTEN POTATOES
O Rotten Potatoes é uma aplicação escrita em Python com o framework Flask que utiliza um banco MongoDb.Essa aplicação faz parte dos desafios do curso Kubedev.

Para criar a estrutura da nossa aplicação em containers para uso em ambiente de desenvolvimento temos um arquivo docker-compose com o que será necessário para rodar a nossa aplicação.

DOCKER COMPOSE
No nosso arquivo docker compose, vamos iniciar informando a rede a ser criada para estabelecer a comunicação entre os containers da nossa solução.

![image](https://user-images.githubusercontent.com/96360563/154437998-9c169fc6-31f8-43b3-8274-df7a3c0f0f53.png)


No serviço rotten-potatoes vamos usar uma imagem que está disponível no meu repositório no Docker Hub.

Para que possamos acessar a nossa aplicação no navegador vamos informar a porta 5000. Que é a porta utiliza por padrão em aplicações Flask.

No item networks vamos informar a rede rotten-potatoes-net a ser usada para a comunicação com o container do mongo-db.

Neste serviço também vamos informar que o serviço rotten-potatoes depende do serviço mongo-db.

A imagem do rotten-potatoes necessita que algumas variáveis de ambiente sejam informadas no item environment. São elas:

MONGODB_DB: Nome do banco Mongo Db que será usado para armazenar os dados da aplicação.
MONGODB_HOST: Nome do serviço que contem o banco Mongo Db(mongo-db).
MONGODB_PORT: Porta a ser utilizada para conectar ao banco Mongo Db(27017).
MONGODB_USERNAME: Usuário do banco Mongo Db.
MONGODB_PASSWORD: Senha do banco Mongo Db.
No serviço mongo_db vamos utilizar a imagem oficial do mongodb na versão 4.4.3.

Para expor as conexões ao nosso container mongo_db vamos utilizar a porta 27017 e especificar no item ports.

Assim como no serviço rotten-potatoes, o serviço mongo_db também deve informar a rede rotten-potatoes-net para a comunicação com os containers da solução.

A imagem do mongodb também espera que algumas variáveis de ambiente sejam informadas. Estas serão informadas no item environments:

MONGO_INITDB_ROOT_USERNAME: Usuário do banco de dados Mongo Db.
MONGO_INITDB_ROOT_PASSWORD: Senha do banco de dados Mongo Db.
Para armazenar os dados dos filmes e avaliações do rotten-potatoes vamos criar um volume e associá-lo a pasta /data/db dentro do container do Mongo Db.

Dentro do nosso arquivo compose também precisamos especificar o volume que será usada no item volumes.

volumes: 
  mongo_rotten_potatoes_vol:
Para rodar o nosso compose. Vamos utilizar o seguinte comando:

docker-compose up
Para acessar a nossa aplicação do rotten-potatoes. Vamos digitar o endereço abaixo no navegador:

http://localhost:5000
