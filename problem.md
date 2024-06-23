Esse problema pode ser facilmente resolvido criando o arquivo de bloqueio e modificando a propriedade.

sudo touch composer.lock

sudo chown -R $USER ./composer.lock

composer update

OU

Basta possuir a pasta do projeto:

sudo chown -R $USER path/to/project/folder

Com isso, você não precisa usar sudopara corrercomposer update

Compartilhar
Editar
Seguir
editado em 27 de abril de 2021 às 16h12
respondido em 27 de abril de 2021 às 16h06
Avatar de usuário de Obinna Nnenanya
Obinna Nnenanya
1.6881515 emblemas de prata1616 emblemas de bronze
Adicione um comentário

Report this ad
3

O que funcionou para mim foi simplesmente fazer cd para /fullpath-to-my-project e executar o comando do compositor.

A documentação do Composer é tão pobre que eu não tinha ideia de que você precisava estar no diretório raiz do site antes de usá-lo. Isto pode ser óbvio para a maioria das pessoas, mas não necessariamente para os novatos.

Esta solução, é claro, implica as permissões corretas conforme fixadas nas outras sugestões.

Compartilhar
Editar
Seguir
respondido em 6 de novembro de 2022 às 14h28
Avatar do usuário de Coventure Joe
Coventura Joe
14911 distintivo de prata66 emblemas de bronze
Adicione um comentário
0

A execução sudo chown -R $USER ~/.composer/não funcionará porque na verdade não há nenhum arquivo/pasta na estrutura do Laravel chamado 'composer', mas sim 'composer.lock'. Em vez disso, executar sudo chown $USER composer.lockfaria mais sentido (substitua $USER pelo seu nome de usuário real). No entanto, isso não resolverá totalmente o problema.

Dito isso, você deve fazer o seguinte para garantir que composer install(ou composer update) seja executado com êxito: Presumo que o caminho do seu projeto seja /var/www/html/seu-projeto.

Altere a propriedade da pasta do seu projeto Laravel: sudo chown -R www-data.www-data /var/www/html/your-project

Altere as permissões da pasta do seu projeto Laravel:sudo chmod -R 755 /var/www/html/your-project

Torne a pasta de armazenamento gravável:sudo chmod -R 777 /var/www/html/your-project/storage

Em seguida, certifique-se de adicionar o usuário atual ao grupo www-data: sudo usermod $USER -g www-data(substitua $USER pelo seu nome de usuário)

Agora você deve conseguir executar composer installou composer updatesem erros de permissão.

#NÃO INICIA NGINX, MYSQL DOCKER - SOLUÇÃO
<pre> https://academy.especializati.com.br/ticket/a-aplicacao-nao-subiu

.. Seu container do redis pode estar ficando down (reiniciando)

.. Faz o seguinte, não usa o redis só para testar.

No arquivo .env, deixa assim:
CACHE_DRIVER=file
QUEUE_CONNECTION=sync
SESSION_DRIVER=file

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

 
